# Инструкция по использованию промпта

## Структура промпта

Этот промпт может быть адаптирован под различные задачи, при этом поля **rules**, **explicit_reminder** и **evaluation_rubric** сохраняются между контекстами и не изменяются. Остальные поля настраиваются в зависимости от задачи.

### Поля, которые меняются:

#### 1. `prompt`
- **Описание**: Основное поле, которое формулирует задание или запрос. Оно меняется в зависимости от контекста задачи.
- **Пример**:
    ```json
    {
      "prompt": "Develop a detailed Software Design Document aligned with the user's business needs."
    }
    ```
- **Другие примеры**:
    ```json
    {
      "prompt": "Create a marketing strategy plan to enhance customer engagement."
    }
    ```

#### 2. `role`
- **Описание**: Роль, которую принимает ChatGPT для выполнения задачи. Обычно это профиль специалиста, требуемого для решения задачи.
- **Пример**:
    ```json
    {
      "role": "expert level software-engineer"
    }
    ```
- **Другие примеры**:
    ```json
    {
      "role": "senior marketing consultant"
    }
    ```

#### 3. `department`
- **Описание**: Определяет подразделение или профессиональную сферу, в рамках которой решается задача.
- **Пример**:
    ```json
    {
      "department": "engineering"
    }
    ```
- **Другие примеры**:
    ```json
    {
      "department": "marketing"
    }
    ```

#### 4. `task`
- **Описание**: Четко описывает, какую задачу необходимо решить. Это всегда зависит от контекста запроса.
- **Пример**:
    ```json
    {
      "task": "Create a Software Design Document"
    }
    ```
- **Другие примеры**:
    ```json
    {
      "task": "Develop a social media content plan for a new product launch"
    }
    ```

#### 5. `task_description`
- **Описание**: Детализирует задачу и конкретизирует требования к выполнению. Описывает, как должен выглядеть конечный результат.
- **Пример**:
    ```json
    {
      "task_description": "As an expert level software engineer in the engineering department, your task is to create a Software Design Document that achieves core benefits for the user."
    }
    ```

---

### Постоянные элементы промпта:

#### 1. `rules`
- **Описание**: Набор правил, которые должны строго соблюдаться при каждом выполнении задачи.
- **Пример**:
    ```json
    "rules": {
        "rule_1": "Initial Message: 👋 I'm Larsen, your {role} AI. Let's design the ideal {end goal} collaboratively.",
        "rule_2": "Ask up to 5 pertinent questions to gather essential information for the task.",
        "rule_3": "Take a deep breath. Think about your task step by step."
        // остальные правила...
    }
    ```

#### 2. `key_references`
- **Описание**: Содержит список источников, которые могут помочь при решении задачи. Может быть пустым, если нет необходимости в дополнительных ресурсах.
- **Пример**:
    ```json
    "key_references": {
        "key_reference_1_title": "Software Architecture in Practice",
        "key_reference_1_author": "Len Bass",
        "key_reference_1_year": "2012",
        "key_reference_1_keyinsights": [
            "Provides a comprehensive understanding of software architecture principles."
        ]
    }
    ```

#### 3. `criteria`
- **Описание**: Задаются критерии для оценки качества выполненной задачи. Эти критерии варьируются в зависимости от контекста задачи.
- **Пример**:
    ```json
    "criteria": {
        "criteria_1": {
            "name": "Clarity of the design document",
            "description": "The design document should be clear and easy to understand."
        },
        "criteria_2": {
            "name": "Comprehensiveness of the design plan",
            "description": "The design document should provide a comprehensive overview of the software."
        }
    }
    ```

#### 4. `explicit_reminder`
- **Описание**: Содержит обязательное напоминание, которое должно использоваться в конце выполнения задачи.
- **Пример**:
    ```json
    "explicit_reminder": {
      "1": "\"After generating content ALWAYS conclude with the following statement: 🤖 Would You Like Me To Evaluate This Work ☝ and Provide Options to Improve It? Yes or No?\""
    }
    ```

#### 5. `evaluation_rubric`
- **Описание**: Определяет шкалу для оценки работы. Используется для тщательной проверки выполнения задачи.
- **Пример**:
    ```json
    "evaluation_rubric": {
        "1": "Poor: Fundamental flaws present.",
        "5": "Average: Adequate execution.",
        "10": "Outstanding: An epitome of perfection."
    }
    ```

---

## Как использовать промпт:

1. Заполните поля **prompt**, **role**, **department**, **task**, **task_description**, **key_references**, и **criteria** в зависимости от конкретной задачи.
2. Поля **rules**, **explicit_reminder** и **evaluation_rubric** рекомендуется оставлять неизменными, они помогут обеспечить высокий стандарт выполнения задачи.
   > Если всё таки того требует ваша задача, то менять их можно, однако для большинства задач этого хватит с головой.
3. Пример полного промпта с JSON-разметкой:

    ```json
    {
        "prompt": "Create a Software Design Document tailored to the user's business needs.",
        "role": "expert level software-engineer",
        "department": "engineering",
        "task": "Create a Software Design Document",
        "task_description": "Your task is to create a detailed and comprehensive design document.",
        "rules": {
            "rule_1": "Initial Message: 👋 I'm Larsen, your {role} AI.",
            "rule_2": "Ask up to 5 pertinent questions...",
            // остальные правила
        },
        "key_references": {
            "key_reference_1_title": "Software Architecture in Practice",
            // остальные ключевые источники
        },
        "criteria": {
            "criteria_1": {
                "name": "Clarity",
                "description": "The design document should be clear and understandable."
            },
            // остальные критерии
        },
        "explicit_reminder": {
            "1": "\"After generating content ALWAYS conclude...\""
        },
        "evaluation_rubric": {
            "1": "Poor: Fundamental flaws present. No redeeming qualities. Fails to meet even basic requirements.",
            "2": "Subpar: Slightly better than level 1, but foundational errors remain. Minimal engagement with the task.",
            "3": "Incomplete: Main components are missing or rushed. Only foundational ideas are present without depth.",
            "4": "Basic: Meets some requirements but lacks depth and insight. Common or generic ideas without originality.",
            // остальные рубрики
        }
    }
    ```

### Есть два примера промпта: на [английском](any_result_is_best_prompt.json)(оригинал) и на [русском](any_result_is_best_prompt_ru.json)(перевод выполнен самим ChatGPT).