# SearchEngine
Программа для поиска текстового запроса по проиндексированным сайтам из конфигурационного файла, основными функциями которой являются:
* предварительная индексация сайтов - движок обходит все страницы сайтов, которые заданы   
  в файле конфигурации, и создаёт индексы на основе лемм, найденных на страницах
* вывод статистики - общее кол-во сайтов, страниц и лемм, подробная информация   
  о состоянии сайта во время/ после индексации
* поиск по ключевым словам и вывод страниц по релевантности
#### Особенности поиска:
* для поиска по сайтам(у) необходимо чтоб все сайты (или один сайт по которому планируется осуществить поиск)
   были проиндексированы, то есть должны иметь статус **INDEXED**
* завершить индексацию сайтов (перевести в статус **INDEXED**) можно дождавшись конца парсинга страниц, или остановить вручную, нажав кнопку STOP
* поиск выдает результаты начиная с полного совпадения по фразе (если такое найдено), далее располагаются совпадения по леммам от наиболее часто встречающихся к менее
* поиск является регистронезависимым
***
## Краткий обзор
### Вкладка Dashboard
На странице отображается подробная статистика по сайтам в статусах:
1. **INDEXING** - идёт индексация
2. **INDEXED** - индексация завершена без ошибок
3. **FAILED** - произошла ошибка
### Вкладка Management
Отображаются элементы управления обработкой сайтов.
* **START INDEXING** - запуск индексации по всем сайтам
* **STOP INDEXING** - остановка индексации, появляется только после запуска
* **Add/update page** - добавление или обновление отдельной страницы
### Вкладка Search
Страница для поиска слов или фраз на страницах проиндексированных сайтов
***
## Стек технологий
* Java 17
* Maven
* Spring Boot
* MySQL 8
* Hibernate
* Lombok
* Jsoup

***
## Локальный запуск проекта
1. Установите СУБД MySQL и создайте БД *search_engine*
2. В файле конфигурации *application.yml* укажите
    * url и название сайтов в параметре *indexing-settings*
    * пользователя и пароль для БД
3. Для доступа к библиотекам лемматизатора необходимо указать токен:  
   Найдите или создайте файл *settings.xml*
    * В Windows он располагается в директории C:/Users/<Имя вашего пользователя>/.m2
    * В Linux — в директории /home/<Имя вашего пользователя>/.m2
    * В macOs — по адресу /Users/<Имя вашего пользователя>/.m2
    

    Если файла *settings.xml* нет, создайте и вставьте в него:  
</b></details>
<details>
<summary> settings.xml </summary><br><b>

```xml  
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
https://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>skillbox-gitlab</id>
            <configuration>
                <httpHeaders>
                    <property>
                        <name>Private-Token</name>
                        <value>wtb5axJDFX9Vm_W1Lexg</value>
                    </property>
                </httpHeaders>
            </configuration>
        </server>
    </servers>
</settings>
```
</b></details>
Если файл уже есть, то добавьте только блок *server* в *servers*

4. Веб-интерфейс запущенного приложения будет доступен на http://localhost:8080/