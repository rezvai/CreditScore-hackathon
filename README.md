# Хакатон от Альфабанка AlfaHack 1.11.2024 - 12.11.2024 
На данном хакатоне был выбран кейс по кредитному скорингу юредических лиц на основе предоставленных данных.

## Участники команды(телеграмм)

**Artem** - @artemrabov_ds

**Ilya** - @ikoryaev

**Kirill** - @KirillAlv

**Aleksander** - @OnFirstSight

**Vadim** - @JetstreamSamTBR

## Файловая структура

- metrics - папка, содержащая в себе метрики обученных катбустов

- models - папка, содержащая в себе сохраненный модели обученных катбустов

- submissions - папка, содержащая в себе сохраненные csv файлы решений на test выборке

- solution - ноутбук, с разбивкой на этапы решения задачи

## Решения и их метрики

Лучшей метрикой от команды оказалось рофляное решение в виде одного радномного катбуста, который показал на лидерборде метрику 79.73

В дальнейшем данный результат перебить не получилось.

Были применены другие варианты решениея:

1. Ансамбль с усреднением ответов от моделей CatboostClassifier

2. Ансамбль с усреднением ответов от моделей CatboostClassifier с мета-моделью LogisticRegressor

3. Ансамбль с усреднением ответов от моделей CatboostClassifier с мета-моделью CatboostRegressor

4. Ансамбль с усреднением ответов от моделей CatboostClassifier с мета-моделью CatboostClassifier

5. Ансамбль с усреднением ответов от моделей CatboostClassifier с мета-моделью из ансамбля - RandomForest, LogisticRegressor, GradientBoostingRegressor

6. Ансамбль с усреднением ответов от моделей CatboostClassifier поверх ансамбля выступила модель LogisticRegressor, а сверху была запихнута нейронная сеть

Помимо этого был какой-то аномальный ответ, на тестовой выборке, полученной из train получился score 90, а на лидерборде 78. Хотя была замечена закономерность, что расход в метриках между проверкой локально и на лидерборде составляет 3 очка, данный момент был очень странный.

Кроме сбора разных моделей, была попытка очистки данных от выбрсоов\мультиколлинеарности, стало понятно, что решения, в которых осутствуют признаки с VIF(коэффициент инфляции дисперсии) выше 10 стоит отбрасывать, тогда метрики получаются больше. Также были попытки по избавлению от признаков с VIF(коэффициент инфляции дисперсии) больше 5, но метрики упали и мы решили оставить выборку с удаленными признаками по VIF > 10.