# cicd-library

Библиотека переиспользуемых GitLab CI/CD Components для проектов CSTLab.

## Компоненты

| Компонент | Описание | README |
|---|---|---|
| `go-build` | Сборка, линт и тесты Go-приложения | [templates/go-build/README.md](templates/go-build/README.md) |

## Quick Start

```yaml
stages: [build]

include:
  - component: $CI_SERVER_FQDN/cstlab/cicd-library/go-build@1.0.0
    inputs:
      stage: build
      go-version: "1.23"
```
