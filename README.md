# Web-News 

Полнофункциональное веб-приложение социальной сети с возможностью создания, просмотра и обсуждения новостей. Проект демонстрирует best practices в разработке React приложений с использованием современного стека технологий.

## Быстрый старт

### Установка и запуск

```bash
# Установить зависимости
npm install

# Запустить проект (Frontend + Backend)
npm run start:dev:vite
```

Проект будет доступен по адресу: **http://localhost:5173/**

### Учетные данные для входа

- **Логин:** `testuser`
- **Пароль:** `123`

## Основные команды

### Запуск приложения

- `npm run start` - Frontend на Webpack
- `npm run start:vite` - Frontend на Vite
- `npm run start:dev` - Frontend + Backend (Webpack)
- `npm run start:dev:vite` - Frontend + Backend (Vite) **Рекомендуется**
- `npm run start:dev:server` - Только Backend

### Сборка проекта

- `npm run build:prod` - Продакшн сборка (минимизирована)
- `npm run build:dev` - Разработка сборка (без минификации)

### Тестирование

- `npm run test:unit` - Unit тесты (Jest + React Testing Library)
- `npm run test:ui` - Скриншотные тесты (Loki)
- `npm run test:ui:ok` - Подтверждение новых скриншотов
- `npm run test:ui:report` - HTML отчет скриншотных тестов
- `npm run test:e2e` - E2E тесты (Cypress)

### Линтинг и форматирование

- `npm run lint:ts` - Проверка TypeScript кода
- `npm run lint:ts:fix` - Автоисправление TypeScript ошибок
- `npm run lint:scss` - Проверка стилей (SCSS)
- `npm run lint:scss:fix` - Автоисправление SCSS ошибок

### Документирование и генерация

- `npm run storybook` - Запуск Storybook для просмотра компонентов
- `npm run storybook:build` - Сборка Storybook
- `npm run generate:slice` - Генерация нового FSD слайса
- `npm run prepare` - Pre-commit хуки (Husky)

## Архитектура проекта

Проект следует методологии **Feature Sliced Design (FSD)** — современной архитектурной системе для масштабируемых приложений.

### Основные слои FSD

```
shared/     ← Переиспользуемый код (UI компоненты, утилиты, API)
entities/   ← Бизнес сущности (Article, User, Comment и т.д.)
features/   ← Бизнес-логика фич (авторизация, фильтры, формы)
widgets/    ← Композитные компоненты (Navbar, Sidebar, Page)
pages/      ← Страницы приложения
app/        ← Инициализация приложения (провайдеры, роутинг)
```

**Ключевые правила:**
- Страницы не импортируют друг друга
- Нельзя импортировать из верхних слоев в нижние (widgets → features запрещено)
- Межмодульное взаимодействие только через public API
- Каждый модуль имеет свой index.ts для экспорта

