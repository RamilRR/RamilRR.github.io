---
title: "Установка Python на Debian"
date: 2020-01-13
tags:
 - python
 - debian 
---
Создаем пользователя `www`, назначаем пароль.
Обновляем репозиторий и устанавливаем необходимые дистрибутивы.
```sh
sudo apt-get update 
sudo apt-get install -y vim zsh mosh tmux htop git curl wget unzip zip gcc build-essential make
```
Устанавливаем дистрибутивы необходимые [python] `3.8.1`.
```sh
sudo apt-get install -y libreadline-gplv2-dev libncursesw5-dev libssl-dev \
libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev
```
Устанавливаем [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) вместо bash.
```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
``` 
Устанавливаем [python]. Скачиваем, разархивируем python, переходим в папку python и создаем в домашней директории скрытую папку `.python`.
```sh
sudo wget https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tgz ; \
tar xvf Python-3.8.* ; \
cd Python-3.8.1 ; \
mkdir ~/.python
```
Собираем python из исходников.
```sh
sudo ./configure --enable-optimizations --prefix=/home/www/.python ; \
make -j12 altinstall
```
Настраиваем пути к python.
```sh
vim ~/.zshrc
	alias cls="clear"
	export PATH=$PATH:/home/www/.python/bin
. ~/.zshrc
```
Обновляем pip.
```sh
sudo /home/www/.python/bin/python3.8 -m pip install -U pip
```
Удаляем файлы исходников и папку python.
```sh
sudo rm -rf Python-3.8.1.tgz Python-3.8.1
```
Создаем виртуальное окружение и активируем его.
```sh
python3.8 -m venv env
source env/bin/activate
```
[python]: <https://www.python.org>
