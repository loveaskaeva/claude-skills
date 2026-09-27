# Claude Skills

Четыре скилла для [Claude Code](https://claude.com/claude-code): аккуратное выполнение задач в коде, подготовка репозитория к GitHub, учебные работы и тёмный минималистичный UI.

Это адаптация скиллов для Codex из [moii-dev/codex-skills](https://github.com/moii-dev/codex-skills) под формат Claude Code.

## Скиллы

| Скилл | Вызов | Что делает |
|---|---|---|
| `task-executor` | `/task-executor <задача>` | Сначала изучает проект, потом вносит минимальную правильную правку, проверяет тестами и сборкой, коротко отчитывается |
| `github-repo-polisher` | `/github-repo-polisher` | README, `.gitignore`, поиск утёкших ключей, инструкции по запуску. Сам не коммитит и не пушит, а выдаёт команды |
| `student-homework-builder` | `/student-homework-builder <задание>` | Делает лабы и домашки строго по заданию и без оверинжиниринга, чтобы их было легко защитить |
| `universal-premium-ui-style` | `/universal-premium-ui-style` | Тёмный минималистичный «дорогой» стиль: палитра, типографика, компоненты, все состояния. Не перебивает существующий дизайн проекта |

Claude подхватывает скиллы и сам, когда задача подходит под описание. Вызывать через `/` не обязательно.

## Установка

Как плагин (рекомендуется):

```bash
claude plugin marketplace add loveaskaeva/claude-skills
claude plugin install claude-skills@loveaskaeva-skills
```

В этом случае скиллы вызываются с префиксом, например `/claude-skills:task-executor`.

Или вручную, скопировав папки в личные скиллы:

```bash
git clone https://github.com/loveaskaeva/claude-skills.git
cp -R claude-skills/skills/* ~/.claude/skills/
```

После установки перезапусти Claude Code.

## Что изменено относительно версии для Codex

- Убраны файлы `agents/openai.yaml`, они нужны только Codex. `codex-task-executor` переименован в `task-executor`.
- Добавлены `argument-hint` и `$ARGUMENTS`: задачу можно передать сразу в команде `/скилл <текст>`.
- Кроме `AGENTS.md`, скиллы читают `CLAUDE.md`. Поиск по проекту идёт через Glob/Grep, требования отслеживаются через todo-список.
- `universal-premium-ui-style` больше не включается на любой задаче с UI, а только когда просят такой стиль или у проекта нет своего.
- `github-repo-polisher` не коммитит и не пушит сам, ищет ключи по типичным префиксам (`sk_`, `AIza`, `ghp_`, `phx_`, приватные ключи) и следит за `.pem` и `.claude/settings.local.json`.
- Скиллы ссылаются друг на друга и на `ui-ux-pro-max`, `docx` и `xlsx`, если те установлены. Итоговые отчёты пишутся на языке пользователя.

## Структура

```text
.claude-plugin/
  plugin.json        # манифест плагина
  marketplace.json   # чтобы ставить через `plugin marketplace add`
skills/
  task-executor/SKILL.md
  github-repo-polisher/SKILL.md
  student-homework-builder/SKILL.md
  universal-premium-ui-style/SKILL.md
```
