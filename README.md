### Домашнее задание к занятию 3 «Использование Ansible» - Баранов Сергей.


---

### Подготовка к выполнению

Подготовьте в Yandex Cloud три хоста: для clickhouse, для vector и для lighthouse.

### Основная часть

Виртуальные машины `clickhouse`, `vector` и `lighthouse` разворачиваются в Yandex Cloud при помощи Terraform:

[Terraform](/08-ansible-03-yandex/tree/main/terraform_vms) 

---

1. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает lighthouse.
2. При создании tasks рекомендую использовать модули: get_url, template, unarchive, file.
3. Tasks должны: скачать статику LightHouse, установить Nginx или любой другой веб-сервер, настроить его конфиг  
   для открытия LightHouse, запустить веб-сервер.


[site.yml](/08-ansible-03-yandex/blob/main/playbook/site.yml)

---

4. Подготовьте свой inventory-файл prod.yml.

### Ответ:

[prod.yml](/08-ansible-03-yandex/blob/main/playbook/inventory/prod.yml)

---

5. Запустите ansible-lint site.yml и исправьте ошибки, если они есть.

### Ответ:

![monitoring]

---

6. Попробуйте запустить playbook на этом окружении с флагом --check.

### Ответ:

![monitoring]

---

7. Запустите playbook на prod.yml окружении с флагом --diff.

### Ответ:

![monitoring]

![monitoring]

![monitoring]

![monitoring]

![monitoring]

![monitoring]

   Убедитесь, что изменения на системе произведены.

![monitoring]

---

8. Повторно запустите playbook с флагом --diff и убедитесь, что playbook идемпотентен.

### Ответ:

![monitoring]


![monitoring]


---

9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги. 

### Playbook

Playbook производит установку и настройку приложений для сбора, передачи и отображения логов на стэк  
серверов `clickhouse`, `vector` и `lighthouse`. Первый play объединяет последовательность задач по  
инсталяции Clickhouse. Блоку соответствует тэг `clickhouse`. Второй play объединяет последовательность  
задач по инсталяции Vector. Блоку соответствует тэг `vector`. Третий play объединяет последовательность  
задач по инсталяции Lighthouse. Блоку соответствует тэг `lighthouse`.

## Variables

Значения переменных устанавливаются в файлах `vars.yml` в соответствующих директориях в `group_vars`.  
При помощи них задаются следующие параметры:
- `clickhouse_version`, `vector_version` - версии устанавливаемых приложений;
- `clickhouse_database_name` - имя базы данных в `clickhouse`;
- `clickhouse_create_table_name` - имя таблицы в `clickhouse`;
- `vector_config` - содержимое конфигурационного файла для приложения `vector`;
- `lighthouse_home_dir` - домашняя директория `lighthouse`;
- `nginx_config_dir` - директория расположения конфига `nginx`.

## Tags

Тэг `ping` - проверяет доступность серверов `clickhouse-01`,`vector-01`,`lighthouse-01`;
тэг `clickhouse` - позволяет производить отдельную настройку приложения `clickhouse`;
тэг `vector` - позволяет производить отдельную настройку приложения `vector`;
по тэгу `vector_config` - возможно производить изменение в конфиге приложения `vector`;
тэг `lighthouse` - позволяет производить отдельную настройку приложения `lighthouse` на одноименных серверах.

---

10. Готовый playbook выложите в свой репозиторий, предоставьте ссылку на него.

### Ответ:

[Playbook]/08-ansible-03-yandex/tree/main/playbook)

---




