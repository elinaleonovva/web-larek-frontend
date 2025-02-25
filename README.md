# Web-ларёк

Интернет-магазин с товарами для веб-разработчиков — Web-ларёк. В нём можно посмотреть каталог товаров, добавить товары в корзину и сделать заказ.

## Используемый стек
- HTML
- SCSS
- TypeScript
- Webpack

## Инструкция по сборке и запуску
После клонирования репозитория установите зависимости:
```sh
npm install
```

Для запуска проекта в режиме разработки выполните команду:
```sh
npm run start
```
Затем откройте браузер и перейдите по адресу `http://localhost:8080`.

## Архитектура
Проект построен на основе паттерна **MVP (Model-View-Presenter)**.
- **Model** отвечает за работу с данными и бизнес-логику, а именно загрузка данных по API, работа с данными, полученными от пользователей.
- **View** предоставляет интерфейс для пользователя и не содержит логики.
- **Presenter** получает пользовательские действия, обновляет модель и передаёт данные обратно во View.

### Структура проекта
```
src/                   # Исходные файлы проекта
├── components/        # Папка с JS-компонентами
│   └── base/         # Базовые классы
├── pages/
│   └── index.html    # HTML-файл главной страницы
├── styles/
│   └── styles.scss   # Корневой файл стилей
├── types/
│   └── types.ts      # Файл с типами данных
├── utils/
│   ├── constants.ts  # Файл с константами
│   └── utils.ts      # Файл с утилитами
└── index.ts          # Точка входа приложения
```

## Описание базовых классов

### `Model<T>`
Абстрактный класс, представляющий базовую модель данных:
- Хранит данные и управляет ими.
- Поддерживает событийную модель (`emitChanges`).

### `Component<T>`
Абстрактный класс для UI-компонентов:
- Управляет взаимодействием с DOM (`toggleClass`, `setText`, `setHidden`, `setVisible`).
- Обеспечивает базовые методы отрисовки (`render`).

### `EventEmitter`
Реализует паттерн **Observer**, управляет событиями:
- `on` — подписка на событие.
- `off` — отписка от события.
- `emit` — вызов событийных подписчиков.
- `trigger` — генерация событий для интеграции с другими классами.

## Модели данных

### `AppState`
Отвечает за состояние приложения:
- Хранит список товаров (`store`) и корзину (`basket`).
- Управляет оформлением заказа (`order`).
- Включает методы работы с корзиной (`addToBasket`, `deleteFromBasket`, `clearBasket`).
- Реализует валидацию (`validateContacts`, `validateOrder`).
- Управляет изменением данных (`setStore`, `resetSelected`).

### `Api`
Класс для работы с сервером:
- `handleResponse(response: Response): Promise<object>` — обработка ответа сервера.
- `get(uri: string)` — получает данные по URI.
- `post(uri: string, data: object)` — отправляет данные на сервер.

## Классы представления

### `Page`
Компонент главной страницы:
- Управляет отображением товаров и корзины.
- Обновляет количество товаров (`counter`).
- Контролирует прокрутку страницы (`locked`).

### `Card`
Компонент карточки товара:
- Отображает название, изображение, цену.
- Позволяет добавлять товар в корзину (`selected`).

### `Basket`
Компонент корзины:
- Хранит список товаров (`list`).
- Управляет отображением общей стоимости (`price`).
- Позволяет оформлять заказ (`disableButton`).

### `Order`
Компонент формы заказа:
- Позволяет вводить данные для доставки (`paymentSelection`).
- Проверяет корректность данных (`validateOrder`).

### `Contacts`
Компонент контактных данных:
- Позволяет вводить email и телефон.
- Проверяет корректность перед оформлением заказа (`validateContacts`).

### `Modal`
Компонент модальных окон:
- Управляет их отображением (`open`, `close`).

### `Success`
Отображает сообщение об успешном оформлении заказа.

## Автор
Леонова Элина ИКБО-10-23

