# stit-core

Форкаемые шаблоны проектов экосистемы stit: стратегия бизнеса, бэкенд на Go и Python, SPA и
SSR-фронтенд, мобилка, Telegram-бот и инфраструктура. В каждом — готовая обвязка: стандарты,
тесты, гейты и релиз. Вы пишете домены, а не каркас.

> Forkable project templates by stit. These repositories are a read-only mirror of our private
> Gitea; the docs are in Russian.

## Шаблоны

| Репозиторий | Что это |
|---|---|
| [business-strategy-template](https://github.com/stit-core/business-strategy-template) | Стратегия бизнеса: бизнес, рынок и стейкхолдеры → SWOT → карта гипотез → задачи проверки |
| [go-backend-template](https://github.com/stit-core/go-backend-template) | Go HTTP-бэкенд: huma/v2, chi, pgx/v5, sqlc, uber/fx поверх `golibinfra` |
| [golibinfra](https://github.com/stit-core/golibinfra) | Инфраструктурные Go-киты с OpenTelemetry: auth, БД, messaging, кэш, аудит, storage, AI-клиент |
| [pylibinfra](https://github.com/stit-core/pylibinfra) | Инфраструктурные Python-киты на dishka с OpenTelemetry, включая Telegram-бот |
| [spa-frontend-template](https://github.com/stit-core/spa-frontend-template) | React SPA: Vite, TypeScript, React 19, TanStack, Feature-Sliced Design, mock-режим |
| [ssr-frontend-template](https://github.com/stit-core/ssr-frontend-template) | Индексируемый сайт на Astro 7: static-first, SEO-слой, FSD, один Docker-образ |
| [mobile-template](https://github.com/stit-core/mobile-template) | Android + iOS: Kotlin Multiplatform-ядро, Jetpack Compose и SwiftUI |
| [telegram-bot-template](https://github.com/stit-core/telegram-bot-template) | Telegram-бот на aiogram 3 и aiogram-dialog поверх `pylibinfra[tgbotkit]` |
| [project-infra-template-compose](https://github.com/stit-core/project-infra-template-compose) | Проектная VPS-инфра одним docker-compose стеком: edge, Postgres, MinIO, бэкенд, сайт, бэкапы |

## С чего начать

1. **Стратегия.** `business-strategy-template` форкается первым: из него получаются стратегия
   и, если нужен продукт, его проектные артефакты, которые потом читают репозитории с кодом.
2. **Код.** Бэкенд — `go-backend-template`. Фронтенд — `spa-frontend-template` для приложения
   за логином и `ssr-frontend-template` для индексируемого сайта. Ещё есть мобилка и бот.
   Общая инфраструктура кода лежит в `golibinfra` и `pylibinfra`.
3. **Инфра.** `project-infra-template-compose`: один форк — один проект, по VPS на среду.

Как форкнуть и запустить конкретный шаблон, написано в его README.

## Это зеркало

Разработка идёт в нашем приватном Gitea (`git.stit.tech`), а сюда репозитории зеркалируются
как есть, с теми же коммитами, ветками и тегами.

- Пулл-реквесты здесь не вливаются: изменения сначала попадают в Gitea и уже оттуда приезжают сюда.
- Вопросы, баги и идеи пишите в Issues нужного репозитория.

## Сборка вне нашей инфраструктуры

Шаблоны ссылаются на библиотеки по путям `git.stit.tech/stit-core/…`, а этот хост снаружи
закрыт. Подключите вместо него зеркала с GitHub.

Go — версию берите из `require` в `go.mod`:

```bash
go mod edit -replace git.stit.tech/stit-core/golibinfra=github.com/stit-core/golibinfra@v1.6.0
go mod tidy
```

Python — источник `pylibinfra` в `[tool.uv.sources]` файла `pyproject.toml`, затем `uv lock`:

```toml
pylibinfra = { git = "https://github.com/stit-core/pylibinfra.git", rev = "v1.0.0" }
```

## Лицензия и безопасность

Все шаблоны распространяются под лицензией Apache-2.0. Об уязвимостях пишите на
security@stit.tech, а не в публичные Issues.
