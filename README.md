# Shortcut Roadmap

Карты навыков для менти [Shortcut Education](https://shortcut.education). Используются в личном кабинете для визуализации прогресса.

## Структура

```
tracks/
├── common/                    # Общие блоки (переиспользуются во всех треках)
│   ├── architecture.yaml      # SOLID, паттерны, REST, микросервисы, DDD
│   ├── cs-fundamentals.yaml   # Структуры данных, алгоритмы, сети, ОС
│   ├── databases.yaml         # SQL, транзакции, индексы, NoSQL, шардирование
│   ├── infra.yaml             # Git, Docker, CI/CD, Kubernetes, мониторинг
│   ├── messaging.yaml         # Kafka, RabbitMQ, async-паттерны
│   └── system-design.yaml     # CAP, балансировка, кеширование, проектирование
├── java-backend.yaml          # ☕ Java Backend Developer
├── go-backend.yaml            # 🐹 Go Backend Developer
└── python-backend.yaml        # 🐍 Python Backend Developer
```

## Формат YAML

### Языковой трек

```yaml
id: java-backend
title: Java Backend Developer
description: Карта навыков Java backend-разработчика
icon: "☕"
grades: [Intern, Junior, Junior+, Middle-, Middle, Middle+, Senior]

includes:                        # Ссылки на общие блоки
  - common/databases
  - common/system-design

categories:
  - id: java-core
    title: Java Core
    skills:
      - id: collections
        title: Collections Framework
        description: Внутреннее устройство HashMap, ArrayList, ...
        min_grade: Junior          # С какого грейда этот скилл нужен
        depends_on: [oop]          # Зависимости (для построения графа)
```

### Общий блок (`common/`)

```yaml
id: databases
title: Базы данных
icon: "🗄️"

skills:
  - id: sql-basics
    title: SQL
    min_grade: Junior
    depends_on: []
```

### Ссылки между файлами

`depends_on` поддерживает кросс-файловые ссылки:

```yaml
# Внутри того же файла
depends_on: [collections, oop]

# Ссылка на другую категорию в этом же треке
depends_on: [concurrency.concurrency-basics]

# Ссылка на общий блок
depends_on: [common/databases.sql-basics]
```

### Грейды

Скиллы привязаны к минимальному грейду через `min_grade`:

| Грейд | Описание |
|-------|----------|
| Intern | Начинающий, базовые знания |
| Junior | Может писать код под ревью |
| Junior+ | Самостоятельно решает типовые задачи |
| Middle- | Переходный, углублённые знания |
| Middle | Самостоятельный разработчик |
| Middle+ | Экспертиза в нескольких областях |
| Senior | Архитектурные решения, менторство |

## Как контрибьютить

1. Форкните репозиторий
2. Создайте ветку: `git checkout -b feature/add-kotlin-track`
3. Добавьте или измените YAML-файлы
4. Откройте Pull Request

### Что можно добавить

- Новые треки (Kotlin, Rust, Frontend, QA, TeamLead, ...)
- Новые скиллы в существующие треки
- Улучшение описаний
- Исправление зависимостей между скиллами

### Правила

- Один YAML-файл = один трек или один общий блок
- `id` скилла уникален в пределах категории
- `min_grade` — минимальный грейд, где скилл становится актуальным
- `depends_on` — только реальные зависимости (не «полезно знать», а «нужно для понимания»)
- Описания на русском языке
