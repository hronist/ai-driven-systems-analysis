# Интенсив: AI-Augmented Systems Analysis for Developers

Этот курс предназначен для разработчиков, которые хотят прокачать навык системного и бизнес-анализа, используя ИИ как рычаг. Мы фокусируемся на поиске «темных пятен», коммуникации с заказчиком и генерации качественной документации.

## 🎯 Общая концепция
* **Срок:** 4 недели (6–8 часов в неделю).
* **Фокус:** Выявление скрытых требований, дизайн ТЗ, критический аудит.
* **Инструментарий:** Claude 3.5 Sonnet / GPT-4o, Mermaid.js, BDD/Gherkin.

---

## 📅 Программа обучения

### Неделя 1: Карта глубин и Поиск «темных пятен»
*   **Теория:** Бизнес-правила (Karl Wiegers), Context Diagrams, основы DDD (Bounded Contexts).
*   **Практика с ИИ:** Анализ верхнеуровневых «хотелок» на предмет логических дыр и скрытых правил.
*   **Результат:** Context Diagram (Mermaid) и список выявленных рисков.

### Неделя 2: Симулятор допроса (Сбор требований)
*   **Теория:** Методология "The Mom Test" (Роб Фитцпатрик), открытые вопросы, техники выявления (Elicitation).
*   **Практика с ИИ:** Ролевая игра, где ИИ — «капризный заказчик», а вы — аналитик.
*   **Результат:** Скрипт-опросник для реального стейкхолдера.

### Неделя 3: Проектирование и Промпт-инжиниринг ТЗ
*   **Теория:** Use Cases (Main, Alternate, Exception flows), Sequence Diagrams.
*   **Практика с ИИ:** Генерация детального ТЗ (Markdown) на основе ответов заказчика.
*   **Результат:** Готовое ТЗ с визуализацией логики в Mermaid.

### Неделя 4: Краш-тест и Валидация
*   **Теория:** Критерии качества требований, BDD (Behavior-Driven Development).
*   **Практика с ИИ:** ИИ в роли «параноидального QA» ищет слабые места в вашем ТЗ.
*   **Результат:** Acceptance Criteria в формате Gherkin и финальный аудит документа.

---

## 🔗 Ресурсы и ссылки (Top 10)

1.  **[Software Requirements Essentials](https://www.karlwiegers.com/books)** — Современная выжимка Карла Вигерса (2023). База анализа.
2.  **[The Mom Test (Роб Фитцпатрик)](https://momtestbook.com/)** — Как задавать вопросы, чтобы вам не врали.
3.  **[Mermaid.js Documentation](https://mermaid.js.org/syntax/sequenceDiagram.html)** — Гайд по созданию диаграмм через код.
4.  **[GitHub: business-analysis-skills](https://github.com/45ck/business-analysis-skills)** — Промпт-паки для бизнес-анализа.
5.  **[GitHub: BA-Kit](https://github.com/olbboy/BA-Kit)** — Агенты для Requirements Engineering.
6.  **[Cucumber: Gherkin Syntax](https://cucumber.io/docs/gherkin/reference/)** — Справочник по формату Given-When-Then.
7.  **[LinkedIn: Karl Wiegers - Core Practices](https://www.linkedin.com/pulse/6-more-core-requirements-practices-success-karl-wiegers/)** — Статья о ключевых практиках в ИТ-аналитике.
8.  **[AI Hero: AGENTS.md Guide](https://www.aihero.dev/)** — Оптимизация инструкций для ИИ-агентов.
9.  **[Prompting Guide (OpenAI Codex)](https://platform.openai.com/docs/guides/prompt-engineering)** — Как эффективно работать с моделями при написании кода и документации.
10. **[DDDesign Reference](https://domainlanguage.com/ddd/reference/)** — Краткий справочник по DDD от Эрика Эванса.

---

## 🤖 МАСТЕР-ПРОМПТ ДЛЯ ЗАПУСКА КУРСА
*Скопируйте этот текст в Claude 3.5 Sonnet или GPT-4o:*

```text
Act as an expert IT Systems Analysis Mentor. We are executing a 4-week intensive program "AI-Augmented Systems Analysis for Developers". I am an experienced developer, so skip SQL, APIs, and basic tech architecture. Focus purely on Elicitation, Finding Blind Spots, Spec Writing, and Document Auditing.

Please provide a detailed, day-by-day breakdown for [CHOOSE WEEK: Week 1 / Week 2 / Week 3 / Week 4]. 

For the chosen week, include:
1. Short theoretical reading points based on Karl Wiegers' and Rob Fitzpatrick's methodologies.
2. A specific "AI Co-Pilot Exercise" prompt that I can copy-paste to use you as a tool (e.g., role-play simulator or spec generator).
3. A concrete Deliverable (e.g., Markdown template, Mermaid script) I must produce by the end of the week.

Let's begin. What is my pet project theme? Ask me briefly, then generate the guide for Week 1.
```
