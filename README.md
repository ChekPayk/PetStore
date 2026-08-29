# PetStore

## Описание

**PetStore** — это веб-приложение на Vue 3, витрина приюта для животных. Пользователь видит питомцев, которые «ищут дом», отдельно — «выпускников» (тех, кого уже забрали), и может добавить нового питомца через диалоговое окно в шапке.

Данные приложение берёт из публичного демо-API [Swagger Petstore](https://petstore.swagger.io/) (`https://petstore.swagger.io/v2`). Типизированный клиент к нему генерируется автоматически из [`src/swagger.json`](src/swagger.json).

## Функционал

- Просмотр списка питомцев со статусом «ищут дом» (`available`)
- Просмотр списка «выпускников» — питомцев со статусом «продан» (`sold`)
- Добавление нового питомца через форму в шапке приложения
- Навигация между разделами (шапка) и блок ссылок на соцсети (футер)

## Стек

| Технология | Назначение |
|---|---|
| [Vue 3](https://vuejs.org/) + `<script setup>` | UI, реактивность |
| [Vuetify 3](https://vuetifyjs.com/) | компоненты интерфейса |
| [Vite 6](https://vitejs.dev/) | сборка и dev-сервер (HMR) |
| TypeScript + [vue-tsc](https://github.com/vuejs/language-tools) | типизация |
| [unplugin-vue-router](https://github.com/posva/unplugin-vue-router) | роутинг по файлам из `src/pages/` |
| [unplugin-vue-components](https://github.com/unplugin/unplugin-vue-components) | автоимпорт компонентов |
| [swagger-typescript-api](https://github.com/acacode/swagger-typescript-api) | генерация API-клиента |
| ESLint (`eslint-config-vuetify`) | линтинг |

## Структура проекта

```
src/
├── Api.ts                 # сгенерированный клиент к Swagger Petstore API
├── swagger.json           # OpenAPI-спецификация, источник для генерации Api.ts
├── App.vue                # корневой layout: шапка, футер, <router-view>
├── main.ts                # точка входа, подключение плагинов
├── components/
│   ├── PetList.vue        # список питомцев, запрос pet.findPetsByStatus
│   ├── AddAnimal.vue      # диалог добавления питомца, запрос pet.addPet
│   └── icons/             # SVG-иконки (лого, соцсети)
├── pages/
│   ├── index.vue          # маршрут "/"  — «Ищут дом»  (PetList status="available")
│   └── Sold.vue           # маршрут "/sold" — «Выпускники» (PetList status="sold")
├── plugins/               # регистрация Vuetify, роутера и пр.
├── router/index.ts        # создание роутера (маршруты генерируются из pages/)
├── styles/                # глобальные стили и настройки Vuetify
└── assets/                # изображения
```

Маршруты **не** прописываются вручную: файл в `src/pages/` = маршрут (`index.vue` → `/`, `Sold.vue` → `/sold`).

## Запуск

Требуется Node.js 22+.

```bash
npm install
npm run dev
```

После запуска приложение доступно на **http://localhost:3000/**.

## Команды

| Команда | Что делает |
|---|---|
| `npm run dev` | dev-сервер с горячей перезагрузкой (порт 3000) |
| `npm run build` | продакшн-сборка в `dist/` (с проверкой типов) |
| `npm run preview` | локальный просмотр собранной версии |
| `npm run type-check` | проверка типов через `vue-tsc` |
| `npm run lint` | ESLint с автоисправлением |
| `npm run swagger` | перегенерировать `src/Api.ts` из `src/swagger.json` |

## Работа с API

Клиент используется так:

```ts
import { Api } from '@/Api.ts'

const petApi = new Api()
const { data } = await petApi.pet.findPetsByStatus({ status: ['available'] })
```

Базовый адрес API зашит в [`src/Api.ts`](src/Api.ts) (`https://petstore.swagger.io/v2`) и формируется из полей `host` + `basePath` в [`src/swagger.json`](src/swagger.json). Чтобы обновить клиент после изменения спецификации — запустите `npm run swagger`.

> ⚠️ `petstore.swagger.io` — общий демонстрационный сервер. Его база периодически очищается, а добавленные питомцы могут не сохраняться. Для продакшена нужен собственный бэкенд.
