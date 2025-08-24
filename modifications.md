# QRP DIGITAL RF POWER & VSWR METER - modifications of Chinese copies

# Chinese copy 15W

![Chinese copy 15W](doc/ddwm07.jpg)

Above is the modified example.

## Issues

On receipt, the Chinese copy had several problems:
- SMA connectors were not soldered properly;
- displayed power was frequency dependent; and
- displayed VSWR was power dependent.

The firmware was modified to evaluate some different user interface ideas.

### Coupled transformers

The use of a binocular ferrite couples the voltage sampling and current sampling transformers, and they are supposed to be independent.

![new transformer](doc/2643250402x2transformers.jpg)

A new transformer was wound using a pair of Fair-rite 2643250402 suppression sleeves, it fits in the same space as the original binocular core.
It would have been better if the I2C display wires were not so close to the transformer, a sub optimal PCB layout.

This one measure improved indicated VSWR independence of power level.

### Detector issues

The detector produced somewhat lower voltage than expected, and was probably the cause of the frequency dependent output.

The diodes were replaced with BAT46JFILM SMD diodes which produced higher output, and much less frequency sensitivity up to 30MHz.
It would appear the manufacturer used SBD intended for switched mode power supplies, diodes with may too much junction capacitance.

G8GYW's diodes were 1n5711. BAT46 diodes are a little more 'sensitive' to very weak signal, so are usable to good accuracy to lower power levels.

To accomodate the increased output voltage, and to raise the calibration limit to 16W, the 18k divider resistors were replaced with 27k 0603 1% resistors.

Beware of buying BAT46 diodes from Aliexpress etc, they offer unbelievable prices and ship power diodes.

![schematic](doc/schematic_v3_15W.jpg)

### Calibration

An LTSPICE model of the detector was constructed and a third order polynomnial fit of Vinpk to Vodc was calculated.

![Curve fit](doc/LTSPICE-BAT46-27k-vi-vo-01.png)

The curve fit above is very good from equivalent to 50mW to 16W.

The parameters are stored in EEPROM.

![EEPROM map](ddwm/eeprom/ddwm-eeprom-BAT46-27k.png)

Parms vref and vrefr are nominally 1.1, and are tweaked for fine calibration of actual build components.

## Result

InsertionVSWR and loss were measured.

![InsertionVSWR and loss](doc/15Wddwm02.png)

The issues listed were satisfactorily resolved:
- accuracy of power is good across 1.8 to 30MHz from 50mW to ~20W;
- InsertionVSWR is good from 3.5-30MHz;
- minimum power displayed is restricted to 50mW so that garbage is not calculated, VSWR will not be calculated if Pref<50mW; and
- VSWR accuracy is good and largely insensitive to power level.

# Chinese copy 100W

![Chinese copy 100W](doc/ddwm-100w-m.jpg)

Above is the modified example.

## Issues

On receipt, the Chinese copy had several problems:
- displayed power was frequency dependent; and
- displayed VSWR was power dependent.

The firmware was modified to evaluate some different user interface ideas.

### Coupled transformers

The use of a binocular ferrite couples the voltage sampling and current sampling transformers, and they are supposed to be independent.

![new transformer](doc/2643250402x2transformers-100W.jpg)

A new transformer was wound using a pair of Fair-rite 2643250402 suppression sleeves, it fits in the same space as the original binocular core.
It would have been better if the I2C display wires were not so close to the transformer, a sub optimal PCB layout.

This one measure improved indicated VSWR independence of power level.

### Detector issues

The detector produced somewhat lower voltage than expected, and was probably the cause of the frequency dependent output.

The diodes were replaced with BAT46JFILM SMD diodes which produced higher output, and much less frequency sensitivity up to 30MHz.
It would appear the manufacturer used SBD intended for switched mode power supplies, diodes with may too much junction capacitance.

G8GYW's diodes were 1n5711. BAT46 diodes are a little more 'sensitive' to very weak signal, so are usable to good accuracy to lower power levels.

To accomodate the increased output voltage, and to raise the calibration limit to 16W, the 18k divider resistors were replaced with 37k 0603 1% resistors.

Beware of buying BAT46 diodes from Aliexpress etc, they offer unbelievable prices and ship power diodes.

![schematic](doc/schematic_v3_100W.jpg)

### Calibration

An LTSPICE model of the detector was constructed and a third order polynomnial fit of Vinpk to Vodc was calculated.

![Curve fit](doc/LTSPICE-BAT46-39k-vi-vo-01.png)

The curve fit above is very good from equivalent to 500mW to 100W.

The parameters are stored in EEPROM.

![EEPROM map](ddwm/eeprom/ddwm-eeprom-BAT46-39k.png)

Parms vref and vrefr are nominally 1.1, and are tweaked for fine calibration of actual build components.

## Result

![thermograph](doc/ddwm-100W-thermal.jpg)

Above is a thermograph of the transformers after 180s at 100W continuous and 9° ambient, a rise of 18° (temperature has stabilised, τ is about 100s).

InsertionVSWR and loss were measured.

![InsertionVSWR and loss](doc/100Wddwm02-m.png)


The issues listed were satisfactorily resolved:
- accuracy of power is good across 1.8 to 30MHz from 500mW to 100W;
- InsertionVSWR is good from 3.5-30MHz;
- minimum power displayed is restricted to 500mW so that garbage is not calculated, VSWR will not be calculated if Pref<500mW; and
- VSWR accuracy is good and largely insensitive to power level.






Owen Duffy
25/08/2025

