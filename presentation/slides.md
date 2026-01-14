---
layout: center
colorSchema: dark
fonts:
  sans: "Inter"
  serif: "Instrument Serif"
  mono: "Fira Code"
---

# Написание алгоритма нахождения оптимальной рассадки учеников в классе
Лицензировано под GNU AGPLv3

Прокофьев Даниил

---
layout: two-cols-header
class: flex flex-col justify-center
---

# **Постановка задачи**

::left::

> ### Разработать алгоритм, генерирующий оптимальную рассадку с учетом данных ограничений и предпочтений
Так как задача относится к классу **NP-полных задач**, оптимальное решение за разумное время способны дать только **эвристические алгоритмы**.

::right::

#### Какие могут ограничения и предпочтения?

- <carbon-hospital class="text-red-400" /> Ограничения, связанные с **медицинскими предписаниями** (например, ученик должен сидеть за первой партой согласно предписанию врача)
- <carbon-user-avatar-filled-alt class="text-orange-400" /> Ограничения, связанные с **нежелательным соседством** двух учеников (например, двое учеников враждуют)
- <carbon-location class="text-blue-400" /> Предпочтения по **рядам и партам** (например, ученик хочет сидеть на первой парте)
- <carbon-group class="text-pink-400" /> Предпочтения учеников по **соседству** (например, двое друзей хотят сидеть вместе)

<style>
.two-cols-header {
  column-gap: 20px;
}
</style>
---
layout: center
---

# **Какие пути решения существуют?**

---
layout: two-cols-header
class: flex flex-col justify-center
---

# **Жадный алгоритм**

::left::

## Примерный принцип работы (жадность)
- Берем одного ученика
- Смотрим на его предпочтения и ограничения
- Сажаем его на лучшее из свободных мест

## Что не так?
#### Алгоритм может **пропустить лучшее решение** из-за предыдущих неудачных, тем самым **застряв в локальном максимуме**

::right::

``` text
            🏔️Глобальный максимум
           / \
          /   \        🚩Жадный застрял тут! 
  _______/     \      / \
 /              \____/   \
/
```
<style>
.two-cols-header {
  column-gap: 20px;
}
</style>

---
layout: two-cols-header
---

# **Метод имитации отжига**

::left::

### Сила и слабость метода
Алгоритм эффективно находит глобальные области, но критически зависит от времени.

**Главные недостатки:**
- **Время:** Требует очень медленного охлаждения.
- **Застревание:** При быстром снижении температуры может застрять

::right::

<div class="grid grid-cols-3 gap-2 items-end h-50 mt-10 text-center">

  <div class="flex flex-col items-center">
    <div class="w-12 h-16 bg-gray-400/20 border-t-2 border-gray-400/30">
      <div class="w-3 h-3 bg-gray-400 rounded-full mx-auto mt-2 opacity-30"></div>
    </div>
    <span class="text-[9px] mt-1 opacity-40 uppercase">Локальный<br>тупик</span>
  </div>

  <div class="flex flex-col items-center">
    <carbon-star class="text-yellow-400 mb-1 opacity-30" />
    <div class="w-12 h-40 bg-emerald-500/10 border-t-2 border-emerald-500/20 border-dashed">
    </div>
    <span class="text-[9px] mt-1 opacity-40 uppercase">Глобальный<br>максимум</span>
  </div>

  <div class="flex flex-col items-center">
    <carbon-warning class="text-orange-500 mb-1 animate-pulse" />
    <div class="w-12 h-28 bg-orange-500/40 border-t-2 border-orange-500">
      <div class="w-3 h-3 bg-white rounded-full mx-auto mt-2 shadow-[0_0_8px_white]"></div>
    </div>
    <span class="text-[9px] mt-1 text-orange-400 font-bold uppercase">Ошибка<br>закалки</span>
  </div>

</div>

<div class="mt-8 p-3 bg-orange-400/5 border-l-2 border-orange-400 text-[13px] leading-tight">
  <strong>Проблема:</strong> Если "температура" падает слишком быстро, алгоритм не успевает дойти до идеала и замерзает на субоптимальном решении.
