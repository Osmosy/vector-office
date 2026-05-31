<div align="center">

<img src="assets/vector-logo.png" alt="Vector Office" width="200"/>

# Vector Office

**Офисный инструментарий для всех виртуальных работников Vector — Word, Excel, PowerPoint без офисного пакета**

[![Hermes Agent](https://img.shields.io/badge/Hermes-Agent-blue.svg)](https://github.com/NousResearch/hermes-agent)
[![Powered by OfficeCLI](https://img.shields.io/badge/Powered%20by-OfficeCLI-green.svg)](https://github.com/iOfficeAI/OfficeCLI)
[![Single binary: 32MB](https://img.shields.io/badge/Binary-32%20MB-orange.svg)](#установка)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-yellow.svg)](LICENSE)

</div>

---

Офисный слой экосистемы Vector. Единый бинарник (`officecli`, 32 МБ) — все виртуальные работники создают, читают и редактируют Word, Excel, PowerPoint через CLI. Без установки офисного пакета.

## Кто использует

| Проект | Кто | Для чего |
|--------|-----|---------|
| **Vector Marketing** | presentation | КП, отчёты, презентации (PPTX) |
| | analytics | Дашборды, сводки в Excel |
| | content | Статьи, документы (DOCX) |
| **Vector Legal** | Все домены | Договоры, иски, претензии (DOCX) |
| **Vector Work** | finance | Финансовые отчёты (XLSX) |
| | hr | Трудовые договоры, приказы (DOCX) |
| | ops | Инвойсы, спецификации (XLSX/DOCX) |
| **Vector Meat** | Бухгалтер | Накладные, отчётность (XLSX) |
| | Юрисконсульт | Договоры поставки (DOCX) |
| | Технолог | Техкарты, рецептуры (DOCX) |

## Установка

```bash
# Одна команда
curl -fsSL https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.sh | bash

# Или вручную
wget https://github.com/iOfficeAI/OfficeCLI/releases/latest/download/officecli-linux-x64
chmod +x officecli-linux-x64 && sudo mv officecli-linux-x64 /usr/local/bin/officecli
```

## Быстрый старт

```bash
# Создать презентацию
officecli create deck.pptx
officecli add deck.pptx /slides --type slide
officecli set deck.pptx "/slides/0" --title "Квартальный отчёт" --subtitle "Q2 2026"

# Смотреть live-превью в браузере
officecli watch deck.pptx
# → http://localhost:26315

# Создать Excel
officecli create report.xlsx
officecli set report.xlsx "/sheets/0" --name "Продажи"
officecli set report.xlsx "/sheets/0/0:1" --values '["Месяц","Выручка","Маржа"]'

# Прочитать Word
officecli get contract.docx /
```

## Возможности

| Формат | Создание | Чтение | Редактирование | Превью |
|--------|---------|--------|---------------|--------|
| **Word (.docx)** | ✅ | ✅ | ✅ | HTML/PNG |
| **Excel (.xlsx)** | ✅ | ✅ | ✅ | HTML/PNG |
| **PowerPoint (.pptx)** | ✅ | ✅ | ✅ | HTML/PNG |

## Интеграция с агентами

Каждый виртуальный работник Vector использует `officecli` через Hermes terminal tool:

```
Агент: "Создай квартальный отчёт в Excel"
→ terminal: officecli create report.xlsx
→ terminal: officecli set report.xlsx "/sheets/0" --name "Q2 Отчёт"
→ terminal: officecli set report.xlsx "/sheets/0/0:2" --values '["Месяц","Выручка"]'
→ результат: report.xlsx готов
```

## PDF-инструментарий: Stirling-PDF

Для работы с PDF в Vector Office используется [Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF) — self-hosted PDF-комбайн (40+ операций):

| Операция | Для чего |
|----------|----------|
| Объединить | Слияние договоров, актов, приложений в один документ |
| Разделить | Разбивка многостраничного PDF на отдельные файлы |
| Сжать | Уменьшение PDF для отправки по email (лучше чем iLovePDF) |
| Конвертировать | PDF → Word/Excel/PPTX и обратно |
| OCR | Распознавание сканов, факсов, фото документов |
| Водяной знак | Добавление грифов, пометок «копия», «черновик» |
| Подпись / штамп | Цифровая подпись, штампы «утверждено» |
| Сравнить | Diff двух PDF (договор v1 vs v2) |
| Санитизация | Удаление метаданных, скрытых слоёв перед отправкой |
| Редактор текста | Прямое редактирование текста в PDF |

### Установка

```bash
docker run -d --name stirling-pdf -p 8080:8080 \
  -v ~/stirling-pdf/data:/usr/share/tessdata \
  -v ~/stirling-pdf/configs:/configs \
  -v ~/stirling-pdf/logs:/logs \
  -e DOCKER_ENABLE_SECURITY=false \
  frooodle/s-pdf:latest
```

API доступен на `http://localhost:8080`. Все файлы обрабатываются локально.

### Интеграция с агентами

```
Агент: "Сожми договор и добавь водяной знак 'Копия'"
→ terminal: curl -X POST http://localhost:8080/api/v1/compress ...
→ terminal: curl -X POST http://localhost:8080/api/v1/add-watermark ...
→ результат: PDF обработан локально
```

## docker-compose

```yaml
# ~/projects/vector-office/docker-compose.yml
services:
  stirling-pdf:
    image: frooodle/s-pdf:latest
    container_name: stirling-pdf
    ports:
      - "8080:8080"
    volumes:
      - ~/stirling-pdf/data:/usr/share/tessdata
      - ~/stirling-pdf/configs:/configs
      - ~/stirling-pdf/logs:/logs
    environment:
      - DOCKER_ENABLE_SECURITY=false
      - SECURITY_ENABLE_LOGIN=false
```

## Источник

На базе [OfficeCLI](https://github.com/iOfficeAI/OfficeCLI) v1.0.102 — Apache 2.0, 5.4K+ звёзд. PDF — [Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF) — GPL v3, 50K+ звёзд.
