Просмотр логов systemd-сервисов

```bash
journalctl -u <svc>         # все логи сервиса
journalctl -b -u <svc>      # логи с текущей загрузки
journalctl -n 50            # последние 50 строк
journalctl --no-pager       # без less (удобно для grep)
journalctl -f               # follow (как tail -f)
```

**Подводные камни:**

- Без sudo обычный юзер видит только свои логи
- `-b` = текущий бут (boot), без него покажет всё с начала времён
- Если юнит битый (inline-комментарии) → `-- No entries --`
