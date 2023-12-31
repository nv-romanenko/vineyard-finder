Vineyards Finder
==
Проект моей производственной практики, небольшой скрипт, который для заданного прямоугольного участка местности находит 
список виноградников путем запроса с помощью [Overpass API](https://wiki.openstreetmap.org/wiki/Overpass_API) и генерирует спутниковое изображение 
для каждого из них, с помощью Selenium Webdriver заходя на [Bing Maps](https://www.bing.com/maps) и делая скриншот контейнера-карты (кустарно, правда?).

Зависимости
--
Для работы скрипта необходимы библиотеки [overpass](https://github.com/mvexel/overpass-api-python-wrapper), selenium и webdriver, поэтому перед выполнением
нужно их установить командой:  
`pip install overpass selenium webdriver`

Принцип работы
--
Участок местности, на котором нужно найти виноградники, задается прямоугольником вида: левая сторона - западная граница области поиска, нижняя - южная,
правая - восточная, верхняя - северная соответственно. Эти границы в виде координат передаются как входные данные. Для заданного участка получается список координат виноградников
в виде пар *широта, долгота*. В ходе работы список сохраняется как файл __vineyards_coordinates.csv__. Далее происходит запуск браузера с помощью драйвера и последовательно для каждой пары
координат находится и фотографируется спутниковое изображение в картографическом сервисе. Все скриншоты сохранятся в подпапке __screenshots__.

Запуск скрипта
--
Скрипт запускается из командной строки следующим образом:  
`python main.py запад юг восток север браузер`  
где `запад юг восток север` - вещественные числа в диапазоне от -90 до 90 для широты, от -180 до 180 для долготы  
`браузер` - название браузера (в данный момент поддерживаются `Chrome` и `Firefox`)
#### Пример
Положим, необходимо заполучить снимки виноградников в окрестностях г. Тамань; в качестве рабочего браузера используется Firefox. Запускается скрипт следующей командой:  
`python main.py 45.154126 36.634410 45.221860 36.749966 Firefox`

Дополнительно
--
Я далеко не самый лучший кодер, и скрипт написан и работает кривовато: например, на скриншотах присутствуют элементы UI, которые не дадут использовать 
полученную выборку в качестве обучающей для
нейронной сети. Поэтому я буду рад любым предложениям по улучшению этого скрипта :blush:
