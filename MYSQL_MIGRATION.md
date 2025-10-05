# Миграция на MySQL - Инструкция

## ✅ Что было сделано:

### 1. Установлены MySQL драйверы
- mysql-connector-python
- pymysql

### 2. Создана база данных MySQL
- Имя базы: `rescue_db`
- Хост: `127.0.0.1:3306`
- Пользователь: `root`
- Пароль: `55646504`

### 3. Созданы таблицы
- `users` - пользователи системы
- `sos_alerts` - экстренные вызовы
- `rescue_teams` - команды спасателей
- `notifications` - уведомления

### 4. Мигрированы данные
- ✅ 6 пользователей успешно перенесены
- Роли: admin, coordinator, operator, rescuer (3)
- Лидер команды: citizen@test.ru

### 5. Обновлена конфигурация
- `.env` файл обновлен на MySQL connection string
- `database.py` настроен для работы с MySQL
- `requirements.txt` добавлены MySQL драйверы

## 📋 Созданные скрипты:

### `create_mysql_database.py`
Создает базу данных и все таблицы в MySQL.
```bash
python create_mysql_database.py
```

### `migrate_sqlite_to_mysql.py`
Переносит данные из SQLite в MySQL.
```bash
python migrate_sqlite_to_mysql.py
```

### `check_mysql_db.py`
Проверяет содержимое MySQL базы данных.
```bash
python check_mysql_db.py
```

## 🚀 Как перезапустить систему:

### 1. Остановить бэкенд
В терминале бэкенда нажмите `Ctrl+C`

### 2. Очистить кеш Python
```powershell
Get-ChildItem -Path "backend/app" -Directory -Filter "__pycache__" -Recurse | Remove-Item -Recurse -Force
```

### 3. Запустить бэкенд заново
```powershell
cd backend
& venv\Scripts\Activate.ps1
python -m uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Или используйте:
```powershell
.\start-backend.ps1
```

## 🔍 Проверка работы:

### 1. Проверить подключение к MySQL
```bash
python check_mysql_db.py
```

### 2. Проверить API
```bash
curl http://localhost:8000/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@test.ru","password":"Test1234"}'
```

### 3. Проверить фронтенд
Откройте http://localhost:3001/

## ⚙️ Настройки подключения к MySQL:

В файле `.env`:
```env
DATABASE_URL=mysql+pymysql://root:55646504@127.0.0.1:3306/rescue_db
```

Формат: `mysql+pymysql://username:password@host:port/database`

## 📊 Текущее состояние БД:

```
USERS: 6
- admin@test.ru (admin)
- 123123@gmail.com (coordinator)
- operator@test.ru (operator)
- citizen@test.ru (rescuer, LEADER)
- newuser@test.ru (rescuer)
- rescuer@test.ru (rescuer)

SOS ALERTS: 0
RESCUE TEAMS: 0
NOTIFICATIONS: 0
```

## ❗ Важно:

1. Убедитесь, что MySQL сервер запущен
2. Проверьте, что порт 3306 доступен
3. Пароль в .env файле соответствует паролю MySQL
4. После изменения .env файла нужно перезапустить бэкенд

## 🛠️ Устранение проблем:

### Ошибка подключения к MySQL
```bash
# Проверить статус MySQL
mysql -u root -p55646504 -e "SELECT VERSION();"
```

### Ошибка "Access denied"
```bash
# Проверить пользователя и пароль
mysql -u root -p
```

### Таблицы не созданы
```bash
# Пересоздать таблицы
python create_mysql_database.py
```

## ✨ Преимущества MySQL:

1. ✅ Лучшая производительность для многопользовательских систем
2. ✅ Поддержка транзакций и блокировок
3. ✅ Масштабируемость
4. ✅ Надежность и безопасность
5. ✅ Поддержка репликации и кластеризации
