1. Узнать IP-адрес интерфейса, подключенного к сети Интернет
```bash
[user@vm]$ ip addr show | grep global | awk '{print $2}'
93.XXX.74.XX/24

```
2. Создать именованный пайп ( named pipe ). Вывести в файл через созданный pipe вывод команды ss -plnt 
```bash
[user@vm]$ mkfifo npipe && ss -plnt > npipe &
[user@vm]$ [1] 215974
[user@vm]$ cat npipe > output.txt
[user@vm]$ cat output.txt
State  Recv-Q Send-Q Local Address:Port Peer Address:PortProcess
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*
```
3. При помощи именованного пайпа заархивировать всё, что в него отправляем. Например, содержимое файла /var/log/messages
На выходе получить архив tar или любой другой
``` bash
[user@vm]$ tar -cf npipe output.txt &
[1] 236126
[user@vm]$ cat npipe > archive.tar
[1]+  Done                    tar -cf npipe output.txt
```

4. Вывести дату в unixtime
На вход команды date через пайп подать свой формат выводимой даты



5. При помощи HEREDOC записать в файл многострочное сообщение
```bash
[user@vm]$ cat << EOF >> output.txt
> The first line followed by ...
> the second line which in turn followed by...
> the third line.The end
> EOF
```
