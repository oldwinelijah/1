# CHANGELOG - Мессенджер

## Iterations History

### Iteration 1 (2026-05-08)
- Добавлена детализация задач с описанием подзадач
- Добавлены спринты дляbacklog задач
- Добавлены статусы DONE/TODO/CANCELED

### Iteration 2 (2026-05-08)
- Добавлена категоризация по типам приложений (Mobile/Web/Desktop/Core)
- Добавлены зависимости между задачами
- Разбивка на major/minor/trace задачи

### Iteration 3 (2026-05-08)
- Добавлен estimated effort в часах
- Добавлены приоритеты P0/P1/P2/P3
- Добавлены метки компонентов

---

## v0.1.0 - Prototype (Спринт 1-2)

### Sprint 1: Backend Core
**Цель**: Развернуть серверную инфраструктуру, аутентификацию и базовые сообщения

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T001 | Backend | Настройка проекта и CI/CD | DONE | Инициализация repo, GitHub Actions, Docker, Makefile | - | 16h | P0 | infra |
| T002 | Backend | PostgreSQL схема | DONE | Таблицы: users, sessions, dialogs, messages, индексы, FK | T001 | 12h | P0 | db |
| T003 | Backend | Redis кэш | DONE | Сессии, presence, кластер конфиг | T001 | 8h | P0 | db |
| T004 | Auth | Регистрация (phone) | DONE | POST /auth/register, валидация E.164, bcrypt | T002 | 8h | P0 | backend |
| T005 | Auth | SMS верификация | DONE | 6-digit код, TTL 5min, 3 попытки, SMS провайдер | T004 | 8h | P0 | backend |
| T006 | Auth | Логин по паролю | POST | /auth/login, device logging, сессии | T005 | 4h | P0 | backend |
| T007 | Auth | JWT токены | DONE | Access 15min, Refresh 30d, инвалидация | T006 | 8h | P0 | backend |
| T008 | Core | NGINX Gateway | DONE | Маршрутизация, SSL, rate limiting | T001 | 6h | P0 | infra |
| T009 | Message | Отправка сообщений | DONE | POST /messages/send, валидация, sanitize | T002 | 8h | P0 | backend |
| T010 | Message | История сообщений | DONE | GET /history, пагинация, soft delete | T010 | 6h | P0 | backend |

### Sprint 2: Client Core
**Цель**: Базовые клиенты для Android, iOS, Web

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T011 | Mobile | Android архитектура | TODO | Kotlin, MVVM, Hilt, Retrofit, Coroutines | T010 | 24h | P0 | mobile |
| T012 | Mobile | iOS архитектура | TODO | Swift, UIKit, MVP, Alamofire, Combine | T010 | 24h | P0 | mobile |
| T013 | Mobile | Экран: Список чатов | TODO | RecyclerView, FAB, pull-refresh, nav | T011 | 12h | P0 | mobile |
| T014 | Mobile | Экран: История | TODO | Chat list, date separators, load-more | T013 | 12h | P0 | mobile |
| T015 | Mobile | Отправка (UI) | TODO | Input field, send button, emoji | T014 | 8h | P0 | mobile |
| T016 | Web | React архитектура | TODO | React 18, TS, Vite, Router, Context | T010 | 20h | P0 | web |
| T017 | Web | Список чатов | TODO | Sidebar, search, badges, click | T016 | 10h | P0 | web |
| T018 | Web | История сообщений | TODO | Message list, input, scroll | T017 | 10h | P0 | web |
| T019 | Web | Login форма | TODO | Phone, password, validation | T016 | 6h | P0 | web |
| T020 | Core | WebSocket клиент | TODO | Socket.io, reconnect, heartbeat | T010 | 10h | P0 | core |

---

## v0.2.0 - Enhanced Messaging (Спринт 3-4)

