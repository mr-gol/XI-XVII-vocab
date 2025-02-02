**Директории**

* База данных оказалась слишком большой, чтобы загрузить ее на гитхаб, поэтому ту ее версию, с которой разрабатывался и редактировался сайт, можно скачать по ссылке на диск: https://drive.google.com/file/d/1fdNCaqjJHIxtGACeOjAB69BHI0nLmtFP/view?usp=sharing

* Дополненная БД (включающая данные 28-31 томов) лежит здесь: https://drive.google.com/file/d/1e99MpwG5K8fGykRN5vKsdYerNxN6qcLO/view?usp=sharing 
  
Файл Dictionary_Final.db стоит добавить в папку flask/rus_dict/Database. В дальнейшем дополненной версией базы можно просто заметить этот файл в папке. 

* В папке *flask* находятся файлы, нужные для запуска докера, а так же папка *rus_dict* — в ней лежит весь код.
* В *rus_dict*:
  * В папке *templates* лежат html-файлы для всех страниц сайта, а так же аналогичные им на английском языке.
  * В файле *backend.py* лежит код функций, в файле *app.py* — основной код. Код для аналогичных страниц на русском и английском языке в файле *app.py* находится рядом.



**Логика функций backend.py:**

по необходимым параметрам подключаются таблицы, все условия соединяются через AND
* функция для создания JOIN части sql запроса - `join_search_tables(params)`
* функций для создания WHERE части sql запроса - `join_search_conditions(conds)`
* функция для поиска заглавных слов по созданному запросу - `search_query(tables, conditions)`
* функция для поиска текста для конкретного слова - `load_page(word)`
* функция для поиска по жанрам источника - `resource_genre(param)` 

на вход мы получаем список списков, где каждый элемент `[имя_заполненного_поля, [значение]]` или `[имя_заполненного_поля, [значение_1, значение_2, и т.д.]]` для параметров со множественным выбором
имя_заполненного_поля состоит из имени общего параметра и конкретного признака.
`source_name` = в источниках смотрим название
`example_date_start_y` = в примерах смотрим раннюю дату в годах

`join_search_tables(params)`
1. имеет список соответствия общего параметра в названии условия поиска и конкретных таблиц, необходимых для поиска
2. в соответствии со списком добавляет необходимые таблицы без повторений
3. возвращает строку `"JOIN.... JOIN..."`

`join_search_conditions(conds)`
1. имеет список соответствия условия поиска и конкретного поискового запроса WHERE, учитывает множественность выбора
2. склеивает запросы в один
3. возвращает строку `"WHERE ... AND ..."`

`search_query(search_tables, conditions)`
1. склеивает все в один запрос и ищет
2. выдает список `[head_word, head_word, head_word]` без повторений, если встретились

`load_page(word)`
1. принимает конкретное слово head_word из списка, составленного ранее
2. возвращает список из `full_text` для слова

т.к. некоторые поиски состоят из нескольких, как поиск по жанру источника, такие поиски будут отдельной функцией
`resource_genre(param)` - поиск по жанрам источников


**Запуск докера**


Запуск из папки flask где 

docker-compose.yml:

docker-compose down && docker-compose build --no-cache && docker-compose up -d

Сайт по адресу: http://127.0.0.1:15555


**Upd:**

Добавлено разное форматирование текста на странице со словарными статьями.





