
[https://www.vagrantup.com/downloads](https://www.vagrantup.com/downloads?spm=a2ty_o01.29997173.0.0.48b05171lxBu8r)

Создаем папку для проекта и в ней открываем PowerShell.

В PowerShell создаем файл Vagrantfile ( без расширения .txt)
``New-Item -Path "C:\temp\newfile.txt" -ItemType File``

Вставим туда этот код (это конфиг для трех тачек с 512 мб )
```
Vagrant.configure("2") do |config|
  # Общие настройки для всех машин
  config.vm.box = "generic/debian11" # Легкий образ Debian
  config.vm.synced_folder ".", "/vagrant", disabled: true # Отключаем лишние шары

  # 1. Машина управления (Ansible Control Node)
  config.vm.define "ansible" do |ansible|
    ansible.vm.hostname = "ansible-control"
    ansible.vm.network "private_network", ip: "192.168.56.10"
    ansible.vm.provider "virtualbox" do |vb|
      vb.memory = "1024" # Дадим чуть больше памяти, тут будет работать мозг
      vb.cpus = 1
    end
  end

  # 2. Целевая машина 1 (Target 1)
  config.vm.define "web1" do |web1|
    web1.vm.hostname = "web-server-1"
    web1.vm.network "private_network", ip: "192.168.56.11"
    web1.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
    end
  end

  # 3. Целевая машина 2 (Target 2)
  config.vm.define "web2" do |web2|
    web2.vm.hostname = "web-server-2"
    web2.vm.network "private_network", ip: "192.168.56.12"
    web2.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
    end
  end
end
```


в PowerShell в папке (```cd D:\Slurm\ansible-lab```)

```
vagrant up
```

_Первый раз он скачает образ (может занять время), дальше будет создавать виртуалки. Это займет минут 5-10._
Когда увидим надпись `Machine 'web2' has been successfully started!`, всё готово.

Теперь нам нужно попасть на тачку ansible, чтобы все настроить.

```
vagrant ssh ansible
```

Мы окажемся внутри виртуалки (промпт изменится на `vagrant@ansible-control:~$`).
