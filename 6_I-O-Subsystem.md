# Подсистемы ввода/вывода
Системы ввода-вывода используются для подключения компьютера к внешним устройствам, которые называются периферийными. В персональном компьютере периферийные устройства включают в себя клавиатуры, мониторы, принтеры и беспроводные сети. Во встраиваемых системах – нагревательный элемент тостера, синтезатор речи куклы, топливный инжектор двигателя, двигатели позиционирования солнечных панелей спутника и так далее. Процессор получает доступ к устройствам ввода-вывода, используя шины адреса и данных так же, как при получении доступа к памяти.

Часть адресного пространства отводится под устройства ввода-вывода вместо памяти. Например, адреса от 0xFFFF0000 до 0xFFFFFFFF расположены в зарезервированной части карты памяти. Каждому устройству ввода-вывода присваивается один или несколько адресов в этом диапазоне. При сохранении по заданному адресу посылаются данные в устройства. При загрузке – данные получаются от устройства. Этот метод связи с устройствами ввода-вывода называется вводом-выводом, отображенным в память.

![Отображение в память](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/отображение.PNG) Рис.1

На рис.1 изображены аппаратные средства, необходимые для поддержки двух устройств ввода-вывода, отображенных в память. Дешифратор адреса определяет, какое устройство связывается с процессором. Он использует сигналы Address и MemWrite, чтобы генерировать управляющие сигналы для остальной части аппаратных средств. Мультиплексор ReadData производит выбор между памятью и различными устройствами ввода-вывода. Регистры с разрешением записи содержат в себе значения, записываемые в устройства ввода-вывода.

Программное обеспечение, которое взаимодействует с устройством ввода-вывода, называется драйвером устройства. Написание драйвера требует детального знания об аппаратной части этого устройства. Другие программы вызывают функции в драйвере для получения доступа к устройству без необходимости понимания низкоуровневого аппаратного обеспечения. Адреса, связанные с устройствами ввода-вывода, часто называются регистрами ввода-вывода, потому что могут соответствовать регистрам устройства, как показано на рис.2.

![Микроконроллеры](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/мк.png) Рис.2

Встроенные системы используют процессор для управления взаимодействиями с физической средой. Обычно они выстроены вокруг микроконтроллеров (МК), которые сочетают в себе микропроцессор с набором простых в использовании периферийных устройств, таких как цифровые и аналоговые пины ввода-вывода общего назначения, последовательные порты, таймеры и т.д. В большинстве своем МК недорогие и спроектированы так, чтобы минимизировать стоимость и размеры систем путем интеграции большинства необходимых компонентов в один чип.

Микроконтроллеры классифицируются по размеру данных, с которыми они оперируют. 8-битные микроконтроллеры – самые маленькие и самые дешевые, в то время как 32-битные микроконтроллеры предоставляют больше памяти и имеют большую производительность.

![PIC](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/микро.PNG) Рис.3

На рис.3 показана блок-схема серии микроконтроллеров (МК) PIC32. В центре системы находится 32-разрядный процессор MIPS. Процессор подключается через 32-разрядные шины к флэш-памяти, содержащей программу, и к СОЗУ, содержащей данные. PIC32MX675F512H имеет 512 КБ флэш-памяти и 64 КБ оперативной памяти. Высокопроизводительные интерфейсы, такие как USB и Ethernet, также напрямую общаются с ОЗУ через матрицу шин данных. Периферия более низкой производительности, включающая последовательные порты, таймеры и аналого-цифровые преобразователи, разделяют между собой отдельную периферийную шину. Чип содержит цепь генерации тактовой частоты и детектор напряжения для определения, когда чип включается или когда он близок к потере питания.

![Карты памяти](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/карта%20памяти.PNG) Рис.4

На Рис.4 показана виртуальная карта памяти микроконтроллера. Все адреса, используемые программистом, виртуальны. Архитектура MIPS предлагает 32-разрядное адресное пространство для доступа до 232 байт = 4 ГБ памяти, но лишь небольшая часть из этой памяти фактически реализована на чипе. Соответствующие разделы из адресов 0xA0000000–0xBFC02FFF включают в себя оперативную память, флэш и регистры специального назначения (Special Function Registers, SFR), используемые для связи с периферийными устройствами. Существует дополнительные 12 КБ загрузочной флэшпамяти, которая, как правило, выполняет некоторую инициализацию, а затем переходит к основной программе во флэш-памяти. При поступлении команды сброса счетчик команд инициализируется на начало загрузочной флэш-памяти с адреса 0xBFC00000.

