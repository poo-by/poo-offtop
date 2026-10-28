# Poo Offtop

Сворачиваемый блок «Оффтоп» для XenForo / HTML-шаблонов.  
Позволяет скрыть контент, не относящийся к основной теме обсуждения, и пометить его как прочитанный.

## Возможности

- Раскрытие и закрытие блока без внешних JavaScript-библиотек.
- Чистый CSS-аккордеон на скрытом `checkbox`.
- Анимация раскрытия, шеврона и иконки.
- Предупреждение «Под спойлером может быть любой контент».
- Метка **«Прочитано»** после первого открытия.
- Сохранение состояния «прочитано» в `localStorage`.
- Поддержка `prefers-reduced-motion`.

## Как работает

Внутри блока находится скрытый `<input type="checkbox">`.  
Клик по `<label class="poo-offtop__summary">` переключает его состояние.

- `checkbox` не отмечен — контент скрыт через `max-height: 0`.
- `checkbox` отмечен — контент раскрывается до `max-height: 5000px`.
- При первом открытии JavaScript добавляет класс `is-seen` и сохраняет ключ в `localStorage`.
- При следующей загрузке страницы блок сразу показывает статус «Прочитано».

## Использование

Замените `{text}` на содержимое оффтопа:

```html
<div class="poo-offtop">
    <div class="poo-offtop__notice">
        <!-- предупреждение -->
    </div>

    <input type="checkbox" id="poo-offtop-toggle" class="poo-offtop__toggle">
    <label for="poo-offtop-toggle" class="poo-offtop__summary">
        <!-- шапка блока -->
    </label>

    <div class="poo-offtop__content">
        <div class="poo-offtop__inner">
            Здесь любой контент: текст, изображения, цитаты, ссылки и т. д.
        </div>
    </div>

    <style>
        <!-- стили компонента -->
    </style>

    <script>
        <!-- логика статуса «Прочитано» -->
    </script>
</div>
```

### В XenForo

Компонент можно оформить как BB-код:

```text
[OFFTOP]Текст оффтопа[/OFFTOP]
```

Где `{text}` — содержимое между открывающим и закрывающим тегами.

Пример HTML-шаблона BB-кода:

```html
<div class="poo-offtop">
    <div class="poo-offtop__notice">
        <svg class="poo-offtop__warning-icon" width="12" height="12" viewBox="0 0 576 512" fill="currentColor" aria-hidden="true">
            <path d="M569.517 440.013C587.975 472.007 564.806 512 527.94 512H48.054c-36.937 0-59.999-40.055-41.577-71.987L246.423 23.985c18.467-32.009 64.72-31.951 83.154 0l239.94 416.028zM288 354c-25.405 0-46 20.595-46 46s20.595 46 46 46 46-20.595 46-46-20.595-46-46-46zm-43.673-165.346l7.418 136c.347 6.364 5.609 11.346 11.982 11.346h48.546c6.373 0 11.635-4.982 11.982-11.346l7.418-136c.375-6.874-5.098-12.654-11.982-12.654h-63.383c-6.884 0-12.356 5.78-11.981 12.654z"/>
        </svg>
        <span class="poo-offtop__warning-text">Под спойлером может быть любой контент — не по теме обсуждения.</span>
    </div>

    <input type="checkbox" id="poo-offtop-toggle" class="poo-offtop__toggle">
    <label for="poo-offtop-toggle" class="poo-offtop__summary">
        <img class="poo-offtop__icon" src="https://poo.by/styles/fa/regular/mug.svg" width="14" height="14" alt="" aria-hidden="true">
        <span class="poo-offtop__title">Оффтоп</span>
        <span class="poo-offtop__sep"></span>
        <span class="poo-offtop__value">
            Контент не по теме
            <span class="poo-offtop__status">
                (<img class="poo-offtop__check" src="https://poo.by/styles/fa/regular/check.svg" width="10" height="10" alt="" aria-hidden="true">Прочитано)
            </span>
        </span>
        <span class="poo-offtop__hint">
            <span class="poo-offtop__hint-open">Открыть</span>
            <span class="poo-offtop__hint-close">Закрыть</span>
        </span>
        <svg class="poo-offtop__chevron" width="16" height="16" viewBox="0 0 16 16" aria-hidden="true">
            <path d="M4 6l4 4 4-4" fill="none" stroke="currentColor" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
    </label>

    <div class="poo-offtop__content">
        <div class="poo-offtop__inner">{text}</div>
    </div>

    <style>
        /* вставьте сюда полный CSS из компонента */
    </style>

    <script>
        // вставьте сюда полный JS из компонента
    </script>
</div>
```

