# Как создать свой собственный git-сервер на Linux

1) Необходимо сделать себе доступ на сервер через SSH по паблик ключу.

2) установить git-core

```
dnf install git-core
```

3) добавить пользователя git

```
adduser git
```

4) Создать каталог пользователя и Скопировать публичный ключ для пользователя git

```
mkdir /home/git/.ssh
cp ~/.ssh/authorized_keys /home/git/.ssh/
chown -R git:git /home/git/.ssh
chmod 700 !$
chmod 600 /home/git/.ssh/*
```

5) Залогинится под git и создать Репозитории

```
mkdir myrepo.git
cd !$
git --bare init
```

6) На локальной машине разработчика отвязываем репозиторий от платных удаленных нестабильных BitBucket?

предварительно выведем текущий удаленный репозиторий

```
git remote - v
```

теперь отвязываем
```
git remote remove origin
```

7) Привязываем наш новенький приватный репо и пушим в него

```
git remote add origin git@server.com:myrepo.git
git push origin master
```

## Ура. Все получилось. И пушится и пулится и входит и выходит. Я настроил себе приватный репо. Гудбай BitBucket
