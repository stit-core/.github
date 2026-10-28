# stit-core

Форкаемые шаблоны и стандарт разработки экосистемы stit: стратегия бизнеса, бэкенд на Go и Python,
SPA- и SEO-фронтенд, мобилка, Telegram-бот и инфраструктура. В каждом шаблоне — готовая обвязка:
стандарты, тесты, гейты и релиз. Вы пишете домены, а не каркас.

> Forkable project templates and a development standard by stit. These repositories are a
> read-only mirror of our private Gitea; the docs are in Russian. Work in progress.

## Статус

Стандарт и шаблоны ещё в разработке. Обвязка доделана не во всех репозиториях, скиллы и
воркфлоу агентов готовы частично, SPA-шаблон — в полуготовом состоянии, а мобильный ещё ни разу
не тестировался и в разработке. Работы впереди много: что-то уже готово, что-то сделано наполовину.

## Как этим пользоваться

Шаблоны — не набор отдельных заготовок, а одна система. Проект — это организация из нескольких
форков, которые лежат рядом в одной папке и знают друг о друге. Правильный путь такой:

1. **Стратегия и дизайн.** Форкните [business-strategy-template](https://github.com/stit-core/business-strategy-template)
   в `<org>/strategy` и спроектируйте в нём всё: бизнес, рынок, гипотезы, продукт, домены и
   дизайн. Это источник истины для остальных репозиториев — они его читают.
2. **Структура репозиториев.** Решите, какие репозитории нужны проекту: бэкенд, фронтенд, сайт,
   бот, мобилка. Карта всех репозиториев и контракты между ними —
   в [`ecosystem.md`](https://github.com/stit-core/project-infra-template-compose/blob/main/docs/reference/ecosystem.md).
3. **Создание репозиториев.** Форкните нужные шаблоны в свою организацию и склонируйте все форки
   рядом, в одну папку.
4. **Работа из инфра-репозитория.** Форк [project-infra-template-compose](https://github.com/stit-core/project-infra-template-compose)
   (`<org>/infra`) — операционный хаб проекта. Из него управляются все остальные репозитории и
   серверы, идёт выкатка, и из него же запускаются агенты в соседние репозитории. Заходите в
   инфра-репозиторий и все действия выполняйте оттуда.

```
<org>/strategy                      стратегия, продукт, домены, дизайн
      │  читается остальными репозиториями
      ▼
<org>/infra                         операционный хаб: план, серверы, выкатка, агенты
      │
      ▼
<org>/{backend,frontend,site,bot}   код; выкатываются из infra
<org>/mobile                        задачи из infra, релиз в магазины
```

## Шаблоны

| Репозиторий | Что это |
|---|---|
| [business-strategy-template](https://github.com/stit-core/business-strategy-template) | Стратегия бизнеса: бизнес, рынок и стейкхолдеры → SWOT → карта гипотез → задачи проверки |
| [project-infra-template-compose](https://github.com/stit-core/project-infra-template-compose) | Инфра-репозиторий проекта: VPS одним docker-compose стеком, выкатка, агенты в соседних репо |
| [go-backend-template](https://github.com/stit-core/go-backend-template) | Go HTTP-бэкенд: huma/v2, chi, pgx/v5, sqlc, uber/fx поверх `golibinfra` |
| [spa-frontend-template](https://github.com/stit-core/spa-frontend-template) | React SPA: Vite, TypeScript, React 19, TanStack, Feature-Sliced Design, mock-режим |
| [seo-frontend-template](https://github.com/stit-core/seo-frontend-template) | Индексируемый сайт на Astro 7: static-first, SEO-слой, FSD, один Docker-образ |
| [mobile-template](https://github.com/stit-core/mobile-template) | Android + iOS: Kotlin Multiplatform-ядро, Jetpack Compose и SwiftUI. В разработке, ещё не тестировался |
| [telegram-bot-template](https://github.com/stit-core/telegram-bot-template) | Telegram-бот на aiogram 3 и aiogram-dialog поверх `pylibinfra[tgbotkit]` |
| [golibinfra](https://github.com/stit-core/golibinfra) | Инфраструктурные Go-киты с OpenTelemetry: auth, БД, messaging, кэш, аудит, storage, AI-клиент |
| [pylibinfra](https://github.com/stit-core/pylibinfra) | Инфраструктурные Python-киты на dishka с OpenTelemetry, включая Telegram-бот |

Как форкнуть и запустить конкретный шаблон, написано в его README.

## Давайте развивать вместе

Пользуетесь шаблонами, дорабатываете их или собрали на них классный кейс — расскажите нам.
Присылайте кейсы, идеи и пулл-реквесты: так мы вместе развиваем шаблоны и сам стандарт и
собираем вокруг него сообщество.

- **Пулл-реквесты** открывайте здесь, на GitHub. Мы переносим изменения в основной репозиторий,
  и они возвращаются сюда вместе с зеркалом.
- **Баги и вопросы** — в Issues нужного репозитория.
- **Связь** — Telegram [@gommgo](https://t.me/gommgo).

## Это зеркало

Разработка идёт в нашем приватном Gitea (`git.stit.tech`), а сюда репозитории зеркалируются как
есть, с теми же коммитами, ветками и тегами.

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

Все шаблоны распространяются под лицензией Apache-2.0. Об уязвимостях пишите в Telegram
[@gommgo](https://t.me/gommgo), а не в публичные Issues.
