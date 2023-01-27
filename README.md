## ТиМП для невдуплёнышей [1]

## Laboratory work I

Данная лабораторная работа посвещена изучению утилит для разработки проектов

## Tasks

- [ ] 1. Ознакомиться со ссылками учебного материала
- [ ] 2. Выполнить инструкцию учебного материала
- [ ] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Теория

**Переменные среды** — у консольной сессии есть куча переменных, получить значения которых можно так: `${<имя переменной>}`. Свои переменные можно создавать командой `export`.

**PATH** — переменная среды, в которой лежат пути к исполняемым файлам. При вводе команды система пробегается по директориям, лежащим в `PATH`, и ищет исполняемый файл, соответствующий команде. Таким образом, чтобы установить утилиту, необходимо, чтобы `PATH` содержал путь к ней.

\~WIP~


## Tutorial
> **export** — позволяет менять переменные среды.
> **alias** — присваивает команде новое имя. Чисто для удобства пользователя.
> Обе команды влияют только на данную сессию консоли, перезапуск консоли потрёт все изменения.
 
```sh
# присвоить переменной GITHUB_USERNAME значение <имя_пользователя>
$ export GITHUB_USERNAME=<имя_пользователя>
# присвоить переменной GIST_TOKEN значение <сохраненный_токен>
$ export GIST_TOKEN=<сохраненный_токен>
# ассоциируем имя edit с одним из исп. файлов nano, vi, vim, subl
$ alias edit=<nano|vi|vim|subl>
```

> **mkdir** (make directory) — создание новой директории. Флаг `-p` позволяет создавать вложенные директории.
> **cd** (change directory) — переход в другую директорию. `.` — текущая директория, `..` — родительская директория.
> **pwd** (print working directory) — вывод текущей директории

```sh
# создаём директорию <имя_пользователя>, в ней директорию workspace
$ mkdir -p ${GITHUB_USERNAME}/workspace
# переходим в неё
$ cd ${GITHUB_USERNAME}/workspace
# выводим текущую директорию
$ pwd
# поднимаемся на уровень выше (в дтиректорию с именем пользователя)
$ cd ..
# снова выводим текущую директорию
$ pwd
```

```sh
# создаём три директории в workspace
$ mkdir -p workspace/tasks/
$ mkdir -p workspace/projects/
$ mkdir -p workspace/reports/
# переходим в workspace
$ cd workspace
```

> **wget** — получаем файл, который лежит по ссылке.
> **tar** — утилита для работы с архивами. Флаг `-xf` — распаковать архив.
> **rm** (remove) — удалить файл. `-r` позволяет удалять вложенные директории, `-f` подавляет сообщение "вы уверены, что хотите удалить это?"
> **mv** (move) — переместить и/или переименовать файл или директорию.

```sh
# скачиваем архив
$ wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
# распаковываем его в текущую директорию
$ tar -xf node-v6.11.5-linux-x64.tar.xz
# удаляем архив
$ rm -rf node-v6.11.5-linux-x64.tar.xz
# переименовываем (перемещаем) созданную при распаковке архива директорию
$ mv node-v6.11.5-linux-x64 node
```

> **ls** — вывести информацию о файлах в директории.
> **echo** — написать что-то в консоль или в файл. Про переменную `PATH` написано в теории.
> **cat** — то же самое, но с несколькими строками.
> **source** — запускает файл с командами консоли

```sh
# выводим список всего, что лежит в node/bin
$ ls node/bin
# выводим PATH, где хранятся пути до исп. файлов
$ echo ${PATH}
# добавляем к PATH путь до исп. файлов nodejs
$ export PATH=${PATH}:`pwd`/node/bin
# выводим PATH
$ echo ${PATH}
# создаём директорию scripts
$ mkdir scripts
# создаём исп. файл и записываеи в него команду для добавления пути к PATH
$ cat > scripts/activate<<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF
# запускаем исп. файл как набор команд
$ source scripts/activate
```

> **gem** — менеджер пакетов, как и `apt`

```sh
# устанавливаем утилиту gist
$ gem install gist
```

> **umask** — указывает изначальные права доступа создаваемых файлов (см. Теория — Права доступа)

```sh
# создаём скрытый файл gist в домашней директории с урезанными правами доступа
$ (umask 0077 && echo ${GIST_TOKEN} > ~/.gist)
```

## Report

```sh
# создаём и инициализируем переменную с номером лабы
$ export LAB_NUMBER=01
# копируем репозиторий в task/lab01
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
# создаём директорию для отчётов, в ней - директорию для первой лабы
$ mkdir reports/lab${LAB_NUMBER}
# копируем readme лабы в report отчёта
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
# переходим в директорию с отчётом
$ cd reports/lab${LAB_NUMBER}
# редактируем файл REPORT.md (собственно, делаем отчёт)
$ edit REPORT.md
# создаём gist с файлом REPORT.md
$ gist REPORT.md
```

## Links

### Unix commands

