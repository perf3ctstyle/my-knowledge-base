1. Вывести информацию об используемом дистрибутиве

Способ первый - читаем через cat из файла os-release: 
`cat /etc/*rel*`

Способ второй: 
`lsb_release -a`

2. Вывести информацию об используемом ядре

Способ - читаем через cat из файла version:
`cat /proc/version`

3. Вывести информацию о потребляемых ресурсах в системе

Способ первый - используем встроенную утилиту top
top показывает:
* Кол-во процессов и сами процессы
* Load Average
* Нагрузка на RAM и swap
* Нагрузка на CPU (по умолчанию объединено, словно у нас 1 ядро процессора)

12. Создать скрипт, который выводит "Hello World" и ограничить доступ, не применяя chown, чтобы никто из пользователей системы (кроме root пользователя), не смог выполнить этот скрипт при условии, что он уже исполняемый.
    Вернуть доступ к файлу после выполнения задания.

Выполнить под root пользователем:
```
echo "echo 'Hello World'" > script.sh
chmod g+x,o-x script.sh
chmod g+x,o+x script.sh
```

13. Включить отладку в скрипте

Отладку можно включить с помощью опции -x разными способами

Способ первый - при вызове bash
```bash -x script.sh```

Способ второй - в первой строке bash скрипта
```#!/bin/bash -x```

Способ третий - через оператор set внутри скрипта
```
set -x # Turn on debugging
echo 'Debugging mode is currently on'
set +x # Turn off debugging
echo 'Debugging mode is currently off'
```

При этом dash (-) включает режим, а plus (+) отключает его.

14. Дополнить скрипт проверкой на наличие в системе пакета vim. В случае его отсутствия установить его без вывода подробностей установки. По завершению вывести строку "Completed"

```
#!/bin/bash
if dpkg -s vim &> /dev/null; then
   echo "Vim is installed"
else
   echo "Vim is not installed. Starting the installation..."

   if apt-get install vim -y > /dev/null 2> error_installing_vim.txt; then
      echo "Vim has been successfully installed"
   fi

   if [ -s error_installing_vim.txt ]; then
      echo "An error occurred while installing vim. See it in error_installing_vim.txt"
   else
      rm error_installing_vim.txt
   fi
fi
```

15. Обрезать строку "Hello World" так, чтобы остались только символы "llo Wo" без использования команды cut

```
#!/bin/bash
string="Hello World"
substring=${string:2:6}
echo ${substring}
```

16. Дополнить скрипт, чтобы он давал возможность вводить данные и передавать их скрипту