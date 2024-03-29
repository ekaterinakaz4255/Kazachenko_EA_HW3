# Домашнее задание 3

## Задачи:

Вам нужно проанализировать [биоинформатический датасет](https://lms.skillfactory.ru/asset-v1:SkillFactory+MFTIBIO+SEP2023+type@asset+block@community_dataset.csv) по пространственной транскриптомике ([дополнительная информация по теме](https://institut-curie.org/popin/spatial-omics)) пациентов с плоскоклеточным раком. В нем клетки (колонка ```cell_type```) объединены в микроокружения (колонка ```cell_interaction```) в зависимости от взаимодействия этих клеток. Вашей основной задачей будет поиск отличий в организации микроокружения у пожилых и молодых пациентов (колонка ```age_group```).

### Также в датасете есть следующие колонки:

 - ```distance_to_vasculature``` — расстояние до ближайших сосудов;
 - ```distance_to_largest_cell``` — расстояние до ближайшей крупной клетки;
 - ```immune_marker_1``` — экспрессия иммунного маркера 1 в данной клетке;
 - ```immune_marker_2``` — экспрессия иммунного маркера 2 в данной клетке;
 - ```cell_type``` — тип клетки;
 - ```area_of_cell``` — размер клетки;
 - ```case_id``` — уникальный ID пациента.

### Вам необходимо:

В ноутбуке проанализировать датасет и сделать статистически обоснованные выводы. Ограничения в использовании библиотек/функций: нет, при желании можно воспользоваться ```pandasql``` для обработки данных. Не забывайте про **PEP8**. Ответы в виде графиков со стат-значимостью на них тоже считаются правильным ответом, не забывайте обосновывать применимость стат-теста. 

## Задачи:

### 1) Есть ли стат-значимость между типом клетки и:

а) Размером клетки (```area_of_cell```), добавьте ```hue``` по возрастным группам.

б) Экспрессией иммунных маркеров (```immune_marker_1```, ```immune_marker_2```), добавьте ```hue``` по возрастным группам.

в) Дистанцией до ближайших объектов (```distance_to_vasculature```, ```distance_to_largest_cell```), добавьте ```hue``` по возрастным группам.

В качестве ответов можно приводить ```box_plot/swarplot```, где по одной оси будет тип клеток, а по другой — оцениваемая вами статистика.

### 2) В каком клеточном микроокружении клеток какого типа статистически больше, чем в других микроокружениях? (колонка ```cell_interaction```). Для ответа используйте ```box_plot/swarplot``` с ```hue``` по микроокружениям, где:

 - по Ох будут типы клеток,
 - по Оу — их количество.

*Не забудьте посчитать количество для каждого пациента отдельно, иначе выборка не будет репрезентативной.*

### 3) Есть ли разница в доле микроокружения в тканях пациентов разных возрастов? Для ответа используйте ```box_plot/swarplot``` с ```hue``` по возрастным группам, где:

 - по Ох будут микроокружения,
 - по Оу — их доля в ткани пациента.

*Не забудьте посчитать доли для каждого пациента отдельно, иначе выборка не будет репрезентативной.*

### 4) Правда ли, что иммунные клетки (```Immune type 1``` и ```Immune type 2```) лежат ближе к сосудам и крупным клеткам (Обе колонки ```distance```), чем стромальные клетки (```Stroma cells```) у молодых, но не у пожилых пациентов? 

Эту гипотезу нужно проверить бутстрапом (как разницу средних для двух выборок).

### 5) Правда ли, что иммунные клетки в среднем лежат ближе к сосудам у молодых, но не у пожилых пациентов? 

Эту гипотезу необходимо проверить пермутационным тестом. В качестве исходной статистики берем массив с расстояниями только для данного типа клеток (длина - ```n```), запоминаем среднее для каждого пациента. На каждой итерации набираем выборку размером ```n``` из всей! колонки с расстояниями до сосудов и смотрим соотношение с исходной статистикой. Проверяем гипотезы. Комбинировать p-values для каждой возрастной группы можно с помощью этого инструмента.

## В каком формате прислать результат:

Ссылка на Github с ноутбуком или ссылка на ваш Colab с решениями (не колаб преподавателя).

## Критерий оценки результата:
### Критерий 1. Правильность решения.

Правильность решения (за каждую задачу — 2 балла). Необходимо убедиться, что данные обработаны верно, выдача соответствует условию задачи. В первых двух заданиях необходимо проконтролировать, что собиралась статистика для каждого пациента, а результирующий график включает в себя данные по всем пациентам. Измененная задача/текст или условия задачи/assert == -3 балла за задачу.

 |  |  |
|:------------|:-----------:|
| Задача решена верно (всего 5 задач)        | 2 балла (все задачи решены верно — 10 баллов)       |
| Ошибка в выборе статистического теста       | 2 балла за задачу (при условии, что всё остальное верно)       |
| Задача решена неверно (Используются неверные выборки, ошибка в расчетах, перепутаны выборки и т.д.)       | 0 баллов       |
| Задача решена почти верно, есть минорные ошибки. Либо правильно выбран стат-тест, либо правильно сформирована выборка.       | 1 балл


 ### Критерий 2. Правильность оформления решения по PEP8 (старайтесь подтягивать в сторону повыше).

 |  |  |
|:------------|:-----------:|
| Код красивый и правильный, есть несколько мелких помарок        | 10 баллов       |
| Нарушения PEP8 примерно в 20% случаев       | 8 баллов       |
| Нарушения PEP8 примерно в 50% случаев       | 5 баллов       |
| PEP8 нет       | 0 баллов       |

# Дополнительные баллы

Обратите внимание, что доп баллы будут выставлены в ведомости, но не отображаются на платформе.

1. Подробное описание результатов анализа и сделанных на их основе выводов. Описание результатов и выводов должно быть понятным и связанным с целью исследования. Ваши выводы должны отражать результаты статистического анализа и позволять сделать осмысленные заключения о наличии или отсутствии статистически значимых различий в исследуемых группах. — **1 балл.**

2. Оценка значимости и величины эффектов, а не только проверка наличия статистически значимых различий. Оценка значимости и величины эффектов позволяет более глубоко проанализировать результаты исследования, определить практическую значимость различий и сделать осмысленные заключения на основе полученных данных.  — **1 балл.**

3. Описание ограничений проведенного анализа и возможных улучшений. Проанализируйте и объясните ограничения, которые могут оказывать влияние на полученные результаты и интерпретацию данных. Предложите конкретные способы улучшить проведенный анализ и минимизировать ограничения.  — **1 балл.**
