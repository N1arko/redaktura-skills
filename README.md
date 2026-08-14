# redaktura-skills

Набор Agent Skills для редполитики, редактуры, статей, постов, промотекстов и UX-текстов на русском языке. Скиллы упакованы по спецификации [Agent Plugins 1.0.0](https://agent-plugins.org/): корень пакета содержит `plugin.json`, а сами скиллы — папка `skills/`. Agent Plugins 1.0 — Working Draft, поэтому способы подключения могут отличаться между клиентами.

Метод основан на практиках Людмилы Сарычевой ([gladlax.ru](https://gladlax.ru)) и собран совместно с Никитой Архиповым ([niar42.com](https://niar42.com)).

Набор совместим с клиентами, которые читают скиллы в формате `SKILL.md`: Claude Code, Codex и другими агентами с поддержкой Agent Skills. Для Claude Code сохранён плагин из собственного marketplace, а `agents/openai.yaml` остаются дополнительными метаданными для Codex.

## Быстрая установка через агента

Скопируйте агенту этот промт. Без автообновлений используйте часть до строки «Сохрани репозиторий».

```text
Установи набор из https://github.com/N1arko/redaktura-skills для текущего пользователя.

Если клиент поддерживает Agent Plugins, подключи корень репозитория как один Agent Plugin: `plugin.json` и папку `skills/`. Используй нативный способ клиента и не копируй скиллы по одному. Marketplace-файл клиента допустим только как каталог установки: сам плагин остаётся переносимым пакетом Agent Plugins. Для Codex это рекомендованный способ: добавь marketplace N1arko/redaktura-skills, установи redaktura-skills@redaktura-skills и проверь его через `codex plugin list`. Если клиент умеет только Agent Skills или Codex не поддерживает установку плагина, установи шесть папок из `skills/`: redpolitika, redaktura, statya, post, promo и ux-copy. Для Claude Code добавь marketplace N1arko/redaktura-skills и установи плагин redaktura-skills@redaktura-skills в user scope.

Проверь, что доступны все шесть скиллов.

Сохрани репозиторий как источник обновлений способом, подходящим для текущего клиента. Если существующая установка или задача обновления ссылается на `<копия-репозитория>/<имя-скилла>`, до обновления переподключи её к `<копия-репозитория>/skills/<имя-скилла>` для всех шести скиллов и только затем проверь их доступность. В Claude Code используй уже добавленный marketplace: включи для redaktura-skills встроенное auto-update. Если переключатель доступен только пользователю, дай один завершающий шаг: `/plugin` → `Marketplaces` → `redaktura-skills` → `Enable auto-update`. Отдельную ежемесячную задачу для Claude Code не создавай.

Если у клиента нет встроенного auto-update, создай постоянную локальную задачу «Обновление redaktura-skills» на 1-е число каждого месяца в 10:00 по местному времени. Для Codex, установленного как плагин, выполни `codex plugin marketplace upgrade redaktura-skills`, для Hermes — `hermes plugins update redaktura-skills`; остальные клиенты обновляй через их нативный механизм. Для отдельных скиллов сохрани управляемую Git-копию в постоянной служебной папке пользователя и обновляй её только через fast-forward, если локальная копия не изменена и новая версия содержит все шесть скиллов; после обновления используй пути из `skills/`. Сообщай результат одной короткой сводкой; при локальных изменениях, конфликте или ошибке сохраняй текущую версию и запрашивай ручную проверку.

После настройки сразу проверь обновления. Если клиент не поддерживает ни автообновление, ни нативное обновление, ни постоянные локальные задачи, установи скиллы и сообщи об этом ограничении.
```

Для установки одного скилла:

```text
Установи ux-copy из https://github.com/N1arko/redaktura-skills.
```

Рекомендуется ставить весь набор: `statya`, `post`, `promo` и `ux-copy` используют справочники `redaktura` на финальной проверке.

### Миграция со старой структуры

До версии `0.5.0` скиллы лежали в корне Git-копии: `<копия-репозитория>/<имя-скилла>`. После `git pull --ff-only` старые ссылки, симлинки и задачи обновления перестанут находить эти папки. Перед обновлением направьте их на `<копия-репозитория>/skills/<имя-скилла>` для всех шести скиллов. Установки, в которые скиллы были скопированы целиком, продолжат работать; при следующем обновлении копируйте их из `skills/`.

## Ручная установка

### Claude Code

Добавьте marketplace из этого репозитория и установите плагин для текущего пользователя:

```bash
claude plugin marketplace add N1arko/redaktura-skills
claude plugin install redaktura-skills@redaktura-skills --scope user
```

Внутри Claude Code marketplace также можно добавить командой `/plugin marketplace add N1arko/redaktura-skills`.

В уже открытой сессии выполните `/reload-plugins`. Скиллы будут доступны во всех проектах:

```text
/redaktura-skills:redpolitika
/redaktura-skills:redaktura
/redaktura-skills:statya
/redaktura-skills:post
/redaktura-skills:promo
/redaktura-skills:ux-copy
```

Чтобы получать обновления после запусков Claude Code, откройте `/plugin` → `Marketplaces` → `redaktura-skills` → `Enable auto-update`. У сторонних marketplace автообновление изначально выключено. Обновлённый плагин подключится после `/reload-plugins` или при следующем запуске Claude Code.

Если набор уже установлен отдельными папками в `~/.claude/skills`, сначала проверьте плагин. Затем удалите старые копии, чтобы в Claude не осталось двух версий одних скиллов.

#### Установка отдельными папками

Этот способ сохраняет короткие команды `/redaktura`, `/statya` и другие. Обновления для него нужно настраивать отдельно.

Личные скиллы, доступные во всех проектах:

macOS / Linux:

```bash
git clone https://github.com/N1arko/redaktura-skills.git
mkdir -p ~/.claude/skills
cp -R redaktura-skills/skills/{redpolitika,redaktura,statya,post,promo,ux-copy} ~/.claude/skills/
```

Windows PowerShell:

```powershell
git clone https://github.com/N1arko/redaktura-skills.git
New-Item -ItemType Directory -Force -Path "$HOME\.claude\skills"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\redpolitika" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\redaktura" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\statya" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\post" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\promo" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\ux-copy" "$HOME\.claude\skills\"
```

Проектные скиллы:

macOS / Linux:

```bash
mkdir -p .claude/skills
cp -R redaktura-skills/skills/{redpolitika,redaktura,statya,post,promo,ux-copy} .claude/skills/
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path ".\.claude\skills"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\redpolitika" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\redaktura" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\statya" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\post" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\promo" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\ux-copy" ".\.claude\skills\"
```

При установке отдельными папками скиллы вызываются напрямую: `/redaktura`, `/redpolitika`, `/statya`, `/post`, `/promo`, `/ux-copy`.

### Codex

#### Установка плагина (рекомендуется)

Codex подключает корневой пакет Agent Plugins через marketplace. Файл `.agents/plugins/marketplace.json` — только каталог установки: сам плагин по-прежнему описан корневым `plugin.json`.

```bash
codex plugin marketplace add N1arko/redaktura-skills
codex plugin add redaktura-skills@redaktura-skills
codex plugin list
```

После установки начните новую сессию Codex.

Автообновление в CLI не включается отдельным переключателем. Для обновления плагина без переустановки выполните:

```bash
codex plugin marketplace upgrade redaktura-skills
```

Для автоматического обновления добавьте эту команду в планировщик ОС, например раз в месяц.

#### Установка скиллов

Этот вариант нужен для версий Codex без установки плагинов или когда скиллы должны быть доступны по отдельности. Обновления для него настраиваются отдельно.

macOS / Linux:

```bash
git clone https://github.com/N1arko/redaktura-skills.git
mkdir -p ~/.codex/skills
cp -R redaktura-skills/skills/{redpolitika,redaktura,statya,post,promo,ux-copy} ~/.codex/skills/
```

Windows PowerShell:

```powershell
git clone https://github.com/N1arko/redaktura-skills.git
New-Item -ItemType Directory -Force -Path "$HOME\.codex\skills"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\redpolitika" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\redaktura" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\statya" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\post" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\promo" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\skills\ux-copy" "$HOME\.codex\skills\"
```

Для обновления сначала выполните `git -C redaktura-skills pull --ff-only`, затем повторите копирование из `redaktura-skills/skills/`. Если вместо копирования используются ссылки, направьте их на эти же пути.

### Hermes

Hermes устанавливает корневой пакет Agent Plugins напрямую из Git:

```bash
hermes plugins install N1arko/redaktura-skills --enable
hermes plugins list --enabled
```

После установки начните новую сессию или выполните `/reset`.

Автообновление в CLI не включается отдельным переключателем. Для обновления плагина без переустановки выполните:

```bash
hermes plugins update redaktura-skills
```

Для автоматического обновления добавьте эту команду в планировщик ОС, например раз в месяц.

### Другие агенты

Для клиента с поддержкой Agent Plugins подключите корень репозитория. Иначе скопируйте нужные папки из `skills/` в директорию агента: каждая содержит `SKILL.md` и нужные материалы в `references/` или `assets/`.

## Скиллы

| Скилл | Что делает |
|---|---|
| `redpolitika` | Создаёт и обновляет `.agents/redpolitika.md`: читатель, площадки, регистр, словарь, фактура |
| `redaktura` | Редактирует готовые тексты: смысл, структура, тональность, предложения, слова, ритм |
| `statya` | Ведёт статью с нуля: бриф, фактура, структура, черновик, самопроверка |
| `post` | Пишет и усиливает короткие посты: одна мысль, хук, тело, финал, площадка |
| `promo` | Собирает лендинги, промостраницы, тексты о себе, страницы компании и пресс-релизы |
| `ux-copy` | Пишет и правит тексты интерфейса: кнопки, ошибки, формы, пустые состояния, уведомления |

## Пример: одна новость, три результата

Мы дали агенту новость NASA о снимке Hubble и попросили телеграм-пост — без скиллов, со скиллом `redaktura` и со скиллом `post`. Полные тексты лежат в [examples/hubble-news](examples/hubble-news).

Без скиллов получается аккуратная справка: факты верные, читать незачем.

> NASA показала новый снимок Hubble к 4 июля: шаровое скопление NGC 6426 на тёмном небе выглядит как красно-бело-синий бенгальский огонь. NGC 6426 находится во внешнем гало Млечного Пути. Это плотная сферическая группа звёзд, связанных гравитацией…

`redaktura` правит черновик и объясняет каждую правку по имени правила. Например, канцелярит:

> Было: плотная сферическая группа звёзд, связанных гравитацией
> Стало: плотный шар из звёзд, которые удерживает общая гравитация

`post` пишет с нуля: выбирает одну мысль, ставит живой хук и убирает нейрошаблоны вроде «не просто X, а Y».

> Hubble снял для 4 июля звёздный «бенгальский огонь».
>
> NASA опубликовала новый снимок шарового скопления NGC 6426: на тёмном небе оно выглядит как россыпь красных, белых и синих точек…

Вместе с текстом скиллы возвращают вопросы по фактуре — то, что агент не вправе выдумать: будет ли приложен снимок, какая аудитория у канала.

## Как устроена работа

`redpolitika` создаёт файл `.agents/redpolitika.md`, который читают остальные скиллы.

```text
redpolitika -> redaktura
             -> statya
             -> post
             -> promo
             -> ux-copy
```

Для разовой задачи можно начинать сразу с нужного скилла. Для постоянной работы с одним проектом полезно сначала создать редполитику.

## Структура репозитория

```text
redaktura-skills/
├── plugin.json
├── .agents/plugins/
│   └── marketplace.json
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── skills/
│   ├── redpolitika/
│   │   ├── SKILL.md
│   │   ├── assets/
│   │   └── references/
│   ├── redaktura/
│   │   ├── SKILL.md
│   │   └── references/
│   ├── statya/
│   │   ├── SKILL.md
│   │   └── references/
│   ├── post/
│   │   ├── SKILL.md
│   │   ├── agents/
│   │   └── references/
│   ├── promo/
│   │   ├── SKILL.md
│   │   ├── agents/
│   │   └── references/
│   └── ux-copy/
│       ├── SKILL.md
│       └── references/
├── examples/
│   └── hubble-news/
├── LICENSE
└── README.md
```

## Лицензия

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) © 2026 Людмила Сарычева, Никита Архипов. Используйте и адаптируйте свободно, указывая авторство и ссылку на [gladlax.ru](https://gladlax.ru). Полный текст — в файле [LICENSE](LICENSE).
