# Bot_Vacanser
Telegramm bot for searching job on head hunter
# Описание проекта

Этот проект представляет собой автоматизированный workflow на платформе n8n, который:

Парсит вакансии с API HeadHunter по заданным критериям
Сохраняет вакансии в PostgreSQL базу данных
Анализирует соответствие кандидата требованиям вакансии с помощью AI (QWEN/QWQ-32B)
Отправляет уведомления в Telegram о подходящих вакансиях
# Особенности

Два параллельных потока для разных поисковых запросов:
Python-вакансии
Удаленные вакансии (n8n, Python, C#)
Интеграция с PostgreSQL для хранения данных
Использование AI для анализа соответствия кандидата
Telegram-уведомления с краткой аналитикой
Расписание запуска каждые 2 часа с 8:00 до 22:00
# Технические требования

n8n (self-hosted или cloud)
PostgreSQL
API ключ для QWEN/QWQ-32B (или другой совместимой модели)
Telegram бот с настроенным webhook
# Установка

Импортируйте workflow в ваш n8n (файл My workflow (3).json)
Настройте credentials для:
PostgreSQL
OpenAI API (QWEN/QWQ-32B)
Telegram бота
Настройте параметры поиска вакансий в узлах get_vacansies и get_vacansies1 при необходимости
Конфигурация

# Параметры поиска вакансий

Python-вакансии (узел get_vacansies):
Ключевые слова: "python"
Минимальная зарплата: 120,000 RUB
Регион: Москва (area: 1)
Удаленные вакансии (узел get_vacansies1):
Ключевые слова: "(n8n OR Python OR C#) AND (удалённо OR удаленно OR remote)"
Минимальная зарплата: 120,000 RUB
Регионы: основные IT-регионы России
Тип работы: удаленная (schedule: remote)
# Параметры кандидата

Настроены в узлах open_aI_requests и open_aI_requests1:

Опыт работы: 8 лет Python, 6 лет Django, 3 года FastAPI
Ключевые навыки: Python, Django, FastAPI, PostgreSQL, Docker и др.
Языки: русский (родной), английский (B2)
Образование: высшее техническое
# Структура базы данных

Проект предполагает наличие двух таблиц в PostgreSQL:

vacancies - хранит информацию о вакансиях:
id, name, description, alternate_url
employer_id, salary_from, salary_to, salary_currency
created_at, updated_at
employers - хранит информацию о работодателях:
id, name
