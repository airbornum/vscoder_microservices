# vscoder_microservices

vscoder microservices repository

# Makefile

## Переменные

| variable               | default                    | description                                                              |
| ---------------------- | -------------------------- | ------------------------------------------------------------------------ |
| BIN_DIR                | ~/bin                      | Путь для установки исполняемых файлов для целей `install_docker_machine` |
| TEMP_DIR               | /tmp                       | Временная директория для загрузки файлов                                 |
| DOCKER_MACHINE_VERSION | v0.16.0                    | Версия docker-machine                                                    |
| DOCKER_MACHINE_OS      | \$(shell uname -s)         | Название операционной системы                                            |
| DOCKER_MACHINE_ARCH    | \$(shell uname -m)         | Название архитектуры                                                     |
| DOCKER_MACHINE         | \${BIN_DIR}/docker-machine | Путь к исполняемому файлу `docker-machine`                               |

## Цели

| target                 | used variables                                                    | description                                                                                        |
| ---------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| debug                  | все                                                               | Показать значения всех переменных                                                                  |
| install_requirements   | нет                                                               | Установить в python virualenv [./venv](./venv) зависимости из [requirements.txt](requirements.txt) |
| install_docker_machine | DOCKER_MACHINE_BASEURL, DOCKER_MACHINE_VERSION, TEMP_DIR, BIN_DIR | Скачать и установить в `${BIN_DIR}` исполняемый файл `docker-machine`                              |

# Домашние задания

## HomeWork 12: Технология контейнеризации. Введение в Docker

### Подготовка проекта. Интеграции

