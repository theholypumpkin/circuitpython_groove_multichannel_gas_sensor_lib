# Circuitpython Groove-Multichannel-Gas-Sensor-library
This is a circuitpython port I created for my [digital Fridays for Future protest sign](https://github.com/theholypumpkin/FFF).
It just a circuit-python Port of the official [Arduino Library privided by Seeedstudios (Download)](https://github.com/Seeed-Studio/Seeed_Multichannel_Gas_Sensor/archive/master.zip)
You can still overwelmingly follow the [Arduino Tutorial provided by Seeedstudio](https://wiki.seeedstudio.com/Grove-Multichannel-Gas-Sensor-V2/) without any complications as long as you have the necessary dependencies installed.
But I added some wrapper methods which passible make it easyer to use.

## Hardware requirements:
[Seeedstrudio Grove - Multichannel Gas Sensor v2](https://www.seeedstudio.com/Grove-Multichannel-Gas-Sensor-v2-p-4569.html)

##Software requirements and dependencies:
- [Adafruit CircuitPython firmware for the supported boards](https://github.com/adafruit/circuitpython/releases)
- [Adafruit's Bus Device library](https://github.com/adafruit/Adafruit_CircuitPython_BusDevice)
- [Adafruit's Register library](https://github.com/adafruit/Adafruit_CircuitPython_Register)
  The libraries and firmware can also be downloaded on [CircuitPython.org](https://circuitpython.org)
  
### Getting started:
Drag the dependencies and this library into the lib folder on your circuit-python device.
__Please note that the .mpy files is only compiled for version Circuit-Python 6.3.0. If you use a version above you can use the uncompressed .py file or compress the files yourself using mpycross__

Start coding:

```python
  import board
  import multichannel_gas_sensor
  from busio import I2C
```

Once this is done you can define your `board.I2C` object and define your sensor object
```python
  i2c = board.I2C()   # uses board.SCL and board.SDA
  gas = multichannel_gas_sensor.GM_Multi_Gas(i2c)
```
Now you can preheat the sensor
Note that this is also done automatically as soon as you call any `measure` functions the first time.
```python
  gas.preheated()
```
Now you have access to the `no2`, `c2h5oh`, `voc` and `co` attributes.
```python
  no2 = gas.measureNO2() # Measures Nitrogen Dioxide and other trace gasses
  co = gas.measureCO() # Measures Carbon Monoxide and other trace gasses
  c2h5oh = gas.measureC2H5OH() # Measures Ethyl alcohol and other trace gasses
  voc = gas.measureVOC() # Measures Volatile organic compounds
```

To get the Sensor ADC Voltage `no2_vol`, `c2h5oh_vol`, `voc_vol` and `co_vol` attributes.
```python
    no2_vol = gas.measureNO2_Voltage()
    co_vol = gas.measureCO_Voltage()
    c2h5oh_vol = gas.measureC2H5OH_Voltage()
    voc_vol = gas.measureVOC_Voltage()
```

If you ant the same experience as with the official Arduino library you can also use the method
```python
no2 = gas._getGM102B() # Measures Nitrogen Dioxide and other trace gasses
co = gas._getGM302B() # Measures Carbon Monoxide and other trace gasses
c2h5oh = gas._getGM502B() # Measures Ethyl alcohol and other trace gasses
voc = gas._getGM502B() # Measures Volatile organic compounds
```
Those methods will return exactly the same as `gas.measureNO2()`, `gas.measureCO()` `gas.measureC2H5OH()` and `gas.measureVOC()` respectivly.
and to get to get the voltage using the Arduino way:
```python
adc = gas._getGM102B()
no2_vol = calcVol(adc) # returns the Voltage of the Sensor
```
The choice is yours. 

### Advanced features:
If you want to change the physical i2c address of the sensor you can do this is software
to do so, call
```python
gas.changeGMAddress(110) # sets the adress of the mutisensor to 0x6E
# Don't  forget to also tell your board to use the new address
gas.setAddress(i2c, 110) # changes the adress your board tries comunicate with the sensor.
```

Thats about it, if there are any troubles make a pull request.