- [ar](https://en.wikipedia.org/wiki/Ar_(Unix)) - **ar**chiver - утилита для работы с архивами
- [cat](https://en.wikipedia.org/wiki/Cat_(Unix)) - con**cat**enate - вывод файлов последовательно
- [cd](https://en.wikipedia.org/wiki/Cd_(command)) - **c**hange **d**irectory - смена рабочей директории
- [cp](https://en.wikipedia.org/wiki/Cp_(Unix)) - **c**o**p**y - копирование файлов/директорий
- [cut](https://en.wikipedia.org/wiki/Cut_(Unix)) - выводит указанные куски строк из файлов
- [echo](https://en.wikipedia.org/wiki/Echo_(command)) - простой вывод
- [env](https://en.wikipedia.org/wiki/Env_(shell)) - **env**ironment - выводит список переменных среды, позволяет исполнять файлы в той же среде с другими значениями переменных
- [ex](https://en.wikipedia.org/wiki/Ex_(editor)) - **ex**tended - строковый редактор
- [file](https://en.wikipedia.org/wiki/File_(command)) - опознаёт тип данных файла
- [find](https://en.wikipedia.org/wiki/Find) - находит файлы по заданным критериям, выводит пути к ним
- [ls](https://en.wikipedia.org/wiki/Ls) - **l**i**s**t - выводит файлы и директории в рабочей директории
- [man](https://en.wikipedia.org/wiki/Man_page) - **man**ual - выводит мануал
- [mkdir](https://en.wikipedia.org/wiki/Mkdir) - **m**a**k**e **dir**ectory - создаёт директорию
- [mv](https://en.wikipedia.org/wiki/Mv) - **m**o**v**e перемещение файлов или директорий
- [nm](https://en.wikipedia.org/wiki/Nm_(Unix)) - **n**ame **m**angling - выводит таблицу имён бинарного файла
- [ps](https://en.wikipedia.org/wiki/Ps_(Unix)) - **p**rocess **s**tatus - вывод рабочих процессов
- [pwd](https://en.wikipedia.org/wiki/Pwd) - **p**rint **w**orking **d**irectory - вывод рабочей директории
- [rm](https://en.wikipedia.org/wiki/Rm_(Unix)) - **r**e**m**ove - удаляет файлы или директории
- [sed](https://en.wikipedia.org/wiki/Sed) - **s**tream **ed**itor - потоковый редактор
- [touch](https://en.wikipedia.org/wiki/Touch_(Unix)) - обновляет время доступа к файлу или создаёт пустой файл

### Package Managers

- [apt](http://help.ubuntu.ru/wiki/apt) | [dnf](https://en.wikipedia.org/wiki/DNF_(software)) | [yum](https://fedoraproject.org/wiki/Yum/ru)
- [brew](https://brew.sh) | [linuxbrew](http://linuxbrew.sh)
- [npm](https://docs.npmjs.com)

### Software

- [curl](https://www.gitbook.com/book/bagder/everything-curl/details)
- [wget](https://www.gnu.org/software/wget/manual/wget.pdf)
- [clang](https://clang.llvm.org)
- [g++](https://gcc.gnu.org/onlinedocs/gcc-4.0.2/gcc/G_002b_002b-and-GCC.html)
- [make](https://en.wikipedia.org/wiki/Make_(software))
- [open](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/open.1.html)
- [openssl](https://www.openssl.org)
- [nano](https://www.nano-editor.org)
- [tree](https://linux.die.net/man/1/tree)
- [vim](http://www.vim.org)

## Homework

> **Homework** — основная часть лабы.

1. Скачайте библиотеку *boost* с помощью утилиты **wget**. Адрес для скачивания `https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz`.
```sh
$ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
```
2. Разархивируйте скаченный файл в директорию `~/boost_1_69_0`
```sh
$ tar -xf boost_1_69_0.tar.gz -C ~
$ cd ~/boost_1_69_0
```
3. Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.
```sh
$ find ! -maxdepth 1 -type d  | wc
#16
```
4. Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.
```sh
$ find ! -type d | wc
#61191
```
5. Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).
```sh
$ find ! -type d -name "*.h" | wc
#296
$ find ! -type d -name "*.cpp" | wc
#13774
$ find ! -type d ! -name "*.cpp" ! -name "*.h" | wc
#47121
```
6. Найдите полный пусть до файла `any.hpp` внутри библиотеки *boost*.
```sh
$ find -name "any.hpp"
./boost/fusion/include/any.hpp
./boost/fusion/algorithm/query/detail/any.hpp
./boost/fusion/algorithm/query/any.hpp
./boost/proto/detail/any.hpp
./boost/hana/fwd/any.hpp
./boost/hana/any.hpp
./boost/xpressive/detail/utility/any.hpp
./boost/any.hpp
./boost/type_erasure/any.hpp
./boost/spirit/home/support/algorithm/any.hpp
```
7. Выведите в консоль все файлы, где упоминается последовательность `boost::asio`.
```sh
$ grep -lr "boost::asio"
```
8. Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).
```sh
$ ./bootstrap.sh
$ ./b2 install
```
9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.
```sh
$ mkdir ~/boost-libs
$ cp stage/lib/*.a ~/boost-libs
```
10. Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.
```sh
$ cd ~/boost-libs
$ find ! -type d -exec du -h {} +
```
11. Найдите *топ10* самых "тяжёлых".
```sh
$ find ! -type d -exec du {} + | sort -rn | head -n 10
4728	./libboost_wave.a
4512	./libboost_log.a
3148	./libboost_math_tr1.a
3116	./libboost_math_tr1l.a
3080	./libboost_math_tr1f.a
2832	./libboost_regex.a
2752	./libboost_log_setup.a
2412	./libboost_test_exec_monitor.a
2392	./libboost_unit_test_framework.a
2096	./libboost_locale.a
```

```
Copyright (c) 2015-2021 The ISC Authors
```
