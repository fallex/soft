---
description: Универсальная установка любого софта из хаба на Windows через Cursor IDE.
---

# Установка на Windows

Универсальная инструкция — подходит для **любого** софта из этого хаба. Конкретный URL репо и название папки бери на странице нужного софта в разделе [📦 Софты](../softs/).

> Гайд написан под **Cursor IDE** (рекомендую новичкам — там встроен бесплатный AI-помощник). Если предпочитаешь PowerShell, PyCharm, VS Code — пропускай шаги про Cursor, остальные команды те же.

## 1. Установить Cursor IDE

1. Зайди на [cursor.sh](https://cursor.sh/) → **Download for Windows**.
2. Запусти `.exe`, ставь по умолчанию (можно поставить галочку **Add to PATH** — пригодится).
3. После установки запусти Cursor.
4. При первом запуске:
   - Войди по Google или email (нужно для бесплатного AI-помощника).
   - Импорт настроек VS Code — можно пропустить.

После запуска Cursor выглядит как VS Code, но с встроенным AI-чатом справа и **Ctrl + K** для инлайн-AI.

## 2. Установить Python 3.10+

1. Скачай с [python.org/downloads](https://www.python.org/downloads/) — версия 3.12.x (или новее).
2. **Важно:** при установке поставь галочку **«Add Python to PATH»**.
3. После установки перезапусти Cursor (чтобы он подхватил новый PATH).

В Cursor открой встроенный терминал: **View → Terminal** или **Ctrl + \`** (Ctrl + бэктик).

Проверь:

```powershell
python --version
```

Должно вывести `Python 3.12.x`.

## 3. Установить Git

1. Скачай с [git-scm.com](https://git-scm.com/download/win).
2. Установщик — все настройки **по умолчанию**, не меняй ничего.
3. Перезапусти Cursor.

Проверь в терминале Cursor:

```powershell
git --version
```

## 4. Клонировать репо софта

URL клона возьми со страницы конкретного софта в разделе [📦 Софты](../softs/). Дальше:

**В Cursor:** **Ctrl + Shift + P** → начни печатать `Git: Clone` → выбери его → вставь URL вида `https://github.com/fallex/<имя-софта>.git`. Выбери папку (например `C:\crypto`). После клонирования Cursor предложит **Open the cloned repository** → жми **Open**.

**Через терминал:**

```powershell
mkdir C:\crypto
cd C:\crypto
git clone https://github.com/fallex/<имя-софта>.git
cursor <имя-софта>
```

> 💡 Где `<имя-софта>` — название из URL репо, например `outcome-MXW`.

## 5. Создать и активировать venv

В Cursor открой терминал (**Ctrl + \`**). Внизу должна быть строка с путём типа `C:\crypto\<имя-софта>`.

```powershell
python -m venv env
env\Scripts\activate
```

Слева появится `(env)` — виртуалка активна.

> ⚠️ Если PowerShell ругается на запрет скриптов (`...running scripts is disabled...`) — выполни **один раз**:
>
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```
>
> Согласись (`Y`), потом снова `env\Scripts\activate`.

> 💡 Cursor обычно сам замечает папку `env/` и предлагает выбрать этот интерпретатор Python. Соглашайся.

> ⚠️ Каждый новый запуск терминала — нужно снова `cd` в папку проекта и `env\Scripts\activate`.

## 6. Установить зависимости

В том же терминале (с активным `(env)`):

```powershell
pip install -r requirements.txt
```

## 7. Подготовить input-файлы

В сайдбаре Cursor (слева, дерево файлов) разверни папку `input/`. У большинства софтов там лежат шаблоны:

- `private_keys.txt.example`
- `proxies.txt.example`

Кликни правой кнопкой → **Rename** → убери `.example`. Открой получившиеся файлы в Cursor, вставь приватники / прокси, по одному на строку. Сохрани (**Ctrl + S**).

> Точный список файлов и формат — смотри на странице конкретного софта.

## 8. Настроить parameters.py

Открой `parameters.py` в Cursor.

Найди (**Ctrl + F**) строку:

```python
CAPSOLVER_API_KEY = "CAP-XXXXXX..."
```

Замени `CAP-XXXX...` на свой ключ. Сохрани.

Остальные параметры — смотри на странице конкретного софта или в комментариях самого `parameters.py`.

> 💡 Если не понимаешь какой-то параметр — выдели его и нажми **Ctrl + L** (AI-чат), спроси «что делает этот параметр». Бесплатный AI Cursor справится.

## 9. Запустить

Два варианта:

**Вариант А — через терминал (рекомендую новичкам):**

```powershell
python main.py
```

Появится меню. Стрелками ↑↓, Enter — выбор. Что делает каждый пункт — смотри на странице конкретного софта.

**Вариант Б — кнопкой ▶ в Cursor:**

Открой `main.py`, в правом верхнем углу — кнопка **▶** (Run). Кликай — запустится в терминале Cursor.

## 10. На последующих запусках

В Cursor:

1. **File → Open Folder** → выбери папку проекта.
2. Открой терминал (**Ctrl + \`**).
3. ```powershell
   env\Scripts\activate
   python main.py
   ```

Можно сделать `.bat`-файл на рабочем столе для быстрого запуска (пример для софта `outcome-MXW`):

```bat
@echo off
cd /d C:\crypto\outcome-MXW
call env\Scripts\activate
python main.py
pause
```

Сохрани как `start_outcome.bat`. Двойной клик — софт запущен (без Cursor). Аналогично можно сделать `.bat` на любой другой софт.

## Если что-то идёт не так

1. **Cursor подсветит ошибку красной волнистой линией** — наведи мышкой, прочитай.
2. **Ошибка в терминале** — выдели её → правой кнопкой → **Send to AI Chat** (или вручную **Ctrl + L** и вставь). Бесплатный AI объяснит.
3. **AI не помог** — пиши в чат MXW со скрином ошибки.

## Частые проблемы Windows

| Проблема | Решение |
|---|---|
| `python: команда не найдена` | Python не в PATH. Переустанови с галочкой **Add to PATH** или перезапусти Cursor. |
| PowerShell не даёт активировать venv | `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned` |
| `pip install` падает с SSL | `python -m pip install --upgrade pip` |
| Меню стрелками не работает | Запускай через **Cursor → Run кнопка**, а не из стороннего PowerShell |
