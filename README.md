# NEXA Messenger

Серверный MVP, веб-клиент и приложения для Windows/Android. Проект создан по ТЗ NEXA 3.0/5.0; часть расширенных функций ещё не реализована. Реальный статус: [STATUS.md](NEXA-Server/docs/STATUS.md).

| Папка | Назначение |
|---|---|
| [NEXA-Server](NEXA-Server) | NestJS, Socket.IO, PostgreSQL/Prisma, Redis, MinIO/S3, SMTP |
| [NEXA-Messenger](NEXA-Messenger) | Next.js/React, чаты, настройки, папки, Media Hub |
| [NEXA-Desktop](NEXA-Desktop) | Windows-клиент Electron |
| [NEXA-Android](NEXA-Android) | Android-клиент Java/WebView |

## Запуск на Windows

1. Скачайте **Code → Download ZIP** и распакуйте весь репозиторий.
2. Установите Node.js LTS 22+ и Docker Desktop. Запустите Docker в режиме Linux containers.
3. Откройте `NEXA-Messenger\INSTALL_NEXA.bat` — установит сайт и соседний сервер.
4. Следующие запуски: `D:\проэкты\NEXA-Messenger\START_NEXA.bat`.
5. Сайт: http://localhost:3000. Письма подтверждения для локального режима: http://localhost:8025.

Написание `D:\проэкты` сохранено намеренно. Непустой другой проект установщик не перезаписывает. Пользовательская база находится в Docker volumes; обновления используют миграции без сброса БД. Подробнее: [инструкция сервера](NEXA-Server/README.md).

## Получить приложения

Откройте [Actions → Build NEXA](../../actions/workflows/build.yml). После **успешной** сборки скачайте в разделе Artifacts:

- **NEXA-Windows-Installer** — Windows x64 EXE.
- **NEXA-Android-APK** — APK для личного тестирования, подписанный debug-ключом сборки.

Наличие workflow не означает, что сборка уже успешна: ориентируйтесь на статус запуска. Артефакты хранятся 14 дней; позже можно запустить workflow вручную. Debug-ключ на новом runner может отличаться; для стабильных Android-обновлений нужна отдельная настройка постоянного release-ключа. Windows code signing и публикация в магазинах не настроены.

Приложения открывают существующий интерфейс NEXA внутри Electron/WebView, используют общий сервер и аккаунты. Desktop: адрес `http://localhost:3000` при локальном сервере. Android: доступный HTTPS-сайт или debug USB с `adb reverse` (см. [инструкцию](NEXA-Android/README.md)). GitHub хранит код и собирает приложения, но **не запускает PostgreSQL/NestJS и не заменяет хостинг**.

## Статус проверки

Сервер и сайт ранее проходили сборку; 9 серверных/установочных тестов были успешны. Исторический отчёт: [VERIFICATION.md](NEXA-Server/docs/VERIFICATION.md). Desktop/Android исходники восстановлены из кода беседы перед загрузкой; текущую проверку выполняет CI. Проверка на реальных устройствах и многопользовательский тест с живыми сервисами всё ещё необходимы.

Нет сквозного шифрования, звонков, полноценных каналов, push, планировщика сообщений и ряда ULTRA-функций. Демо-пользователей нет. Секреты, базы, node_modules, APK/EXE и ZIP не включены в Git-историю. Для публичного сервера: [DEPLOY.md](NEXA-Server/docs/DEPLOY.md).