### Sprint 3: Messaging Features
**Цель**: Расширенный функционал сообщений

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T021 | Message | Редактирование | TODO | PATCH /messages/{id}, edited_at | T010 | 4h | P1 | backend |
| T022 | Message | Удаление (мягкое) | TODO | DELETE, is_deleted flag | T010 | 4h | P1 | backend |
| T023 | Message | Статусы | TODO | sent/delivered/read, update via WS | T010 | 8h | P1 | backend |
| T024 | Message | "Печатает..." | TODO | typing_start/stop events, debounce | T020 | 6h | P1 | backend |
| T025 | Message | Реакции | TODO | Emoji reactions, upsert, list | T010 | 8h | P1 | backend |
| T026 | Message | Пересылка | TODO | forward_message, copy with ref | T010 | 4h | P1 | backend |
| T027 | Core | WS уведомления | TODO | Real-time updates, event dispatch | T020 | 8h | P0 | core |
| T028 | Dialog | Личные чаты | TODO | CREATE dialog type=private | T010 | 4h | P1 | backend |
| T029 | Dialog | Список диалогов | TODO | GET /dialogs, сортировка, unread | T010 | 6h | P1 | backend |
| T030 | Dialog | Закрепление | TODO | Pin/unpin, pinned_top flag | T029 | 4h | P2 | backend |

### Sprint 4: Groups
**Цель**: Групповые чаты

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T031 | Group | Создание групп | TODO | CREATE dialog type=group, title, members | T033 | 8h | P1 | backend |
| T032 | Group | Инвайт ссылка | TODO | invite_link, /groups/join/{link} | T031 | 4h | P1 | backend |
| T033 | Group | Покинуть группу | TODO | leave_group, cleanup | T031 | 4h | P1 | backend |
| T034 | Group | Приглашение | TODO | invite_user, notifications | T031 | 4h | P1 | backend |
| T035 | Group | Удаление участника | TODO | remove_user (admin only) | T031 | 4h | P1 | backend |
| T036 | Group | Админы | TODO | set_admin, permissions | T031 | 6h | P1 | backend |
| T037 | Group | Название | TODO | update_title (admin/member) | T031 | 3h | P2 | backend |
| T038 | Group | Аватар | TODO | group_avatar upload | T031 | 4h | P2 | backend |
| T039 | Group | Инфо | TODO | get_info, invite_code | T031 | 2h | P2 | backend |
| T040 | Group | Участники | TODO | get_members, pagination | T031 | 4h | P1 | backend |

---

## v0.3.0 - Media & Contacts (Спринт 5-6)

### Sprint 5: Media
**Цель**: Загрузка и передача файлов

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T041 | Media | Загрузка (S3) | TODO | POST /media/upload, multipart, limits | T010 | 10h | P1 | backend |
| T042 | Media | Скачивание | TODO | GET /media/{id}, stream | T041 | 4h | P1 | backend |
| T043 | Media | Превью | TODO | Image preview generation, thumb | T041 | 6h | P1 | backend |
| T044 | Media | Сжатие | TODO | Image compression, WebP/AVIF | T041 | 8h | P2 | backend |
| T045 | Media | Pre-signed URLs | TODO | download_url, expires=1h | T042 | 4h | P1 | backend |
| T046 | Message | Файлы в чате | TODO | attachment field, file message | T041 | 6h | P1 | backend |
| T047 | Message | Голосовые | TODO | Voice message, record, upload | T041 | 10h | P1 | backend |
| T048 | Message | Видео | TODO | Video message, thumb generation | T041 | 10h | P1 | backend |
| T049 | Message | Геолокация | TODO | Location message, coordinates | T010 | 6h | P2 | backend |
| T050 | Message | Контакты | TODO | Contact card, vCard | T010 | 4h | P2 | backend |