[Подробнее о FSD](https://feature-sliced.design/docs/get-started/tutorial)

## Структура проекта

### Сущности (entities)

Основные бизнес-сущности приложения:

- **Article** — Новостные статьи с комментариями и рейтингом
- **Comment** — Комментарии к статьям
- **Counter** — Счетчик (демонстрационная сущность)
- **Country** — Страны (справочник)
- **Currency** — Валюты (справочник)
- **Notification** — Уведомления пользователя
- **Profile** — Профиль пользователя с редактированием
- **Rating** — Система рейтинга для статей и профилей
- **User** — Данные авторизованного пользователя

### Основные функции (features)

Независимые бизнес-логики функциональности:

- **AuthByUsername** — Авторизация через логин/пароль
- **editableProfileCard** — Редактирование профиля с валидацией
- **articleEditForm** — Форма создания/редактирования статей
- **articleRating** — Оценка статей пользователями
- **articleRecommendationsList** — Рекомендуемые статьи
- **addCommentForm** — Форма добавления комментариев
- **avatarDropdown** — Меню профиля в шапке
- **notificationButton** — Кнопка уведомлений
- **LangSwitcher** — Переключение языка (EN/RU)
- **ThemeSwitcher** — Переключение темы оформления
- **ArticleSortSelector** — Фильтры и сортировка статей
- **ArticleTypeTabs** — Вкладки по типам статей
- **ArticleViewSelector** — Переключение представления статей (список/плитка)

## Технологический стек

### Frontend
- **React 18** — UI библиотека
- **TypeScript** — Типизированный JavaScript
- **Redux Toolkit** — Управление состоянием
- **RTK Query** — Кэширование и синхронизация данных с сервером
- **React Router v6** — Маршрутизация
- **Axios** — HTTP клиент

### Сборка и развертывание
- **Vite 3** — Быстрая сборка (рекомендуется)
- **Webpack 5** — Альтернативная сборка
- **Babel** — Трансформация JavaScript

### Тестирование (четыре уровня)
- **Jest** — Unit тесты логики
- **React Testing Library** — Тесты компонентов
- **Loki** — Скриншотные тесты (регрессионное тестирование)
- **Cypress** — E2E тесты пользовательских сценариев

### Документирование
- **Storybook 6** — Каталог компонентов с интерактивными примерами
- **storybook-addon-mock** — Мокирование API запросов в Storybook

### Качество кода
- **ESLint** — Линтинг TypeScript/JavaScript
- **Stylelint** — Линтинг SCSS стилей
- **Husky** — Pre-commit хуки
- **eslint-plugin-ulbi-tv-plugin** — Кастомный плагин для контроля FSD архитектуры

### Backend для разработки
- **JSON Server** — Mock сервер (порты 8000 и 8443)

## Ключевые особенности

### Управление состоянием
- Redux Toolkit для глобального состояния
- Асинхронные редюсеры подгружаются динамически через `DynamicModuleLoader`
- RTK Query для кэширования и синхронизации данных с API

### Интернационализация (i18n)
- Библиотека **i18next** для многоязычности
- Поддержка русского и английского языков
- Файлы переводов в `public/locales/`

### Feature Flags
- Система условных фич через `toggleFeatures` хелпер
- Автоматическое удаление фич скриптом `remove-feature.ts`
- Удобное переключение функциональности без деплоя

### Архитектурный контроль
Кастомный ESLint плагин **eslint-plugin-ulbi-tv-plugin** обеспечивает:
- **path-checker** — Запрет абсолютных импортов внутри модуля
- **layer-imports** — Соблюдение иерархии слоев FSD (widgets не может импортировать из features)
- **public-api-imports** — Импорты между модулями только через public API (с автоисправлением)

## Качество и CI/CD

### Pre-commit хуки (Husky)
Автоматическая проверка перед коммитом:
- Линтинг TypeScript кода
- Линтинг SCSS стилей
- Форматирование кода

### GitHub Actions CI Pipeline
Полная автоматизация при push:
- Unit тесты (Jest + React Testing Library)
- Скриншотные тесты (Loki)
- E2E тесты (Cypress)
- Сборка проекта (Webpack и Vite)
- Сборка Storybook
- Проверка линтерами

## Конфигурационные файлы

```
config/
  ├── babel/              # Конфигурация Babel
  ├── build/              # Конфигурация Webpack
  ├── jest/               # Конфигурация Jest
  └── storybook/          # Конфигурация Storybook

scripts/
  ├── generate-visual-json-report.js   # Отчеты тестов
  ├── remove-feature.ts                # Удаление фич флагов
  └── createSlice/                     # Генерация FSD слайсов
```

## Дополнительная документация

- [Подробное руководство по тестам](/docs/tests.md)
- [Руководство Storybook](/docs/storybook.md)
- [Документация Feature Sliced Design](https://feature-sliced.design/docs/get-started/tutorial)
- [Документация i18next](https://react.i18next.com/)
- [Redux Toolkit](https://redux-toolkit.js.org/)
- [RTK Query](https://redux-toolkit.js.org/rtk-query/overview)

## Разработка

### Создание нового FSD слайса
```bash
npm run generate:slice
```

Будет интерактивно создана структура нового модуля со всеми необходимыми файлами.

### Примеры компонентов в Storybook
Каждый переиспользуемый компонент имеет примеры использования в Storybook с мокированными API запросами через `storybook-addon-mock`.

Файлы историй создаются рядом с компонентом: `ComponentName.stories.tsx`