## Структура

```text
.poo-offtop
├── .poo-offtop__notice       Предупреждение о возможном оффтопе
├── .poo-offtop__toggle       Скрытый checkbox
├── .poo-offtop__summary      Кликабельная шапка блока
│   ├── .poo-offtop__icon     Иконка кружки
│   ├── .poo-offtop__title    Слово «Оффтоп»
│   ├── .poo-offtop__value    Подпись и статус «Прочитано»
│   ├── .poo-offtop__hint     «Открыть» / «Закрыть»
│   └── .poo-offtop__chevron  Стрелка
├── .poo-offtop__content      Контейнер с анимацией раскрытия
│   └── .poo-offtop__inner    Непосредственно контент
├── <style>                   Стили компонента
└── <script>                  Логика статуса «Прочитано»
```

## Ключевые классы

| Класс | Назначение |
|---|---|
| `.poo-offtop` | Корневой контейнер компонента |
| `.poo-offtop__toggle` | Скрытый `checkbox`, управляющий раскрытием |
| `.poo-offtop__summary` | Заголовок, по которому кликают |
| `.poo-offtop__content` | Обёртка скрываемого содержимого |
| `.poo-offtop__inner` | Внутренний контент оффтопа |
| `.poo-offtop__notice` | Красное предупреждение над блоком |
| `.is-seen` | Модификатор: оффтоп уже открывался |

## Настройка

### Акцентный цвет

```css
.poo-offtop {
    --poo-accent: #7681FF;
}
```

### Внутренние отступы

```css
.poo-offtop {
    --poo-pad: 12px;
}
```

### Максимальная высота контента

По умолчанию:

```css
.poo-offtop__toggle:checked ~ .poo-offtop__content {
    max-height: 5000px;
}
```

Если оффтоп может быть очень длинным, увеличьте значение, например до `10000px`.

## Хранение состояния

JavaScript формирует ключ по первым 60 символам текста оффтопа:

```js
var key = 'poo_offtop_seen_' + inner.textContent.trim().slice(0, 60);
```

Особенности:

- одинаковый текст в двух блоках будет иметь общее состояние «Прочитано»;
- изменение первых символов текста создаст новое состояние;
- очистка `localStorage` сбрасывает статус «Прочитано».

## Доступность

- Раскрытие реализовано через нативный `checkbox` и `label`, поэтому работает с клавиатуры.
- При фокусе на `checkbox` шапка получает видимую обводку через `:focus-visible`.
- Декоративные иконки помечены `aria-hidden="true"`.
- Анимации отключаются при `prefers-reduced-motion: reduce`.

## Совместимость

Требуется поддержка:

- CSS `:has()` — для скрытия предупреждения после открытия;
- `localStorage`;
- современных CSS transitions и custom properties.

Рекомендуемые браузеры: актуальные версии Chrome, Edge, Firefox и Safari.

## Возможные улучшения

- Заменить `max-height` на анимацию `grid-template-rows: 0fr -> 1fr`.
- Добавить `aria-expanded` и роль `button` для более точной семантики.
- Вынести CSS и JavaScript в отдельные файлы.
- Добавить собственный заголовок: `[OFFTOP=Мои мысли]...[/OFFTOP]`.
