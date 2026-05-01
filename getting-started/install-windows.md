---
description: Установка софта на Windows — пошагово.
---

# Установка на Windows

## 1. Установить Python 3.10+

1. Скачай с [python.org/downloads](https://www.python.org/downloads/) — версия 3.12.x (или новее).
2. **Важно:** при установке поставь галочку **«Add Python to PATH»**.
3. Перезагрузи компьютер (не обязательно, но избавит от проблем с PATH).

Проверь в PowerShell:

```powershell
python --version
```

Должно вывести `Python 3.12.x`.

## 2. Установить Git

1. Скачай с [git-scm.com](https://git-scm.com/download/win).
2. Установщик — все настройки **по умолчанию**, не меняй ничего.

Проверь:

```powershell
git --version
```

## 3. Клонировать репо

Открой PowerShell (Win+X → Terminal или PowerShell):

```powershell
mkdir C:\crypto
cd C:\crypto
git clone https://github.com/fallex/outcome-MXW.git
cd outcome-MXW
```

## 4. Создать и активировать venv

```powershell
python -m venv env
env\Scripts\activate
```

Слева появится `(env)` — виртуалка активна.

> ⚠️ Если PowerShell ругается на запрет скриптов — выполни **один раз** от админа:
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```
> Согласись на изменение, потом снова `env\Scripts\activate`.

> ⚠️ Каждый новый запуск PowerShell — нужно снова `cd C:\crypto\outcome-MXW` и `env\Scripts\activate`.

## 5. Установить зависимости

```powershell
pip install -r requirements.txt
```

## 6. Подготовить input-файлы

```powershell
move input\private_keys.txt.example input\private_keys.txt
move input\proxies.txt.example      input\proxies.txt
notepad input\private_keys.txt
notepad input\proxies.txt
```

Положи туда приватники и прокси (по одному на строку), сохрани.

## 7. Настроить parameters.py

```powershell
notepad parameters.py
```

Впиши свой `CAPSOLVER_API_KEY`, сохрани.

## 8. Запустить

```powershell
python main.py
```

Меню — стрелки ↑↓, Enter. Первый раз — **«Создать базу данных»**.

## 9. На последующих запусках

```powershell
cd C:\crypto\outcome-MXW
env\Scripts\activate
python main.py
```

Можно сделать `.bat`-файл `start_outcome.bat` на рабочем столе:

```bat
@echo off
cd /d C:\crypto\outcome-MXW
call env\Scripts\activate
python main.py
pause
```

Двойной клик — софт запущен.

## Если ничего не работает

* Проверь: открой PowerShell, набери `python --version` и `git --version`. Оба должны выдать версии.
* Если `python` пишет «не найдена» — Python не в PATH. Переустанови с галочкой **Add to PATH**.
* Если `pip install` падает с ошибкой про SSL — обнови pip: `python -m pip install --upgrade pip`.
* Если совсем тупик — пиши в чат MXW с скриншотом ошибки.
