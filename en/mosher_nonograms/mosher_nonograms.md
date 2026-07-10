# Solving Nonograms

Robert Mosher

### Решение японских кроссвордов (нонограмм)


### 1. Описание проблемы (Problem Description)


### Условие

В данном проекте генетические алгоритмы (ГА) применяются для решения нонограмм (логических головоломок «раскраска по номерам»). Нонограмма представляет собой прямоугольную сетку пикселей, каждый из которых должен быть либо закрашен, либо оставлен пустым. Для определения цвета пикселей для каждой строки и столбца задается список чисел — подсказок. Каждое число указывает длину одной непрерывной группы закрашенных пикселей в этой строке или столбце. Группы разделяются как минимум одним пустым пикселем. Порядок чисел указывает на порядок расположения групп слева направо (для строк) или сверху вниз (для столбцов). Задача состоит в том, чтобы определить, сколько пустых пикселей предшествует первой группе и разделяет каждую последующую группу. **Пример:** Рассмотрим строку из 15 пикселей с подсказкой `[5, 3]`. В этой строке есть две непрерывные группы закрашенных пикселей: первая длиной 5 пикселей, вторая — 3 пикселя. Группа из 5 пикселей находится левее группы из 3. Других закрашенных пикселей в этой строке нет. Группы разделены как минимум одним пустым пикселем. Перед первой группой может быть ноль или более пустых пикселей, и после последней группы — также ноль или более. Суммарное количество всех пустых пикселей в строке равно 7 (15 - (5 + 3)). 
### Решение

Для работы с нонограммами в Python нам сначала нужно научиться генерировать один из вариантов строки, который бы строго соответствовал заданным подсказкам и ограничениям по длине. 
```python
def generate_valid_row(clues, total_length):
    # Простейшая начальная генерация строки по подсказкам
    # Размещаем группы, разделяя их ровно одним пустым пикселем
    row = []
    for i, clue in enumerate(clues):
        row.extend([1] * clue)
        if i < len(clues) - 1:
            row.append(0) # обязательный разделитель
            
    # Дозаполняем оставшуюся длину нулями в конец
    remaining = total_length - len(row)
    if remaining > 0:
        row.extend([0] * remaining)
        
    return row

# Пример для строки длиной 15 с подсказками [5, 3]
example_clues = [5, 3]
length = 15
generated = generate_valid_row(example_clues, length)

print("Пример валидной строки (1 - закрашен, 0 - пуст):")
print(generated)
print(f"Длина: {len(generated)}, Закрашено: {sum(generated)}")
```

### 2. Подход к представлению (Approach: Representation)


### Условие

Представление решения нонограммы в виде простой бинарной строки, где каждый пиксель является отдельным аллелем, сопряжено с серьезной проблемой. Если строки сетки просто объединить (склеить) в одну длинную хромосому, то любой стандартный кроссовер будет полностью разрушать строительные блоки вдоль столбцов. Альтернативно можно использовать однородный (uniform) кроссовер. Хотя он не имеет позиционного смещения в пользу строк или столбцов, он полностью игнорирует значимость того, что пиксели находятся в одной строке или столбце. Другой вариант — использовать «умный» кроссовер, который обменивается целыми двумерными блоками пикселей, близких в сетке. Но и он разрушителен для структуры. Главный недостаток всех этих вариантов — они игнорируют подсказки, которые жестко ограничивают задачу. Лучший способ использовать подсказки — ограничить варианты строк **только теми, которые изначально им соответствуют**. Вводится альтернативное представление: каждый аллель хромосомы представляет собой **стартовую позицию (индекс)** закрашенной группы пикселей в строке. Теперь задача ГА меняется: алгоритм не красит случайные пиксели, а двигает (сдвигает) уже сформированные группы внутри строк до тех пор, пока они не удовлетворят ограничениям, заданным вдоль столбцов. При этом операции кроссовера и мутации должны контролировать, чтобы группы не наползали друг на друга и не выходили за границы сетки. 
### Решение

Вместо хранения матрицы пикселей хромосома хранит только смещения (отступы) групп. Напишем функцию, которая преобразует хромосому отступов в реальную строку пикселей для проверки ограничений. 
```python
def decode_row_from_offsets(offsets, clues, total_length):
    # offsets: список левых индексов (начал) для каждой группы из clues
    row = [0] * total_length
    for start_idx, clue_len in zip(offsets, clues):
        for i in range(clue_len):
            row[start_idx + i] = 1
    return row

# Пример: строка 15 пикселей, группы. 
# Зададим левые границы (индексы начала) для этих групп:
# Первая группа (5) стартует с индекса 2. Вторая группа (3) стартует с индекса 9.
clues = [5, 3]
offsets = [2, 9] 
row_length = 15

# Проверка на валидность: группы не должны пересекаться и выходить за границы
# (В реальном ГА этот шаг зашивается в оператор мутации/кроссовера)
decoded_row = decode_row_from_offsets(offsets, clues, row_length)
print("Восстановленная из отступов строка:")
print(decoded_row)
```

