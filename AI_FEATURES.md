# 🤖 AI Функционал - Документация

## Обзор

Система интегрирует OpenAI GPT-4o для анализа чрезвычайных ситуаций с помощью текста, голоса и изображений.

## 🔑 API Ключ

**Новый ключ установлен:** `sk-proj-5UhNpl3Il5ZsypEIJr81...pe-hMA`

Файлы с ключом:
- `backend/app/core/config.py`
- `backend/.env`

## 📡 API Endpoints

### 1. Анализ текста `/api/v1/ai/analyze/text`

**Метод:** POST

**Запрос:**
```json
{
  "text": "Пожар в жилом доме на улице Ленина 15, видны языки пламени",
  "analysis_type": "classify"
}
```

**Ответ:**
```json
{
  "success": true,
  "analysis": {
    "type": "fire",
    "priority": 1,
    "severity": "critical",
    "keywords": ["пожар", "жилой дом", "пламя"],
    "confidence": 0.95,
    "estimated_victims": null,
    "location_hints": ["улица Ленина 15"],
    "required_resources": ["Пожарная бригада", "Медики"],
    "immediate_actions": ["Эвакуация жителей", "Тушение пожара"],
    "risk_assessment": "Высокий риск распространения"
  }
}
```

### 2. Анализ голоса `/api/v1/ai/analyze/voice`

**Метод:** POST

**Запрос:**
```json
{
  "audio_base64": "base64_encoded_audio_data",
  "language": "ru"
}
```

**Ответ:**
```json
{
  "success": true,
  "analysis": {
    "transcription": "Помогите! Человек упал в воду!",
    "emergency_type": "water_rescue",
    "priority": 1,
    "severity": "critical",
    "location_info": "не указано в записи",
    "victim_count": 1,
    "victim_condition": "в опасности",
    "caller_state": "паника",
    "hazards": ["Утопление", "Холодная вода"],
    "recommendations": ["Немедленно вызвать водных спасателей"],
    "confidence": 0.88
  }
}
```

### 3. Анализ изображения `/api/v1/ai/analyze/image`

**Метод:** POST

**Запрос:**
```json
{
  "image_base64": "base64_encoded_image_data",
  "emergency_type": "fire"
}
```

**Ответ:**
```json
{
  "success": true,
  "analysis": {
    "severity": "high",
    "description": "Пожар средней интенсивности в двухэтажном здании. Видны языки пламени из окон второго этажа, густой черный дым.",
    "hazards": ["Обрушение конструкций", "Задымление", "Высокая температура"],
    "recommendations": [
      "Эвакуировать соседние здания",
      "Установить водяные завесы",
      "Использовать дыхательные аппараты"
    ],
    "priority": 2,
    "confidence": 0.92,
    "estimated_victims": null,
    "required_resources": ["2 пожарных расчета", "Автолестница", "Скорая помощь"],
    "immediate_actions": ["Подача воды", "Эвакуация"],
    "accessibility": "средний",
    "weather_conditions": "ясно, безветренно",
    "time_sensitivity": "срочно"
  }
}
```

### 4. Генерация плана операции `/api/v1/ai/generate/rescue-plan`

**Метод:** POST

**Запрос:**
```json
{
  "emergency_type": "mountain_rescue",
  "description": "Турист сорвался на высоте 1500м, травма ноги",
  "location": "Гора Белуха, северный склон",
  "resources_available": ["Вертолет МИ-8", "Альпинисты-спасатели", "Медики"]
}
```

**Ответ:**
```json
{
  "success": true,
  "plan": {
    "operation_name": "Спасение на горе Белуха",
    "phases": [
      {
        "phase_number": 1,
        "phase_name": "Воздушная разведка",
        "duration_estimate": "20 минут",
        "actions": ["Вылет вертолета", "Поиск пострадавшего", "Оценка погоды"],
        "required_personnel": ["Пилот", "Штурман", "Наблюдатель"],
        "equipment_needed": ["Вертолет МИ-8", "Бинокли", "Радио"]
      },
      {
        "phase_number": 2,
        "phase_name": "Высадка спасателей",
        "duration_estimate": "30 минут",
        "actions": ["Поиск площадки", "Десантирование", "Подход к пострадавшему"],
        "required_personnel": ["2 альпиниста", "1 медик"],
        "equipment_needed": ["Страховка", "Носилки", "Медикаменты"]
      }
    ],
    "team_composition": {
      "team_leader": "Старший спасатель-альпинист",
      "members": ["Альпинист 1", "Альпинист 2", "Медик"],
      "specialists": ["Пилот вертолета"]
    },
    "safety_measures": [
      "Постоянная радиосвязь",
      "Страховка при спуске",
      "Мониторинг погоды"
    ],
    "estimated_duration": "2-3 часа",
    "success_criteria": ["Пострадавший эвакуирован", "Команда в безопасности"]
  }
}
```

### 5. Транскрибация аудио `/api/v1/ai/transcribe`

**Метод:** POST

**Запрос:**
```json
{
  "audio_base64": "base64_encoded_audio_data",
  "language": "ru"
}
```

**Ответ:**
```json
{
  "success": true,
  "transcription": "Здравствуйте, нужна помощь на улице Пушкина дом 20"
}
```

