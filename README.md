# Первый коммит

1. Сделать папку репозиторием - `git init`
2. Разгитить папку, если чтто-то пошло не так, - `rm -rf .git`
   Ключ -r (от англ. recursive — «рекурсивно») позволяет удалять папки вместе с их содержимым;
   ключ -f (от англ. force — «заставить») избавит вас от вопросов вроде «Вы точно хотите удалить этот файл? А этот? И этот тоже?».
3. Проверить состояние репозитория - `git status`
4. Подготовить файлы к сохранению - `git add `
5. Выполнить коммит - `git commit`
6. Просмотреть историю коммитов - `git log`

# SSH-ключи

1. Проверка наличия SSH-ключа - `ls -la .ssh`
2. Генерация SSH-ключа - `ssh-keygen -t ed25519 -C "Электронная почта, к которой привязан ваш аккаунт на GitHub"`
   Если произошла ошибка, то попробуйте ввести эту комманду - `ssh-keygen -t rsa -b 4096 -C`
3. Скопировать содержимое файлы с публичным ключом в буфер обмена:
   MacOs - `pbcopy < ~/.ssh/id_rsa.pub`
   для ed25519:
   `pbcopy < ~/.ssh/id_ed25519.pub`

   Windows - `clip < ~/.ssh/id_rsa.pub`
   для ed25519:
   `clip < ~/.ssh/id_ed25519.pub`

4. Привязать удаленный репозиторий к локальному - `git remote add`
   P.S. придется написать - `git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git `
5. Убедиться, что репозитории связаны - `git remote -v`
6. Отправить изменения на удаленный репозиторий - `git push`
   P.s. в первый раз нужно писать команду в такой форме - `git push -u origin master`

# Навигация по коммитам. Статусы файлов.

1. Хеш - идентификатор коммита (`git log`)
   1.1 Git преобразует информацию о коммитах с помощью алгоритма SHA-1 и для каждого из них рассчитывает уникальный идентификатор — хеш.
   1.2 Хеш — основной идентификатор коммита и позволяет узнать его автора, дату и содержимое закоммиченных файлов.
   1.3 Все хеши, а также таблицу соответствий хеш → информация о коммите Git хранит в папке .git.

2. Исследуем лог:
   строка из цифр и латинских букв после слова commit — это хеш коммита;
   Author — имя автора и его электронная почта;
   Date — дата и время создания коммита;
   в конце находится сообщение коммита.

3. HEAD - всему голова
   3.1 В числе прочих файлов в папке .git есть служебный файл HEAD. Он указывает на самый свежий коммит.
   3.2 Вместо хеша последнего коммита можно написать слово HEAD — Git вас поймёт.

4. Статусы файлов в Git
   Статусы untracked/tracked, staged и modified
   Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные.

   untracked (англ. «неотслеживаемый»)
   Мы говорили, что новые файлы в Git-репозитории помечаются как untracked, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У untracked-файла нет предыдущих версий, зафиксированных в коммитах или через команду git add.

   staged (англ. «подготовленный»)
   После выполнения команды git add файл попадает в staging area (от англ. stage — «сцена», «этап [процесса]» и area — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии staged.
   В одном из предыдущих уроков мы сравнили коммит с фотографией. Можно развить эту аналогию и сказать, что команда git add добавляет персонажей (текущее содержимое файла или нескольких файлов) на сцену (англ. stage) для общей фотографии, а git commit делает снимок всей сцены целиком.

   tracked (англ. «отслеживаемый»)
   Состояние tracked — это противоположность untracked. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью git commit, а также файлы, которые были добавлены в staging area командой git add. То есть все файлы, в которых Git так или иначе отслеживает изменения.
   modified (англ. «изменённый»)

   Состояние modified означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.

5. Как читать Git статус
   5.1 Команда git status всегда подскажет, что происходит с файлом: например, он добавлен в список «на коммит» или ещё вообще не отслеживается, или изменён.
   5.2 Git status показывает явно следующие состояния файлов: untracked, staged и modified.
   5.3 Git status подсказывает, какие команды можно выполнить, чтобы поменять состояние файла.

# Оформление сообщений к коммитам

Правильно описывать коммиты — искусство, к которому стоит приобщиться как можно раньше. Хорошо, когда:

1. Сообщение коммита легко читается;
2. Оно информативное;
3. Все сообщения оформлены в одном стиле.
