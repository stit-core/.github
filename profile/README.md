# stit-core

Открытые шаблоны и стандарт разработки stit: как вести продукт от стратегии до кода и выкатки
вместе с Claude Code. Здесь стратегия бизнеса и проектирование продукта, инфраструктура, бэкенд на
Go, SPA и индексируемый сайт, мобильное приложение, Telegram-бот и библиотеки к ним. В каждом
шаблоне — готовая обвязка: стандарты, скиллы для Claude Code, тесты, гейты и релиз. Вы пишете
домены, а не каркас.

> Open project templates and a development standard by stit. One project is one folder with a root
> `CLAUDE.md`; strategy and design come first; Claude Code works in every repository through its
> own skills and gates. These repositories are a read-only mirror of our private Gitea; the docs
> are in Russian. Work in progress.

## Подход

- **Сначала проект продуман, потом код.** Бизнес, рынок, гипотезы, продукт, домены и сервисы,
  инфраструктура, интерфейсы и экраны, FSD-карта и дизайн проектируются в репозитории стратегии.
  Это источник истины: репозитории кода читают его, а не придумывают своё.
- **Проект — одна папка.** Все репозитории проекта лежат в одной папке, а в её корне — `CLAUDE.md`,
  карта проекта: что где лежит, как проект развивается, как в нём работать. Работа ведётся из
  корня одной сессией Claude Code.
- **Работа — через скиллы.** У каждого репозитория свои скиллы Claude Code: входы, проектирование
  слоёв, аудиты, планы, заготовки кода, релиз. Агент работает ими и гейтами репозитория, а не
  правит файлы в обход.
- **Берите и владейте.** Шаблоны открыты под Apache-2.0: форк становится вашим проектом, а
  `/de-template` убирает из него шаблонную мету.

## Статус

Стандарт и шаблоны ещё в разработке. Обвязка доделана не во всех репозиториях, скиллы и
воркфлоу агентов готовы частично, SPA-шаблон — в полуготовом состоянии, а мобильный ещё ни разу
не тестировался и в разработке. Работы впереди много: что-то уже готово, что-то сделано наполовину.

## Как этим пользоваться

Шаблоны — не набор отдельных заготовок, а одна система. Проект — это одна папка: в ней лежат
форки шаблонов, а в её корне — `CLAUDE.md`, карта проекта, по которой Claude Code ведёт всю работу.
Правильный путь такой:

1. **Папка проекта.** Заведите корень проекта `~/git/<org>/`. Это небольшой репозиторий
   `<org>/project`: `CLAUDE.md` — карта проекта (что где лежит, как проект развивается, как в нём
   работать), `.claude/settings.json` — общие запреты для сессии, `local/` — локальные черновики,
   выгрузки и логи, которые не хранятся в git. Устройство и образцы файлов —
   в [`project-root.md`](https://github.com/stit-core/project-infra-template-compose/blob/main/docs/reference/project-root.md).
2. **Сначала стратегия и проектирование.** Форкните [business-strategy-template](https://github.com/stit-core/business-strategy-template)
   в `<org>/strategy`, склонируйте в папку проекта и продумайте в нём весь проект до кода: бизнес,
   рынок, гипотезы, продукт, домены и сервисы, инфраструктуру, интерфейсы и экраны, FSD-карту,
   дизайн. Это источник истины для остальных репозиториев — они его читают.
3. **Структура репозиториев.** Решите, какие репозитории нужны проекту: инфра, бэкенд, фронтенд,
   сайт, бот, мобилка. Карта всех репозиториев и контракты между ними —
   в [`ecosystem.md`](https://github.com/stit-core/project-infra-template-compose/blob/main/docs/reference/ecosystem.md).
4. **Реализация.** Форкните нужные шаблоны в свою организацию, склонируйте форки в папку проекта и
   впишите их в корневой `CLAUDE.md`.
5. **Работа — из корня проекта.** Запускайте `claude` в `~/git/<org>/`, а не в отдельном
   репозитории. Корневой `CLAUDE.md` ведёт сессию по всем репозиториям, а в каждом из них она
   работает его скиллами: в стратегии — `/entrypoint` и скиллами слоёв, в инфре — `/init-project`,
   `/plan` и выкаткой `make bump`, в коде — `/smartdev`, `/scaffold`, `/release`. Скиллы
   репозитория появляются в сессии, когда она открыла его файлы, — начните задачу словами, и агент
   сам откроет нужный репозиторий.

```
~/git/<org>/                       корень проекта (<org>/project) — отсюда ведётся вся работа
├─ CLAUDE.md                       карта проекта: что где, как он развивается, как работать
├─ .claude/settings.json           общие запреты для сессии
├─ local/                          локальные черновики, выгрузки, логи — не в git
├─ strategy/                       стратегия и проектирование — первым; остальные его читают
├─ infra/                          серверы, выкатка, программы сквозных задач
├─ backend/ frontend/ site/ bot/   код; образы выкатываются через infra
└─ mobile/                         приложение; релиз — в магазины
```

Начало нового проекта (`acme` — ваша организация):

```bash
mkdir -p ~/git/acme/local && cd ~/git/acme && git init   # корень проекта
# CLAUDE.md, .claude/settings.json, .gitignore — по образцам из project-root.md
git clone git@github.com:acme/strategy.git              # ваш форк business-strategy-template
claude                                                   # «начнём со стратегии»
```

## Шаблоны

| Репозиторий | Папка в проекте | Что это |
|---|---|---|
| **Стратегия и проектирование** | | |
| [business-strategy-template](https://github.com/stit-core/business-strategy-template) | `strategy/` | Бизнес, рынок и стейкхолдеры → SWOT → карта гипотез → продукт: домены и сервисы, интерфейсы и экраны, FSD-карта, сайт, дизайн; ИТ-периметр бизнеса |
| **Инфраструктура** | | |
| [project-infra-template-compose](https://github.com/stit-core/project-infra-template-compose) | `infra/` | VPS одним docker-compose стеком, выкатка, программы сквозных задач; канон экосистемы и корня проекта |
| **Код** | | |
| [go-backend-template](https://github.com/stit-core/go-backend-template) | `backend/` | Go HTTP-бэкенд: huma/v2, chi, pgx/v5, sqlc, uber/fx поверх `golibinfra` |
| [spa-frontend-template](https://github.com/stit-core/spa-frontend-template) | `frontend/` | Кабинет на React SPA: Vite, TypeScript, React 19, TanStack, Feature-Sliced Design, mock-режим |
| [seo-frontend-template](https://github.com/stit-core/seo-frontend-template) | `site/` | Индексируемый сайт на Astro 7: static-first, SEO-слой, FSD, один Docker-образ |
| [telegram-bot-template](https://github.com/stit-core/telegram-bot-template) | `bot/` | Telegram-бот на aiogram 3 и aiogram-dialog поверх `pylibinfra[tgbotkit]` |
| [mobile-template](https://github.com/stit-core/mobile-template) | `mobile/` | Android + iOS: Kotlin Multiplatform-ядро, Jetpack Compose и SwiftUI. В разработке, ещё не тестировался |
| **Библиотеки** — подключаются зависимостью | | |
| [golibinfra](https://github.com/stit-core/golibinfra) | — | Инфраструктурные Go-киты с OpenTelemetry: auth, БД, messaging, кэш, аудит, storage, AI-клиент |
| [pylibinfra](https://github.com/stit-core/pylibinfra) | — | Инфраструктурные Python-киты на dishka с OpenTelemetry, включая Telegram-бот |

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
