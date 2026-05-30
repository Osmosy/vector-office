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

## Источник

На базе [OfficeCLI](https://github.com/iOfficeAI/OfficeCLI) v1.0.102 — Apache 2.0, 5.4K+ звёзд.
