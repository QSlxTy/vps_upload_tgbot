<H2>Установка зависимостей</H2>  

Обновляемся  
```sudo apt update```  
```sudo apt -y upgrade```  
  
Качаем пип  
```sudo apt install -y python3-pip```  
  
Доп пакеты   
```sudo apt install -y build-essential libssl-dev libffi-dev python3-dev```  
  
Качаем сам venv  
```sudo apt install -y python3-venv```  
  
Создаём папку с проектом и переключаемся на неё  
```mkdir tg_bot | cd tg_bot```

Создаём виратульное окружение в папке с проектом  
```python3 -m venv venv```
 
Можно его активировать для установки библиотек и т.д.  
```source env/bin/activate```

Качаем нужные библиотеки из файла  
```pip install -r requirements.txt```

Или вручную  
```pip install aiogram aiomysql ... ```

Можно проверить как запускается приложение через главный main.py файл  
```python3 main.py```

Чтобы выйти из виратульного окружения  
```exit```  
<H2>Создание службы</H2>

Теперь создаём службу  
```sudo nano /etc/systemd/system/НАЗВАНИЕ СЛУЖБЫ.service```  
Вставляем этот текст туда и исправляем названия  
(Служба сама перезапускается в случае ошибки в ней и псоле перезапуска сервера)  

```
[Unit]  
Description=Название службы  
[Service]  
User=root  
Group=root  
Type=simple  
Restart=always  
WorkingDirectory=/root/Папка с ботом  
ExecStart=/root/ПАПКА С БОТОМ/venv/bin/python /root/ПАПКА С БОТОМ/main.py  
RestartSec=10  
Restart=always  
[Install]  
WantedBy=multi-user.target
```
Чтобы сохранить  
CTL+X -> Y -> Enter  

Создадим связь, чтобы служба перезапускалась сама  
```systemctl enable НАЗВАНИЕ СЛУЖБЫ.service```  

Запустим службу   
```systemctl start НАЗВАНИЕ СЛУЖБЫ.service```  

Проверим её статус. Если есть зелёный кружок или написано (active), то всё отлично работает  
```systemctl status НАЗВАНИЕ СЛУЖБЫ.service```

Если мы внесли в файл службы изменения, то нужно её обновить  
```systemctl daemon-reload```