### 6. Тест сервисов `/api/v1/ai/test`

**Метод:** GET

**Ответ:**
```json
{
  "success": true,
  "services": {
    "text_analyzer": "available",
    "voice_assistant": "available",
    "image_analyzer": "available"
  },
  "models": {
    "text": "gpt-4o",
    "voice": "whisper-1 + gpt-4o",
    "image": "gpt-4o-vision"
  }
}
```

## 🔧 Улучшения

### 1. Анализ текста
- **Модель:** GPT-4o (последняя версия)
- **Новые поля:**
  - `severity` - уровень серьезности
  - `estimated_victims` - оценка количества пострадавших
  - `location_hints` - подсказки по местоположению
  - `required_resources` - необходимые ресурсы
  - `immediate_actions` - немедленные действия
  - `risk_assessment` - оценка рисков

### 2. Анализ изображений
- **Модель:** GPT-4o Vision (улучшенная)
- **Детальный анализ по типам ЧС:**
  - Пожары: размер, тип, интенсивность, дым
  - Медицина: травмы, состояние, срочность
  - Вода: количество людей, условия, опасности
  - Экология: тип загрязнения, масштаб
- **Новые поля:**
  - `accessibility` - доступность места
  - `weather_conditions` - погодные условия
  - `time_sensitivity` - временная критичность
  - `high detail` режим для лучшего качества

### 3. Анализ голоса
- **Модель:** Whisper-1 + GPT-4o
- **Расширенный анализ:**
  - `location_info` - информация о местоположении из речи
  - `victim_count` - количество пострадавших
  - `victim_condition` - состояние пострадавших
  - `caller_state` - эмоциональное состояние звонящего
  - `time_sensitive` - критичность по времени

### 4. Генерация плана операций (НОВОЕ!)
- Детальный план спасательной операции
- Разделение на фазы
- Состав команды
- Меры безопасности
- План связи и эвакуации
- Запасные планы

### 5. Анализ отчетов (НОВОЕ!)
- Извлечение ключевой информации
- Определение текущего статуса
- Анализ прогресса
- Выявление проблем
- Рекомендации следующих шагов

## 🧪 Тестирование

### Через Swagger UI
1. Откройте http://localhost:8000/docs
2. Найдите раздел **AI Analysis**
3. Протестируйте любой endpoint

### Через curl

**Тест текстового анализа:**
```bash
curl -X POST http://localhost:8000/api/v1/ai/analyze/text \
  -H "Content-Type: application/json" \
  -d '{"text": "Автомобильная авария на трассе М7, есть пострадавшие"}'
```

**Тест AI сервисов:**
```bash
curl http://localhost:8000/api/v1/ai/test
```

## 📊 Использование в системе

### Интеграция с алертами

AI можно использовать при создании вызова:

```python
# При создании алерта
ai_analysis = await text_analyzer.classify_emergency(alert.description)

# Автоматически определить тип и приоритет
alert.type = ai_analysis["type"]
alert.priority = ai_analysis["priority"]
```

### Помощь операторам

```python
# Оператор получает вызов с голосовым сообщением
analysis = await voice_assistant.analyze_emergency_audio(audio_data)

# Показать рекомендации оператору
show_recommendations(analysis["recommendations"])
show_required_resources(analysis["required_resources"])
```

### Анализ фото с места ЧС

```python
# Гражданин отправил фото
image_analysis = await image_analyzer.analyze_emergency_image(photo_base64, "fire")

# Автоматически оценить серьезность
update_alert_severity(alert_id, image_analysis["severity"])
send_recommendations_to_rescuers(image_analysis["recommendations"])
```

## 💡 Примеры использования

### Пример 1: Умный анализ при создании вызова

```javascript
// Frontend - при создании вызова
const description = "Пожар в доме, много дыма!";
const aiAnalysis = await fetch('/api/v1/ai/analyze/text', {
  method: 'POST',
  body: JSON.stringify({ text: description })
});

// Автоматически заполнить поля
alertForm.type = aiAnalysis.type;
alertForm.priority = aiAnalysis.priority;
alertForm.resources = aiAnalysis.required_resources;
```

### Пример 2: Генерация плана для координатора

```javascript
// Координатор выбирает алерт
const plan = await fetch('/api/v1/ai/generate/rescue-plan', {
  method: 'POST',
  body: JSON.stringify({
    emergency_type: alert.type,
    description: alert.description,
    location: alert.address,
    resources_available: team.available_resources
  })
});

// Показать детальный план
displayRescuePlan(plan);
```

## 🔐 Безопасность

- API ключ хранится в `.env` (не в git)
- Ключ не логируется в консоль
- Timeout для запросов: 30 секунд
- Обработка ошибок с fallback

## 📈 Метрики

Система отслеживает:
- Время ответа AI
- Использованную модель
- Confidence score
- Успешность запросов

## 🚀 Дальнейшее развитие

Планы:
1. Кэширование частых запросов
2. Мультиязычность (автоопределение)
3. Анализ видео в реальном времени
4. Предсказание развития ЧС
5. Обучение на собственных данных

---

**Статус:** ✅ Работает  
**Модели:** GPT-4o, Whisper-1, GPT-4o-Vision  
**API Версия:** v1  
**Дата обновления:** 05.10.2025
