# Домашние задания по курсу «Виртуализация, базы данных и Terraform»

## Задача 1 - Выберете использования виртуальных машин  / докер контейнера или физического сервера / пк для конкретного сценария. Мотивируйте свой выбор.

Cценарии:

- Высоконагруженный централизованный кластер Oracle, содержащий базы данных для всей организации
- Сервер для нагрузочного тестирования
- Билд агент Jenkins
- Продуктивный сервер системы риск мониторинга карточного процессинга с высокими требованиями к ОЗУ и ресурсам процессора 
- Продуктивная база Postgre SQL
- Дев сервер для tomcat java web приложения 
- Продуктивная система управления артефатами Nexus / Artifactory, задейтсвованная в процессе CI/CD
- Веб сервер для статического веб сайта - html / css 

## Задача 2 - Детально опишите сценарий миграции инфраструктуры с физических серверов на виртуальные машины 

Необходимо описать два сценария - миграция на виртуальные машины в Hyper-v или VMWare и второй сценарий - миграция на AWS ЕС2 / Azure virtual machines. Можно использовать графические и тестовые представления для описания, а также комбинированный подход. 

Описание инфраструктуры:

Продуктивные сервера для легаси системы -

4  - (2 основных, 2 колд реплики )Сервера приложений для программного продукта на базе java 4
2 сервера для создания и хранения резервных копий
Два сервера баз данных Sybase - основной и реплика

Тестовые и демо сервера для нового поколения ПО -

Kubernetes кластер - 3 ноды 


Инфраструктура разработки -

Jenkins сервер и 10 агентов
Gitlab community 
Jira plus Confluence 
Sonatype nexus 

Инфраструктура для вспомогательных систем -

Сервер 1С
Сервер SAP 
Сервер баз данных MS SQL для 1С
Сервер Jasper reports 