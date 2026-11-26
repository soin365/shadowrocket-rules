# Shadowrocket rules

Personal domain rule lists for Shadowrocket. The repository does **not** contain VPN credentials or server settings.

## Files

- [proxy.list](proxy.list): route these domains through a proxy.
- [direct.list](direct.list): route these domains directly.
- [block.list](block.list): reject these domains.

Only `proxy.list` contains starter entries (ChatGPT/OpenAI, Claude and basic YouTube domains). The other lists are templates and do not change routing until you add domains.

## Use in Shadowrocket

In your existing Shadowrocket configuration, add these entries to the **existing** `[Rule]` section (do not create a second `[Rule]` header):

```ini
RULE-SET,https://raw.githubusercontent.com/soin365/shadowrocket-rules/main/block.list,REJECT
RULE-SET,https://raw.githubusercontent.com/soin365/shadowrocket-rules/main/direct.list,DIRECT
RULE-SET,https://raw.githubusercontent.com/soin365/shadowrocket-rules/main/proxy.list,PROXY
```

Insert them **above** your existing `FINAL` (or `MATCH`) rule, leaving that fallback unchanged. Rules are considered in order: earlier matching entries take precedence.

`PROXY` must be a valid policy in your current configuration; otherwise replace it with the actual proxy group/policy name. These files contain **matching rules only**, not proxies.

## Edit the lists

One rule per line, for example:

```text
DOMAIN-SUFFIX,example.com
DOMAIN,api.example.com
```

A line beginning with `#` is a comment. Edit files on GitHub and refresh the associated remote rules in Shadowrocket to apply changes. Be aware that remotely fetched lists may be cached.

## Notes

- Do not publish UUIDs, keys, subscription URLs or other secrets in this public repository.
- The starter YouTube list is not guaranteed to cover every host used by YouTube.
