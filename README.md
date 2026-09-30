## 🚀 REST API Endpoints

### 1. 🔐 Authentication (`/auth`)
* `POST /api/v1/auth/login` — Аутентификация сотрудника по PIN/паролю и выдача JWT-токена.
* `POST /api/v1/auth/logout` — Завершение сессии и инвалидация токена.
* `GET /api/v1/auth/me` — Получение профиля и прав доступа (`permissions`) текущего сотрудника.

### 2. 🪑 Tables Management (`/tables`)
* `GET /api/v1/tables` — Получить список всех столов в зале, их вместимость и статус.
* `GET /api/v1/tables/<id>` — Детальная информация по конкретному столу.
* `POST /api/v1/tables` — Добавление нового стола на схему зала (Админ).
* `PATCH /api/v1/tables/<id>/status` — Быстрое изменение статуса стола (`free`, `occupied`, `reserved`, `dirty`).
* `DELETE /api/v1/tables/<id>` — Удаление стола из системы.

### 3. 🗓️ Reservations (`/reservations`)
* `GET /api/v1/reservations` — Список всех бронирований с фильтрацией по дате.
* `POST /api/v1/reservations` — Создание новой брони (имя, телефон, время, номер стола).
* `PATCH /api/v1/reservations/<id>` — Изменение статуса брони (`confirmed`, `cancelled`, `no-show`).
* `DELETE /api/v1/reservations/<id>` — Удаление записи о бронировании.

### 4. 🍽️ Digital Menu (`/menu`)
* `GET /api/v1/menu` — Получить полное меню ресторана (с группировкой по категориям).
* `GET /api/v1/menu/<id>` — Карточка конкретного блюда (цена, состав, КБЖУ).
* `POST /api/v1/menu` — Создание новой позиции в меню (Админ).
* `PUT /api/v1/menu/<id>` — Полное редактирование данных блюда.
* `PATCH /api/v1/menu/<id>/toggle-availability` — Переключение стоп-листа (доступность блюда на кухне).
* `DELETE /api/v1/menu/<id>` — Архивация/удаление блюда из меню.

### 5. 🍕 Menu Modifiers (`/menu/modifiers`)
* `GET /api/v1/menu/modifiers` — Список всех групп модификаторов (добавки, степень прожарки).
* `POST /api/v1/menu/modifiers` — Создание новой группы модификаторов для блюд.

### 6. 📝 Order Management (`/orders`)
* `GET /api/v1/orders` — Список всех заказов (фильтры: `active`, `completed`, `by-waiter`).
* `GET /api/v1/orders/<id>` — Детальный просмотр чека со статусом готовности каждого блюда.
* `POST /api/v1/orders` — Создание нового заказа (черновик, привязка к столу).
* `PATCH /api/v1/orders/<id>/items` — Добавление новых блюд в открытый чек или удаление позиций.
* `PATCH /api/v1/orders/<id>/status` — Изменение статуса заказа (`draft`, `sent-to-kitchen`, `cooking`, `ready`, `paid`).
* `POST /api/v1/orders/<id>/split` — Разделение одного счета на несколько гостей.

### 7. 🍳 Kitchen Display System / KDS (`/kds`)
* `GET /api/v1/kds/tickets` — Очередь блюд для поваров, разделенная по цехам (горячий, холодный, бар).
* `PATCH /api/v1/kds/items/<order_item_id>/status` — Изменение поваром статуса блюда (`waiting`, `cooking`, `ready`).

### 8. 💳 Payments & Fiscalization (`/payments`)
* `POST /api/v1/payments/checkout` — Закрытие счета и проведение оплаты (карты, наличные, СБП).
* `GET /api/v1/payments/transactions` — История всех транзакций за текущую смену.
* `POST /api/v1/payments/refund` — Полный или частичный возврат средств (Менеджер).

### 9. 📦 Inventory & Stocks (`/inventory`)
* `GET /api/v1/inventory/stocks` — Текущие остатки продуктов на складе в реальном времени.
* `POST /api/v1/inventory/supply` — Оформление прихода новой партии продуктов от поставщика.
* `POST /api/v1/inventory/write-off` — Акт списания испорченных продуктов.
* `GET /api/v1/inventory/alerts` — Список критически заканчивающихся позиций на складе.

### 10. 👥 Staff & Shifts (`/staff`)
* `GET /api/v1/staff/users` — Список всех сотрудников ресторана и их ролей.
* `POST /api/v1/staff/shifts/clock-in` — Фиксация открытия рабочей смены сотрудником.
* `POST /api/v1/staff/shifts/clock-out` — Фиксация закрытия рабочей смены.
* `GET /api/v1/staff/performance` — Статистика выручки и среднего чека по каждому официанту.
* 
## 11. 📊 Reports & Analytics (`/reports`)
* `GET /api/v1/reports/dashboard` — Сводные метрики за день (выручка, средний чек, загрузка зала в %).
* `GET /api/v1/reports/abc-analysis` — Отчет по самым продаваемым и маржинальным позициям меню.
* `GET /api/v1/reports/revenue-period` — Данные графиков выручки по дням/неделям для React-дашборда.