### Sprint 6: Contacts
**Цель**: Контакт-лист и профили

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T051 | Contact | Поиск | TODO | GET /users/search, name/phone | T010 | 6h | P1 | backend |
| T052 | Contact | Добавить | TODO | POST /contacts/add | T051 | 4h | P1 | backend |
| T053 | Contact | Удалить | TODO | DELETE /contacts/{user_id} | T052 | 2h | P1 | backend |
| T054 | Contact | Список | TODO | GET /contacts | T052 | 4h | P1 | backend |
| T055 | Contact | Блокировка | TODO | POST /contacts/block | T054 | 4h | P1 | backend |
| T056 | Contact | Разблокировка | TODO | POST /contacts/unblock | T055 | 2h | P1 | backend |
| T057 | Contact | Черный список | TODO | GET /contacts/blocked | T055 | 3h | P2 | backend |
| T058 | Contact | Синхронизация | TODO | Phonebook sync, detect contacts | T010 | 10h | P2 | backend |
| T059 | Profile | Профиль | TODO | GET /profile, user data | T010 | 4h | P1 | backend |
| T060 | Profile | Чужой профиль | TODO | GET /users/{id}, public info | T059 | 3h | P1 | backend |

---

## v0.4.0 - Profile & Settings (Спринт 7-8)

### Sprint 7: Profile Features
**Цель**: Управление профилем и настройками

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T061 | Profile | Редактирование | TODO | PATCH /profile, name/bio | T059 | 4h | P1 | backend |
| T062 | Profile | Аватар | TODO | POST /profile/avatar, upload | T061 | 6h | P1 | backend |
| T063 | Profile | Удалить аватар | TODO | DELETE /profile/avatar | T062 | 2h | P2 | backend |
| T064 | Profile | Bio/статус | TODO | Status text, about | T061 | 3h | P2 | backend |
| T065 | Profile | Приватность | TODO | PATCH /profile/privacy | T061 | 8h | P1 | backend |
| T066 | Profile | Видимость онлайн | TODO | last_seen visibility | T065 | 4h | P2 | backend |
| T067 | Profile | Видимость фото | TODO | photo visibility options | T065 | 4h | P2 | backend |
| T068 | Profile | Видимость входа | TODO | last_seen settings | T065 | 4h | P2 | backend |
| T069 | Profile | Уведомления | TODO | PATCH /profile/notifications | T061 | 6h | P1 | backend |
| T070 | Profile | Темы | TODO | Dark/light mode settings | T012/T016 | 8h | P2 | mobile/web |

### Sprint 8: Security
**Цель**: Безопасность аккаунта

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T071 | Security | Смена пароля | TODO | POST /auth/password/change | T007 | 4h | P1 | backend |
| T072 | Security | 2FA SMS | TODO | POST /auth/2fa/enable, verify | T071 | 10h | P1 | backend |
| T073 | Security | Восстановление | TODO | POST /auth/password/reset | T071 | 8h | P1 | backend |
| T074 | Security | Сессии | TODO | GET /profile/sessions, list | T010 | 4h | P1 | backend |
| T075 | Security | Завершение сессий | TODO | DELETE /sessions/{id} | T074 | 3h | P1 | backend |
| T076 | Security | Логи | TODO | Event logging, audit | T010 | 6h | P1 | backend |
| T077 | Security | Rate limiting | TODO | Per-user, per-IP limits | T008 | 6h | P1 | infra |
| T078 | Security | Валидация | TODO | Input sanitization, XSS | T010 | 6h | P0 | backend |
| T079 | Security | SQL инъекции | TODO | Parameterized queries | T002 | 4h | P0 | backend |
| T080 | Security | CSRF | TODO | CSRF tokens for forms | T016 | 4h | P1 | web |

---

## v0.5.0 - Advanced Features (Спринт 9-10)

