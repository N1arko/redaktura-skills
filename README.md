# redaktura-skills

Набор Agent Skills для редполитики, редактуры, статей, постов, промотекстов и UX-текстов на русском языке.

Метод основан на практиках Людмилы Сарычевой ([gladlax.ru](https://gladlax.ru)) и собран совместно с Никитой Архиповым ([niar42.com](https://niar42.com)).

Папки совместимы с клиентами, которые читают скиллы в формате `SKILL.md`: Claude Code, Codex и другие агенты с поддержкой Agent Skills. Для Codex дополнительно есть `agents/openai.yaml`; остальные клиенты могут его игнорировать.

## Быстрая установка через агента

Скопируйте агенту эту фразу:

```text
Установи все скиллы из https://github.com/N1arko/redaktura-skills: redpolitika, redaktura, statya, post, promo, ux-copy. Поставь их как personal skills.
```

Для установки одного скилла:

```text
Установи ux-copy из https://github.com/N1arko/redaktura-skills.
```

Рекомендуется ставить весь набор: `statya`, `post`, `promo` и `ux-copy` используют справочники `redaktura` на финальной проверке.

## Ручная установка

### Claude Code

Личные скиллы, доступны во всех проектах:

macOS / Linux:

```bash
git clone https://github.com/N1arko/redaktura-skills.git
mkdir -p ~/.claude/skills
cp -R redaktura-skills/{redpolitika,redaktura,statya,post,promo,ux-copy} ~/.claude/skills/
```

Windows PowerShell:

```powershell
git clone https://github.com/N1arko/redaktura-skills.git
New-Item -ItemType Directory -Force -Path "$HOME\.claude\skills"
Copy-Item -Recurse -Force ".\redaktura-skills\redpolitika" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\redaktura" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\statya" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\post" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\promo" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\ux-copy" "$HOME\.claude\skills\"
```

Проектные скиллы:

macOS / Linux:

```bash
mkdir -p .claude/skills
cp -R redaktura-skills/{redpolitika,redaktura,statya,post,promo,ux-copy} .claude/skills/
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path ".\.claude\skills"
Copy-Item -Recurse -Force ".\redaktura-skills\redpolitika" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\redaktura" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\statya" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\post" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\promo" ".\.claude\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\ux-copy" ".\.claude\skills\"
```

В Claude Code скиллы можно вызывать напрямую: `/redaktura`, `/redpolitika`, `/statya`, `/post`, `/promo`, `/ux-copy`.

### Codex

Попросите Codex установить набор из репозитория:

```text
Установи все скиллы из https://github.com/N1arko/redaktura-skills: redpolitika, redaktura, statya, post, promo, ux-copy.
```

Если используете установочный скрипт Codex:

```bash
install-skill-from-github.py --repo N1arko/redaktura-skills --path redpolitika redaktura statya post promo ux-copy
```

Ручная установка:

macOS / Linux:

```bash
git clone https://github.com/N1arko/redaktura-skills.git
mkdir -p ~/.codex/skills
cp -R redaktura-skills/{redpolitika,redaktura,statya,post,promo,ux-copy} ~/.codex/skills/
```

Windows PowerShell:

```powershell
git clone https://github.com/N1arko/redaktura-skills.git
New-Item -ItemType Directory -Force -Path "$HOME\.codex\skills"
Copy-Item -Recurse -Force ".\redaktura-skills\redpolitika" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\redaktura" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\statya" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\post" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\promo" "$HOME\.codex\skills\"
Copy-Item -Recurse -Force ".\redaktura-skills\ux-copy" "$HOME\.codex\skills\"
```

### Другие агенты

Скопируйте нужные папки в директорию, где агент ищет skills. Каждая папка автономна по формату: внутри есть `SKILL.md`, а дополнительные материалы лежат в `references/` или `assets/`.

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
├── redpolitika/
│   ├── SKILL.md
│   ├── assets/
│   └── references/
├── redaktura/
│   ├── SKILL.md
│   └── references/
├── statya/
│   ├── SKILL.md
│   └── references/
├── post/
│   ├── SKILL.md
│   ├── agents/
│   └── references/
├── promo/
│   ├── SKILL.md
│   ├── agents/
│   └── references/
├── ux-copy/
│   ├── SKILL.md
│   └── references/
├── examples/
│   └── hubble-news/
├── LICENSE
└── README.md
```

## Лицензия

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) © 2026 Людмила Сарычева, Никита Архипов. Используйте и адаптируйте свободно, указывая авторство и ссылку на [gladlax.ru](https://gladlax.ru). Полный текст — в файле [LICENSE](LICENSE).