</div>

---
layout: two-cols-header
---

# **Генетический алгоритм**

::left::
Алгоритм развивает не одно решение, а целую популяцию, и отбирает лучшие из них

**Механизмы:**
- **Скрещивание:** Объединение признаков двух родителей
- **Мутация:** Случайное изменение для поддержания разнообразия
- **Отбор:** Выживают только лучшие

**Главный минус** - **слепая эволюция**. Алгоритм не пытается улучшить ситуацию, а ждет, пока случайная мутация все исправит, что может занять тысячи поколений и увеличить вычислительную сложность

::right::

<div class="flex flex-col items-center justify-center h-full space-y-4">
  <div class="flex space-x-8 relative">
    <div class="flex flex-col items-center">
      <div class="grid grid-cols-2 gap-1 p-1 bg-blue-500/20 border border-blue-500/50 rounded">
        <div class="w-4 h-4 bg-blue-500"></div><div class="w-4 h-4 bg-blue-500"></div>
        <div class="w-4 h-4 bg-gray-400 opacity-20"></div><div class="w-4 h-4 bg-gray-400 opacity-20"></div>
      </div>
      <span class="text-[9px] mt-1 opacity-50 uppercase">Родитель A</span>
    </div>
    <div class="flex flex-col items-center">
      <div class="grid grid-cols-2 gap-1 p-1 bg-purple-500/20 border border-purple-500/50 rounded">
        <div class="w-4 h-4 bg-gray-400 opacity-20"></div><div class="w-4 h-4 bg-gray-400 opacity-20"></div>
        <div class="w-4 h-4 bg-purple-500"></div><div class="w-4 h-4 bg-purple-500"></div>
      </div>
      <span class="text-[9px] mt-1 opacity-50 uppercase">Родитель B</span>
    </div>
  </div>
  <carbon-arrow-down class="text-gray-400 animate-bounce" />
  <div class="flex flex-col items-center bg-emerald-500/10 p-4 rounded-xl border border-emerald-500/30">
    <div class="grid grid-cols-2 gap-1 p-1 bg-emerald-500/20 border border-emerald-500 rounded shadow-[0_0_15px_rgba(16,185,129,0.3)]">
      <div class="w-4 h-4 bg-blue-500"></div><div class="w-4 h-4 bg-blue-500"></div>
      <div class="w-4 h-4 bg-purple-500"></div><div class="w-4 h-4 bg-purple-500"></div>
    </div>
    <span class="text-[10px] mt-2 text-emerald-400 font-bold uppercase text-center">Лучший потомок<br>(Собрал все плюсы)</span>
  </div>
</div>
---
layout: two-cols-header
---

# **Меметический алгоритм**

::left::

Меметический подход объединяет глобальный охват генетики и ювелирную точность локальной оптимизации.

**Как работает**
- **Гены:** Наследуем общую структуру рассадки.
- **Локальный поиск:** Обучаем каждую или некоторые особи, исправляя локальные ошибки.

::right::

<div class="flex flex-col items-center justify-center h-full space-y-2">
  <div class="p-2 border border-gray-500/30 rounded bg-gray-500/5 text-center w-full">
    <div class="text-[9px] uppercase opacity-50 mb-2">Шаг 1: Генетический алгоритм</div>
    <div class="flex justify-center space-x-1">
       <div class="w-4 h-4 bg-blue-500"></div><div class="w-4 h-4 bg-blue-500"></div>
       <div class="w-4 h-4 bg-red-400 animate-pulse"></div> <div class="w-4 h-4 bg-blue-500"></div>
    </div>
    <span class="text-[10px] text-orange-400 italic">Почти готово (есть 1 ошибка)</span>
  </div>
  <div class="flex flex-col items-center text-emerald-400 py-1">
    <carbon-tools class="text-xl" />
    <span class="text-[9px] font-bold uppercase">Локальный поиск</span>
    <carbon-arrow-down />
  </div>
  <div class="p-2 border border-emerald-500 rounded bg-emerald-500/10 text-center w-full shadow-[0_0_20px_rgba(16,185,129,0.2)]">
    <div class="text-[9px] uppercase text-emerald-400 mb-2">Шаг 2: Шлифовка решения</div>
    <div class="flex justify-center space-x-1">
       <div class="w-4 h-4 bg-blue-500"></div><div class="w-4 h-4 bg-blue-500"></div>
       <div class="w-4 h-4 bg-emerald-500"></div> <div class="w-4 h-4 bg-blue-500"></div>
    </div>
    <span class="text-[10px] text-emerald-500 font-bold uppercase">Идеальная рассадка</span>
  </div>
