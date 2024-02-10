# Circuitpython Groove-Multichannel-Gas-Sensor-library

This is a circuitpython port I created for my [digital Fridays for Future protest sign](https://github.com/theholypumpkin/FFF).
It just a circuit-python Port of the official [Arduino Library privided by Seeedstudios (Download)](https://github.com/Seeed-Studio/Seeed_Multichannel_Gas_Sensor/archive/master.zip)
You can still overwelmingly follow the [Arduino Tutorial provided by Seeedstudio](https://wiki.seeedstudio.com/Grove-Multichannel-Gas-Sensor-V2/) without any complications as long as you have the necessary dependencies installed.
But I added some wrapper methods which passible make it easyer to use.

## Hardware requirements

[Seeedstrudio Grove - Multichannel Gas Sensor v2](https://www.seeedstudio.com/Grove-Multichannel-Gas-Sensor-v2-p-4569.html)

## Software requirements and dependencies

- [Adafruit CircuitPython firmware for the supported boards](https://github.com/adafruit/circuitpython/releases)
- [Adafruit's Bus Device library](https://github.com/adafruit/Adafruit_CircuitPython_BusDevice)
- [Adafruit's Register library](https://github.com/adafruit/Adafruit_CircuitPython_Register)
  
  The libraries and firmware can also be downloaded on [CircuitPython.org](https://circuitpython.org)
  
### Getting started

Drag the dependencies and this library into the lib folder on your circuit-python device.
__Please note that the .mpy files is only compiled for version Circuit-Python 8.2.9. If you use a version above you can use the uncompressed .py file or compress the files yourself using mpycross__

Start coding:

```python
  import board
  import multichannel_gas_sensor
  from busio import I2C
```

Once this is done you can define your `board.I2C` object and define your sensor object

```python
  i2c = board.I2C()   # uses board.SCL and board.SDA
  gas = multichannel_gas_sensor.MultichannelGas(i2c)
```

Now you can preheat the sensor
Note that this is also done automatically as soon as you call any `measure` functions the first time.

```python
  gas.preheat()
```

Now you have access to the `no2`, `c2h5oh`, `voc` and `co` attributes.

```python
  no2 = gas.measure_NO2() # Measures Nitrogen Dioxide and other trace gasses
  co = gas.measure_CO() # Measures Carbon Monoxide and other trace gasses
  c2h5oh = gas.measure_C2H5OH() # Measures Ethyl alcohol and other trace gasses
  voc = gas.measure_VOC() # Measures Volatile organic compounds
```

To get the Sensor ADC Voltage `no2_vol`, `c2h5oh_vol`, `voc_vol` and `co_vol` attributes.

```python
    no2_vol = gas.measure_NO2_voltage()
    co_vol = gas.measure_CO_voltage()
    c2h5oh_vol = gas.measure_C2H5OH_voltage()
    voc_vol = gas.measure_VOC_voltage()
```

### Advanced features

If you want to change the physical i2c address of the sensor you can do this is software
to do so, call

```python
gas.i2c_ddress(0x6E) # sets the new address of the mutisensor to 0x6E
```

Thats about it, if there are any troubles create an issue.
