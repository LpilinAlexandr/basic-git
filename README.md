# Основные команды git

## Полезные ссылки:
- [Статья про параметр core.autocrlf](https://habr.com/ru/articles/703072/)
- [Разница между switch и checkout](https://stackoverflow.com/questions/57265785/whats-the-difference-between-git-switch-and-git-checkout-branch)


---

## help

```shell
git <command> --help  # Откроет информацию по запрашиваемой команде
git commit --help  # Пример
```


## init

```shell
git init <name>  # Создать репозиторий. (Сделать текущую директорию новым репозиторием)
git init <name>  # Создать репозиторий в текущей директории с именем <name>
git init basic-git  # Пример
```


## clone
```shell
git clone <remote-url>
git clone https://github.com/LpilinAlexandr/basic-git.git  # Пример через http
git clone git@github.com:LpilinAlexandr/basic-git.git  # Пример через ssh
```


## remote
```shell
git remote set-url origin https://github.com/LpilinAlexandr/basic-git123.git  # Изменить в origin remote адрес
git remote add test https://github.com/LpilinAlexandr/basic-git123.git  # Установить новый remote адрес
git remote -v  # Посмотреть список всех remote адресов
```


## config
```shell
git config -l # Список текущих настроек
git config --global -l  # Список глобальных настроек
git config --local -l  # Список локальных настроек репозитория

git config --global user.name Name  # Установить имя пользователя в глобальной области
git config --global user.email email@example.com # Установить email пользователя в глобальной области

git config --unset <var> # Удалить переменную из настроек

git config alias.<your-alias> <command>  # Создание алиаса для команды
git config alias.st status  # Пример: теперь сможем писать git st вместо git status

git config --global core.autocrlf <input|false|true>  # Настройка параметра окончания строки.
```


## status
```shell
git status
git status -s  # Статус в короткой форме
```


# add | restore | rm
```shell
git add <path>  # Добавить в индекс всю директорию или файл по указанному пути
git add .  # Добавить всё в текущей директории
git restore --staged <path>  # Исключает из индекса добавленную директорию или файл по указанному пути
git restore <path>  # Отменить изменения в указанном месте 
git rm  # Фактически то же самое, что и удаление файла/директории
```


# stash
```shell
git stash -m 'my stash name'  # Спрячет все изменения в стеш 
git stash pop  # Достанет последние изменения из стеша, удалив его оттуда. По дефолту 0
git stash apply  # Достанет последние изменения из стеша, сохранив его. По дефолту 0
git stash list  # Посмотреть список всех стешей
git stash show <stash>  # Посмотреть стеш. По дефолту 0
git stash drop <stash>  # Удалить стеш. По дефолту 0
```


# commit
```shell
git commit -m 'Заголовок коммита'  # Сделать коммит
git commit -m 'Заголовок коммита' -m 'Текст под заголовком коммита'  # Сделать коммит с заголовком и доп. текстом

git commit <path> -m 'Заголовок'  # Закоммитить выбранный каталог

git commit --amend [-m] # Закоммитить изменения в предыдущий коммит
git commit --amend  --no-edit # Закоммитить изменения в предыдущий коммит без редактирования заголовка и описания
```


# log
```shell
git log  # Посмотреть логи по порядку
git log <branch-name>  # Посмотреть логи по конкретной ветке
git log --grep <pattern>  # Поиск коммитов с подходящей подстрокой
git log --invert-grep <pattern>  # Поиск коммитов, не входящих в подстроку
git log --oneline  # Список логов, каждый в одной строке
```


# revert
```shell
git revert <commit>  # Отменить коммит
git revert -n <commit>  # Отменить коммит и оставить изменения в индексе
```


# reset
```shell
git reset <commit>  # Сбросить коммиты в индекс до указанного коммита
--soft  # Изменения сбрасываются в индекс (Дефолтное значение)
--hard  # Изменения удаляются
git reset --soft HEAD~  # Сбросить последний коммит в индекс
git reset --hard HEAD~4  # Убить последние 4 коммита

# squash life-hack
git reset --soft HEAD~3  # Сбрасываем 3 последних коммита в 1
git commit -m 'Обьединили 3 коммита'  # Коммитим заново, тем самым объединяя 3 коммита в 1
```


# cherry-pick
```shell
git cherry-pick <commit>  # Перенести коммит в HEAD текущей ветки
git cherry-pick -n <commit>  # Перенести коммит в HEAD текущей ветки, но не делать коммит
```


# branch
```shell
git branch  # Посмотреть список локальных веток
git branch <branch-name> # Создать новую ветку от текущей ветки
git branch -a  # Посмотреть полный список веток вместе с remotes
git branch -m  # Переименовать ветку
git branch -d / -D  # Удалить ветку. Мягкое и жесткое удаление
```


# switch | checkout
```shell
git checkout <branch> | <commit>  # Переключиться на ветку или коммит по его хешу
git checkout -b <new_branch>  # Отбранчеваться от текущей ветки в новую ветку и сразу переключиться на нее со всеми изменениями

git switch <branch> | <commit> # Переключиться на ветку или коммит по его хешу
git switch -c <new_branch>  # Отбранчеваться от текущей ветки в новую ветку и сразу переключиться на нее со всеми изменениями
``` 


# merge
```shell
git merge <branch>  # Слить изменения из ветки <branch> в текущую ветку
git merge --continue  # Продолжить слияние в случае решения конфликтов
git merge --abort  # Отменить merge
```


# rebase
```shell
git rebase <commit>  # Встать коммитами текущей ветки на выбранный коммит 
git rebase <branch>  # Встать коммитами текущей ветки на выбранную ветку
git rebase --continue  # Продолжить слияние в случае решения конфликтов
git rebase --abort  # Отменить rebase
```


# fetch
```shell
git fetch # Запросить все изменения из origin 
git fetch <remote> # Запросить все изменения из remote
git fetch <remote> --prune # Запросить все изменения из remote и синхронизировать их
```


# pull
```shell
git pull origin <branch>  # Стянуть из remote актуальную ветку <branch> (По умолчанию режим merge)
git pull origin <branch> --rebase  # Стянуть из remote актуальную ветку в режиме rebase
```


# push
```shell
git push <remote> <branch>  # Отправить локальную ветку на remote 
git push -f <remote> <branch>  # Отправить принудительно локальную ветку на remote, перезаписав её 
git push -u <remote> <branch>  # Отправляем локальную ветку на remote и устанавливаем отслеживание
```


# reflog
```shell
git reflog  # Показать историю
git reflog <branch> # Показать историю по конкретной ветке
```