</div>
---
layout: default
---

# **Как работает меметический алгоритм?**

- Создаём начальную популяцию случайных рассадок
- Оцениваем каждую рассадку с помощью функции fitness
- Применяем локальный поиск к лучшей особи и (с шансом 0,05) к случайным особям
- Отбираем родителей для скрещивания (через турнирную селекцию)
- Генерируем потомство:

 --- Скрещивание (CrossOver) родителей

 --- Мутация (SwapMutation) с заданной вероятностью

 --- Переносим лучшую особь в новое поколение (элитизм)

 --- Повторяем шаги 2–6 заданное число поколений
---
layout: default
---

# **Как хранить рассадки в памяти?**
--

Для удобства работы с функциями мутации, скрещивания и фитнеса мною было принято решение использовать одномерные массивы. Их удобно хранить в памяти и совершать различные операции.

```text
[1, 3, 5, 6, 7, 2, 4, 8, 9, 10] - класс размером 2 ряда * 5 парты в ряду, но только 8 учеников
```
```text
 1        3
 5        6
 7        2
 4        8
9(-1)   10(-1)
```

Для индексов больше, чем количество учеников будем считать, что это место пустует. Они при сборке ответа будут обозначаться как -1.

---
layout: default
---

# **Как работает меметический алгоритм?**
```go
func RunGA(req Request) ([]Response, int) { 
  // Создаем популяцию размером popSize и заполняем ее случайными рассадками
	population := make([][]int, popSize)
	for i := range population {
		population[i] = rand.Perm(N)
	}
  // Для каждого поколения:
	for gen := 0; gen < generations; gen++ {
		scores := make([]int, popSize)
		for i, seat := range population {
      // Оцениванием рассадку с помощью функции fitness
			scores[i] = fitness(seat, req.Students, req.Preferences, req.Forbidden, req.ClassConfig, weights, ...)
		}
    // Создаем новую популяцию, которая будет содержать детей нынешнего поколения
		newPop := make([][]int, popSize)
    // Ищем лучшую на данный момент рассадку
		iBest := 0
		for j := 1; j < popSize; j++ {
			if scores[j] > scores[iBest] {
				iBest = j
			}
		}
		// ...
}
```
---
layout: default
---

# **Как работает меметический алгоритм?**

```go
// Применяем локальный поиск к лучшей особи и с шансом 0.05 к случайной особи
for i := 0; i < popSize; i++ {
			if i == iBest || rand.Float64() < 0.05 {
				population[i] = localSearch(population[iBest], req.Students, req.ClassConfig, weights, friends, enemies)
				scores[i] = fitness(population[iBest], req.Students, req.Preferences, req.Forbidden, req.ClassConfig, ...)
			}
		}
    // Переносим одну наилучшую особь в новое поколение без изменений (элитизм)
		newPop[0] = make([]int, N)
		copy(newPop[0], population[iBest])
    // Отбираем родителей для скрещивания с помощью турнира
		for i := 1; i < popSize; i++ {
			parent1 := tournamentSelection(population, scores, 3)
			parent2 := tournamentSelection(population, scores, 3)
			child := CrossOver(parent1, parent2)
			if rand.Float64() < req.CrossOverChance {
        // Реализуем случайную мутацию (меняем двух учеников местами)
				child = SwapMutation(child)
			}
			newPop[i] = child
		}
		population = newPop
	}
	// ...
```

---


# **Фитнес функция: как оценить рассадку?**


