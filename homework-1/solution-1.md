1. Узнать IP-адрес интерфейса, подключенного к сети Интернет
```bash
[user@vm]$ ip addr show | grep global | awk '{print $2}'
93.XXX.74.XX/24

```
2. Создать именованный пайп ( named pipe ). Вывести в файл через созданный pipe вывод команды ss -plnt
terminal 1:
```bash
[user@vm]$ mkfifo npipe
[user@vm]$ ss -plnt > npipe
```
terminal 2:
```bash
[user@vm]$ cat npipe > output.txt
[user@vm]$ cat output.txt
State  Recv-Q Send-Q Local Address:Port Peer Address:PortProcess
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*
 
```

3. При помощи именованного пайпа заархивировать всё, что в него отправляем. Например, содержимое файла /var/log/messages
На выходе получить архив tar или любой другой


4. Вывести дату в unixtime
На вход команды date через пайп подать свой формат выводимой даты



5. При помощи HEREDOC записать в файл многострочное сообщение