![Пины](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/пины.PNG) Рис.5

На рис.5 можно увидеть схему расположения пинов микроконтроллера. Они включают в себя питание и землю, тактовый сигнал, сброс и множество пинов, которые можно использовать как пины ввода-вывода общего назначения и/или как периферийные устройства специального назначения.

![](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/рд.PNG) Рис.6

Пины ввода-вывода общего назначения (GPIO) используются для чтения или записи цифровых сигналов.Например, на Рис.6 показаны восемь светодиодов (LED) и четыре переключателя, подключенных к 12-битному GPIO-порту. На схеме показаны названия и номер пина каждого из 12 выводов порта; отсюда программист узнает функции каждого пина, а разработчик аппаратной части – данные о том, какие соединения необходимо реализовать физически. Светодиоды подключены таким образом, чтобы светиться, когда на них приходит логическая «1», и затухают, когда приходит «0». Переключатели соединены определенным образом для получения «1», когда они закрыты, и «0» – при открытом состоянии. Микроконтроллер может использовать порт как для управления светодиодами, так и для чтения состояний переключателей.

![](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/схема.PNG) Рис.7

Последовательный Периферийный Интерфейс SPI – простой синхронный последовательный протокол, легкий в использовании и относительно быстрый. Физический интерфейс состоит из трех пинов: SerialClock (SCK), SerialDataOut (SDO) и Serial Data In (SDI).
SPI подключает ведущее устройство (master) к ведомому устройству (slave), как это показано на Рис.7 (а). Ведущее устройство производит сигнал тактовой частоты. Оно инициирует установку связи путем посылки серии импульсов тактовой частоты на SCK. Если оно хочет послать данные на ведомое устройство, оно посылает их на SDO, начиная со старшего бита. Ведомое устройство может одновременно ответить, посылая данные на SDI ведущего устройства. На Рис.7 (б) показана диаграмма сигналов SPI для передачи 8 битов данных.
У PIC32 есть до 4-х портов SPI, названных, что неудивительно, SPI1– SPI4. Каждый порт может выступать в роли ведущего или ведомого устройства. В данном разделе описан режим ведущего устройства, но режим ведомого похож на него. Чтобы использовать SPI-порт, программа PICR сначала должна сконфигурировать порт. Затем она может записывать данные в регистр; данные последовательно передаются на ведомое устройство. Данные, полученные от ведомого устройства, собираются в другом регистре. Когда передача завершена, PIC32 может прочитать полученные данные.


![](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/асинхрон.PNG) Рис.8

UART ("ю-арт") является периферийным устройством последовательного ввода-вывода без пересылки тактового сигнала. Вместо этого системы должны заранее договориться о скорости передачи данных, и каждая из них должна локально генерировать свои собственный тактовый сигнал. Хотя эти системные тактовые сигналы могут иметь небольшую погрешность частоты и неизвестное соотношение фаз, UART обеспечивает надежную асинхронную связь. 

На Рис. 8(a) показана асинхронная последовательная связь. DTE посылает данные в DCE по линии TX и получает данные обратно по линии RX. На Рис.8 (b) показана одна из этих линий, отправляющая символ со скоростью передачи данных 9600 бод.
Линия простаивает при логической "1", когда не используется. Каждый знак состоит из стартового бита (0), 7–8 битов данных, опционального бита четности и одного или более стоп-битов (1). UART детектирует перепад сигнала от состояния простоя до старта для своевременного начала осуществления передачи. Хотя семи битов данных достаточно, чтобы отправить ASCII-символ, как правило, используется восемь битов, потому что они могут передать произвольный байт данных.


Встроенные системы обычно нуждаются в измерении времени. Например, микроволновой печи необходим один таймер для отслеживания времени суток и другой, чтобы определить, как долго готовить. Она может использовать еще один таймер, чтобы генерировать импульсы двигателя, вращающего блюдо, а четвертый – чтобы контролировать уровень мощности, активируя микроволны лишь на долю каждой секунды.
PIC32 имеет пять 16-разрядных таймеров на плате. Таймер 1 называется таймером типа А, который может принять асинхронный внешний источник сигнала синхронизации, например, кварцевый генератор, дающий частоту 32 кГц. Таймеры 2/3 и 4/5 имеют тип B. Они работают синхронно с периферическим сигналом синхронизации и могут работать в паре (например, 2 с 3), чтобы образовать 32-разрядные таймеры для измерения длительных периодов времени.
Каждый таймер связан с тремя 16-разрядными регистрами: TxCON, TMRx и PRX. Например, T1CON является регистром управления для Таймера 1. CON является регистром управления. TMR содержит текущее значение счетчика времени. PR является регистром периода. Когда таймер достигнет указанного периода, он откатывается обратно в 0 и устанавливает бит TXIF в регистре флагов прерывания IFS0. Программа может опрашивать этот бит для обнаружения переполнения. Кроме того, он может генерировать прерывание.