Общая оценка рассадки $F(S)$ считается как сумма учтенности предпочтений каждого из учеников в отдельности

```go
func fitness(seating []int, config ClassConfig, w Weights, friends SocialMap, enemies SocialMap, ...) float64 {
	score := 0.0
	for i, studentIdx := range seating {
		if studentIdx < 0 || studentIdx >= nStudents {
			continue
		}
		row, col := i/config.Columns, i%config.Columns
		fScore := checkFriends(studentIdx, seating, row, col, config, friends, nStudents, friendsCount)
		ePenalty := checkEnemies(studentIdx, seating, row, col, config, enemies, nStudents)

		sScore := (fScore * w.FriendBonus * 100.0) - (ePenalty * w.EnemyPenalty * 5.0 * 100.0)
		sScore += staticScores[studentIdx*config.Rows*config.Columns+i]

		score += sScore
	}
	return score
}
```
---
layout: two-cols-header
class: flex flex-col justify-center
---

# **Веса, настройка, калибровка фитнес функции**

::left::

Самая важная часть алгоритма. От того, как конкретно функция fitness оценит рассадку, зависит, куда дальше пойдет эволюция.
Однако, у каждого пользователя могут быть разные запросы. Поэтому важно разработать максимально гибкую и настраиваемую систему.

Вместе с запросом к бекенду посылаются **веса** - какие предпочтения учитывать больше, а какие меньше. От их правильной настройки зависит качество решения.

::right::

```json
...
"PriorityWeights": {
          "Medical": 0.9,
          "Friends": 0.65,
          "Enemies": 0.7,
          "Preferences": 0.6,
          "Fill": 0.3
      }
...
```

---
layout: two-cols-header
---

# **Как работает проверка предпочтений?**

::left::

Каждая функция, которая что-то проверяет, возвращает **нормализованное значение** от 0.0 до 1.0. 
Такая функция считает учтенность какого-либо предпочтения для отдельного ученика и делит полученное значение на максимальное значение учтенности этого конкретного предпочтения.

Затем, значение этой функции умножается на некий вес, который пришел с фронтенда.

::right::

```go
// функция проверки учтенности предпочтений по рядам и партам
func checkPref(student optStudent, row, col int) float64 {
	score := 0.0
	maxPossible := 0.0
	if len(student.pCols) > 0 {
		maxPossible += 1.0 // если есть предпочтения по рядам
	}
	if len(student.pRows) > 0 {
		maxPossible += 1.0  // если есть предпочтения по партам
	}
	if maxPossible == 0 {
		return 1.0 // если предпочтений вообще нету
	}
	if student.pCols[col] {
		score += 1.0 // если предпочтение по ряду выполнено
	}
	if student.pRows[row] {
		score += 1.0 // если предпочтение по парте выполнено
	}
  // возвращаем нормализованное значение от 0.0 до 1.0
	return score / maxPossible
}
```

---
layout: two-cols-header
---

# **Почему в качестве языка бекенда выбран Go?**

::left::

<img src="/ladder.svg" class="w-7/8" />

::right::

- Go язык компилируемый =>

  -- Легкость развертывания (всего один бинарный файл, который можно запустить где угодно)
 
  -- Работает быстрее пресловутого Python
- Параллельные вычисления с помощью горутинов
- Масштабируемость и приспособленность языка к реализации на нем высоконагруженных микросервисов
- Простой, минималистичный синтаксис
- Строгая типизация позволяет избежать досадных ошибок
---
layout: two-cols
---

### **Проект реализован по принципу разделения ответственности**
* Backend (Go)
  * Выполнение меметического алгоритма, изоляция ради стабильности
* Frontend (Vue 3)
  * Клиентское приложение для настройки параметров и весов, визуализация результата
* Взаимодействие (REST API)
  * Обмен данными через JSON-объекты, возможность работы с другими клиентами
* Инфраструктура (Docker + Github Actions)
  * Развертывание одной командой без установки зависимостей.

::right::

