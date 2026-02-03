<img width="733" height="461" alt="543263857-5e78b1f4-3f42-45ab-bafa-e03305c19d77" src="https://github.com/user-attachments/assets/bddfe2e8-2424-4306-bc44-14f00198ce28" /> <br>

Производим установку серверного ПО <br>

<img width="747" height="769" alt="Screenshot From 2026-02-03 20-41-57" src="https://github.com/user-attachments/assets/4b011e9f-38fd-494d-a058-fa2ca79236e1" /> <br>


Заходим в кофигурационный файл nano /etc/freeradius/3.0/clients.conf и указваем в этом файле ip клиента и ключ который должен совпадать с ключём введенным при настроке AAA на клиенте <br>

<img width="747" height="769" alt="Screenshot From 2026-02-03 21-07-03" src="https://github.com/user-attachments/assets/b4a617fa-14e6-4107-af04-4deeda5ff3c2" /> <br>

Заходим в кофигурационный файл nano /etc/freeradius/3.0/users и указываем в этом файле рабочие пары логин-пароль <br>

<img width="837" height="768" alt="Screenshot_2" src="https://github.com/user-attachments/assets/309bbfe6-0d9c-4f85-b848-75f75017e83b" /> <br>

командой freeradius -X запускаем сервер в тестовом режиме <br>

<img width="836" height="338" alt="Screenshot_3" src="https://github.com/user-attachments/assets/9875d414-873a-4bfb-a2ce-1998602a6813" /> <br>

в другом окне  пробуем зайти под рабочей паро логин пароль. при успешной настройке будет вывод как на скриншоте выше. <br>