### Sprint 9: Advanced Messaging
**Цель**: Продвинутый функционал сообщений

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T081 | Message | Игнорирование | TODO | Mute dialog, no notifications | T069 | 4h | P2 | backend |
| T082 | Message | Поиск в чате | TODO | Full-text search in dialog | T010 | 8h | P2 | backend |
| T083 | Message | Пагинация | TODO | Cursor-based pagination | T010 | 4h | P1 | backend |
| T084 | Message | Медиа-галерея | TODO | Media gallery in dialog | T084 | 6h | P2 | backend |
| T085 | Message | pinned message | TODO | Dialog pinned message | T010 | 4h | P2 | backend |
| T086 | Message | Непрочитанные | TODO | Unread counters, badges | T010 | 4h | P1 | backend |
| T087 | Message | Архив | TODO | Archive dialogs | T010 | 6h | P2 | backend |
| T088 | Message | Удаление чата | TODO | Delete dialog, hard | T010 | 4h | P2 | backend |
| T089 | Message | Эмодзи-паки | TODO | Unicode emoji support | T010 | 6h | P2 | backend |
| T090 | Message | Стикеры | TODO | Sticker packs, send | T089 | 10h | P2 | backend |

### Sprint 10: Push Notifications
**Цель**: Push-уведомления на всех платформах

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T091 | Push | FCM Android | TODO | Firebase Cloud Messaging | T011 | 10h | P1 | mobile |
| T092 | Push | APNS iOS | TODO | Apple Push Notification | T012 | 10h | P1 | mobile |
| T093 | Push | Web Push | TODO | Chrome notifications | T016 | 10h | P2 | web |
| T094 | Push | Регистрация | TODO | POST /notifications/register | T091 | 4h | P1 | backend |
| T095 | Push | Удаление токена | TODO | DELETE /notifications/{token} | T094 | 2h | P1 | backend |
| T096 | Push | Open handling | TODO | Deep linking on tap | T091 | 4h | P1 | mobile |
| T097 | Push | Тихие | TODO | Silent pushes, background | T091 | 6h | P2 | mobile |
| T098 | Push | Звуки | TODO | Custom notification sounds | T094 | 4h | P2 | mobile |
| T099 | Push | Группировка | TODO | Notification grouping | T094 | 6h | P2 | mobile |
| T100 | Push | Отложенные | TODO | Scheduled notifications | T100 | 8h | P3 | mobile |

---

## v0.6.0 - Desktop & Web Enhanced (Спринт 11-12)

### Sprint 11: Desktop App
**Цель**: Нативные десктопные приложения

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T101 | Desktop | Electron | TODO | Electron app wrapper | T010 | 16h | P1 | desktop |
| T102 | Desktop | OAuth | TODO | Login window | T101 | 6h | P1 | desktop |
| T103 | Desktop | Main window | TODO | Chats list window | T101 | 10h | P1 | desktop |
| T104 | Desktop | Messages | TODO | Chat window | T103 | 10h | P1 | desktop |
| T105 | Desktop | Tray | TODO | System tray, menu | T101 | 6h | P1 | desktop |
| T106 | Desktop | Native notif | TODO | Windows notifications | T105 | 6h | P1 | desktop |
| T107 | Desktop | Hotkeys | TODO | Global shortcuts | T101 | 4h | P2 | desktop |
| T108 | Desktop | C++ Windows | TODO | Native Windows client | T010 | 40h | P3 | desktop |
| T109 | Desktop | Linux | TODO | GTK/Qt Linux client | T010 | 30h | P3 | desktop |
| T110 | Desktop | macOS | TODO | AppKit client | T010 | 30h | P3 | desktop |

### Sprint 12: Web Enhanced
**Цель**: Продвинутый Web-клиент

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T111 | Web | PWA | TODO | Progressive Web App | T016 | 12h | P2 | web |
| T112 | Web | ServiceWorker | TODO | Offline support | T111 | 8h | P2 | web |
| T113 | Web | Offline mode | TODO | Queue messages offline | T112 | 10h | P2 | web |
| T114 | Web | Push Web | TODO | Web push notifications | T113 | 10h | P2 | web |
| T115 | Web | Profile | TODO | Profile editing | T016 | 6h | P2 | web |
| T116 | Web | Groups | TODO | Create/manage groups | T016 | 10h | P2 | web |
| T117 | Web | Drag&Drop | TODO | File upload drag-drop | T016 | 6h | P2 | web |
| T118 | Web | Link preview | TODO | OG metadata fetch | T010 | 10h | P2 | web |
| T119 | Web | Bundle optimization | TODO | Code splitting | T016 | 8h | P2 | web |
| T120 | Web | SSR | TODO | Server render | T016 | 16h | P2 | web |

