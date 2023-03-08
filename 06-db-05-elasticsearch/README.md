# Домашнее задание к занятию "6.5. Elasticsearch"

## Задача 1

В этом задании вы потренируетесь в:
- установке elasticsearch
- первоначальном конфигурировании elastcisearch
- запуске elasticsearch в docker

Используя докер образ [centos:7](https://hub.docker.com/_/centos) как базовый и 
[документацию по установке и запуску Elastcisearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/targz.html):

- составьте Dockerfile-манифест для elasticsearch
- соберите docker-образ и сделайте `push` в ваш docker.io репозиторий
- запустите контейнер из получившегося образа и выполните запрос пути `/` c хост-машины

Требования к `elasticsearch.yml`:
- данные `path` должны сохраняться в `/var/lib`
- имя ноды должно быть `netology_test`

В ответе приведите:
- текст Dockerfile манифеста
- ссылку на образ в репозитории dockerhub
- ответ `elasticsearch` на запрос пути `/` в json виде

Подсказки:
- возможно вам понадобится установка пакета perl-Digest-SHA для корректной работы пакета shasum
- при сетевых проблемах внимательно изучите кластерные и сетевые настройки в elasticsearch.yml
- при некоторых проблемах вам поможет docker директива ulimit
- elasticsearch в логах обычно описывает проблему и пути ее решения

Далее мы будем работать с данным экземпляром elasticsearch

![изображение](https://user-images.githubusercontent.com/89098193/223233507-de89c712-a3bd-4b2b-9292-535977419da9.png)

![изображение](https://user-images.githubusercontent.com/89098193/223233546-dc9b39c1-9b3f-4d8a-9f31-7e26c4926975.png)


https://hub.docker.com/r/toto20002/elasticsearch/tags


## Задача 2

В этом задании вы научитесь:
- создавать и удалять индексы
- изучать состояние кластера
- обосновывать причину деградации доступности данных

Ознакомтесь с [документацией](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html) 
и добавьте в `elasticsearch` 3 индекса, в соответствии со таблицей:

| Имя | Количество реплик | Количество шард |
|-----|-------------------|-----------------|
| ind-1| 0 | 1 |
| ind-2 | 1 | 2 |
| ind-3 | 2 | 4 |

![изображение](https://user-images.githubusercontent.com/89098193/223827925-ac81617f-3aaa-44a2-8f54-d6a689a92c3a.png)


Получите список индексов и их статусов, используя API и **приведите в ответе** на задание.

![изображение](https://user-images.githubusercontent.com/89098193/223828054-3e02b584-b7a3-41c8-854b-97fdd6548afe.png)

Получите состояние кластера `elasticsearch`, используя API.

![изображение](https://user-images.githubusercontent.com/89098193/223828176-4a2b296a-04db-4954-92c8-9272a0a5d7a9.png)

Как вы думаете, почему часть индексов и кластер находится в состоянии yellow?

Потому что в кластере всего один узел, для индексов созданы реплики, но привязать их некуда.

Удалите все индексы.

![изображение](https://user-images.githubusercontent.com/89098193/223828125-0a9c8c3f-d0f4-42e2-ac64-811b81173f8d.png)


**Важно**

При проектировании кластера elasticsearch нужно корректно рассчитывать количество реплик и шард,
иначе возможна потеря данных индексов, вплоть до полной, при деградации системы.

## Задача 3

В данном задании вы научитесь:
- создавать бэкапы данных
- восстанавливать индексы из бэкапов

Создайте директорию `{путь до корневой директории с elasticsearch в образе}/snapshots`.

Используя API [зарегистрируйте](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-register-repository.html#snapshots-register-repository) 
данную директорию как `snapshot repository` c именем `netology_backup`.

**Приведите в ответе** запрос API и результат вызова API для создания репозитория.

![изображение](https://user-images.githubusercontent.com/89098193/223829299-513c9e3b-8893-4c7a-9045-a5819e289a30.png)

Создайте индекс `test` с 0 реплик и 1 шардом и **приведите в ответе** список индексов.

![изображение](https://user-images.githubusercontent.com/89098193/223834735-7688afee-e61c-40c4-be43-71a4a84cd107.png)


![изображение](https://user-images.githubusercontent.com/89098193/223834888-785ef41f-a785-4210-8012-7108fafe7881.png)


[Создайте `snapshot`](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-take-snapshot.html) 
состояния кластера `elasticsearch`.

![изображение](https://user-images.githubusercontent.com/89098193/223836849-e5033477-fb6f-424f-8b2b-8487899f80c1.png)


**Приведите в ответе** список файлов в директории со `snapshot`ами.

![изображение](https://user-images.githubusercontent.com/89098193/223831096-4a466685-fcae-4f91-b9aa-44b61a0f0bee.png)

Удалите индекс `test` и создайте индекс `test-2`. **Приведите в ответе** список индексов.

![изображение](https://user-images.githubusercontent.com/89098193/223830939-37d9150c-f201-480e-80d8-6315aef660a6.png)


[Восстановите](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-restore-snapshot.html) состояние
кластера `elasticsearch` из `snapshot`, созданного ранее. 




**Приведите в ответе** запрос к API восстановления и итоговый список индексов.

![изображение](https://user-images.githubusercontent.com/89098193/223830446-0f4d83b6-7b98-487e-9e00-8aa9b13f16a1.png)



Подсказки:
- возможно вам понадобится доработать `elasticsearch.yml` в части директивы `path.repo` и перезапустить `elasticsearch`

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
