uSDX-lgt This is my fork of uSDX to work on compatible LGT8F328P MCU.
During the semiconductor crisis, when the prices for a regular Arduino soared 5 times, my attention was drawn to the Chinese clone LGT8F328P.
This microcontroller is almost completely compatible with the ATMEGA328P in terms of command system and has significant advantages:
1) 32 MHz clock frequency right out of the box,
2) 12-bit ADC.
3) uDSC computing accelerator with access to the SRAM area.
4) and many other goodies.
The only downside of this MCU is the lack of EEPROM, but for ATMEGA this is also a known problem, because the built-in EEPROM has a limited number of rewrites, only 100,000. And the uSDX program rewrites bytes with each frequency change. In my version, it was decided to take the EEPROM out as a separate chip.

Во время кризиса полупроводников, когда цены на обычную Ардуинку взлетели в 5 раз, мое внимание привлек китайский клон LGT8F328P
Этот микроконтроллер практически полностью совместим по системе команд с ATMEGA328P и имеет существенные приимущества:
1) Тактовая частота 32МГц сразу из коробки,
2) 12 разрядов АЦП.
3) Ускоритель вычислений uDSC, имеющий доступ к области SRAM.
4) и много других плюшек.
Единственный минус данного MCU является отсутсвие EEPROM, однако для ATMEGA это тоже известная проблема, ведь встроенная EEPROM имеет ограниченное число перезаписей, всего 100000. А программа uSDX перезаписывает байты при каждом изменении частоты. В моем варианте решено вынести EEPROM в виде отдельной микросхемы. Итак просто вешаем на шину I2C микросхему EEPROM ST24C08, такая была под рукой из старого CRT диплея. Предупреждение!!! это может не сработать с похожими микросхемами EEPROM, так как логика работы с ними может отличаться, и потребует изменения в коде.![ST24C08 w uSDX](https://github.com/user-attachments/assets/d678972e-f4b9-4234-818c-53d1562d2970)





