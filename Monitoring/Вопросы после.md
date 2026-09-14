#### Разбор команд

```
echo slave1 | sudo tee /etc/hostname
sudo sed -i 's/mon-01/slave1/g' /etc/hosts
sudo hostname -F /etc/hostname   # применит без ребута
```

```
ip a | grep inet
systemctl status ssh --no-pager
sudo ss -tlnp | grep :22
```

```
sudo useradd --no-create-home --shell /bin/false prometheus  # Юзер без home и без shell - принцип минимальных привилегий, даже если прометей взломают, пойти будет некуда
```

```
sudo cp prometheus promtool /usr/local/bin/
sudo cp prometheus.yml /etc/prometheus/
sudo chown -R prometheus:prometheus /etc/prometheus /var/lib/prometheus
promtool --version    # работает без sudo? отлично, бинарники на месте

### Бинарники оставляем root:root — исполняемым файлам не нужно владение prometheus, ему нужны только конфиг и data-директория.
```

