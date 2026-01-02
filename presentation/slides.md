---
layout: center
fonts:
  sans: 'Inter'            
  serif: 'Instrument Serif'   
  mono: 'Fira Code'           
---

# Написание алгоритма нахождения оптимальной рассадки учеников в классе
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
- **Застревание:** Прибыстром снижении температуре может застрять

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
layout: center
---

# **Как работает меметический алгоритм?**

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
	// ...
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
// Применяем локальный поиск к лучшей особи и шансом 0.05 к случайной особи
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


# **Подробнее про фитнес функцию и как она работает или как оценить рассадку?**


Общая оценка рассадки $F(S)$:


<span class="small-math">
$$
F(S) = \sum_{i=0}^{N-1} \left[
  \underbrace{w_R \cdot (R - r_i)}_{\text{ряд}} +
  \underbrace{w_P \cdot (C - c_i)}_{\text{колонка}} +
  \underbrace{M(s_i, r_i, c_i)}_{\text{медицина}} +
  \underbrace{P(s_i, r_i, c_i)}_{\text{предпочтения}} +
  \underbrace{F(s_i, S, r_i, c_i)}_{\text{друзья}} +
  \underbrace{E(s_i, S, r_i, c_i)}_{\text{враги}}
\right]
$$
</span>

## Обозначения

- $F(S)$ — общая оценка рассадки $S$ (максимизируется);
- $N = \text{Rows} \times \text{Columns}$ — общее число мест;
- $i$ — индекс места ($0 \leq i < N$);
- $r_i = \left\lfloor \dfrac{i}{C} \right\rfloor$ — номер ряда места $i$;
- $c_i = i \bmod C$ — номер колонки места $i$;
- $s_i = S[i]$ — индекс ученика на месте $i$ (или недопустимое значение);
- $R = \text{Rows}$, $C = \text{Columns}$ — размеры класса.
<style>
.small-math {
  font-size: 0.9em;
  display: block;
  margin: 1rem 0;
}
</style>