<div class="flex flex-col items-center justify-center h-full">
  <div class="p-3 border-2 border-emerald-500 rounded-lg bg-emerald-500/10 w-48 text-center">
    <carbon-code class="mb-1" />
    <div class="text-xs font-bold">Backend (Go)</div>
    <div class="text-[10px] opacity-70">Вычисления и логика</div>
  </div>
  
  <div class="h-8 w-0.5 bg-gray-500 my-1 border-dashed border-l-2"></div>
  <div class="text-[10px] text-orange-400 font-mono">JSON API</div>
  <div class="h-8 w-0.5 bg-gray-500 my-1 border-dashed border-l-2"></div>

  <div class="p-3 border-2 border-blue-500 rounded-lg bg-blue-500/10 w-48 text-center">
    <carbon-screen class="mb-1" />
    <div class="text-xs font-bold">Frontend (Vue 3)</div>
    <div class="text-[10px] opacity-70">Визуализация и UX</div>
  </div>
</div>
---
layout: two-cols-header
---

# **Как выглядит запрос к серверу?** 

::left::

```json
{
    "students": [
        {
            "id": 1767369989264,
            "name": "Иван",
            "preferredRows": [],
            "preferredColumns": [],
            "medicalPreferredRows": [],
            "medicalPreferredColumns": []
        },
        {
            "id": 1767369995544,
            "name": "Петр",
            "preferredRows": [],
            "preferredColumns": [],
            "medicalPreferredRows": [],
            "medicalPreferredColumns": []
        },
        {
            "id": 1767369998215,
            "name": "Елизавета",
            "preferredRows": [],
            "preferredColumns": [],
            "medicalPreferredRows": [],
            "medicalPreferredColumns": []
        }
    ],
```

::right::

```json
  "preferences": [
          [
              1767369989264,
              1767369995544
          ]
      ],
      "forbidden": [
          [
              1767369995544,
              1767369998215
          ]
      ],
      "classConfig": {
          "rows": 3,
          "columns": 4
      },
      "popSize": 300,
      "generations": 400,
      "crossOverChance": 0.3,
      "PriorityWeights": {
          "Medical": 0.9,
          "Friends": 0.65,
          "Enemies": 0.7,
          "Preferences": 0.6,
          "Fill": 0.3
      }
}
```

<style>
pre {
  max-height: 400px;
  overflow-y: hidden;
  font-size: 0.6rem !important;
  line-height: 1.2 !important;
}
</style>
---
layout: default
---

# **В попытках разработать дружественный интерфейс...**

![](/screenshots/main.png)
---

![](/screenshots/editor.png)

---

![](/screenshots/generator.png)
---

![](/screenshots/seatings.png)
---

![](/screenshots/view-seating.png)
---
layout: two-cols-header
class: flex flex-col justify-center
---

# **Что использовано?**
смотрим на package.json проекта

::left::

```json
{
  "name": "frontend",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "@popperjs/core": "^2.11.8",
    "axios": "^1.13.2",
    "bootstrap": "^5.3.8",
    "bootstrap-vue-next": "^0.40.9",
```

::right::
```json
    "jspdf": "^4.0.0",
    "jspdf-autotable": "^5.0.7",
    "papaparse": "^5.5.3",
    "unplugin-icons": "^22.5.0",
    "vue": "^3.5.26",
    "vue-router": "^4.6.4",
    "vuedraggable": "^4.1.0"
  },
  "devDependencies": {
    "@iconify-json/bi": "^1.2.7",
    "@vitejs/plugin-vue": "^6.0.3",
    "unplugin-vue-components": "^29.2.0",
    "vite": "^7.3.1"
  }
}
```
---

# **Структура файлов фронтенда**

```text
.
├── Caddyfile
├── Dockerfile
├── index.html
├── LICENSE
├── package-lock.json
├── package.json
├── public
│   └── fonts
│       └── Roboto-Regular.ttf // лицензирован Apache License, v. 2.0
├── src
│   ├── App.vue
│   ├── ClassEditor.vue
│   ├── ClassesList.vue
│   ├── ClassMap.vue
│   ├── composables
│   │   ├── useClasses.js
│   │   └── useSeating.js
│   ├── Generator.vue
│   ├── main.js
│   └── SeatingHistory.vue
└── vite.config.js
```
---
class: flex flex-col justify-center
---