---

## v0.7.0 - Scalability & Performance (Спринт 13-14)

### Sprint 13: Performance
**Цель**: Оптимизация производительности

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T121 | Perf | Redis caching | TODO | Cache queries | T003 | 10h | P1 | backend |
| T122 | Perf | DB queries | TODO | Query optimization | T002 | 10h | P1 | db |
| T123 | Perf | Индексы | TODO | PostgreSQL indexes | T002 | 8h | P1 | db |
| T124 | Perf | Connection pool | TODO | PgBouncer setup | T002 | 6h | P1 | infra |
| T125 | Perf | CDN | TODO | CloudFront for media | T041 | 10h | P1 | infra |
| T126 | Perf | Gzip | TODO | Response compression | T008 | 4h | P1 | infra |
| T127 | Perf | Cache profiles | TODO | User profile cache | T121 | 6h | P1 | backend |
| T128 | Perf | Cache dialogs | TODO | Dialog list cache | T121 | 6h | P1 | backend |
| T129 | Perf | Batched load | TODO | Batch message loading | T010 | 8h | P1 | backend |
| T130 | Perf | Binary protocol | TODO | Binary message format | T010 | 20h | P2 | backend |

### Sprint 14: Scaling
**Цель**: Горизонтальное масштабирование

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T131 | Scale | Horiz scaling | TODO | Multiple instances | T001 | 16h | P1 | infra |
| T132 | Scale | Kubernetes | TODO | K8s deployment | T131 | 20h | P1 | infra |
| T133 | Scale | Auto-scaling | TODO | HPA rules | T132 | 10h | P1 | infra |
| T134 | Scale | Load balancing | TODO | Ingress, routes | T131 | 8h | P1 | infra |
| T135 | Scale | DB replication | TODO | Read replicas | T002 | 12h | P1 | db |
| T136 | Scale | Sharding | TODO | Data partitioning | T135 | 30h | P2 | db |
| T137 | Scale | Kafka cluster | TODO | Message queue cluster | T010 | 16h | P1 | infra |
| T138 | Scale | Redis cluster | TODO | Cluster mode | T003 | 10h | P1 | db |
| T139 | Scale | Prometheus | TODO | monitoring metrics | T001 | 10h | P1 | infra |
| T140 | Scale | ELK | TODO | centralized logging | T001 | 10h | P1 | infra |

---

## v0.8.0 - E2E Encryption (Спринт 15-16)

### Sprint 15: Security Advanced
**Цель**: Сквозное шифрование

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T141 | Security | Signal Protocol | TODO | E2E encryption | T007 | 30h | P1 | backend |
| T142 | Security | Key generation | TODO | X25519, Ed25519 keys | T141 | 10h | P1 | backend |
| T143 | Security | Key exchange | TODO | DH, prekey bundle | T142 | 10h | P1 | backend |
| T144 | Security | Double Ratchet | TODO | Ratcheting algorithm | T143 | 15h | P1 | backend |
| T145 | Security | Forward secrecy | TODO | Future secrecy | T144 | 8h | P1 | backend |
| T146 | Security | Media encryption | TODO | Encrypt media files | T041 | 10h | P1 | backend |
| T147 | Security | Device verify | TODO | Device fingerprinting | T074 | 6h | P2 | backend |
| T148 | Security | QR verify | TODO | QR code verification | T147 | 8h | P2 | backend |
| T149 | Security | Trust contacts | TODO | Verified contacts | T148 | 6h | P2 | backend |
| T150 | Security | Key check | TODO | Key fingerprint check | T149 | 4h | P2 | backend |

