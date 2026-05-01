---
description: Установка софта на macOS — пошагово.
---

# Установка на macOS

## 1. Установить Python 3.10+

Открой Terminal (⌘+Space → «Terminal»). Проверь, есть ли Python:

```bash
python3 --version
```

Если выдаёт `Python 3.10.x` или выше — пропусти шаг.

Если нет — поставь через [Homebrew](https://brew.sh/):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install python@3.12
```

## 2. Установить Git

```bash
git --version
```

Если выдаёт что-то типа `xcode-select: note: install requested...` — нажми «Установить» в появившемся окне. Дальше просто `git --version` снова → всё.

## 3. Клонировать репо

```bash
mkdir -p ~/crypto && cd ~/crypto
git clone https://github.com/fallex/outcome-MXW.git
cd outcome-MXW
```

## 4. Создать и активировать venv

```bash
python3 -m venv env
source env/bin/activate
```

Слева в строке появится `(env)` — это значит, виртуалка активна.

> ⚠️ Каждый новый запуск Terminal — нужно **снова** делать `source env/bin/activate` перед работой с софтом.

## 5. Установить зависимости

```bash
pip install -r requirements.txt
```

Подождать минуту-две.

## 6. Подготовить input-файлы

```bash
mv input/private_keys.txt.example input/private_keys.txt
mv input/proxies.txt.example      input/proxies.txt
```

Открой их в любом редакторе:

```bash
open -a TextEdit input/private_keys.txt
open -a TextEdit input/proxies.txt
```

Положи туда приватники и прокси (по одному на строку).

## 7. Настроить parameters.py

```bash
open -a TextEdit parameters.py
```

Минимум — впиши `CAPSOLVER_API_KEY`. Остальное можно оставить дефолтным.

## 8. Запустить

```bash
python main.py
```

Появится меню. Стрелками ↑↓, Enter — выбор. Первый раз выбери **«Создать базу данных»** — софт зашифрует приватники и очистит txt-файлы.

## 9. На последующих запусках

```bash
cd ~/crypto/outcome-MXW
source env/bin/activate
python main.py
```

Три команды. Можно положить в alias:

```bash
echo 'alias outcome="cd ~/crypto/outcome-MXW && source env/bin/activate && python main.py"' >> ~/.zshrc
source ~/.zshrc
```

Дальше — просто `outcome` в Terminal.

## Деактивация venv

```bash
deactivate
```

(Или просто закрой окно Terminal.)
