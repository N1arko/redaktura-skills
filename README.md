# redaktura-skills

Набор Agent Skills для редполитики, редактуры, статей, постов, промотекстов и UX-текстов на русском языке. Скиллы упакованы по спецификации [Agent Plugins 1.0.0](https://agent-plugins.org/): корень пакета содержит `plugin.json`, а сами скиллы — папка `skills/`.

Метод основан на практиках Людмилы Сарычевой ([gladlax.ru](https://gladlax.ru)) и собран совместно с Никитой Архиповым ([niar42.com](https://niar42.com)).

Набор совместим с клиентами, которые читают скиллы в формате `SKILL.md`: Claude Code, Codex и другими агентами с поддержкой Agent Skills. Для Claude Code сохранён плагин из собственного marketplace, а `agents/openai.yaml` остаются дополнительными метаданными для Codex.

## Быстрая установка через агента

Скопируйте агенту этот промт. Без автообновлений достаточно первого абзаца — до слов «Сохрани репозиторий».

```text
Установи набор из https://github.com/N1arko/redaktura-skills для текущего пользователя.

Если клиент поддерживает Agent Plugins, подключи корень репозитория как один Agent Plugin: `plugin.json` и папку `skills/`. Используй нативный способ клиента; не превращай набор в Codex marketplace. Если клиент умеет только Agent Skills, установи шесть папок из `skills/`: redpolitika, redaktura, statya, post, promo и ux-copy. Для Claude Code добавь marketplace N1arko/redaktura-skills и установи плагин redaktura-skills@redaktura-skills в user scope.

Проверь, что доступны все шесть скиллов.

Сохрани репозиторий как источник обновлений способом, подходящим для текущего клиента. В Claude Code используй уже добавленный marketplace: включи для redaktura-skills встроенное auto-update. Если переключатель доступен только пользователю, дай один завершающий шаг: `/plugin` → `Marketplaces` → `redaktura-skills` → `Enable auto-update`. Отдельную ежемесячную задачу для Claude Code не создавай.

Если клиент не умеет обновлять marketplace, сохрани управляемую Git-копию в постоянной служебной папке пользователя и подключи из неё папки скиллов. Используй ссылки на папки, когда клиент и операционная система их поддерживают. В остальных случаях настрой безопасное копирование с сохранением предыдущей версии. Создай постоянную локальную задачу «Обновление redaktura-skills» на 1-е число каждого месяца в 10:00 по местному времени. На каждом запуске проверяй origin/main. Применяй обновление только через fast-forward, если локальная копия не изменена и новая версия содержит все шесть скиллов. Сообщай результат одной короткой сводкой; при локальных изменениях, конфликте или ошибке сохраняй текущую версию и запрашивай ручную проверку.

После настройки сразу проверь обновления. Если клиент не поддерживает ни автообновление marketplace, ни постоянные локальные задачи, установи скиллы и сообщи об этом ограничении.
```

Для установки одного скилла:

```text
Установи ux-copy из https://github.com/N1arko/redaktura-skills.
```

Рекомендуется ставить весь набор: `statya`, `post`, `promo` и `ux-copy` используют справочники `redaktura` на финальной проверке.

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

Если Codex предлагает нативную установку Agent Plugins, используйте первый абзац из быстрой установки. Иначе установите скиллы вручную:

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

### Hermes

Добавьте репозиторий как источник скиллов и установите набор:

```bash
hermes skills tap add N1arko/redaktura-skills
for skill in redpolitika redaktura statya post promo ux-copy; do
  hermes skills install "N1arko/redaktura-skills/$skill"
done
hermes skills list
```

Windows PowerShell:

```powershell
hermes skills tap add N1arko/redaktura-skills
$skills = "redpolitika", "redaktura", "statya", "post", "promo", "ux-copy"
$skills | ForEach-Object { hermes skills install "N1arko/redaktura-skills/$_" }
hermes skills list
```

После установки начните новую сессию или выполните `/reset`. Для обновления: `hermes skills update`.

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
