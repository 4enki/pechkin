# 📮 «Печкин»
«Печкин» помогает быстро начать вёрстку писем

## С чего начать?
1. Склонировать репозиторий в папку `new-mails`, перейти в созданную папку проекта, удалить скрытую папку `.git`:
    ```shell
    git clone https://github.com/4enki/pechkin.git new-mails && cd $_ && rm -rf ./.git
    ```

1. Перед первым запуском нужно установить зависимости (_быстрее через [Yarn](https://yarnpkg.com); один раз на проект_):
    ```shell
    npm/yarn install
    ```

1. Перейти в дирректорию эталонного письма и запустить сборку с вотчером:
    ```shell
    gulp
    ```

## Как всё устроено
В корне «Печкина» есть директория `projects` в которой находятся отдельные проекты каждого письма/рассылки. Пример можно смотреть в `projects/reference-mail`. Внутри отдельного проекта должен быть файл `gulpfile.js`.

Запуск сборки с вотчером происходит по команде:
```shell
gulp
```

### Шаблонизация
Для шаблонизации использован [Nunjucks](https://mozilla.github.io/nunjucks/templating.html). Файлы разметки живут в папке отдельного проекта `src/templates/`, страницы размещаются в `src/templates/pages/` и состоят из компонентов _(= строк/этажей)_ `src/templates/components/`.

Лйэаут письма находится в `src/templates/layouts/layout.html`.

Набор снипетов-помощников для вывода типовых блоков `macro` находится в `projects/reference-mail/src/templates/utils/utils.html`. Пример использования есть внутри этого файла.

### Стили
Используемый препроцессор — [SASS](https://sass-scss.ru/).

Готовый CSS компилируются в файл `src/templates/pages` (не попадает в `git`, смотрите файл `.gitignore`) и инлайнится в документе с помощью [`gulp-inline-css`](https://github.com/jonkemp/gulp-inline-css).

### Графика
Вся графика размещается в `src/images`, собираются в `dist/assets/images/` с сохранением структуры.

Изображения для отдельного блока размещаются в папке `src/templates/components/**/images/` и копируются в `dist/assets/images/` без сохранения структуры.

Для сжатия растовой графики рекомендуется использовать [Squoosh](https://squoosh.app/).

## Структура папок и файлов
```
├── gulpfile.js/                      # Конфиг Gulp.js
│   ├── tasks/                        # Gulp-такси
│   │   ├── server.js                 # Таск browser-sync
│   │   ├── styles.js                 # Таск сборки стилей из SCSS для инлайна
│   │   ├── template.js               # Таск шаблонизации: nunjucks, markdown, inline-css
│   │   └── watch.js                  # Бдительные вотчеры изменений
│   ├── utils/                        # Помогаторы
│   ├── paths.js                      # Пути к ресурсам проекта
│   ├── config.js                     # Конфиг gulp-сборки: путь, структура и т.п.
│   └── index.js                      # Основные задачи
├── projects                          # Отдельные проекты писем, рассылки и проч.
│   └── reference-mail                # Пример эталонного письма и стуктуры сборки
│       ├── README.md                 # Пример файла-документации
│       ├── dist                      # Готовое письмо (автогенерация)
│       ├── gulpfile.js               # Стартовый gulp-файлы отдельного письма
│       └── src                       # Исходники проекта
│           ├── images                # Графика
│           ├── styles                # Стили
│           │   ├── buttons.scss      #
│           │   ├── content.scss      #
│           │   ├── layout.scss       #
│           │   ├── style.scss        #
│           │   ├── typo.scss         #
│           │   └── variables.scss    #
│           └── templates             # Шаблоны HTML-разметки писем
│               ├── components        # Отдельные части
│               ├── layouts           # Лэйаут
│               ├── pages             # Отдельные страницы
│               └── utils             # Набор снипетов-помощников
├── resources/                        # Файлы для работы: макеты, данные и проч.
├── .editorconfig                     # Конфигурационный файл IDE
├── .gitignore                        # Список исключённых файлов из Git
├── package.json                      # Файл-конфиг «Печкина»: пакеты, скприты, выходные данные
├── CHANGELOG.md                      # Летопись версий
└── README.md                         # Документация «Печкина» (вы сейчас здесь, кстати)
```

## ⚗️ В тему
* http://emailframe.work/
* https://litmus.com/resources/free-responsive-email-templates ★
* https://www.campaignmonitor.com/email-templates/
* https://foundation.zurb.com/emails.html
* https://mjml.io/ ★
* https://tedgoas.github.io/Cerberus/
* https://github.com/mailchimp/email-blueprints
* https://github.com/InterNations/antwort
* https://www.muicss.com/docs/v1/email/boilerplate-html
* Поддерживаемые CSS-свойства в разных почтовых клиентах: https://www.campaignmonitor.com/css/
* https://github.com/dudeonthehorse/kilogram ★ — к сожалению, не поддерживается автором
