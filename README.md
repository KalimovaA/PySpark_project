# PySpark_project
Разработка одного из типовых процессов для банковского хранилища - построение зеркал.

Зеркало - это таблица в сыром или детальном слое, в которой содержится последнее (актуальное) состояние каждой еë сущности (записи/строки). То есть, если 3 раза запускался процесс загрузки, который выделял дельту и в каждой такой дельте была одна и так же сущность (какой-то один счëт), у которой менялись вторичные параметры - то в зеркале должна остаться одна строка с последним состоянием, каждого из вторичных параметров.

Данный механизм создан универсальным - в него передаются:  путь где хранятся дельты, наименование таблицы и список полей, являющийся уникальным ключом. 
Дельты в директории "data_deltas" всегда хранятся в виде вложенных директорий с наименованием в порядке возрастания (например: 1000, 1001…..). Каждая дельта - это csv-файл внутри директории с наименованием id-дельты.

Итоговый результат сохранëн в csv-файл в директории «mirr_md_account_d».
В механизм добавлен процесс логирования, что бы не обрабатывать повторно, ранее загруженные дельты - это будет экономить время и ресурсы сервера.
Логи в отдельной директории "logs" с файлом csv формата. В нем содержится информация с датой-время старта и завершения загрузки каждой из дельт, а также наименование обновляемой таблицы.
