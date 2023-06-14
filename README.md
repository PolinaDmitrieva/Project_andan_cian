# Исследование рынка новостроек в Москве:house: 
Проект создан с целью проанализировать рынок первичного жилья в Москве и выявить факторы, наиболее влияющие на стоимость жилья.   


Планируется анализ признаков, выдвижение гипотез и их проверка, на основе чего будет создана модель, предсказывающая стоимость квартир в новостройках в Москве. 
____
## `Сбор данных`
> [parcing_cian_1.ipynb](https://github.com/PolinaDmitrieva/Project_andan_cian/blob/main/parcing_cian_1.ipynb)

Парсинг данных проводился с сайта циан с использованием библиотеки selenium. В результате удалось получить 18 признаков и 1356 объявлений о продаже. В качестве целевой переменной используется цена квартиры, либо цена квадратного метра, если для анализа будет необходимо минимизировать влияние площади.

## `EDA, визуализация полученных данных и работа с пропусками` 
> [eda_cian_2.ipynb](https://github.com/PolinaDmitrieva/Project_andan_cian/blob/main/eda_cian_2.ipynb)

В ходе исследования рассмотрены такие признаки как: 
 - `Округ` - округ Москвы, в котором расположена квартира
 - `Ближайшая станция метро` - ближайшая станция метро, рядом с которой расположен ЖК
 - `Время до метро` - кратчайшее время пешком до метро
 - `Метро рядом` - количество станций метро расположенных в пешей доступности
 - `Застройщик` - застройщик дома
 - `ЖК` - жилой комплекс, в котором расположена квартира
 - `Класс` - класс жилья (премиум - класс, бизнес - класс, комфорт - класс)
 - `Тип квартиры` - тип жилплощади (квартира, апартаменты, студия, студия - апартаменты)
 - `Этаж` - этаж, на котором расположена квартира
 - `Этажей в доме` - количеств этажей в доме
 - `Отделка` - тип отделки квартиры (без отделки, чистовая, предчитовая и тд)
 - `Количество комнат` - количество комнат в квартире
 - `Площадь квартиры` - суммарная площадь квартиры
 - `Жилая площадь` - жилая площадь из всей площади квартиры
 - `Площадь кухни` - площадь кухни
 - `Тип дома` - из чего сделан дом
 - `Парковка` - наличие и вид парковки 
 - `Год сдачи` - когда был сдан или будет 
 
 __Целевая переменная__ - `Цена квартира`, так же в ходе анализа было принято решение рассмотреть альтернативную целевую переменную - `Цена за квадратный метр` для случаев, когда необхоимо выявить закономерности не связанные с квадратурой 
 
 ## `Создание новых признаков`
 > [new_features.ipynb](https://github.com/PolinaDmitrieva/Project_andan_cian/blob/main/new_features.ipynb)

1.Из такой характеристики, как Ближайшая станция метро мы могли бы узнать, находится ли квартира в пределах Московской Кольцевой Автомобильной Дороги (МКАД): обычно недвижимость за пределами МКАДа стоит намного дешевле.

2.Также было предположение оценить близость квартир к последнему этажу (чем выше этаж, тем красивее вид). Но здесь мы пришли к выводу о том, что при непропорциональном распределении этажей в здании достаточно сложно определить, с какого именно этажа начинает открываться так называемый "красивый вид", ведь кому-то хочется видеть двор, кому-то — крыши домов, а кому-то нравится смотреть на облака. Создание данного признака было также отвергнуто.

3.Третьей из предполагаемых новых характеристик стало отношение Жилая площадь к Площадь квартиры: с ее помощью можно было бы предположить, какая часть квартиры реально пригодна для жилья.
## `Тестирование гипотез`
> [hypotheses_cian_3.ipynb](https://github.com/PolinaDmitrieva/Project_andan_cian/blob/main/hypotheses_cian_3.ipynb)

Исходя из EDA и визуализаций, нами были выдвинуты следующие гипотезы:
1. Квартиры на первом и последнем этажах в среднем дешевле, чем остальные
2. Цена за квадратный метр квартиры распределена нормально
3. Квартиры в высотках дороже
4. В высотках квартиры премиум и бизнес класса
5. В ЦАО квартиры премиум и бизнес класса
6. Разброс цен на квартиры не зависит от округа
7. Средние цены на апартаменты/апартаменты-студии равны ценам на другие типы квартир
8. В среднем цены на обычные квартиры и апартаменты равны
9. Квартиры с чистовой отделкой в среднем стоят столько же, сколько и без отделки

## `Машинное обучение`
> [ML_cian_4.ipynb](https://github.com/PolinaDmitrieva/Project_andan_cian/blob/main/ML_cian_4.ipynb)

В качестве задачи машинного обучения была выбрана регрессия, с помощью которой мы построили ряд моделей для предсказания цен на новостройки в Москве.
В рамках нашего исследования были построены следующие модели:
- Lasso - регрессия
- Ridge - регрессия
- Случайный лес
- Градиентный бустинг
- XGBoost
