# Cabbage Escape

## Хасанов Анвар

### Как играть

В начале игры вы спавнитесь в комнате с ловушками. Ваша задача дойти до “островка” с дверьми. На выбор у вас есть две двери: красная - на следующем уровне будет больше ловушек, но также и будут бафы, синяя - уровень не будет отличаться от текущего по сложности, но там не будет бафов. Для взаимодействия с дверьми нажмите “E”

В левом нижнем углу есть ваше здоровье, при получении урона от ловушек оно будет уменьшаться. Всего у вас 10 хп, при достижении 0 хп игра будет проиграна

В самой последней комнате вы увидите кочан капусты на том же островке с дверьми, при его достижении вы выиграете

### Алгоритм генерации комнат и их содержимого

В игре используется только 1 комната. Есть блюпринт “LevelGenerator”, в котором содержатся параметры уровня:

- CurrentLevel - текущий номер комнаты
- MaxLevels - общее число комнат
- FloorTrapsCount - число напольных ловушек
- CeilTrapsCount - число динамических ловушек
- IsHigherLevel - сложнее ли уровень, чем предыдущий

На каждом уровне есть два типа ловушек: 

1) Статические напольные, который наносят единичный урон игроку при взаимодействии с ними и периодический урон при нахождении на ловушке

2) Динамические ловушки, которые двигаются вверх-вниз и наносят урон игроку, если он задевает их нижнюю часть

Есть “запрещенные” места для ловушек, они описаны в переменной `ForbiddenTrapPositions` , следовательно на остальных местах их можно расставить. Циклом по кол-ву ловушек расставляем их на места и смотрим, чтобы на этом месте еще не было ловушки данного типа. 

При прохождении уровня и взаимодействия с дверью, игрока телепортирует в начало, удаляются все предметы с уровня и генерируются заново в зависимости от параметров

### Баффы на уровне

При выборе игрока более сложного уровня генерируются 3 баффа:

- Чеснок: позволяет на 1.5 секунды не получать урон от статических ловушек
- Тыква: увеличивает задержку на 1 секунду динамических ловушек перед очередной итерацией
- Красная капуста: восстанавливает 2 единицы здоровья

### Изменение сложности

Уровень сложности зависит от количества ловушек. При прохождении в красную дверь количество ловушек на следующем уровне увеличивается на 4. Изначально количество ловушек находится в диапазоне от 20 до 25. Соответственно, если будет 10 уровней и на каждом количество ловушек будет увеличиваться, то на 10 уровне их будет от 56 до 60
