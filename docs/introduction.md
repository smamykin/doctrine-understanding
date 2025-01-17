Введение
--

Содержание

*   [1.1. Начало](introduction.md#11-начало)
*   [1.2. Достоверность информации](introduction.md#12)
*   [1.3. Применение ORM](introduction.md#13_ORM)
*   [1.4. Требования](introduction.md#14)
*   [1.5. Составляющие Doctrine 2](introduction.md#15_Doctrine_2)
    *   [1.5.1. Библиотека Common](introduction.md#151_Common)
    *   [1.5.2. Библиотека DBAL](introduction.md#152_DBAL)
    *   [1.5.3. Библиотека ORM](introduction.md#153_ORM)
*   [1.6. Установка](introduction.md#16)
    *   [1.6.1. PEAR](introduction.md#161_PEAR)
    *   [1.6.2. Загрузка с сайта](introduction.md#162)
    *   [1.6.3. GitHub](introduction.md#163_GitHub)
    *   [1.6.4. Subversion](introduction.md#164_Subversion)
*   [1.7. Песочница](docs/introduction.md#17)
    *   [1.7.1. Обзор](introduction.md#171)
    *   [1.7.2. Небольшая обучалка](introduction.md#172)


# 1.1. Начало

_Doctrine 2_ представляет собой хороший пример механизма объектно-реляционного отображения (ORM) для _PHP 5.3+_, позволяющий работать с базой данных максимально прозрачно, где в качестве промежуточного слоя используются обычные объекты _PHP_. В качестве основы используется весьма мощный слой абстракции от базы данных (_DBAL_). Основная задача_ORM_ — связать две концепции: объекты _PHP_ и записи в реляционной базе данных.

Одна из ключевых особенностей Doctrine — возможность написания запросов на собственном объектно-ориентированном языке, чем-то напоминающим SQL, называемым _Doctrine Query Language (DQL)_, созданным под вдохновением от _Hibernates HQL_. Помимо небольших отличий от _SQL_, он позволяет значительно усилить степень абстракции между объектами и строками базы данных, что позволяет создавать мощные и гибкие запросы, при этом сохраняя целостность.

# 1.2. Достоверность информации

Данный документ представляет собой справочную документацию по _Doctrine 2_. Руководства для начинающих и обучалки, как это было для _Doctrine 1.x_ будут доступны позднее.

# 1.3. Применение ORM

Как уже было сказано, задача _Doctrine 2_ — упростить взаимодействие между строками в СУБД и объектной моделью _PHP_. Так что основной эффект от ее применения может быть достигнут лишь в объектно-ориентированной среде и приложениях, использующих парадигму ООП. В остальных случаях от _Doctrine 2_ будет мало пользы.

# 1.4. Требования

_Doctrine 2_ требуется версия _PHP_ не менее _5.3.0_. Для увеличения производительность рекомендуется использовать модуль _APC_для _PHP_.

# 1.5. Составляющие Doctrine 2

_Doctrine 2_ состоит из трех основных библиотек.

*   _Common_
*   _DBAL_ (включает в себя _Common_)
*   _ORM_ (включает в себя как _DBAL_, так и _Common_)

Данное руководство в основном относится к пакету _ORM_, однако иногда будут затронуты и остальные два. Есть определенные причины, по которым _Doctrine_ была разбита на несколько частей:

*   Декомпозиция библиотеки дает большую гибкости
*   Пакет _Common_ можно использовать отдельно от пакетов _ORM_ и _DBAL_
*   _DBAL_ можно использовать отдельно от _ORM_

## 1.5.1. Библиотека Common

Этот пакет содержит несколько компонентов, которые не имеют никаких внешних зависимостей, в т.ч. и от PHP. В _Common_ в качестве корневого пространства имен используется **Doctrine\Common**.

## 1.5.2. Библиотека DBAL

_DBAL_ содержит слой абстракции от БД, в качестве надстройки над библиотекой _PDO_, однако плотно на ней не завязана. Задача этого слоя — дать один общий API, который покрывает все различия между интерфейсами СУБД. В качестве корневого пространства имен для классов _DBAL_ используется **Doctrine\DBAL**.

## 1.5.3. Библиотека ORM

Пакет _ORM_ содержит в себе реализацию алгоритма объектно-реляционного отображения, реализуя прозрачные взаимосвязи и отношения для обычных _PHP_ объектов. В_ ORM_ в качестве корневого пространства имен используется **Doctrine\ORM**.

# 1.6. Установка

Существует несколько способов установки Doctrine. Ниже будут описаны все возможные варианты, так выбирайте какой вам больше нравится.

## 1.6.1. PEAR

Все три части _Doctrine_ можно легко установить из командной строки _PEAR_.

Установка только библиотеки _Common_ осуществляется следующей командой:

```
$ sudo pear install pear.doctrine-project.org/DoctrineCommon-<version>
```

_DBAL_ устанавливается так:

```
$ sudo pear install pear.doctrine-project.org/DoctrineDBAL-<version>
```

А _ORM_ так:

```
$ sudo pear install pear.doctrine-project.org/DoctrineORM-<version>
```

Тэг _<version>_ представляет собой номер версии, которую нужно установить. Например, если текущая версия _ORM 2.07_, то команда будет выглядеть так:

```
$ sudo pear install pear.doctrine-project.org/DoctrineORM-2.0.7
```

Когда установка будет завершена, вам нужно будет подключить загрузчик классов _ClassLoader_:

```php  
require 'Doctrine/ORM/Tools/Setup.php';  

Doctrine\ORM\Tools\Setup::registerAutoloadPEAR();
```

Все установленные библиотеки будут находится в корневой директории _PEAR_ в подкаталоге _Doctrine/_. Помимо этого, вы получите в свое распоряжении небольшую утилиту командной строки, с ее помощью вы будете выполнять типовые задачи. Запустите команду _doctrine_ без параметров, чтобы просмотреть доступные ключи запуска:

```
$ doctrine  
Doctrine Command Line Interface version 2.0.0BETA3-DEV  

Usage:  
  [options] command [arguments]  

Options:  
  --help -h Display this help message.  
  --quiet -q Do not output any message.  
  --verbose -v Increase verbosity of messages.  
  --version -V Display this program version.  
  --color -c Force ANSI color output.  
  --no-interaction -n Do not ask any interactive question.  

Available commands:  
  help Displays help for a command (?)  
  list Lists commands  
dbal  
  :import Import SQL file(s) directly to Database.  
  :run-sql Executes arbitrary SQL directly from the command line.  
orm  
  :convert-d1-schema Converts Doctrine 1.X schema into a Doctrine 2.X schema.  
  :convert-mapping Convert mapping information between supported formats.  
  :ensure-production-settings Verify that Doctrine is properly configured for a production  environment.  
  :generate-entities Generate entity classes and method stubs from your mapping information.  
  :generate-proxies Generates proxy classes for entity classes.  
  :generate-repositories Generate repository classes from your mapping information.  
  :run-dql Executes arbitrary DQL directly from the command line.  
  :validate-schema Validate that the mapping files.  
orm:clear-cache  
  :metadata Clear all metadata cache of the various cache drivers.  
  :query Clear all query cache of the various cache drivers.  
  :result Clear result cache of the various cache drivers.  
orm:schema-tool  
  :create Processes the schema and either create it directly on EntityManager Storage Connection or generate the SQL output.  
  :drop Processes the schema and either drop the database schema of EntityManager Storage Connection or generate the SQL output.  
  :update Processes the schema and either update the database schema of EntityManager Storage Connection or generate the SQL output.
```

## 1.6.2. Загрузка с сайта

_Doctrine 2_ можно также установить, скачав последнюю версию пакета со [страницы загрузки](http://www.doctrine-project.org/downloads).

Настройка и инициализация этой версии _Doctrine_ описываются в разделе [Настройка](http://odiszapc.ru/doctrine/configuration) данного руководства.

## 1.6.3. GitHub

В качестве альтернативы можно загрузить последнюю версию Doctrine 2 с GitHub.com:

```
$ git clone git://github.com/doctrine/doctrine2.git doctrine
```

Но, таким образом, у вас будут только исходные коды для пакета _ORM_. Для пакетов _Common_ и _DBAL_ нужно будет отдельно инициализировать дочерние модули:

```
$ git submodule init  
$ git submodule update
```

Этот финт обновит вашу рабочую копию для использования _Doctrine_ и тех версий ее дочерних библиотек, которые подходят к клонированной master-ветви _Doctrine 2_.

В разделе [Настройка](http://odiszapc.ru/doctrine/configuration) описано как настроить установленную с _Github_ версию _Doctrine_ для использования автозагрузки классов.

> Не стоит пытаться совместно использовать модули Doctrine-Common, Doctrine-DBAL и Doctrine-ORM, полученные из основной ветви репозитория. ORM просто может не захотеть работать с текущими версиями Common и DBAL из основной ветви. Вместо этого используйте Git Submodules

## 1.6.4. Subversion

> Не рекомендуется использовать зеркала Subversion. Они предоставят доступ только к последнему коммиту основной ветви и не загрузят дочерние модули.

Если вы предпочитаете _Subversion_, код можно получить как и раньше с _GitHub.com_ по протоколу _Subversion_:

```
$ svn co http://svn.github.com/doctrine/doctrine2.git doctrine2
```

Однако, так вы получите лишь основную ветвь _Doctrine 2_, без зависимых модулей _Common_ и _DBAL_. Их вам придется получить самостоятельно, но тут есть риск столкнуться с несовместимостью версий разных master-ветвей этих библиотек, о чем уже было сказано ранее.

# 1.7. Песочница

> Песочница доступна только в версии Doctrine 2, полученной из репозитория GitHub либо в ближайшее время будет доступна в качестве отдельного пакета на [странице загрузки](http://www.doctrine-project.org/projects/orm/download) (на сегодняшний день (11.02.12) отдельного пакета с песочницей нет на странице загрузки). Вы найдете ее в каталоге $root/tools/sandbox folder.

Песочница представляет собой настроенное и готовое к работе окружение для проведения разных экспериментов или с целью просто поиграться с _Doctrine 2_.

## 1.7.1. Обзор

Каталог с песочницей имеет следующую структуру:

```
sandbox/  
    Entities/  
        Address.php  
        User.php  
    xml/  
        Entities.Address.dcm.xml  
        Entities.User.dcm.xml  
    yaml/  
        Entities.Address.dcm.yml  
        Entities.User.dcm.yml  
    cli-config.php  
    doctrine  
    doctrine.php  
    index.php</div>
```

Ниже краткое описание того, какие директории и файлы за что отвечают:

В каталоге _Entities_ будут располагаться классы ваших моделей-сущностей. В качестве примера там уже лежат две сущности.

В каталоге _xml_ находятся описания сущностей в формате XML (если, конечно, вы предпочтете этот формат для их описания). Тут тоже есть два примера их использования.

Каталог _yaml_ — то же самое, но для формата YAML.

Файл _cli-config.php_ содержит код инициализации, необходимый для консольной утилиты.

_doctrine/doctrine.php_ — это утилита командной строки.

index.php — обычный индексный файл приложения на PHP, в котором используется _Doctrine 2_.

## 1.7.2. Небольшая обучалка

Выполните следующую команду из директории _tools/sandbox_:

```
$ php doctrine orm:schema-tool:create  
Creating database schema... Database schema created successfully!
```

Еще раз взгляните на каталог _tools/sandbox_. Внутри появилась новая база данных _SQLite_ под названием _database.sqlite_.

Откройте _index.php_ и в самом низу добавьте несколько строк кода, что-то вроде этого:

```php
<?php  
//... bootstrap stuff  

## PUT YOUR TEST CODE BELOW  

$user = new \Entities\User();  
$user->setName('Garfield');  
$em->persist($user);  
$em->flush();  

echo "User saved!";
```

Запустите _index.php_ через браузер или из командной строки. На экране появится строка “User saved!”.

Теперь давайте заглянем в наше хранилище _SQLite_. Снова выполните команду из папки _tools/sandbox_:

```
$ php doctrine dbal:run-sql “select * from users”
```

Результат выполнения:

```
array(1) {  
  [0]=>  
  array(2) {  
    ["id"]=>  
    string(1) "1"  
    ["name"]=>  
    string(8) "Garfield"  
  }  
}
```

Поздравляем, вы только что сохранили в базе _SQLite_  вашу первую сущность с автоматически сгенерированным ID.

Теперь внесите следующие правки в _index.php_:

```php
<?php  
//... bootstrap stuff  

## PUT YOUR TEST CODE BELOW  

$q = $em->createQuery('select u from Entities\User u where u.name = ?1');  
$q->setParameter(1, 'Garfield');  
$garfield = $q->getSingleResult();  

echo "Hello " . $garfield->getName() . "!";
```

Вы создали свой первый _DQL_-запрос для получения из базы данных пользователя с именем ‘Garfield’. Безусловно, это можно было сделать и более простым способом, мы лишь хотели продемонстрировать сам _DQL_. Догадаетесь как это можно сделать проще?

Когда вы создаете новые классы моделей или изменяете существующе, можно перестроить схему базы данных с помощью двух последовательных команд: команды **doctrine orm:schema-tool –drop** для удаления базы (будьте внимательны) а затем **doctrine orm:schema-tool –create** для создание новой схемы.