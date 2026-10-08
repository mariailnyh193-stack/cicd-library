# go-build

Компонент для сборки, линтинга и тестирования Go-приложения.

## Что делает

- Собирает бинарник через `go build`.
- Запускает `golangci-lint`.
- Запускает `go test` с race-детектором и покрытием.

## Inputs

| Input | Тип | Default | Описание |
|---|---|---|---|
| `stage` | string | `build` | Стадия для всех трёх джоб |
| `go-version` | string | `1.23` | Тег образа `golang` |
| `binary-name` | string | `app` | Имя выходного бинарника |
| `main-path` | string | `.` | Путь к main-пакету |
| `golangci-lint-version` | string | `v1.62.2` | Тег образа golangci-lint |
| `go-flags` | string | `` | Доп. флаги (`-mod=vendor` и т.п.) |
| `test-command` | string | `go test -race -covermode=atomic -coverprofile=coverage.out ./...` | Команда тестов |
| `tags` | array | `[]` | Теги раннера |
| `job-prefix` | string | `go` | Префикс имён джоб |

## Example

```yaml
stages: [build]

include:
  - component: $CI_SERVER_FQDN/cstlab/cicd-library/go-build@1.0.0
    inputs:
      stage: build
      go-version: "1.23"
      binary-name: "myapp"
      main-path: "./cmd/myapp"
      job-prefix: build
```

## Troubleshooting

### Пайплайн висит в `pending`
Нет раннера с указанными `tags`. Убери `tags` или укажи существующие.

### `go: command not found`
Версия в `go-version` не существует в Docker Hub. Проверь теги образа `golang`.

### Бинарник не появляется в артефактах
Проверь `main-path`: он должен указывать на директорию с `package main`.

### Долгая сборка
Убедись, что в репозитории есть `go.sum` — кэш завязан на него.
