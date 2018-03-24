# video-board

Это бортовая часть
Серверная https://github.com/roboflot-ru/video-server


## Установка

    git clone https://github.com/roboflot-ru/video-board.git video
    cd video
    chmod +x install.sh
    ./install.sh
    cd Drone
    make



## Настройки

    nano VideoService.ini



## Автозапуск

Создаем файл

    sudo nano /etc/systemd/system/video.service

С таким содержимым

    [Unit]
    Description=VideoService

    [Service]
    Type=simple
    User=pi
    WorkingDirectory=/home/pi/video/Drone
    ExecStart=/home/pi/video/Drone/VideoService
    Restart=on-abort

    [Install]
    WantedBy=default.target

Ctrl+X сохраняем
Обновляем сервисы запуска

    sudo systemctl daemon-reload

Включаем автозапуск при загрузке

    sudo systemctl enable video

Запустить вручную

    sudo systemctl start video

Состояние

    sudo systemctl status video

Остановить

    sudo systemctl stop video



## Трансляция

Запускаем трасляцию на бортовой части после серверной

    curl -v 'http://localhost:9009/start_live?width=640&height=480&framerate=25&bitrate=1000000&server=SERVER_HOST&port=PORT_IN'

Адрес для плеера

    rtsp://SERVER_HOST:PORT_OUT/UID

Остановить трансляцию

    curl -v 'http://localhost:9009/stop_live'

Состояние трансляции

    curl -v 'http://localhost:9009/status'



Автор: Дмитрий Кирсанов
для БПЛА Roboflot
https://www.roboflot.ru


