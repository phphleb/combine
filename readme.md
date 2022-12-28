COMBINATOR
=====================



[![COMBINATOR LOGO](https://raw.githubusercontent.com/phphleb/combinator/0de1d4cc1243cd623f843f01073cf010453b3f1b/logo.png)](https://github.com/phphleb/combinator/tree/master)

**Сборщик компонентов для библиотек фреймворка HLEB ([github.com/phphleb/hleb](https://github.com/phphleb/hleb))**

При наличии установленных библиотек (компонентов), которые внедряются в проект или удаляются по образцу
библиотеки UPDATER ([github.com/phphleb/updater](https://github.com/phphleb/updater)), позволяет автоматизировать такие
процессы, запуская выполнение поочерёдно. 

Образец оформления вы можете увидеть в библиотеках HLOGIN и DRAFT, принцип подключения их последовательно в том, что
их файлы _start.php_ включаются последовательно, поэтому нужно следить, чтобы при подключении общие файлы добавлялись с помощью
_include_once_ и файлы подключения не содержали конфликтующие функции и константы. Если делать по образцу, то там всё просто и последние не будут нужны.

Установка при помощи Composer:
```bash
$ composer require phphleb/combinator
```
_____

### Стандартное обновление компонентов

Установка/обновление компонентов:

```bash
$ php console phphleb/combinator --add
```

Удаление компонентов из проекта:

```bash
$ php console phphleb/combinator --remove
```

Если вызвать эту команду, то можно увидеть список найденных подходящих библиотек.
```bash
$ php console phphleb/combinator --help
```

_________________________

### Автоматическое обновление компонентов

Для автоматического цикла действий с компонентами (без участия пользовательского ввода данных), нужно создать конфигурационный файл
в корневой директории проекта по образцу прилагаемого в библиотеке файла 'updater.json'. Теперь, при обнаружении этого файла в корне проекта, установщик заполнит
недостающую информацию из него. Файл по структуре разбит на глобальные и конкретные данные компонентов:

**global** - Глобальные настройки.

**global.paths** - Настройки для глобального соответствия директорий (шаблон => реальная).

**include_special_names** - Настройки для отдельных компонентов по имени первого параметра, установленного
в компоненте как  `$uploader->setSpecialNames('`**example-directory**`', ...);`В каждом из них можно задать текущий дизайн.
Если компонент не указан в этом перечислении,  он будет пропущен при установке.


Вызов добавления и удаления компонентов аналогичен стандартному, но можно использовать ещё несколько настроек. Следующим добавлением параметра
_--with-config-file-path=_ позволяет указать файл конфигурации по пути из корневой папки проекта.

```bash
$ php console phphleb/combinator --add --with-config-file-path=/storage/lib/combinator/updater.json
```

Также можно отменить вывод команды в консоль:

```bash
$ php console phphleb/combinator --add --quiet
```

При помощи автоматических действий можно разбить компоненты на наборы, описанные в конфигурационных файлах. Также это будет полезным при 
обновлении библиотек пользователями проекта, чтобы он каждый раз не указывал соответствие папок в установщике, а один раз изменил в
конфигурационном файле.




_________________________

Чтобы в процессе установки выводилась краткая информация о библиотеке, создайте в её корневой директории файл _combinator-info.txt_ c описанием.
