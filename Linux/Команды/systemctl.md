
```bash
# Linux Commands by Topic

Каждая тема = 3-5 команд, которые я реально использовал. Не больше.

---

## Systemd / Services


### systemctl

**Зачем:** управление сервисами (старт, стоп, статус, автозапуск)

**Синтаксис:**

systemctl start <svc>       # запустить
systemctl stop <svc>        # остановить
systemctl restart <svc>     # перезапустить
systemctl enable <svc>      # добавить в автозапуск (создаёт симлинк)
systemctl disable <svc>     # убрать из автозапуска
systemctl status <svc>      # статус
systemctl daemon-reload     # перечитать юнит-файлы после правки
```

**Подводные камни:**

- `enable` создаёт симлинк в `/etc/systemd/system/multi-user.target.wants/`
- После `disable` симлинк удаляется, но юнит остаётся в `/etc/systemd/system/`
- Если юнит падал 36 раз подряд → `reset-failed` чтобы сбросить счётчик