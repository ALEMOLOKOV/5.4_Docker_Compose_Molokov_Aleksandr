# 5.4_Docker_Compose_Molokov_Aleksandr

Задание 1
Создать собственный образ операционной системы с помощью Packer

Установка Packer
vagrant@vagrant:~$ sudo curl -sSL https://storage.yandexcloud.net/yandexcloud-yc/install.sh | bash

проверка
vagrant@vagrant:~$ ls yandex-cloud/bin
docker-credential-yc  yc

инициализация yc
vagrant@vagrant:~$ sudo yc init

Копирование yc  в .local/bin  и инициализация yc (sudo yc init)

vagrant@vagrant:~$ cp yandex-cloud/bin/yc .local/bin | echo $?
0
vagrant@vagrant:~$ sudo yc init
Welcome! This command will take you through the configuration process.
Please go to https://oauth.yandex.ru/authorize?response_type=token&client_id=1a6990aa636648e9b2ef855fa7bec2fb in order to obtain OAuth token.

Перешел по ссылке ввел токен
Please enter OAuth token: y0_AgAAAAAK41XNAATuwQAAAADT-3mPtwf9gXa1THinE4l-9BVWM7oEQyo
You have one cloud available: 'cloud-sanmol88' (id = b1ga8hp5qimcnoglaoe9). It is going to be used by default.
Please choose folder to use:
 [1] default (id = b1gd90e13r1hhqi7jflu)
 [2] Create a new folder
Please enter your numeric choice:

Проверка наличия образов
vagrant@vagrant:~$ sudo yc compute image list
+----+------+--------+-------------+--------+
| ID | NAME | FAMILY | PRODUCT IDS | STATUS |
+----+------+--------+-------------+--------+
+----+------+--------+-------------+--------+

Инициализация сети
vagrant@vagrant:~$ sudo yc vpc network create --name mynet  --labels my-label=netology --description "first network via yc"

id: enp00q2mrge91art2ked
folder_id: b1gd90e13r1hhqi7jflu
created_at: "2022-11-14T19:47:21Z"
name: mynet
description: first network via yc
labels:
  my-label: netology

Инициализация подсети
vagrant@vagrant:~$ sudo yc vpc subnet create --name mysubnet-a --zone ru-central1-a --range 10.1.2.0/24 --network-name mynet --description "first subnet via yc"

id: e9briqt831sbbn1o9q06
folder_id: b1gd90e13r1hhqi7jflu
created_at: "2022-11-14T19:51:47Z"
name: mysubnet-a
description: first subnet via yc
network_id: enp00q2mrge91art2ked
zone_id: ru-central1-a
v4_cidr_blocks:
  - 10.1.2.0/24

Установка Packer и проверка версии
vagrant@vagrant:~$ sudo apt install packer
vagrant@vagrant:~$ sudo packer --version
1.3.4

Ошибка при проверке валидации
vagrant@vagrant:/packer$ sudo packer validate packer_file.json
Failed to initialize build 'yandex': builder type not found: yandex
vagrant@vagrant:/packer$





