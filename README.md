# Ansible Role: Vector


Роль Ansible для установки и настройки [Vector](https://vector.dev) - высокопроизводительного конвейера данных наблюдаемости.<br>
Эта роль устанавливает Vector из официального репозитория APT, инсталлирует его, настраивает на пересылку логов в базу данных ClickHouse и обеспечивает работу службы Vector.


## Requirements

- Целевые хосты должны поддерживать менеджер пакетов APT (например, Debian, Ubuntu).
- Для получения репозитория и пакетов Vector необходим доступ в Интернет на целевых узлах.

## Role Variables

Все переменные можно переопределить в `host_vars`, `group_vars` или при вызове роли.

| Переменная             | Описание                                 | Значение по умолчанию                             |
| ---------------------- | ---------------------------------------- | ------------------------------------------------- |
| `vector_config_path`   | Путь к конфигурационному файлу Vector    | `/etc/vector/vector.toml`                         |
| `clickhouse_database`  | Название базы данных ClickHouse          | `logs`                                            |
| `clickhouse_table`     | Название таблицы ClickHouse              | `system_logs`                                     |
| `clickhouse_http_host` | IP-адрес или hostname ClickHouse-сервера | `{{ hostvars['db-clickhouse']['ansible_host'] }}` |
| `clickhouse_http_port` | Порт HTTP-интерфейса ClickHouse          | `8123`                                            |


## Dependencies

Нет внешних зависимостей от других ролей.

## Example Playbook

```yaml
- hosts: vector
  roles:
    - role: vector-role
      vars:
        clickhouse_database: logs
        clickhouse_table: system_logs
        clickhouse_http_host: "{{ hostvars['db-clickhouse']['ansible_host'] }}"
```

