---
description: Где брать сотни кошельков под софты.
---

# Кошельки

## Главное правило

Кошельки для софтов — **отдельные**. Не основные. Подробнее: [Безопасность → Аккаунты](../security/wallets.md).

## Способ 1 — Сгенерить локально (бесплатно)

EVM-кошелёк — это просто 32 случайных байта. Сгенерить можно в одну команду.

### macOS / Linux

```bash
python3 -c "
from eth_account import Account
import secrets
for i in range(100):
    pk = '0x' + secrets.token_hex(32)
    acc = Account.from_key(pk)
    print(f'{pk} {acc.address}')
" > wallets.txt
```

Получишь файл с 100 строками вида `0x... 0xADDRESS`. Приватники → в `input/private_keys.txt`, адреса → отдельно для пополнения газом.

> Перед запуском проверь, что `eth_account` установлен: `pip install eth-account`. Он уже есть в `requirements.txt` любого софта.

### Windows (PowerShell)

```powershell
python -c "from eth_account import Account; import secrets; [print(f'0x{secrets.token_hex(32)} {Account.from_key(\"0x\" + secrets.token_hex(32)).address}') for _ in range(100)]" > wallets.txt
```

## Способ 2 — ct.app

[ct.app](https://ct.app/) — сервис для массовой генерации/менеджмента кошельков. Полезен, если нужны не только EVM, но и Solana / Aptos / Sui / etc. в одном интерфейсе.

Бесплатный, удобный и проверенный.

## Способ 3 — Из других источников

* Импорт из старых ферм/софтов (если уже есть пул).
* Просто руками нагенерировать в кошельках (например Rabby)

## Финансирование

После того как есть приватники:

1. Снять адреса в отдельный список.
2. Залить газ.
3. Для тестнетов — дополнительно собрать тестовые токены (faucets, либо через сам софт, как в Outcome-MXW).

### Сколько газа закладывать

Для каждого софта в `parameters.py` указаны амуны транзакций. Прикинь:

```
газ_на_тx × количество_тx_за_цикл × количество_циклов = запас_на_акк
```

Для Outcome-MXW на HYPE вообще не нужен газ.