### 3. Функция приспособленности (Fitness)


### Условие

Учитывая выбранное представление (где каждая строка по умолчанию всегда идеально соответствует своим строчным подсказкам), функция приспособленности (фитнес) должна оцениваться **исключительно по вертикальным столбцам**. Если столбец идеально совпадает со своими подсказками, он не должен уменьшать общую приспособленность хромосомы. Основная сложность заключается в определении штрафов: насколько сильно несовершенства в столбце должны снижать приспособленность? Считается ли появление лишней изолированной группы пикселей худшим нарушением, чем группа неправильного размера? Должен ли маленький ошибочный блок весить меньше, чем большой? Эти параметры требуют настройки. 

### Решение

Простой и эффективный способ оценки столбца — перевести получившиеся пиксели столбца в фактический список групп и сравнить его с целевой подсказкой для этого столбца (например, методом расстояния Левенштейна или подсчетом несовпадающих элементов). Ниже приведен пример функции, которая вычисляет реальные блоки закрашенных пикселей в получившемся столбце и сравнивает их с требуемыми по условию задачи. 
```python
def get_column_clues(column_pixels):
    # Функция считывает фактические группы единиц в столбце
    clues = []
    current_length = 0
    for pixel in column_pixels:
        if pixel == 1:
            current_length += 1
        else:
            if current_length > 0:
                clues.append(current_length)
                current_length = 0
    if current_length > 0:
        clues.append(current_length)
    return clues

def evaluate_column_fitness(actual_pixels, target_clues):
    # Получаем фактические подсказки из получившегося столбца
    actual_clues = get_column_clues(actual_pixels)
    
    # Штрафуем за несовпадение списков подсказок
    # Если списки полностью совпадают — штраф 0 (идеально)
    if actual_clues == target_clues:
        return 0
        
    # Базовая метрика штрафа: разница в количестве групп + разница в сумме пикселей
    penalty = abs(len(actual_clues) - len(target_clues)) * 2
    penalty += abs(sum(actual_pixels) - sum(target_clues))
    
    return penalty

# Тест: столбец должен содержать блоки [3, 1]
target = [3, 1]

# Сценарий А: Получился идеальный столбец
col_A = [1, 1, 1, 0, 0, 1, 0]
# Сценарий Б: Ошибка в размере первой группы (4 вместо 3)
col_B = [1, 1, 1, 1, 0, 1, 0]

print(f"Штраф для столбца А (идеал): {evaluate_column_fitness(col_A, target)}")
print(f"Штраф для столбца Б (ошибка): {evaluate_column_fitness(col_B, target)}")
```

Вот готовый, полностью рабочий генетический алгоритм на Python для решения японского кроссворда (нонограммы) размером 5x5 [INDEX].
Алгоритм использует предложенное Робертом Мошером представление хромосомы [INDEX]: каждая особь состоит из валидных строк (сдвигов блоков пикселей) [INDEX]. Оценка (фитнес) рассчитывается исключительно по нарушениям в столбцах [INDEX].