### Sprint 16: Privacy
**Цель**: Приватные функции

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T151 | Privacy | Secret chats | TODO | E2E-only chats | T150 | 15h | P1 | backend |
| T152 | Privacy | Timer | TODO | Message timer | T151 | 8h | P1 | backend |
| T153 | Privacy | Self-destruct | TODO | Auto-delete messages | T152 | 8h | P1 | backend |
| T154 | Privacy | Anonymous group | TODO | Hidden membership | T031 | 10h | P2 | backend |
| T155 | Privacy | Incognito mode | TODO | No read receipts | T065 | 6h | P2 | backend |
| T156 | Privacy | Hidden chats | TODO | Hidden chat list | T010 | 8h | P2 | backend |
| T157 | Privacy | App PIN | TODO | Application lock | T010 | 6h | P2 | mobile |
| T158 | Privacy | Biometrics | TODO | Fingerprint/FaceID | T157 | 6h | P2 | mobile |
| T159 | Privacy | Stealth mode | TODO | Hidden online status | T065 | 6h | P3 | mobile |
| T160 | Privacy | Destructive | TODO | No-copy delete | T160 | 8h | P3 | backend |

---

## v0.9.0 - Bot API & Extensions (Спринт 17-18)

### Sprint 17: Bot API
**Цель**: Платформа для ботов

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T161 | Bot | Bot платформа | TODO | Bot infrastructure | T010 | 20h | P1 | backend |
| T162 | Bot | Create bots | TODO | Bot registration | T161 | 8h | P1 | backend |
| T163 | Bot | Bot tokens | TODO | Bot authentication | T162 | 4h | P1 | backend |
| T164 | Bot | Webhook | TODO | HTTPS webhook endpoint | T161 | 10h | P1 | backend |
| T165 | Bot | Long polling | TODO | getUpdates API | T161 | 8h | P1 | backend |
| T166 | Bot | Inline keyboard | TODO | Inline keyboard markup | T164 | 6h | P1 | backend |
| T167 | Bot | Action buttons | TODO | Callback buttons | T166 | 6h | P1 | backend |
| T168 | Bot | Keyboard API | TODO | Reply keyboard | T166 | 6h | P1 | backend |
| T169 | Bot | Callback queries | TODO | Handle callbacks | T167 | 6h | P1 | backend |
| T170 | Bot | Deep linking | TODO | Bot start params | T162 | 6h | P2 | backend |

### Sprint 18: Extensions
**Цель**: Расширения платформы

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T171 | Ext | Android plugins | TODO | Plugin system | T011 | 20h | P2 | mobile |
| T172 | Ext | Custom stickers | TODO | User sticker packs | T090 | 10h | P2 | backend |
| T173 | Ext | Themes | TODO | Theme system | T070 | 15h | P2 | mobile/web |
| T174 | Ext | Language packs | TODO | i18n system | T016 | 10h | P1 | mobile/web |
| T175 | Ext | Translator | TODO | Built-in translate | T174 | 15h | P2 | backend |
| T176 | Ext | Voice input | TODO | Speech-to-text | T015 | 10h | P2 | mobile |
| T177 | Ext | QR scanner | TODO | Scan QR codes | T011 | 8h | P2 | mobile |
| T178 | Ext | QR generator | TODO | Create QR codes | T177 | 6h | P2 | backend |
| T179 | MiniApp | Mini Apps | TODO | Platform for apps | T010 | 25h | P2 | backend |
| T180 | MiniApp | Payments | TODO | Payment integration | T179 | 20h | P2 | backend |

---

## v1.0.0 - Release (Спринт 19-20)