- Склонирован репозиторий [Otus-DevOps-2019-08/vscoder_microservices
  ](https://github.com/Otus-DevOps-2019-08/vscoder_microservices)
- Выполнена интеграция со slack:
  - workspace `devops-team-otus.slack.com`
  - В чате aleksey_koloskov выполнена команда `/github subscribe Otus-DevOps-2019-08/vscoder_microservices commits:all`
- Настроены уведомления в slack от travis-ci
  - В клиенте: _+ Add apps_ -> _Travis-CI_ -> _Settings_ -> _Add to Slack_
  - В [.travis.yml](.travis.yml) настроены уведомления по инструкции с открывшейся страницы
    ```yaml
    notifications:
      slack: slackchannel:faketoken
    ```
- Добавлен [.gitignore](.gitignore)
- Добавлен Makefile. Цели:
  - install_requirements
  - install_docker_machine

### Установка docker

- Установлен docker как описано в документации https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/

  <details><summary>docker version</summary>
  <p>

  ```
  Client: Docker Engine - Community
   Version:           19.03.4
   API version:       1.40
   Go version:        go1.12.10
   Git commit:        9013bf583a
   Built:             Fri Oct 18 15:54:09 2019
   OS/Arch:           linux/amd64
   Experimental:      false

  Server: Docker Engine - Community
   Engine:
    Version:          19.03.4
    API version:      1.40 (minimum version 1.12)
    Go version:       go1.12.10
    Git commit:       9013bf583a
    Built:            Fri Oct 18 15:52:40 2019
    OS/Arch:          linux/amd64
    Experimental:     false
   containerd:
    Version:          1.2.10
    GitCommit:        b34a5c8af56e510852c35414db4c1f4fa6172339
   runc:
    Version:          1.0.0-rc8+dev
    GitCommit:        3e425f80a8c931f88e6d94a8c831b9d5aa481657
   docker-init:
    Version:          0.18.0
    GitCommit:        fec3683
  ```

  </p>
  </details>
  <br>
  <details><summary>docker info</summary>
  <p>

  ```
  Client:
   Debug Mode: false

  Server:
   Containers: 0
    Running: 0
    Paused: 0
    Stopped: 0
   Images: 0
   Server Version: 19.03.4
   Storage Driver: overlay2
    Backing Filesystem: extfs
    Supports d_type: true
    Native Overlay Diff: true
   Logging Driver: json-file
   Cgroup Driver: cgroupfs
   Plugins:
    Volume: local
    Network: bridge host ipvlan macvlan null overlay
    Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
   Swarm: inactive
   Runtimes: runc
   Default Runtime: runc
   Init Binary: docker-init
   containerd version: b34a5c8af56e510852c35414db4c1f4fa6172339
   runc version: 3e425f80a8c931f88e6d94a8c831b9d5aa481657
   init version: fec3683
   Security Options:
    apparmor
    seccomp
     Profile: default
   Kernel Version: 5.0.0-32-generic
   Operating System: Ubuntu 18.04.3 LTS
   OSType: linux
   Architecture: x86_64
   CPUs: 12
   Total Memory: 31.28GiB
   Name: vsc-home
   ID: RPZE:O6VJ:2IMK:H4GU:AGV7:BHBM:C5HT:MI5X:GYSH:MHZ5:BWDV:HHUC
   Docker Root Dir: /var/lib/docker
   Debug Mode: false
   Registry: https://index.docker.io/v1/
   Labels:
   Experimental: false
   Insecure Registries:
    127.0.0.0/8
   Live Restore Enabled: false

  WARNING: No swap limit support
  ```

  </p>
  </details>
  <br>
  <details><summary>docker run hello-world</summary>
  <p>

  ```
  Unable to find image 'hello-world:latest' locally
  latest: Pulling from library/hello-world
  1b930d010525: Pull complete
  Digest: sha256:c3b4ada4687bbaa170745b3e4dd8ac3f194ca95b2d0518b417fb47e5879d9b5f
  Status: Downloaded newer image for hello-world:latest

  Hello from Docker!
  This message shows that your installation appears to be working correctly.

  To generate this message, Docker took the following steps:
   1. The Docker client contacted the Docker daemon.
   2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
      (amd64)
   3. The Docker daemon created a new container from that image which runs the
      executable that produces the output you are currently reading.
   4. The Docker daemon streamed that output to the Docker client, which sent it
      to your terminal.

  To try something more ambitious, you can run an Ubuntu container with:
   $ docker run -it ubuntu bash

  Share images, automate workflows, and more with a free Docker ID:
   https://hub.docker.com/

  For more examples and ideas, visit:
   https://docs.docker.com/get-started/
  ```

  </p>
  </details>

- Установлен docker-compose в [./venv](.venv)
  ```shell
  docker-compose version 1.24.1, build 4667896
  ```
- Установлен бинарник `docker-machine`
  ```shell
  docker-machine version 0.16.0, build 702c267f
  ```

### Работа с docker

- Список основных команд docker
  
  | Команда                                                                       | Описание                                                                                                                                            |
  | ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
  | docker ps                                                                     | Список запущенных контейнеров                                                                                                                       |
  | docker ps -a                                                                  | Список всех контейнеров                                                                                                                             |
  | docker images                                                                 | Список локально сохранённых образов                                                                                                                 |
  | docker run -it ubuntu:16.04 /bin/bash                                         | Запустить `/bin/bash` в контейнере ubuntu:16:04. Каждый раз создаётся новый контейнер. Без флага `--rm` остановленный контейнер останется на диске. |
  | docker ps -a --format "table {{.ID}}\t{{.Image}}\t{{.CreatedAt}}\t{{.Names}}" | Список всех контейнеров. Выводятся таблица с указанными столбцами                                                                                   |
  | docker start <u_container_id>                                                 | Запустить ранее остановленный контейнер                                                                                                             | docker attach <u_container_id> | Подключить терминал к созданному контейнеру. Для отключения нажать `CTRL+p` `CTRL+q` |
  | docker create                                                                 | Создать контейнер, не запуская его                                                                                                                  |
  | docker exec -it <u_container_id> bash                                         | Запустить новый процесс внутри контейнера                                                                                                           |
  | docker commit <u_container_id> yourname/ubuntu-tmp-file                       | Создать образ yourname/ubuntu-tmp-file из контейнера <u_container_id>. Контейнер при этом останется запущенным.                                     |

- Примечание _docker run = docker create + docker start + docker attach\*_ \* _docker attach_ выполняется при наличии опции `-i`
- Основный опции
  | Опция        | Описание                                                   |
  | ------------ | ---------------------------------------------------------- |
  | -i           | запускает контейнер в foreground режиме (docker attach)    |
  | -d           | запускает контейнер в background режиме                    |
  | -t           | создает TTY                                                |
  | --entrypoint | позволяет переопределить ENTRYPOINT при запуске контейнера |
- После выполнения команд из ДЗ, список образов сохранён в [docker-monolith/docker-1.log](docker-monolith/docker-1.log)

### Задание со \*: Отличия образа и контейнера

* Сылки по теме:
  * An Image is an ordered collection of root filesystem changes and the corresponding execution parameters for use within a container runtime.
  * [About storage drivers](https://docs.docker.com/storage/storagedriver/)
  * [How the overlay2 driver works](https://docs.docker.com/storage/storagedriver/overlayfs-driver/#how-the-overlay2-driver-works)
  * [Docker Image Specification v1.2.0. Image JSON Field Descriptions](https://github.com/docker/docker-ce/blob/master/components/engine/image/spec/v1.2.md)
  * [Образы и контейнеры Docker в картинках](https://habr.com/en/post/272145/)
  * [What to Inspect When You're Inspecting](https://www.ctl.io/developers/blog/post/what-to-inspect-when-youre-inspecting)
  * [Engine API v1.24](https://docs.docker.com/engine/api/v1.24/)
  * [Подключение контейнера к нескольким сетям](https://success.docker.com/article/multiple-docker-networks)
* Произведён анализ результатов вывода команды `docker inspect <u_image_id>`.
  <details><summary>Результаты</summary>
  <p>

  ```json
  [
    {
      "Id": "sha256:5f2bf26e35249d8b47f002045c57b2ea9d8ba68704f45f3c209182a7a2a9ece5",  # SHA256 hash of its configuration JSON
      "RepoTags": [  # Список тегов образа
        "ubuntu:16.04"
      ],
      "RepoDigests": [  # Чексумма образа
        "ubuntu@sha256:bb5b48c7750a6a8775c74bcb601f7e5399135d0a06de004d000e05fd25c1a71c"
      ],
      "Parent": "",  # ID вышестоящего слоя в хранилище образов. Пуст в связи с отсутствием родительских слоёв в локальном хранилище. Подробнее: https://stackoverflow.com/questions/45820905/docker-image-inspection-json-interpretation Документация: https://docs.docker.com/storage/storagedriver/
      "Comment": "",  # Комментарий
      "Created": "2019-10-31T22:21:29.640561379Z",  # Дата создания образа
      "Container": "363288fa6924e2d1e1b00da6525ffde40bb0de65b1da6ce6e44e363df532614e",  # Временный идентификатор контейнера, созданного во время сборки образа. Docker will create a container during the image construction process, and this identifier is stored in the image data.
      "ContainerConfig": {  # This data again is referring to the temporary container created when the Docker build command was executed
        "Hostname": "363288fa6924",
        "Domainname": "",
        "User": "",
        "AttachStdin": false,
        "AttachStdout": false,
        "AttachStderr": false,
        "Tty": false,
        "OpenStdin": false,
        "StdinOnce": false,
        "Env": [
          "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        ],
        "Cmd": [
          "/bin/sh",
          "-c",
          "#(nop) ",
          "CMD [\"/bin/bash\"]"
        ],
        "ArgsEscaped": true,
        "Image": "sha256:66d791e2304a4caa9fda9b56ad9fff2679e7b933c83d23fca8e3ec3b5595c4dc",
        "Volumes": null,
        "WorkingDir": "",
        "Entrypoint": null,
        "OnBuild": null,
        "Labels": {}
      },
      "DockerVersion": "18.06.1-ce",  # Версия docker, используемая при сборке образа
      "Author": "",  # Автор образа
      "Config": {  # Конфигурационные параметры, которые должны быть взяты за основу при запуске контейнера на основе данного образа. Судя по документации, все эти параметры можно переопределить при создании контейнера
        "Hostname": "",
        "Domainname": "",
        "User": "",  # Пользователь запускаемого контейнера по-умолчанию
        "AttachStdin": false,
        "AttachStdout": false,
        "AttachStderr": false,
        "Tty": false,
        "OpenStdin": false,
        "StdinOnce": false,
        "Env": [  # Переменные окружения
          "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        ],
        "Cmd": [  # CMD по умолчанию
          "/bin/bash"
        ],
        "ArgsEscaped": true,
        "Image": "sha256:66d791e2304a4caa9fda9b56ad9fff2679e7b933c83d23fca8e3ec3b5595c4dc",
        "Volumes": null,  # Тома по-умолчанию
        "WorkingDir": "",  # Рабочая директория по-умолчанию
        "Entrypoint": null,  # ENTRYPOINT по-умолчанию
        "OnBuild": null,
        "Labels": null
      },
      "Architecture": "amd64",  # Архитектура, для которой созданы бинарные файлы образа [i386, amd64, arm]
      "Os": "linux",  # Название ОС, в которой должен запускаться образ
      "Size": 122564827,
      "VirtualSize": 122564827,  # The size of the image reported in bytes
      "GraphDriver": { # https://docs.docker.com/storage/storagedriver/select-storage-driver/
        "Data": {  # https://stackoverflow.com/a/56551786/3488348
          "LowerDir": "/var/lib/docker/overlay2/897edb9e383005a310bb7685eda9b259c5c0b7740d2d65e7d1c44f228dc73ce9/diff:/var/lib/docker/overlay2/bc1b6b3a839591c8870d5aa8ad328af83c5325b82a88163986a0186b11016921/diff:/var/lib/docker/overlay2/11810c8b5bbff1b9b14089bcef62d0029a39ae0686c51a5ce0e616e71f2573bf/diff",
          "MergedDir": "/var/lib/docker/overlay2/8dac1ac5277e9c3bf4e3d7111d947bf2f4553dd85764077b0ed057d3e1b93022/merged",
          "UpperDir": "/var/lib/docker/overlay2/8dac1ac5277e9c3bf4e3d7111d947bf2f4553dd85764077b0ed057d3e1b93022/diff",
          "WorkDir": "/var/lib/docker/overlay2/8dac1ac5277e9c3bf4e3d7111d947bf2f4553dd85764077b0ed057d3e1b93022/work"
        },
        "Name": "overlay2" # https://docs.docker.com/storage/storagedriver/overlayfs-driver/#how-the-overlay2-driver-works
      },
      "RootFS": {  # Ссылается на адреса содержимого слоёв, используемых образом
        "Type": "layers",
        "Layers": [
          "sha256:788b17b748c23d38ec62e913e87b084b7e3efda49843b3c0809b1857559b553e",
          "sha256:a5a5f8c62487121247923a4df970f2094725ac2fea8c1347236466c4a3265ae0",
          "sha256:903669ee720750938f08f95f7c8f1022d7fd7c57602af847b316f0b39efbd01c",
          "sha256:bc72fb2e7b7487b3b9f9135437319525feaf1fab6ba61dab7e2e961e5c1dbb8b"
        ]
      },
      "Metadata": {  # Метаданные
        "LastTagTime": "0001-01-01T00:00:00Z"
      }
    }
  ]
  
  ```

  </p>
  </details>
* Произведён анализ вывода команды `docker inspect <u_container_id>`
  <details><summary>Результаты</summary>
    <p>

  ```json
  [
      {
          "Id": "03a9eea159ef6e417a2e67802c5fa021f4a8d0b634ba377cd0074d6ff5eef511",
          "Created": "2019-11-02T16:08:06.723203393Z",  # Дата создания контейнера
          "Path": "bash",
          "Args": [],
          "State": {  # Описание статуса контейнера
              "Status": "running",  # Текущее состояние
              "Running": true,  # Запущен?
              "Paused": false,  # Приостановлен?
              "Restarting": false,  # Перезапускается?
              "OOMKilled": false,  # Убит OOM-киллером?
              "Dead": false,  # Упал (умер)?
              "Pid": 25711,  # ID процесса контейнера в host os
              "ExitCode": 0,  # Кот завершения (используется для перезапуска после падения)
              "Error": "",  # Ошибка в случае падения
              "StartedAt": "2019-11-02T16:08:07.16481008Z",  # Время запуска
              "FinishedAt": "0001-01-01T00:00:00Z"  # Время завершения
          },
          "Image": "sha256:5f2bf26e35249d8b47f002045c57b2ea9d8ba68704f45f3c209182a7a2a9ece5",  # ID образа, на базе которого создан контейнер
          "ResolvConfPath": "/var/lib/docker/containers/03a9eea159ef6e417a2e67802c5fa021f4a8d0b634ba377cd0074d6ff5eef511/resolv.conf",
          "HostnamePath": "/var/lib/docker/containers/03a9eea159ef6e417a2e67802c5fa021f4a8d0b634ba377cd0074d6ff5eef511/hostname",
          "HostsPath": "/var/lib/docker/containers/03a9eea159ef6e417a2e67802c5fa021f4a8d0b634ba377cd0074d6ff5eef511/hosts",
          "LogPath": "/var/lib/docker/containers/03a9eea159ef6e417a2e67802c5fa021f4a8d0b634ba377cd0074d6ff5eef511/03a9eea159ef6e417a2e67802c5fa021f4a8d0b634ba377cd0074d6ff5eef511-json.log",
          "Name": "/wonderful_blackwell",  # Имя контейнера. Генериться случайным образом, если не задано явно
          "RestartCount": 0,  # Количество перезапусков. Используется для https://docs.docker.com/engine/reference/commandline/run/#restart-policies---restart
          "Driver": "overlay2",
          "Platform": "linux",
          "MountLabel": "",
          "ProcessLabel": "",
          "AppArmorProfile": "docker-default",
          "ExecIDs": null,
          "HostConfig": {  # Конфигурация хост-системы
              "Binds": null,
              "ContainerIDFile": "",
              "LogConfig": {  # Настройки логгирования
                  "Type": "json-file",
                  "Config": {}
              },
              "NetworkMode": "default",  # Sets the networking mode for the container. Supported standard values are: bridge, host, none, and container:<name|id>. Any other value is taken as a custom network’s name to which this container should connect to.
              "PortBindings": {},  # Пробросы портов
              "RestartPolicy": {  # Политика перезапуска https://docs.docker.com/engine/reference/commandline/run/#restart-policies---restart
                  "Name": "no",
                  "MaximumRetryCount": 0
              },
              "AutoRemove": false,  # Автоматически удалять контейнер после установки
              "VolumeDriver": "",  # Driver that this container users to mount volumes.
              "VolumesFrom": null,  # A list of volumes to inherit from another container. Specified in the form <container name>[:<ro|rw>]
              "CapAdd": null,  # A list of kernel capabilities added to the container.
              "CapDrop": null,  # A list of kernel capabilities dropped from the container.
              "Capabilities": null,
              "Dns": [],  # dns-сервера, используемые контейнером
              "DnsOptions": [],
              "DnsSearch": [],
              "ExtraHosts": null,  # Дополнительные записи в /etc/hosts
              "GroupAdd": null,  # A list of additional groups that the container process will run as
              "IpcMode": "private",
              "Cgroup": "",
              "Links": null,  # A list of links for the container. Each link entry is in the form of container_name:alias.
              "OomScoreAdj": 0,  # An integer value containing the score given to the container in order to tune OOM killer preferences.
              "PidMode": "",  # Set the PID (Process) Namespace mode for the container; "container:<name|id>": joins another container’s PID namespace "host": use the host’s PID namespace inside the container
              "Privileged": false,  # Контейнер запущен в привилегированном режиме https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities
              "PublishAllPorts": false,  # Allocates an ephemeral host port for all of a container’s exposed ports. Specified as a boolean value. Ports are de-allocated when the container stops and allocated when the container starts. The allocated port might be changed when restarting the container.
              "ReadonlyRootfs": false,  # Файловая система контейнера смонтирована только для чтения
              "SecurityOpt": null,  # A list of string values to customize labels for MLS systems, such as SELinux.
              "UTSMode": "",
              "UsernsMode": "",  # Sets the usernamespace mode for the container when usernamespace remapping option is enabled. supported values are: host.
              "ShmSize": 67108864,  # Size of /dev/shm in bytes. The size must be greater than 0. If omitted the system uses 64MB.
              "Runtime": "runc",  # Используемый рантайм
              "ConsoleSize": [
                  0,
                  0
              ],
              "Isolation": "",  # isolation=(default	process	hyperv) (Windows daemon only)
              "CpuShares": 0,  # An integer value containing the container’s CPU Shares (ie. the relative weight vs other containers).
              "Memory": 0,  # Memory limit in bytes.
              "NanoCpus": 0,
              "CgroupParent": "",  # Path to cgroups under which the container’s cgroup is created. If the path is not absolute, the path is considered to be relative to the cgroups path of the init process. Cgroups are created if they do not already exist.
              "BlkioWeight": 0,  # Block IO weight (relative weight) accepts a weight value between 10 and 1000.
              "BlkioWeightDevice": [],
              "BlkioDeviceReadBps": null,
              "BlkioDeviceWriteBps": null,
              "BlkioDeviceReadIOps": null,
              "BlkioDeviceWriteIOps": null,
              "CpuPeriod": 0,  # The length of a CPU period in microseconds.
              "CpuQuota": 0,  # Microseconds of CPU time that the container can get in a CPU period.
              "CpuRealtimePeriod": 0,
              "CpuRealtimeRuntime": 0,
              "CpusetCpus": "",  # String value containing the cgroups CpusetCpus to use.
              "CpusetMems": "",  # Memory nodes (MEMs) in which to allow execution (0-3, 0,1). Only effective on NUMA systems.
              "Devices": [],  # A list of devices to add to the container specified as a JSON object in the form { "PathOnHost": "/dev/deviceName", "PathInContainer": "/dev/deviceName", "CgroupPermissions": "mrw"}
              "DeviceCgroupRules": null,
              "DeviceRequests": null,
              "KernelMemory": 0,  # Kernel memory limit in bytes.
              "KernelMemoryTCP": 0,
              "MemoryReservation": 0,  # Memory soft limit in bytes.
              "MemorySwap": 0,  # Total memory limit (memory + swap); -1 is unlimited swap. You must use this with memory and make the swap value larger than memory.
              "MemorySwappiness": null,  # Tune a container’s memory swappiness behavior. Integer between 0 and 100.
              "OomKillDisable": false,  # Boolean value, whether to disable OOM Killer for the container or not.
              "PidsLimit": null,  # A container’s pids limit. -1 if unlimited.
              "Ulimits": null,  # A list of ulimits to set in the container, specified as { "Name": <name>, "Soft": <soft limit>, "Hard": <hard limit> }, for example: Ulimits: { "Name": "nofile", "Soft": 1024, "Hard": 2048 }
              "CpuCount": 0,
              "CpuPercent": 0,  # An integer value containing the usable percentage of the available CPUs. (Windows daemon only)
              "IOMaximumIOps": 0,  # Maximum IO absolute rate in terms of bytes per second.
              "IOMaximumBandwidth": 0,  # Maximum IO absolute rate in terms of IOps.
              "MaskedPaths": [
                  "/proc/asound",
                  "/proc/acpi",
                  "/proc/kcore",
                  "/proc/keys",
                  "/proc/latency_stats",
                  "/proc/timer_list",
                  "/proc/timer_stats",
                  "/proc/sched_debug",
                  "/proc/scsi",
                  "/sys/firmware"
              ],
              "ReadonlyPaths": [
                  "/proc/bus",
                  "/proc/fs",
                  "/proc/irq",
                  "/proc/sys",
                  "/proc/sysrq-trigger"
              ]
          },
          "GraphDriver": {
              "Data": {
                  "LowerDir": "/var/lib/docker/overlay2/7ebf817bfc93f412448a4e804d2f149b25d4072c6985ab185216648194786889-init/diff:/var/lib/docker/overlay2/8dac1ac5277e9c3bf4e3d7111d947bf2f4553dd85764077b0ed057d3e1b93022/diff:/var/lib/docker/overlay2/897edb9e383005a310bb7685eda9b259c5c0b7740d2d65e7d1c44f228dc73ce9/diff:/var/lib/docker/overlay2/bc1b6b3a839591c8870d5aa8ad328af83c5325b82a88163986a0186b11016921/diff:/var/lib/docker/overlay2/11810c8b5bbff1b9b14089bcef62d0029a39ae0686c51a5ce0e616e71f2573bf/diff",
                  "MergedDir": "/var/lib/docker/overlay2/7ebf817bfc93f412448a4e804d2f149b25d4072c6985ab185216648194786889/merged",
                  "UpperDir": "/var/lib/docker/overlay2/7ebf817bfc93f412448a4e804d2f149b25d4072c6985ab185216648194786889/diff",
                  "WorkDir": "/var/lib/docker/overlay2/7ebf817bfc93f412448a4e804d2f149b25d4072c6985ab185216648194786889/work"
              },
              "Name": "overlay2"  # https://docs.docker.com/storage/storagedriver/overlayfs-driver/#how-the-overlay2-driver-works
          },
          "Mounts": [],  # Specification for mounts that was added to containers created as part of the service.
          "Config": {
              "Hostname": "03a9eea159ef",  # Имя хоста
              "Domainname": "",  # Домен
              "User": "",  # Пользователь внутри контейнера
              "AttachStdin": true,  # Attached to stdin
              "AttachStdout": true,  # Attached to stdout
              "AttachStderr": true,  # Attached to stderr
              "Tty": true,  # Standart streams attached to tty
              "OpenStdin": true,
              "StdinOnce": true,
              "Env": [  # A list of environment variables in the form of ["VAR=value", ...]
                  "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
              ],
              "Cmd": [  # CMD runned in container
                  "bash"
              ],
              "Image": "ubuntu:16.04",  # Имя образа контейнера
              "Volumes": null,  # An object mapping mount point paths (strings) inside the container to empty objects.
              "WorkingDir": "",  #  string specifying the working directory for commands to run in.
              "Entrypoint": null,  # ENTRYPOINT of a container
              "OnBuild": null,
              "Labels": {}  # A map of labels of a container
          },
          "NetworkSettings": {  # Настройки сети контейнера.
              "Bridge": "",
              "SandboxID": "b8b58bb4f3a477aca4a6d05ee397e6cb62859afa30d8806e64e8e8e130af9e05",
              "HairpinMode": false,  # https://en.wikipedia.org/wiki/Hairpinning
              "LinkLocalIPv6Address": "",
              "LinkLocalIPv6PrefixLen": 0,
              "Ports": {},  #  Mapped ports
              "SandboxKey": "/var/run/docker/netns/b8b58bb4f3a4",
              "SecondaryIPAddresses": null,
              "SecondaryIPv6Addresses": null,
              "EndpointID": "e7f60af3ade6a1ecba41456c0f3252f8edd502287c826a214c6318ef74f8efdf",
              "Gateway": "172.17.0.1",  # Network gateway
              "GlobalIPv6Address": "",
              "GlobalIPv6PrefixLen": 0,
              "IPAddress": "172.17.0.2",  # Container's ip address
              "IPPrefixLen": 16,
              "IPv6Gateway": "",
              "MacAddress": "02:42:ac:11:00:02",  # mac-address
              "Networks": {  # Сети и контейнера
                  "bridge": {
                      "IPAMConfig": null,
                      "Links": null,
                      "Aliases": null,
                      "NetworkID": "156780e8135120a2650a4d34c2a0aee35cd4d3cde3d98fb0e3b1ebfd3a797bfd",
                      "EndpointID": "e7f60af3ade6a1ecba41456c0f3252f8edd502287c826a214c6318ef74f8efdf",
                      "Gateway": "172.17.0.1",
                      "IPAddress": "172.17.0.2",
                      "IPPrefixLen": 16,
                      "IPv6Gateway": "",
                      "GlobalIPv6Address": "",
                      "GlobalIPv6PrefixLen": 0,
                      "MacAddress": "02:42:ac:11:00:02",
                      "DriverOpts": null
                  }
              }
          }
      }
  ]
  ```

  </p>
  </details>
* В файле [docker-monolith/docker-1.log](docker-monolith/docker-1.log) описаны различия между образом и контейнером

### Больше docker-команд

#### Docker kill & stop

Подробнее про [Сигналы в Linux](https://ru.wikipedia.org/wiki/Сигналы_(UNIX))

Описание:
* kill сразу посылает SIGKILL
* stop посылает SIGTERM, и через 10 секунд(настраивается) посылает SIGKILL
* SIGTERM - сигнал остановки приложения
* SIGKILL - безусловное завершение процесса

Практика:
* `docker ps -q`
  ```log
  cc75429464ba
  03a9eea159ef
  ```
* `docker kill cc75429464ba`
  ```log
  cc75429464ba
  ```
* `docker ps -q` - остался один запущенный контейнер
  ```log
  03a9eea159ef
  ```

#### docker system df

* Отображает сколько дискового пространства занято образами, контейнерами и volume’ами
* Отображает сколько из них не используется и возможно удалить

`docker system df`
```log
TYPE                TOTAL               ACTIVE              SIZE                RECLAIMABLE
Images              4                   3                   248.8MB             122.6MB (49%)
Containers          5                   1                   15B                 9B (60%)
Local Volumes       0                   0                   0B                  0B
Build Cache         0                   0                   0B                  0B
```

#### Docker rm & rmi

* rm удаляет контейнер, можно добавить флаг -f, чтобы удалялся работающий container(будет послан sigkill)
* rmi удаляет image, если от него не зависят запущенные контейнеры

`docker rm $(docker ps -a -q)` # удалит все незапущенные контейнеры
```log
cc75429464ba
5d9a698c4c62
2cf9183503e2
89716fceca99
Error response from daemon: You cannot remove a running container 03a9eea159ef6e417a2e67802c5fa021f4a8d0b634ba377cd0074d6ff5eef511. Stop the container before attempting removal or force remove
```

`docker rmi $(docker images -q)`
```log
Untagged: vscoder/ubuntu-tmp-file:latest
Deleted: sha256:e63bb81dd3f064fb9fe854a1e66ca76e30c79fbc54eb9f09c5ab054a8d0d8cd3
Untagged: nginx:latest
Untagged: nginx@sha256:922c815aa4df050d4df476e92daed4231f466acc8ee90e0e774951b0fd7195a4
Deleted: sha256:540a289bab6cb1bf880086a9b803cf0c4cefe38cbb5cdefa199b69614525199f
Deleted: sha256:ab18af7cee69bfb22c1771e54d5e0e68b1a1bf57bb46516142da0380b1771f4a
Deleted: sha256:02f7daf1e14541cd61a3dda1a61cc0f78fee8de2984d488b8ba5bbd3cbad9b57
Deleted: sha256:b67d19e65ef653823ed62a5835399c610a40e8205c16f839c5cc567954fcf594
Untagged: hello-world:latest
Untagged: hello-world@sha256:c3b4ada4687bbaa170745b3e4dd8ac3f194ca95b2d0518b417fb47e5879d9b5f
Deleted: sha256:fce289e99eb9bca977dae136fbe2a82b6b7d4c372474c9235adc1741675f587e
Deleted: sha256:af0b15c8625bb1938f1d7b17081031f649fd14e6b233688eea3c5483994a66a3
Error response from daemon: conflict: unable to delete 5f2bf26e3524 (cannot be forced) - image is being used by running container 03a9eea159ef
```


### Docker контейнеры

#### GCE

* Создан новый проект _docker_ id `docker-257914`
* gcloud SDK установлен ранее
* Выполнен `gcloud init` с созданием новой конфигурации _otus-devops-docker_
* Выполнен `gcloud auth application-default login` чтобы получить файл с авторизационными данными для docker-machine.
  Файл сохранён по пути `/home/<myuser>/.config/gcloud/application_default_credentials.json`

#### Docker machine

Установка в Linux https://docs.docker.com/machine/install-machine/

* docker-machine - встроенный в докер инструмент для создания хостов и установки на них docker engine. Имеет поддержку облаков и систем виртуализации (Virtualbox, GCP и др.)
* Команда создания - `docker-machine create <имя>`. Имен может быть много, переключение между ними через `eval $(docker-machine env <имя>)`. Переключение на локальный докер - `eval $(docker-machine env --unset)`. Удаление - `docker-machine rm <имя>`.
* docker-machine создает хост для докер демона со указываемым образом в --googlemachine-image, в ДЗ используется ubuntu-16.04. Образы которые используются для построения докер контейнеров к этому никак не относятся.
* Все докер команды, которые запускаются в той же консоли после `eval $(docker-machine env <имя>)` работают с удаленным докер демоном в GCP.

* Создан файл [env](env) с переменными окружения, необходимыми для работы с docker-machine
* Для проекта разрешено использование API как было сказано при первой попытке создать машину
* Создана машина
  ```shell
  docker-machine create --driver google \
  --google-machine-image https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/family/ubuntu-1604-lts \
  --google-machine-type n1-standard-1 \
  --google-zone europe-west1-b \
  docker-host
  ```
  ```log
  Running pre-create checks...
  (docker-host) Check that the project exists
  (docker-host) Check if the instance already exists
  Creating machine...
  (docker-host) Generating SSH Key
  (docker-host) Creating host...
  (docker-host) Opening firewall ports
  (docker-host) Creating instance
  (docker-host) Waiting for Instance
  (docker-host) Uploading SSH Key
  Waiting for machine to be running, this may take a few minutes...
  Detecting operating system of created instance...
  Waiting for SSH to be available...
  Detecting the provisioner...
  Provisioning with ubuntu(systemd)...
  Installing Docker...
  Copying certs to the local machine directory...
  Copying certs to the remote machine...
  Setting Docker configuration on the remote daemon...
  Checking connection to Docker...
  Docker is up and running!
  To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env docker-host
  ```
* docker-machine успешно создана `docker-machine ls`
  ```log
  NAME          ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER     ERRORS
  docker-host   -        google   Running   tcp://34.76.188.197:2376           v19.03.4
  ```
* Выполнено переключение на созданную машину `eval $(docker-machine env docker-host)`

#### Работа с namespaces

##### PID namespace

* По умолчанию контейнер запускается в отдельном PID namespace
  Команда `docker run --rm -ti tehbilly/htop` результатом своим показывает только запущенный процесс htop
  Команда `docker run --rm -ti ubuntu:16.04 ps auxf` возвращает похожий результат
  ```log
  USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root         1  0.0  0.0  25976  1456 pts/0    Rs+  18:29   0:00 ps auxf
  ```
* Запуск контейнера в PID namespace хоста
  Команда `docker run --rm --pid host -ti tehbilly/htop` возвращает все процессы хост-системы
  Команда `docker run --rm --pid host -ti ubuntu:16.04 ps auxf` возвращает похожий
  <details><summary>результат</summary>
  <p>

  ```log
  USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root         2  0.0  0.0      0     0 ?        S    15:27   0:00 [kthreadd]
  root         4  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [kworker/0:
  root         6  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [mm_percpu_
  root         7  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [ksoftirqd/
  root         8  0.0  0.0      0     0 ?        I    15:27   0:00  \_ [rcu_sched]
  root         9  0.0  0.0      0     0 ?        I    15:27   0:00  \_ [rcu_bh]
  root        10  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [migration/
  root        11  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [watchdog/0
  root        12  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [cpuhp/0]
  root        13  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [kdevtmpfs]
  root        14  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [netns]
  root        15  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [rcu_tasks_
  root        16  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [kauditd]
  root        17  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [khungtaskd
  root        18  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [oom_reaper
  root        19  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [writeback]
  root        20  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [kcompactd0
  root        21  0.0  0.0      0     0 ?        SN   15:27   0:00  \_ [ksmd]
  root        22  0.0  0.0      0     0 ?        SN   15:27   0:00  \_ [khugepaged
  root        23  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [crypto]
  root        24  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [kintegrity
  root        25  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [kblockd]
  root        26  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [ata_sff]
  root        27  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [md]
  root        28  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [edac-polle
  root        29  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [devfreq_wq
  root        30  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [watchdogd]
  root        34  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [kswapd0]
  root        35  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [kworker/u3
  root        36  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [ecryptfs-k
  root        78  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [kthrotld]
  root        79  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [acpi_therm
  root        80  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [scsi_eh_0]
  root        81  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [scsi_tmf_0
  root        87  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [ipv6_addrc
  root        97  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [kstrp]
  root        99  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [kworker/0:
  root       115  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [charger_ma
  root       268  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [raid5wq]
  root       321  0.0  0.0      0     0 ?        S    15:27   0:00  \_ [jbd2/sda1-
  root       322  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [ext4-rsv-c
  root       393  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [iscsi_eh]
  root       403  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [ib-comp-wq
  root       404  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [ib_mcast]
  root       405  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [ib_nl_sa_w
  root       408  0.0  0.0      0     0 ?        I<   15:27   0:00  \_ [rdma_cm]
  root      7628  0.0  0.0      0     0 ?        I    17:41   0:00  \_ [kworker/u2
  root      7678  0.0  0.0      0     0 ?        I    17:44   0:00  \_ [kworker/0:
  root      8019  0.0  0.0      0     0 ?        I    18:10   0:00  \_ [kworker/0:
  root      8094  0.0  0.0      0     0 ?        I    18:15   0:00  \_ [kworker/u2
  root      8189  0.0  0.0      0     0 ?        I    18:23   0:00  \_ [kworker/u2
  root      8254  0.0  0.0      0     0 ?        I    18:27   0:00  \_ [kworker/u2
  root      8385  0.0  0.0      0     0 ?        I    18:27   0:00  \_ [kworker/0:
  root      8601  0.0  0.0      0     0 ?        I    18:29   0:00  \_ [kworker/0:
  root         1  0.0  0.1  37732  5844 ?        Ss   15:27   0:02 /sbin/init
  root       402  0.0  0.1  31808  4304 ?        Ss   15:27   0:00 /lib/systemd/sy
  root       423  0.0  0.0  94772  1580 ?        Ss   15:27   0:00 /sbin/lvmetad -
  root       449  0.0  0.1  43068  4264 ?        Ss   15:27   0:00 /lib/systemd/sy
  root       910  0.0  0.0  16120  2864 ?        Ss   15:27   0:00 /sbin/dhclient 
  root      1133  0.0  0.0   5220   148 ?        Ss   15:27   0:00 /sbin/iscsid
  root      1135  0.0  0.0   5720  3504 ?        S<Ls 15:27   0:01 /sbin/iscsid
  root      1150  0.0  0.0  28620  3024 ?        Ss   15:27   0:00 /lib/systemd/sy
  root      1169  0.0  0.1 272944  5796 ?        Ssl  15:27   0:00 /usr/lib/accoun
  root      1179  0.0  0.0  26068  2492 ?        Ss   15:27   0:00 /usr/sbin/cron 
  root      1207  0.0  0.0   4396  1304 ?        Ss   15:27   0:00 /usr/sbin/acpid
  107       1249  0.0  0.0  42892  3744 ?        Ss   15:27   0:00 /usr/bin/dbus-d
  daemon    1265  0.0  0.0  26044  2184 ?        Ss   15:27   0:00 /usr/sbin/atd -
  root      1297  0.0  0.0  95368  1524 ?        Ssl  15:27   0:00 /usr/bin/lxcfs 
  root      1312  0.0  0.0  81068  2212 ?        Ssl  15:27   0:00 /usr/sbin/sshgu
  root      1351  0.0  0.5 171696 19376 ?        Ssl  15:27   0:00 /usr/bin/python
  root      1357  0.0  0.1 277180  6020 ?        Ssl  15:27   0:00 /usr/lib/policy
  root      1406  0.0  0.0  13372   156 ?        Ss   15:27   0:00 /sbin/mdadm --m
  112       1550  0.0  0.1  40268  4840 ?        Ss   15:27   0:00 /usr/sbin/ntpd 
  root      1553  0.0  0.5  65388 21424 ?        Ss   15:27   0:00 /usr/bin/python
  root      1580  0.0  0.5  65452 21540 ?        Ss   15:27   0:01 /usr/bin/python
  root      1581  0.0  0.5  65368 21264 ?        Ss   15:27   0:00 /usr/bin/python
  root      1595  0.0  0.1  65512  6160 ?        Ss   15:27   0:00 /usr/sbin/sshd 
  root      1602  0.0  0.0  14656  1804 ?        Ss+  15:27   0:00 /sbin/agetty --
  root      1635  0.0  0.0  12840  1780 ?        Ss+  15:27   0:00 /sbin/agetty --
  root      4552  0.1  1.2 440504 46512 ?        Ssl  15:28   0:11 /usr/bin/contai
  root      9754  0.0  0.1 108976  6044 ?        Sl   18:32   0:00  \_ containerd-
  root      9784 20.0  0.0  34560  2904 pts/0    Rs+  18:32   0:00      \_ ps auxf
  root      9817  0.0  0.0      0     0 ?        Z    18:32   0:00      \_ [runc] 
  root      5528  0.0  2.9 502264 109968 ?       Ssl  15:28   0:06 /usr/bin/docker
  _apt      8014  0.0  0.0 256392  3204 ?        Ssl  18:10   0:00 /usr/sbin/rsysl
  ```

  </p>
  </details>

##### NET namespace

Нашёл статью по теме: https://platform9.com/blog/container-namespaces-deep-dive-container-networking/

* Запустил контейнер nginx `docker run --rm --name wwweb -d nginx`
* Подключился по ssh к _docker-machine_ `gcloud compute ssh docker-host`
* `docker ps`
  ```log
  CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
  0e2ba62df689        nginx               "nginx -g 'daemon of…"   4 seconds ago       Up 3 seconds        80/tcp              wwweb
  ```
* По умолчанию, докер не добавляет сетевые неймспейсы контейнеров в `/var/run`. Чтобы это сделать, нужно выполнить последовательность команд:
  ```shell
  CONTAINER_PID="$(docker inspect -f '{{.State.Pid}}' wwweb)"
  echo $CONTAINER_PID
  sudo mkdir -p /var/run/netns
  sudo ln -sf /proc/$CONTAINER_PID/ns/net "/var/run/netns/wwweb"
  ```
* после этого можно посмотреть и получить доступ в network namespace контейнера
  * Список неймспейсов теперь пополнился
    ```shell
    # sudo ip netns list
    wwweb (id: 0)
    ```
* ip-адреса
  * просмотр ip-адресов интерфейсов в неймспейсе
    ```shell
    # sudo ip netns exec wwweb ip addr
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
    29: eth0@if30: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
        link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
        inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
           valid_lft forever preferred_lft forever
    ```
  * Список ip-адресов внутри контейнера wwweb (предварительно пришлось установить в контейнере пакет iproute2)
    ```shell
    # docker exec -ti wwweb ip addr
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
    29: eth0@if30: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
        link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
        inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
           valid_lft forever preferred_lft forever
    ```
    Как видно, совпадает со списком внутри net namespace
  * Список ip-адресов интерфейсов хоста
    ```shell
    # ip addr
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host 
           valid_lft forever preferred_lft forever
    2: ens4: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1460 qdisc pfifo_fast state UP group default qlen 1000
        link/ether 42:01:0a:84:00:02 brd ff:ff:ff:ff:ff:ff
        inet 10.132.0.2/32 brd 10.132.0.2 scope global ens4
           valid_lft forever preferred_lft forever
        inet6 fe80::4001:aff:fe84:2/64 scope link 
           valid_lft forever preferred_lft forever
    4: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
        link/ether 02:42:4c:d3:0b:bb brd ff:ff:ff:ff:ff:ff
        inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
           valid_lft forever preferred_lft forever
        inet6 fe80::42:4cff:fed3:bbb/64 scope link 
           valid_lft forever preferred_lft forever
    30: veth602f36b@if29: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default 
        link/ether 16:c8:f2:fc:08:ce brd ff:ff:ff:ff:ff:ff link-netnsid 0
        inet6 fe80::14c8:f2ff:fefc:8ce/64 scope link 
           valid_lft forever preferred_lft forever
    ```
    Различается со списком внутри неймспейса. При этом так же есть loopback-интерфейс с именем `lo`
* Таблицы маршрутизации
  * Внутри неймспейса
    ```shell
    # sudo ip netns exec wwweb ip route
    default via 172.17.0.1 dev eth0 
    172.17.0.0/16 dev eth0  proto kernel  scope link  src 172.17.0.2
    ```
  * Внутри контейнера
    ```shell
    # docker exec -ti wwweb ip route
    default via 172.17.0.1 dev eth0 
    172.17.0.0/16 dev eth0 proto kernel scope link src 172.17.0.2
    ```
  * Список маршрутов хоста
    ```shell
    # ip route
    default via 10.132.0.1 dev ens4 
    10.132.0.1 dev ens4  scope link 
    172.17.0.0/16 dev docker0  proto kernel  scope link  src 172.17.0.1
    ```
    Таблица маршрутизации отличается
* Открытые порты
  * Внутри неймспейса
    ```shell
    # sudo ip netns exec wwweb netstat -an
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN     
    Active UNIX domain sockets (servers and established)
    Proto RefCnt Flags       Type       State         I-Node   Path
    unix  3      [ ]         STREAM     CONNECTED     54759    
    unix  3      [ ]         STREAM     CONNECTED     54758
    ```
  * На хост-системе
    ```shell
    # netstat -an
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     
    tcp        0      0 10.132.0.2:47508        169.254.169.254:80      CLOSE_WAIT 
    tcp        0      0 10.132.0.2:47514        169.254.169.254:80      ESTABLISHED
    tcp        0      0 10.132.0.2:47512        169.254.169.254:80      ESTABLISHED
    tcp        0    316 10.132.0.2:22           176.62.181.4:36416      ESTABLISHED
    tcp        0      0 10.132.0.2:47510        169.254.169.254:80      ESTABLISHED
    tcp6       0      0 :::2376                 :::*                    LISTEN     
    tcp6       0      0 :::22                   :::*                    LISTEN     
    udp        0      0 0.0.0.0:68              0.0.0.0:*                          
    udp        0      0 172.17.0.1:123          0.0.0.0:*                          
    udp        0      0 10.132.0.2:123          0.0.0.0:*                          
    udp        0      0 127.0.0.1:123           0.0.0.0:*                          
    udp        0      0 0.0.0.0:123             0.0.0.0:*                          
    udp6       0      0 fe80::14c8:f2ff:fef:123 :::*                               
    udp6       0      0 fe80::42:4cff:fed3::123 :::*                               
    udp6       0      0 fe80::4001:aff:fe84:123 :::*                               
    udp6       0      0 ::1:123                 :::*                               
    udp6       0      0 :::123                  :::*                               
    ...
    ```
* Запущен контейнер с `--network host`, не использующий отдельного net namespace
  ```shell
  # docker run --rm --name wwwhost --network host -d nginx
  168c62352a51bcda9457f11480f935275202f51bab6232dd55e2edf8ee8f5245
  # docker ps
  CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
  168c62352a51        nginx               "nginx -g 'daemon of…"   3 seconds ago       Up 2 seconds                            wwwhost
  0e2ba62df689        nginx               "nginx -g 'daemon of…"   38 minutes ago      Up 38 minutes       80/tcp              wwweb
  ```
  * Список открытых портов на хост-системе
    ```shell
    # netstat -pan
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
    tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      13390/nginx: master
    tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1595/sshd       
    tcp        0      0 10.132.0.2:47556        169.254.169.254:80      CLOSE_WAIT  1581/python3    
    tcp        0      0 10.132.0.2:47562        169.254.169.254:80      ESTABLISHED 1581/python3    
    tcp        0      0 10.132.0.2:47560        169.254.169.254:80      ESTABLISHED 1553/python3    
    tcp        0      0 10.132.0.2:47558        169.254.169.254:80      ESTABLISHED 1580/python3    
    tcp        0    332 10.132.0.2:22           176.62.181.4:36416      ESTABLISHED 10854/sshd: vscoder
    tcp6       0      0 :::2376                 :::*                    LISTEN      5528/dockerd    
    tcp6       0      0 :::22                   :::*                    LISTEN      1595/sshd       
    udp        0      0 0.0.0.0:68              0.0.0.0:*                           910/dhclient    
    udp        0      0 172.17.0.1:123          0.0.0.0:*                           1550/ntpd       
    udp        0      0 10.132.0.2:123          0.0.0.0:*                           1550/ntpd       
    udp        0      0 127.0.0.1:123           0.0.0.0:*                           1550/ntpd       
    udp        0      0 0.0.0.0:123             0.0.0.0:*                           1550/ntpd       
    udp6       0      0 fe80::14c8:f2ff:fef:123 :::*                                1550/ntpd       
    udp6       0      0 fe80::42:4cff:fed3::123 :::*                                1550/ntpd       
    udp6       0      0 fe80::4001:aff:fe84:123 :::*                                1550/ntpd       
    udp6       0      0 ::1:123                 :::*                                1550/ntpd       
    udp6       0      0 :::123                  :::*                                1550/ntpd
    ...
    ```
    видно, что запущен процесс nginx на порту 80
  * Та же команда из контейнера
    ```shell
    # docker exec -ti wwwhost netstat -pan
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
    tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      1/nginx: master pro 
    tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
    tcp        0      0 10.132.0.2:47608        169.254.169.254:80      ESTABLISHED -                   
    tcp        0      0 10.132.0.2:35058        217.196.149.233:80      TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:39352        151.101.120.204:80      TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:39340        151.101.120.204:80      TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:52780        130.89.148.77:80        TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:47578        169.254.169.254:80      CLOSE_WAIT  -                   
    tcp        0      0 10.132.0.2:34988        149.20.4.15:80          TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:39358        151.101.120.204:80      TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:47594        169.254.169.254:80      ESTABLISHED -                   
    tcp        0      0 10.132.0.2:39338        151.101.120.204:80      TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:39344        151.101.120.204:80      TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:22           176.62.181.4:36416      ESTABLISHED -                   
    tcp        0      0 10.132.0.2:34996        149.20.4.15:80          TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:34974        149.20.4.15:80          TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:35072        217.196.149.233:80      TIME_WAIT   -                   
    tcp        0      0 10.132.0.2:47580        169.254.169.254:80      ESTABLISHED -                   
    tcp        0      0 10.132.0.2:39354        151.101.120.204:80      TIME_WAIT   -                   
    tcp6       0      0 :::2376                 :::*                    LISTEN      -                   
    tcp6       0      0 :::22                   :::*                    LISTEN      -                   
    udp        0      0 0.0.0.0:68              0.0.0.0:*                           -                   
    udp        0      0 172.17.0.1:123          0.0.0.0:*                           -                   
    udp        0      0 10.132.0.2:123          0.0.0.0:*                           -                   
    udp        0      0 127.0.0.1:123           0.0.0.0:*                           -                   
    udp        0      0 0.0.0.0:123             0.0.0.0:*                           -                   
    udp6       0      0 fe80::14c8:f2ff:fef:123 :::*                                -                   
    udp6       0      0 fe80::42:4cff:fed3::123 :::*                                -                   
    udp6       0      0 fe80::4001:aff:fe84:123 :::*                                -                   
    udp6       0      0 ::1:123                 :::*                                -                   
    udp6       0      0 :::123                  :::*                                -
    ...
    ```
    Видно все открытые порты хоста

* Попытка перехватить трафик
  * Создано 2 контейнера nginx
    ```shell
    docker run --rm --name wwweb1 -d nginx
    docker run --rm --name wwweb2 -d nginx
    ```
  * В контенере wwweb1 запущен периодический `curl` на wwweb2
    wwweb1:
    ```shell
    while sleep 1; do curl 172.17.0.2; done
    Ctrl+p Ctrl+q
    ```
  * На хост-системе выполнен захват пакетов на интерфейсе docker0
    <details><summary><b>tcpdump</b></summary>
    <p>

    ```shell
    # tcpdump -ni docker0 
    tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
    listening on docker0, link-type EN10MB (Ethernet), capture size 262144 bytes
    19:55:33.578680 IP 172.17.0.3.54102 > 172.17.0.2.80: Flags [S], seq 2237485892, win 29200, options [mss 1460,sackOK,TS val 4136154315 ecr 0,nop,wscale 7], length 0
    19:55:33.578763 IP 172.17.0.2.80 > 172.17.0.3.54102: Flags [S.], seq 3234450953, ack 2237485893, win 28960, options [mss 1460,sackOK,TS val 1810839543 ecr 4136154315,nop,wscale 7], length 0
    19:55:33.578783 IP 172.17.0.3.54102 > 172.17.0.2.80: Flags [.], ack 1, win 229, options [nop,nop,TS val 4136154315 ecr 1810839543], length 0
    19:55:33.579042 IP 172.17.0.3.54102 > 172.17.0.2.80: Flags [P.], seq 1:75, ack 1, win 229, options [nop,nop,TS val 4136154315 ecr 1810839543], length 74: HTTP: GET / HTTP/1.1
    19:55:33.579059 IP 172.17.0.2.80 > 172.17.0.3.54102: Flags [.], ack 75, win 227, options [nop,nop,TS val 1810839543 ecr 4136154315], length 0
    19:55:33.579146 IP 172.17.0.2.80 > 172.17.0.3.54102: Flags [P.], seq 1:239, ack 75, win 227, options [nop,nop,TS val 1810839543 ecr 4136154315], length 238: HTTP: HTTP/1.1 200 OK
    19:55:33.579410 IP 172.17.0.2.80 > 172.17.0.3.54102: Flags [P.], seq 239:851, ack 75, win 227, options [nop,nop,TS val 1810839543 ecr 4136154315], length 612: HTTP
    19:55:33.582222 IP 172.17.0.3.54102 > 172.17.0.2.80: Flags [F.], seq 75, ack 851, win 247, options [nop,nop,TS val 4136154318 ecr 1810839543], length 0
    19:55:33.582351 IP 172.17.0.2.80 > 172.17.0.3.54102: Flags [F.], seq 851, ack 76, win 227, options [nop,nop,TS val 1810839546 ecr 4136154318], length 0
    19:55:33.582364 IP 172.17.0.3.54102 > 172.17.0.2.80: Flags [.], ack 852, win 247, options [nop,nop,TS val 4136154318 ecr 1810839546], length 0
    19:55:34.593306 IP 172.17.0.3.54104 > 172.17.0.2.80: Flags [S], seq 3311237005, win 29200, options [mss 1460,sackOK,TS val 4136155329 ecr 0,nop,wscale 7], length 0
    19:55:34.593393 IP 172.17.0.2.80 > 172.17.0.3.54104: Flags [S.], seq 1172657176, ack 3311237006, win 28960, options [mss 1460,sackOK,TS val 1810840557 ecr 4136155329,nop,wscale 7], length 0
    19:55:34.593414 IP 172.17.0.3.54104 > 172.17.0.2.80: Flags [.], ack 1, win 229, options [nop,nop,TS val 4136155329 ecr 1810840557], length 0
    19:55:34.593738 IP 172.17.0.3.54104 > 172.17.0.2.80: Flags [P.], seq 1:75, ack 1, win 229, options [nop,nop,TS val 4136155330 ecr 1810840557], length 74: HTTP: GET / HTTP/1.1
    19:55:34.593754 IP 172.17.0.2.80 > 172.17.0.3.54104: Flags [.], ack 75, win 227, options [nop,nop,TS val 1810840558 ecr 4136155330], length 0
    19:55:34.593911 IP 172.17.0.2.80 > 172.17.0.3.54104: Flags [P.], seq 1:239, ack 75, win 227, options [nop,nop,TS val 1810840558 ecr 4136155330], length 238: HTTP: HTTP/1.1 200 OK
    19:55:34.594329 IP 172.17.0.2.80 > 172.17.0.3.54104: Flags [P.], seq 239:851, ack 75, win 227, options [nop,nop,TS val 1810840558 ecr 4136155330], length 612: HTTP
    19:55:34.594439 IP 172.17.0.3.54104 > 172.17.0.2.80: Flags [.], ack 239, win 237, options [nop,nop,TS val 4136155330 ecr 1810840558], length 0
    19:55:34.594493 IP 172.17.0.3.54104 > 172.17.0.2.80: Flags [.], ack 851, win 247, options [nop,nop,TS val 4136155330 ecr 1810840558], length 0
    19:55:34.597087 IP 172.17.0.3.54104 > 172.17.0.2.80: Flags [F.], seq 75, ack 851, win 247, options [nop,nop,TS val 4136155333 ecr 1810840558], length 0
    19:55:34.597247 IP 172.17.0.2.80 > 172.17.0.3.54104: Flags [F.], seq 851, ack 76, win 227, options [nop,nop,TS val 1810840561 ecr 4136155333], length 0
    19:55:34.597261 IP 172.17.0.3.54104 > 172.17.0.2.80: Flags [.], ack 852, win 247, options [nop,nop,TS val 4136155333 ecr 1810840561], length 0
    19:55:35.608138 IP 172.17.0.3.54106 > 172.17.0.2.80: Flags [S], seq 3998885043, win 29200, options [mss 1460,sackOK,TS val 4136156344 ecr 0,nop,wscale 7], length 0
    19:55:35.608228 IP 172.17.0.2.80 > 172.17.0.3.54106: Flags [S.], seq 1711094452, ack 3998885044, win 28960, options [mss 1460,sackOK,TS val 1810841572 ecr 4136156344,nop,wscale 7], length 0
    19:55:35.608247 IP 172.17.0.3.54106 > 172.17.0.2.80: Flags [.], ack 1, win 229, options [nop,nop,TS val 4136156344 ecr 1810841572], length 0
    19:55:35.608587 IP 172.17.0.3.54106 > 172.17.0.2.80: Flags [P.], seq 1:75, ack 1, win 229, options [nop,nop,TS val 4136156344 ecr 1810841572], length 74: HTTP: GET / HTTP/1.1
    19:55:35.608602 IP 172.17.0.2.80 > 172.17.0.3.54106: Flags [.], ack 75, win 227, options [nop,nop,TS val 1810841573 ecr 4136156344], length 0
    19:55:35.608776 IP 172.17.0.2.80 > 172.17.0.3.54106: Flags [P.], seq 1:239, ack 75, win 227, options [nop,nop,TS val 1810841573 ecr 4136156344], length 238: HTTP: HTTP/1.1 200 OK
    19:55:35.609098 IP 172.17.0.2.80 > 172.17.0.3.54106: Flags [P.], seq 239:851, ack 75, win 227, options [nop,nop,TS val 1810841573 ecr 4136156344], length 612: HTTP
    19:55:35.609252 IP 172.17.0.3.54106 > 172.17.0.2.80: Flags [.], ack 239, win 237, options [nop,nop,TS val 4136156345 ecr 1810841573], length 0
    19:55:35.609309 IP 172.17.0.3.54106 > 172.17.0.2.80: Flags [.], ack 851, win 247, options [nop,nop,TS val 4136156345 ecr 1810841573], length 0
    19:55:35.611656 IP 172.17.0.3.54106 > 172.17.0.2.80: Flags [F.], seq 75, ack 851, win 247, options [nop,nop,TS val 4136156348 ecr 1810841573], length 0
    19:55:35.611775 IP 172.17.0.2.80 > 172.17.0.3.54106: Flags [F.], seq 851, ack 76, win 227, options [nop,nop,TS val 1810841576 ecr 4136156348], length 0
    19:55:35.611788 IP 172.17.0.3.54106 > 172.17.0.2.80: Flags [.], ack 852, win 247, options [nop,nop,TS val 4136156348 ecr 1810841576], length 0
    ^C
    34 packets captured
    36 packets received by filter
    2 packets dropped by kernel
    ```

    </p>
    </details>
    В результате видим преиодические запросы на 172.17.0.2.80 от 172.17.0.3, и ответы.
    Вывод: для диагностики может пригодиться такая возможность


##### USER namespace

Документация по теме https://docs.docker.com/engine/security/userns-remap/
Известные ограничения https://docs.docker.com/engine/security/userns-remap/#user-namespace-known-limitations

Одно из ограничений:
This re-mapping is transparent to the container, but introduces some configuration complexity in situations where the container needs access to resources on the Docker host, such as bind mounts into areas of the filesystem that the system user cannot write to.

Важно про RHEL/CentOS
The way the namespace remapping is handled on the host is using two files, `/etc/subuid` and `/etc/subgid`. These files are typically managed automatically when you add or remove users or groups, but on a few distributions such as RHEL and CentOS 7.3, you may need to manage these files manually.

Пример `/etc/subuid`:
```
testuser:231072:65536
```
This means that user-namespaced processes started by testuser are owned by host UID 231072 (which looks like UID 0 inside the namespace) through 296607 (231072 + 65536 - 1). These ranges should not overlap, to ensure that namespaced processes cannot access each other’s namespaces.

Про достуа к ресурсам `/var/lib/docker`:
Enabling userns-remap effectively masks existing image and container layers, as well as other Docker objects within /var/lib/docker/. This is because Docker needs to adjust the ownership of these resources and actually stores them in a subdirectory within /var/lib/docker/. It is best to enable this feature on a new Docker installation rather than an existing one.

Along the same lines, if you disable userns-remap you can’t access any of the resources created while it was enabled.


* В `/etc/docker/daemon.json` добавлен `userns-remap`
  ```json
  {
    "userns-remap": "testuser"
  }
  ```
* docker перезапущен `systemctl restart docker`
* автоматически создан пользователь `dockremap`
  ```shell
  # id dockremap
  uid=113(dockremap) gid=117(dockremap) groups=117(dockremap)
  # grep dockremap /etc/subuid
  dockremap:362144:65536
  # grep dockremap /etc/subgid
  dockremap:362144:65536
  ```
* ранее загруженные образы недоступны
  ```shell
  # docker image ls
  REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
  ```
* запущен контейнер `hello-world`
  ```shell
  # docker run hello-world
  Unable to find image 'hello-world:latest' locally
  latest: Pulling from library/hello-world
  1b930d010525: Pull complete 
  Digest: sha256:c3b4ada4687bbaa170745b3e4dd8ac3f194ca95b2d0518b417fb47e5879d9b5f
  Status: Downloaded newer image for hello-world:latest
  ...
  ```
  образ заново загружен
* проверка наличия namspace-директории
  ```shell
  # sudo ls -ld /var/lib/docker/362144.362144/
  drwx------ 14 362144 362144 4096 Nov  3 20:21 /var/lib/docker/362144.362144/
  ```
  и её содержимого
  ```shell
  # sudo ls -l /var/lib/docker/362144.362144/
  total 48
  drwx------ 2 root   root   4096 Nov  3 20:21 builder
  drwx--x--x 4 root   root   4096 Nov  3 20:21 buildkit
  drwx------ 3 362144 362144 4096 Nov  3 20:25 containers
  drwx------ 3 root   root   4096 Nov  3 20:21 image
  drwxr-x--- 3 root   root   4096 Nov  3 20:21 network
  drwx------ 6 362144 362144 4096 Nov  3 20:25 overlay2
  drwx------ 4 root   root   4096 Nov  3 20:21 plugins
  drwx------ 2 root   root   4096 Nov  3 20:21 runtimes
  drwx------ 2 root   root   4096 Nov  3 20:21 swarm
  drwx------ 2 362144 362144 4096 Nov  3 20:25 tmp
  drwx------ 2 root   root   4096 Nov  3 20:21 trust
  drwx------ 2 362144 362144 4096 Nov  3 20:21 volumes
  ```
* Отключить user ns для контенйера: `--userns=host`
  There is a side effect when using this flag: user remapping will not be enabled for that container but, because the read-only (image) layers are shared between containers, ownership of the the containers filesystem will still be remapped.
  What this means is that the whole container filesystem will belong to the user specified in the `--userns-remap` daemon config (362144 in the example above). This can lead to unexpected behavior of programs inside the container. For instance sudo (which checks that its binaries belong to user 0) or binaries with a setuid flag.