Таймеры часто используются в сочетании с прерываниями таким образом, что программа может работать как обычно и затем периодически обрабатывать задачу, когда таймер генерирует прерывание. Запросы на прерывание возникают, когда происходит событие в аппаратной части, такое как переполнение таймера, получение символа по UART или переключение определенных выводов GPIO. Каждый тип запроса прерывания устанавливает конкретный бит в регистры Статуса флага прерывания. Затем процессор проверяет соответствующий бит в регистрах разрешения прерываний управления. Если бит установлен, микроконтроллер должен ответить на запрос прерывания посредством вызова программы обработки прерывания. ISR). ISR представляет собой функцию с аргументами пустого типа данных (void), которая обрабатывает прерывание и очищает бит из IFS до возврата из обработки. Система прерываний PIC32 поддерживает одно- и многовекторные режимы. В одновекторном режиме все прерывания вызывают один и тот же ISR, который должен проверить регистр CAUSE, чтобы определить причину прерывания (если может возникнуть несколько типов прерываний) и обрабатывать его соответствующим образом. В многовекторном режиме каждый тип прерывания вызывает свой ISR. MVEC-бит в регистре INTCON определяет режим. В любом случае, система прерываний MIPS должна быть включена с командой EI, прежде чем она будет принимать какие-либо прерывания. PIC32 также позволяет каждому источнику прерываний иметь настраиваемый приоритет и субприоритет. Приоритет выставляется в диапазоне 0–7, где 7 – наивысший приоритет. Прерывание с более высоким приоритетом приостановит обработку прерывания, которое имело место в текущий момент. 

![](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/аналог.PNG) Рис.9

Многие встроенные системы нуждаются в аналоговых входах и выходах для взаимодействия с миром. Они используют аналого-цифровые преобразователи (АЦП) для квантования аналоговых сигналов в цифровые значения и цифроаналоговые преобразователи (ЦАП), чтобы сделать обратное.На Рис.9 показаны условные графические обозначения для этих компонентов. Такие преобразователи характеризуются разрешением, динамическим диапазоном, частотой дискретизации и точностью.

![](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/жк.PNG) Рис.10

Микроконтроллеры часто взаимодействуют с другими внешними периферийными устройствами. В этом разделе приведены различные распространенные примеры таких устройств, в том числе символьные жидкокристаллические дисплеи (LCD), VGA мониторы, беспроводные линии Bluetooth и управление двигателем.Символьный ЖК-дисплей – небольшой жидкокристаллический дисплей, способный показывать одну или несколько строк текста. Они широко используются в передних панелях приборов, таких как кассовые аппараты, лазерные принтеры и факсы, которые должны отображать лишь ограниченное количество информации. Они легко взаимодействуют с микроконтроллером через параллельный интерфейс, RS-232 или SPI.

![](https://github.com/KatyaEvdokimova/I-O-subsystem/blob/main/подкл.PNG) Рис.11

На Рис. 11 показан ЖК-дисплей, соединенный с PIC32 через параллельный 8-битный интерфейс. Логика у него работает на 5 В, но совместима с 3,3В входными сигналами от PIC32. Контрастность ЖК-дисплея устанавливается вторым напряжением, производимым с помощью потенциометра; как правило, экран наилучшим образом читается в диапазоне напряжений 4,2–4,8 В. ЖК-экран получает три управляющих сигнала: RS (1 – для символов, 0 – для команды), R/W (1 читать с дисплея, 0 записать) и E (поднимаемый до высокого уровня, по крайней мере, на 250 нс для того, чтобы включить ЖК-дисплей, когда следующий байт будет готов). Когда читается команда, бит 7 возвращает флаг занятости, указывая 1, если ЖК-экран занят, и 0, когда он готов принять еще одну команду.
Более гибкий вариант – управлять монитором компьютера. Стандарт монитора Video Graphics Array (VGA) был введен в 1987 году для компьютеров IBM PS/2, с разрешением 640 × 480 пикселей на электронно-лучевой трубке (Cathode Ray Tube, CRT) и 15-контактным разъемом, передающим цветовую информацию с помощью аналоговых напряжений. Современные ЖК-мониторы имеют более высокое разрешение, но остаются обратно совместимы со стандартом VGA.
