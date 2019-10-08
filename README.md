## Using NTC Thermistor with Arduino and esp32

The sketch works for both Arduino and ESP32 by just changing the line:

    bool esp32 = true;       // change to false when using Arduino

The sketch assumed that NTC Thermistor with 10k resistance at 25 degree Celcius and B parameter of 3950 to be used, if you have an Thermistor with 100k value, you may need to change some of the parameters accordingly.

### ESP32 Linearity issue

To address the ESP32 ADC non-linear issue, a lookup table is used to correct the non-linearity. You may need to generate your own lookup table as it varies from device to device due to the variation of ESP32 internal reference voltage. The code for generating the lookup table is written by Helmut Weber and can be found [here](https://esp32.com/viewtopic.php?f=19&t=2881&start=30#p47663).

[![ESP32 ADC linearity](https://github.com/e-tinkers/ntc-thermistor-with-arduino-and-esp32/blob/master/images/esp32_ADClinearity.png)](https://github.com/e-tinkers/ntc-thermistor-with-arduino-and-esp32/blob/master/images/esp32_ADClinearity.png)

### Noise on ESP32

The ESP32 is much noisy compare to Arduino. Add a 0.1uF capacity on Vout would help a little bit in smoothing out the noise or alternative write a filter algorithm to handle it.

*** Arduino ADC reading from thermistor ***
[![Arduino ADC reading from thermistor](https://github.com/e-tinkers/ntc-thermistor-with-arduino-and-esp32/blob/master/images/Arduino_ADC_reading.png)](https://github.com/e-tinkers/ntc-thermistor-with-arduino-and-esp32/blob/master/images/Arduino_ADC_reading.png)

*** ESP32 ADC reading from thermistor ***
[![ESP32 ADC reading from thermistor](https://github.com/e-tinkers/ntc-thermistor-with-arduino-and-esp32/blob/master/images/ESP32_ADC_reading.png)](https://github.com/e-tinkers/ntc-thermistor-with-arduino-and-esp32/blob/master/images/ESP32_ADC_reading.png)

### References

For more detail discussion and references, read my [blog post](https://www.e-tinkers.com/2019/10/using-a-thermistor-with-arduino-and-unexpected-esp32-adc-non-linearity/) on the subject.
