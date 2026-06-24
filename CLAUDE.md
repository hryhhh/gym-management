# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FitReserve is a gym management system with a Spring Boot backend and Vue 2 frontend (separated architecture). It supports two roles: admin and member, covering membership management, course booking, product purchasing, balance top-up, and expiration reminders.

## Key Commands

### Backend (Maven, Java 8)
- **Run**: `mvn spring-boot:run` — starts on `http://localhost:8080/gym`
- **Build**: `mvn clean package -DskipTests`
- **Test**: `mvn test` — note: `pom.xml` has `<skipTests>true</skipTests>` by default; override with `-DskipTests=false`

### Frontend (Vue 2, located at `src/main/resources/admin/admin/`)
- **Install deps**: `cd src/main/resources/admin/admin && npm install`
- **Run dev server**: `npm run serve`
- **Build**: `npm run build`
- **Lint**: `npm run lint`

## Architecture

### Backend — `src/main/java/com/`
Standard Spring Boot layered architecture:

- **`controller/`** — REST controllers handling HTTP requests (12 controllers covering all business modules)
- **`service/` + `service/impl/`** — business logic layer, one Service interface/impl pair per entity
- **`dao/`** — MyBatis Plus Mapper interfaces
- **`entity/`** — domain objects
  - `model/` — request parameter models
  - `view/` — view models for joined queries
  - `vo/` — value objects for responses
- **`utils/`** — shared utilities (FileUtil, BaiduUtil, MD5Util, HttpClientUtils, R for unified response wrapping, etc.)
- **`SpringbootSchemaApplication.java`** — main entry point with `@MapperScan("com.dao")`

MyBatis XML mappers live in `src/main/resources/mapper/` (one per entity).

### Frontend — `src/main/resources/admin/admin/src/`
- **`views/modules/`** — page components organized by business module (mirrors backend entities)
- **`router/`** — Vue Router configuration
- **`store/`** — Vuex state management
- **`components/`** — shared layout components (index, home, common, SvgIcon)
- **`utils/`** — axios wrappers, constants
- Uses Element UI for UI, ECharts for charts, vue-quill-editor for rich text, vue-amap for maps

### Configuration
- `src/main/resources/application.yml` — server port (8080), context-path (/gym), MySQL connection (database `gym4`), MyBatis Plus settings, file upload limits (300MB)
- Database: MySQL with utf8mb4, primary key strategy is user-input ID (`id-type: 1`)
- Auth: Apache Shiro 1.3.2 for role-based access control (admin vs member)

### Entity-Controller mapping (backend)
| Entity | Controller | Business |
|---|---|---|
| Huiyuan | HuiyuanController | Member management |
| Huiyuanleixing | HuiyuanleixingController | Card types |
| Huiyuanbanka | HuiyuanbankaController | Member cards |
| Huiyuanxuka | HuiyuanxukaController | Card renewal |
| Jiaolian | JiaolianController | Coach management |
| Jianshenkecheng | JianshenkechengController | Course management |
| Baomingkecheng | BaomingkechengController | Course enrollment |
| Jianshenshangpin | JianshenshangpinController | Product catalog |
| Goumaishangpin | GoumaishangpinController | Product purchases |
| Yuechongzhi | YuechongzhiController | Balance top-up |
| Daoqitixing | DaoqitixingController | Expiration reminders |
| Storeup | StoreupController | Favorites |
| News | NewsController | Announcements |
| Aboutus | AboutusController | About us |
| Systemintro | SystemintroController | System intro |
| Config | ConfigController | System config |
| Users | UsersController | Admin users |
