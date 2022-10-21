# 📒 Подключение датчиков Vernier к Arduino Uno

- 🪧 Содержание
    
    [1.  Установка библиотеки](https://www.notion.so/Vernier-Arduino-Uno-68befa1ac8fc4eedb7d641f2069749c9) 
    
    [2. Код для работы с датчиками](https://www.notion.so/Vernier-Arduino-Uno-68befa1ac8fc4eedb7d641f2069749c9)
    
    [3. Сборка цепи](https://www.notion.so/Vernier-Arduino-Uno-68befa1ac8fc4eedb7d641f2069749c9)
    
    [4. Конечный результат](https://www.notion.so/Vernier-Arduino-Uno-68befa1ac8fc4eedb7d641f2069749c9)
    

---

Итак, методом научного тыка и долгих мучений мне всё-таки удалось подключить датчики к ардуино. Тут будет (надеюсь понятное) объяснение этого всего.

1. Заходим в Arduino IDE, нам надо установить библиотеку `VernierLib` . Для этого в Arduino IDE тыкаем: `Инструменты/Управление библиотеками` , в открывшимся окне вводим `VernierLib` и нажимаем `Установка` .

![Untitled](%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%BE%D0%B2%20Vernier%20%D0%BA%20Arduino%20Uno%2068befa1ac8fc4eedb7d641f2069749c9/Untitled.png)

> P.S. Как поменять язык написано [тут](https://support.arduino.cc/hc/en-us/articles/4403365287826-Change-the-language-in-Arduino-IDE).
> 

1. После установки библиотеки, копируем вот этот страшный код:

```c++
/* VernierLibTutorialAnalogRead (v2017)
 * This sketch reads a data point from a Vernier Analog (BTA) 
 * sensor once every half second and prints the sensor reading 
 * with units to the Serial Monitor.
 * 
 * Plug the sensor into the Analog 1 port on the Vernier Arduino 
 * Interface Shield or into an Analog Protoboard Adapter wired 
 * to Arduino pin A0.
 */
 
#include "VernierLib.h" //include Vernier functions in this sketch
VernierLib Vernier; //create an instance of the VernierLib library
 
float sensorReading; //create global variable to store sensor reading
 
void setup() {
  Serial.begin(9600); //setup communication to display
  Vernier.autoID(); //identify the sensor being used
}
 
void loop() {
  sensorReading = Vernier.readSensor(); //read one data value
  Serial.print(sensorReading); //print data value 
  // Serial.print("fggbjbjh"); //print a space
  Serial.println(Vernier.sensorUnits()); //print units and skip to next line
  delay(500); //wait half second
}
```

И вставляем его в поле для кода:

![Untitled](%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%BE%D0%B2%20Vernier%20%D0%BA%20Arduino%20Uno%2068befa1ac8fc4eedb7d641f2069749c9/Untitled%201.png)

1. Теперь надо взять и соединить между собой:
    - SparkFun Vernier Interface Shield (дополнение, позволяющее Arduino взаимодействовать с датчиками Vernier)

![Untitled](%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%BE%D0%B2%20Vernier%20%D0%BA%20Arduino%20Uno%2068befa1ac8fc4eedb7d641f2069749c9/Untitled%202.png)

- Плату Arduino Uno

![Untitled](%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%BE%D0%B2%20Vernier%20%D0%BA%20Arduino%20Uno%2068befa1ac8fc4eedb7d641f2069749c9/Untitled%203.png)

- Какой-нибудь аналоговый датчик Vernier (у меня будет датчик света)

![Untitled](%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%BE%D0%B2%20Vernier%20%D0%BA%20Arduino%20Uno%2068befa1ac8fc4eedb7d641f2069749c9/Untitled%204.png)

**Обратите внимание, что Vernier Interface Shield вставляется в Arduino сверху!**

В итоге должно получиться что-то типа этого:

![Untitled](%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%BE%D0%B2%20Vernier%20%D0%BA%20Arduino%20Uno%2068befa1ac8fc4eedb7d641f2069749c9/Untitled.jpeg)

1. После того, как всё соединили, подключаем Arduino к компьютеру и запускаем код. Если всё сделано правильно вылезет вот такая надпись:

![Untitled](%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%BE%D0%B2%20Vernier%20%D0%BA%20Arduino%20Uno%2068befa1ac8fc4eedb7d641f2069749c9/Untitled%205.png)

Чтобы посмотреть показания датчиков нажимаем `Инструменты/Монитор порта` и у нас открывается окно с какими-то циферками, в моём случае это значения, передаваемые датчиком освещённости, в люксах (LX).

![Untitled](%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B0%D1%82%D1%87%D0%B8%D0%BA%D0%BE%D0%B2%20Vernier%20%D0%BA%20Arduino%20Uno%2068befa1ac8fc4eedb7d641f2069749c9/Untitled%206.png)

> P.S. Я надеюсь, что это статья вам точно помогла, поэтому просто необходимо тыкнуть [**сюда**](https://www.tinkoff.ru/rm/savateev.dmitriy12/Jgqwn3240/), ну или [**сюда**](https://yoomoney.ru/to/4100110960641547).
>