### Sprint 19: Final Features
**Цель**: Финальный функционал перед релизом

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T181 | Feature | VoIP audio | TODO | Audio_calls | T010 | 30h | P1 | backend |
| T182 | Feature | Video calls | TODO | Video calling | T181 | 30h | P1 | backend |
| T183 | Feature | Group video | TODO | Conference calling | T182 | 25h | P1 | backend |
| T184 | Feature | Screen share | TODO | Screen sharing | T183 | 15h | P1 | backend |
| T185 | Feature | Call recording | TODO | Record calls | T184 | 10h | P2 | backend |
| T186 | Feature | Live streaming | TODO | Broadcast to group | T031 | 25h | P2 | backend |
| T187 | Feature | Каналы | TODO | Broadcast channels | T010 | 20h | P2 | backend |
| T188 | Feature | Подписчики | TODO | Channel subscribers | T187 | 10h | P2 | backend |
| T189 | Feature | Рассылки | TODO | Bulk messaging | T188 | 15h | P2 | backend |
| T190 | Feature | TPayments | TODO | In-chat payments | T190 | 30h | P2 | backend |

### Sprint 20: Release Prep
**Цель**: Подготовка к публичному релизу

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T191 | Release | Alpha | TODO | Internal testing | T010 | 20h | P0 | qa |
| T192 | Release | Beta | TODO | External beta | T191 | 15h | P0 | qa |
| T193 | Release | QA | TODO | Full test cycle | T192 | 30h | P0 | qa |
| T194 | Release | Security audit | TODO | Penetration testing | T193 | 20h | P0 | qa |
| T195 | Release | Bug fixing | TODO | Fix critical bugs | T194 | 20h | P0 | backend |
| T196 | Release | API docs | TODO | OpenAPI/Swagger | T010 | 15h | P1 | docs |
| T197 | Release | Dev docs | TODO | Developer docs | T196 | 15h | P1 | docs |
| T198 | Release | App Store | TODO | iOS submission | T012 | 10h | P1 | mobile |
| T199 | Release | Google Play | TODO | Android submission | T011 | 10h | P1 | mobile |
| T200 | Release | Public release | TODO | GA release | T199 | 8h | P0 | release |

---

## v1.1.0+ - Future (Backlog)

| ID | Категория | Задача | Статус |_detailed |_dep |_effort |_prio |_comp |
|----|------------|--------|--------|-----------|-----------|------|--------|------|------|
| T201 | Future | Collab editing | CANCELED | Google Docs-like | T010 | 40h | P3 | - |
| T202 | Future | Calendar | CANCELED | Calendar integration | T010 | 25h | P3 | - |
| T203 | Future | Email client | CANCELED | Built-in email | T010 | 50h | P3 | - |
| T204 | Future | Mesh networking | CANCELED | P2P connections | T010 | 40h | P3 | - |
| T205 | Future | Decentralized | CANCELED | Federation | T204 | 50h | P3 | - |
| T206 | Future | NFT badges | CANCELED | Profile NFTs | T059 | 20h | P3 | - |
| T207 | Future | Crypto wallet | CANCELED | Wallet integration | T190 | 30h | P3 | - |
| T208 | Future | DAO | CANCELED | Group governance | T031 | 30h | P3 | - |
| T209 | Future | AR filters | CANCELED | Camera filters | T012 | 25h | P3 | - |
| T210 | Future | Metaverse | CANCELED | 3D spaces | T209 | 50h | P3 | - |

---

## Легенда колонок (Iteration 3)

- **ID**: Уникальный идентификатор задачи
- **Категория**: Область функционала
- **Задача**: Название задачи
- **Статус**: DONE/TODO/CANCELED
- **_detailed**: Детальное описание подзадач
- **_dep**: ID задачи-зависимости
- **_effort**: Estimated effort в часах
- **_prio**: P0 (критично), P1 (высокий), P2 (средний), P3 (низкий)
- **_comp**: Компонент: backend/mobile/web/desktop/core/infra/db/qa/release/docs
