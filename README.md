uSDX-lgt This is my fork of uSDX to work on compatible LGT8F328P MCU.
During the semiconductor crisis, when the prices for a regular Arduino soared 5 times, my attention was drawn to the Chinese clone LGT8F328P.
This microcontroller is almost completely compatible with the ATMEGA328P in terms of command system and has significant advantages:
1) 32 MHz clock frequency right out of the box,
2) 12-bit ADC.
3) uDSC computing accelerator with access to the SRAM area.
4) and many other goodies.
The only downside of this MCU is the lack of EEPROM, but for ATMEGA this is also a known problem, because the built-in EEPROM has a limited number of rewrites, only 100,000. And the uSDX program rewrites bytes with each frequency change. In my version, it was decided to take the EEPROM out as a separate chip. So, we simply hang the EEPROM ST24C08 chip on the I2C bus, we had one at hand from an old CRT display. Warning!!! This may not work with similar EEPROM chips, since the logic of working with them may be different, and will require changes in the code.
![ST24C08 w uSDX](https://github.com/user-attachments/assets/d678972e-f4b9-4234-818c-53d1562d2970)



Во время кризиса полупроводников, когда цены на обычную Ардуинку взлетели в 5 раз, мое внимание привлек китайский клон LGT8F328P
Этот микроконтроллер практически полностью совместим по системе команд с ATMEGA328P и имеет существенные приимущества:
1) Тактовая частота 32МГц сразу из коробки,
2) 12 разрядов АЦП.
3) Ускоритель вычислений uDSC, имеющий доступ к области SRAM.
4) и много других плюшек.
Единственный минус данного MCU является отсутсвие EEPROM, однако для ATMEGA это тоже известная проблема, ведь встроенная EEPROM имеет ограниченное число перезаписей, всего 100000. А программа uSDX перезаписывает байты при каждом изменении частоты. В моем варианте решено вынести EEPROM в виде отдельной микросхемы. Итак просто вешаем на шину I2C микросхему EEPROM ST24C08, такая была под рукой из старого CRT диплея. Предупреждение!!! это может не сработать с похожими микросхемами EEPROM, так как логика работы с ними может отличаться, и потребует изменения в коде.![ST24C08 w uSDX](https://github.com/user-attachments/assets/d678972e-f4b9-4234-818c-53d1562d2970)
И так функция запоминания текущих насторек uSDX с микроконтроллером LGT8F328P полностью работоспособна. Теперь перейдем к дальнейшей адаптации, Дело в том, что в MCU LGT8F328P пин с похожим названием у ATMEGA - AREF -- AVREF, является не выходом, а входом опроного напряжения АЦП, тоесть ацп может работать с любым опорным напряжением в диапазоне до напряжения питания, и теоретически это можно использовать для более точного аттенюатора и даже АРУ(это улучшение пока неиспользуется). Что хорошо, так это наличие у данного микроконтроллера ЦАП, и можно формировать опорное напряжение с помощью него. Сразу приходит на ум подключить резистивные делители входов А0, А1, А2 напрямую к выходу ЦАП, но тут проблемка возникает, в том что выход ЦАП объединен с PD4, а он используется для дисплея, Используем для дисплея PD5

![usdx-lgt-01](https://github.com/user-attachments/assets/c4fe2169-d97c-4f65-8a71-d32c8a6c9fae) Тогда выход DAO можно использовать для формирования опорного напряжения для резистивного делителя на входе ацп, но проблема в том что выход DAC очень слабый и напряжение на нем просядет, поэтому его необходимо усилить, для этого конечно лучше использовать rail-to-rail операционный усилитель, но используем что есть под рукой -- половинку LM358, запитав его от напряжения питания VIN , это конечно рискованно, потому что случайное замыкание ножек OPAMP может привести к тому, что полное внешнее напряжение питания окажется на входах микроконтроллера, вобщем лучше заменить его на любой rail-to-р  ail opamp и подключить к шине 5 вольт.
![usdx-lgt-02](https://github.com/user-attachments/assets/c7a91214-cea1-4162-89ba-fba50d543512)
Теперь схема полностью готова к экспериментам и доработкам.







