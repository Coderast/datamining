***URL***: https://www.kaggle.com/uciml/mushroom-classification

## Описание:
Датасет представляет из себя данные о грибах, о их размерах, цветах, формах, деталях и съедобности
Кол-во: 8 124

##### Есть следующие поля у записей (всего их 23):
* class - съедобный или ядовитый
* cap-shape - форма шляпки
* cap-surface - поверхность шляпки
* cap-color - цвет шляпки
* bruises - гнилость
* odor - запах
* gill-attachment - вид крепления жабр
* gill-spacing - вид отступов жабр
* gill-size - размер жабр
* gill-color - цвет жабр
* stalk-shape - форма ножки
* stalk-root - основание ножки
* stalk-surface-above-ring - поверхность ножки над кольцом
* stalk-surface-below-ring - поверхность ножки под кольцом
* stalk-color-above-ring - цвет ножки над кольцом
* stalk-color-below-ring - цвет ножки под кольцом
* veil-type - тип вуали
* veil-color - цвет вуали
* ring-number - количество колец
* ring-type - тип колец
* spore-print-color - цвет спор
* population - вид популяции
* habitat - место обитания

## Формулировка задачи:
Обучить модель, которая получая на вход данные сможет кластеризировать выборку на съедобные и не съедобные
Для этого будет выкинуто поле `class`

В ходе анализа данных для их подготовки поля были выделены в следующие группы:

##### Удалить:
* veil-type - везде один тип
* class - признак класстера
##### Заменить на категорию (dummy кодирование):
  _Все остальные_

## Итог работы
В ходе работы было испытано 3 вида класстеризации:
* K-means
* Agglomerative
* DBSCAN

В качестве метрик использовались:
* Adjusted Rand Index
* Adjusted Mutual Information
* Силуэт

Результат:
* K-means:
  * ARI - 0.6298873430993006
  * AMI - 0.592469785867801
  * Силуэт - 0.15813269373129735
  
* Agglomerative:
  * ARI - 0.6089520723199133
  * AMI - 0.593595052914013
  * Силуэт - 0.15611389457343575
  
* DBSCAN:
  * ARI - 0.27406861564247237
  * AMI - 0.4468071843599488
  * Силуэт - 0.2776880539870809

Отсюда мы видим, что K-means показал себя лучше по показателям ARI и AMI, однако показатель Силуэта оказался лучше у DBSCAN