```python
import random

# Определяем условия задачи (целевые подсказки для нонограммы 5x5 "X")
ROW_CLUES = [[1, 1], [1, 1], [1], [1, 1], [1, 1]]
COL_CLUES = [[1, 1], [1, 1], [1], [1, 1], [1, 1]]
GRID_SIZE = 5

def get_all_valid_rows(clues, length):
    """Генерирует все возможные валидные комбинации пикселей для одной строки по её подсказкам."""
    if not clues:
        return [[0] * length]
    
    results = []
    
    def backtrack(clue_idx, current_pos, current_row):
        if clue_idx == len(clues):
            # Дозаполняем нулями до конца заданной длины строки
            extended_row = list(current_row)
            while len(extended_row) < length:
                extended_row.append(0)
            results.append(extended_row)
            return
            
        clue = clues[clue_idx]
        
        # Вычисляем минимальное место, необходимое для оставшихся блоков
        remaining_blocks = clues[clue_idx + 1:]
        min_remain_space = sum(remaining_blocks) + len(remaining_blocks)
        max_start = length - min_remain_space - clue
        
        for start in range(current_pos, max_start + 1):
            # Создаем копию текущей строки и добавляем нули до позиции старта, затем сам блок
            new_row = list(current_row)
            for _ in range(start - current_pos):
                new_row.append(0)
            for _ in range(clue):
                new_row.append(1)
            
            # Если это не последний блок, добавляем обязательный разделяющий ноль
            if clue_idx < len(clues) - 1:
                new_row.append(0)
                backtrack(clue_idx + 1, start + clue + 1, new_row)
            else:
                backtrack(clue_idx + 1, start + clue, new_row)

    backtrack(0, 0, [])
    return results

# Заранее генерируем пул всех возможных вариантов для каждой строки
VALID_ROWS_POOL = [get_all_valid_rows(clues, GRID_SIZE) for clues in ROW_CLUES]

def get_actual_col_clues(col_pixels):
    """Извлекает подсказки (блоки единиц) из получившегося столбца."""
    clues = []
    current_len = 0
    for pixel in col_pixels:
        if pixel == 1:
            current_len += 1
        else:
            if current_len > 0:
                clues.append(current_len)
                current_len = 0
    if current_len > 0:
        clues.append(current_len)
    return clues

def calculate_fitness(chromosome):
    """
    Вычисляет штраф хромосомы. Чем меньше штраф, тем лучше.
    Идеальное решение имеет штраф = 0.
    """
    penalty = 0
    for col_idx in range(GRID_SIZE):
        col_pixels = [chromosome[row_idx][col_idx] for row_idx in range(GRID_SIZE)]
        actual_clues = get_actual_col_clues(col_pixels)
        target_clues = COL_CLUES[col_idx]
        
        if actual_clues != target_clues:
            penalty += abs(len(actual_clues) - len(target_clues)) * 10
            penalty += abs(sum(col_pixels) - sum(target_clues)) * 5
    return penalty

def create_individual():
    """Создает случайную хромосому, где каждая строка выбрана из пула валидных."""
    return [random.choice(VALID_ROWS_POOL[i]) for i in range(GRID_SIZE)]

def crossover(parent1, parent2):
    """Кроссовер обменивается целыми строками, чтобы не нарушать их валидность."""
    point = random.randint(1, GRID_SIZE - 1)
    child1 = parent1[:point] + parent2[point:]
    child2 = parent2[:point] + parent1[point:]
    return child1, child2

def mutate(chromosome, mutation_rate=0.3):
    """Мутация заменяет одну из строк на другой случайный вариант из пула."""
    if random.random() < mutation_rate:
        row_idx = random.randint(0, GRID_SIZE - 1)
        chromosome[row_idx] = random.choice(VALID_ROWS_POOL[row_idx])

def print_grid(chromosome):
    """Вывод кроссворда в консоль."""
    for row in chromosome:
        print(" ".join(["██" if pixel == 1 else "  " for pixel in row]))

def run_genetic_algorithm(pop_size=50, generations=1000):
    population = [create_individual() for _ in range(pop_size)]
    
    for gen in range(generations):
        population = sorted(population, key=calculate_fitness)
        best_fitness = calculate_fitness(population[0])
        
        if best_fitness == 0:
            print(f"Решение найдено на поколении {gen}!")
            return population[0]
            
        new_population = population[:5] # Элитизм
        
        while len(new_population) < pop_size:
            p1 = min(random.sample(population, 3), key=calculate_fitness)
            p2 = min(random.sample(population, 3), key=calculate_fitness)
            
            ch1, ch2 = crossover(p1, p2)
            mutate(ch1)
            mutate(ch2)
            
            new_population.append(ch1)
            if len(new_population) < pop_size:
                new_population.append(ch2)
            
        population = new_population
        
    print("Достигнут лимит поколений. Лучшее приближенное решение:")
    return population[0]

# Запуск алгоритма
solution = run_genetic_algorithm()
print("\nВизуализация решения нонограммы:")
print_grid(solution)
```


## Как это работает:

   1. Генерация пула (get_all_valid_rows): Для каждой строки мы заранее находим все математически возможные комбинации пикселей, удовлетворяющие подсказке [INDEX]. Для строки [1, 1] это будут варианты вроде [1, 0, 1, 0, 0], [0, 1, 0, 1, 0] и т.д.
   2. Хромосома: Алгоритм оперирует не отдельными пикселями, а комбинациями строк [INDEX]. Это гарантирует, что по горизонтали кроссворд всегда правильный [INDEX].
   3. Кроссовер и мутация: Кроссовер меняет строки между родителями целиком, а мутация выбирает альтернативный сдвиг блоков для случайной строки [INDEX].
   4. Фитнес (calculate_fitness): Считает штрафные баллы на основе вертикальных столбцов. Как только штраф падает до 0 — нонограмма решена [INDEX].

