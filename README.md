# Зачем все это нужно
Мне не нравится дискорд, так его еще и заблокировали. Эта инструкция поможет сделать свой сервер тим спика и болтать с друзьями в чудесном качестве. 
В дополнение скажу, что тим спик позволяет использовать аудио 100 Кб/с, а дискорд бесплатным пользователям дает только 64 Кб/с.

**Сколько стоит?**
Вам понадобится арендовать сервер (VPS), это стоит от 100р/месяц. Наберите в поиске "недорогие VPS" и вы все найдете. Лучше почитайте отзывы и выбирайте большие компании, а не слишком мелкие. 
После оплаты вы получите следующие данные:
- IP-адрес сервера для подключения по SSH
- логин и пароль от root или пользователя с правами sudo. Инструкция рассчитана на этот вариант

# Установка сервера
Установщик всё сделает сам в 1 команду. Код скрипта находится тут же, [можете ознакомиться](https://github.com/Avonae/TS-Docker-Install/blob/main/install_script.sh).

Процесс установки довольно прост:
1. Подключаетесь к серверу по SSH. Для этого открываете терминал и пишете: `ssh IP_адрес_вашего_сервера`
2. Нажимаете `Y` для принятия сертификата
3. Запускаете код скрипта:
```
sudo bash -c "$(curl -L https://raw.githubusercontent.com/Avonae/TS-Docker-Install/refs/heads/main/install_script.sh)"
```

Тим спик будет работать как [контейнер в докере](https://ru.wikipedia.org/wiki/Docker), что позволит не замусоривать систему и удобно им управлять.
Установка займет минут 5. По завершению вы получите админ-токен, который пригодится для управления сервером:

![image](https://github.com/user-attachments/assets/3d3a1445-9566-46cd-b1ca-d3bd65245a1e)

На скриншоте `c30d0d7da81f77f8b0ae38ef82af1ae82d33f32ef3e8e5606c49440f5cea1fc7` — это админский токен. Его необходимо держать в секрете, я показываю для примера.

Далее установите клиент тимспика и подключитесь к своему серверу. У вашего сервера есть IP-адрес, его и вводите в поле для подключения:

![image](https://github.com/user-attachments/assets/bb30250a-70db-4a2f-97e6-52dcb71b55a2)

Пароль не вводите, нажимайте подключиться
После подключения сервер спросит у вас токен администратора. Скопируйте его из консоли и вставьте сюда:

![image](https://github.com/user-attachments/assets/88852e0c-26b0-45c8-943b-a65d8cb2f86e)

Ваш сервер готов, а вы его администратор. Можете звать друзей, только установите пароль для начала.

## Установка пароля
1. Нажмите правой кнопкой мыши на сервер → Редактировать виртуальный сервер
2. Укажите пароль в поле Пароль
3. Нажмите ОК.
4. Пароль установлен.

## Настройка сервера
Качества звука настраивается непосредственно в каналах. Поэтому для настройки, нажмите правой кнопкой на канал и выберите **Редактировать канал**

![image](https://github.com/user-attachments/assets/7edc429a-cdb3-45f6-ade2-2fcaae363a86)

На вкладке **Звук** можно выкрутить качество на **10**. Значение по умолчанию — 6. Я лично делаю это в первую очередь, т.к. качество просто потрясающее. Не зря же вы делали свой сервер! 
# Полезные команды
## Показать список запущенных контейнеров
```
sudo docker ps
```
Первый столбец — ID контейнера. Скопируйте его, если хотите работать конкретно с ним. ID обычно выглядит как набор символов, вроде `90b8831a4a2`

## Перезапустить контейнер тим спика
```
sudo docker restart ID_контейнера 
```
Здесь необходимо использовать ID контейнера, который вы получили с помощью `docker ps`.
## Перезапустить все контейнеры
```
sudo docker restart $(docker ps -a -q)
```
# Дополнительная информация
Если хотите управлять контейнерами, не заходя на сервер, а через удобный веб интерфейс, рассмотрите установку Portainer. Хорошая инструкция на русском [есть по ссылке]([url](https://timeweb.cloud/tutorials/docker/ustanovka-i-ispolzovanie-portainer)).