# **Почему все запускается одной командой?**

- Триггер: Push в ветку main.
- Сборка: Сборка Docker-образа фронта и бэка.
- Загрузка образа: Пуш в GitHub Container Registry (GHCR).
- Развертывание: Обновление контейнеров на сервере через WatchTower / запуск вручную через ```docker compose up```

```mermaid
graph LR
    subgraph GitHub_Cloud [GitHub Cloud]
        A[Push Code] --> B[GitHub Actions]
        B -->|Build & Tag| C[Docker Image]
        C -->|Push| D[(GHCR.io)]
    end

    subgraph Your_Server [Ваш Сервер / ПК]
        D -->|Pull| E[Docker Engine]
        E -->|Run Container| F[Live Application]
    end

    style B fill:#24292e,color:#fff
    style D fill:#44cc11,color:#000
    style F fill:#007bff,color:#fff
```

---
layout: two-cols-header
class: flex flex-col justify-center items-start
---

# **Прямо во Всемирную паутину!**

::left::

- **Домен:** `seating-generator.ru`
- **Провайдер:** Cloud.ru (VPS на Linux, Cloud Free Evolution Tier)
- **Защита:** Cloudflare (WAF/DDoS)

### Архитектура
- **Caddy:** Реверс-прокси + SSL
- **Docker:** Те самые контейнеры
- **Безопасность:** Весь трафик только через прокси

::right::


<div class="scale-120 origin-left ml-12">

```mermaid
graph TD
    U((Юзер)) --> CF[Cloudflare]
    CF --> VPS[Cloud.ru]
    
    subgraph Server [Host]
        VPS --> Caddy[Caddy]
        subgraph Docker [Docker Network]
            Caddy --> Front[Frontend]
            Caddy --> Back[Backend API]
        end
    end

    style CF fill:#f38020,color:#fff
    style Caddy fill:#00a2ff,color:#fff
    style Front fill:#42b883,color:#fff
    style Back fill:#384d54,color:#fff
```
</div>

---
layout: center
---

# **Демонстрация работы**
---

<div class="flex justify-center">
  <video 
    src="/demo.mp4" 
    controls 
    muted 
    class="w-1024 rounded-lg shadow-xl"
  ></video>
</div>
---
layout: two-cols-header
class: flex flex-col justify-center
---

# **Лицензирование**

::left::

### ***GNU Affero GPL v3.0***

- **Copyleft:** Любые изменения должны распространяться на тех же условиях
- **Remote Network Interaction:** Если сервис доступен через сеть, исходный код **обязан** быть открыт
- **Прозрачность:** Пользователь имеет право знать, как обрабатываются его данные

### **Что это значит для проекта?**

- **Доступность:** Ссылка на репозиторий закреплена в Navbar приложения
- **Свобода:** Любой желающий может развернуть свою копию для школы или университета

::right::

<img src="/GNU_logo.png"></img>

---
layout: center
class: text-center
---

# **Изучить проект**

<div class="flex flex-col items-center mt-8">
  <div class="p-4 bg-white rounded-xl shadow-2xl">
    <img src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=https://github.com/chashkakefira/seating-generator" 
         class="w-50 h-50" />
  </div>
  
  <p class="mt-4 text-xl font-mono">github.com/chashkakefira/seating-generator</p>
  
  <div class="mt-6 flex gap-4 opacity-70">
    <span class="flex items-center gap-1"><div class="i-mdi-docker" /> Go</span>
    <span class="flex items-center gap-1"><div class="i-mdi-github" /> Vue</span>
    <span class="flex items-center gap-1"><div class="i-mdi-github" /> Docker</span>
    <span class="flex items-center gap-1"><div class="i-mdi-web" /> AGPLv3</span>
  </div>
</div>

<p class="mt-12 text-sm opacity-50">
  Проект оптимизирован для работы в десктопных браузерах.<br>
  QR-код ведет на документацию и исходный код.
</p>