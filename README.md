# Shadowrocket rules

Личные списки правил Shadowrocket, перенесённые из `soin-mini-2.conf` 26.11.2026.

## Файлы

- [proxy.list](proxy.list) — 20 пользовательских правил, политика `PROXY`.
- [direct.list](direct.list) — 11 пользовательских правил, политика `DIRECT`.
- [block.list](block.list) — пустой список блокировок (только комментарии).

Внешние списки YouTube и Telegram от blackmatrix7 не дублируются: подключаются отдельно из основной конфигурации. Существующие настройки DNS в секциях `[General]` и `[Host]` тоже остаются в конфигурации.

## Подключение

Добавь в существующий раздел `[Rule]` текущего конфигурационного файла Shadowrocket (выше `FINAL,DIRECT`):

```ini
RULE-SET,https://raw.githubusercontent.com/soin365/shadowrocket-rules/main/block.list,REJECT
RULE-SET,https://raw.githubusercontent.com/soin365/shadowrocket-rules/main/direct.list,DIRECT
RULE-SET,https://raw.githubusercontent.com/soin365/shadowrocket-rules/main/proxy.list,PROXY
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Shadowrocket/YouTube/YouTube.list,PROXY
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Shadowrocket/Telegram/Telegram.list,PROXY
FINAL,DIRECT
```

`DIRECT` намеренно стоит выше `PROXY`, чтобы явные исключения обрабатывались первыми. Это небольшое изменение приоритета по сравнению с исходным файлом при пересечении правил; политики самих правил не менялись. Если требуется буквальное сохранение порядка каждого правила исходника, используйте исходную конфигурацию.

Сохраняй существующие `[General]`, `[Host]` и остальные секции без изменений. `PROXY` должно соответствовать названию политики клиента.

## Редактирование

В каждом `.list` одна запись в строке:

```text
DOMAIN-SUFFIX,example.com
DOMAIN-KEYWORD,example
```

Не добавляй `,PROXY` или `,DIRECT` внутрь списка — политика задана строкой `RULE-SET` в основной конфигурации.

После изменения списков обнови удалённые ресурсы в Shadowrocket. Не публикуй в репозитории пароли, UUID, приватные ключи или ссылки на приватные подписки.
