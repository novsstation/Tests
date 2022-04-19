---
title: jest-performance-research
description: 
published: true
date: 2022-04-18T11:24:40.874Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:24:38.215Z
---

# Jest Pipeline

1. Инициализация *jest*;
2. Сбор тестов и их зависимостей;
3. Транспиляция и сохранение в кеш;
4. Запуск *Runner*-а,(-ов если не *runInBand*);
5. Runner;
6. resetModules;
7. загрузка модулей;
8. выполнение теста(ов).

**На скорость прохождения тестов влияют:**

* Каждый модуль используемый в тестах проходит этап транспиляции (*babel* или *ts*) и попадает в кэш. Тесты после *--clearCache* или на чистой машине ходят медленнее, так как все модули транспилируются. На количество *ts* транспилируемых модулей влияет *isolatedModules* и *include* (*ts-jest-optimization*);
* *runInBand* - последовательный запуск, либо параллельный и количество потоков автоматическое или *maxWorkers*;
* количество модулей загружаемых тестом. Перед прогоном *jest* чистит все (*resetModules*) загруженные модули и грузит их вновь этот процесс отнимает от 0.5 до 1с;
* Количество тестовых файлов. Условно говоря, если собрать все тесты в один файл то они пройдут быстрее так, как будет только один *resetModules*, а не много (по количеству файлов).

С *isolatedModules* надо быть аккуратным, так как они могут сломать *coverage* с декораторами. У нас был включен *emitDecoratorMetadata* и он приводил к неправильному коверейджу следующего кода:

```typescript
export class CellBaseProps {
@OneWay() contentTemplateProps?: ContentTemplateProps;
```

**Без *isolatedModules* и без кеша в много потоков.**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --clearCache`

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --runInBand`

Test Suites: 59 passed, 59 total

Tests:       794 passed, 794 total

Snapshots:   0 total

Time: **63.172s**

***isolatedModules*, запуск без кеша в много потоков.**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --clearCache`

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest`

...

Time: **29.1s**

**Вывод**. Так как *isolatedModules* дает существенный выигрыш, все дальнейшее тестирование будем производить с ним.

**Запуск без кеша в один поток.**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --clearCache`

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --runInBand`

...

Time: **37.35s**

**Запуск с кешем в один поток.**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --runInBand`

...

Time: **18.76s**

**Запуск с кешем, много потоков (7 потоков на тестовой машине).**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest`

...

Time: **13.498s, estimated 17s**

**Запуск без кеша в количество потоков равно 3.**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --clearCache`

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest jest --maxWorkers=3`

...

Time: **24.711s**

**Вывод**. Кэш модулей влияет очень сильно и дает порядка 2-3 раз (19 сек). Прогон тестов в параллели дает выигрыш порядка 30% (8 сек и 4 сек). Еще можно немного выиграть, если задать количество потоков вручную (я брал по формуле CPU Core - 1 = 3). Выигрыш составил 20% (5 сек).

**Прогон теста в *watch* режиме (параллельный прогон).**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --watch widget.test`

...

Time: **3.761s**

...

Time: **4.548s**

...

Time: **4.53s**

**Прогон теста в watch режиме (*runInBand*).**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --watch --runInBand widget.test`

Time: **3.872s**

...

Time: **2.034s**

...

Time: **2.003s**

**Зависимость от количества модулей (1000 vs 500).**

PS `D:\devextreme\DevExtreme> node .\node_modules\jest\bin\jest --watch --runInBand`

combine_classes.test

...

Time: **3.444s**

...

Time: **1.71s**

С закоментаренным `./js/renovation/test_utils/setup_enzyme.ts`

Time: **2.53s**

Time: **1.004s**

**Вывод**. Запуск теста (небольшого количества тестов) в параллели неэффективен из-за роста накладных расходов на обслуживания параллельных *runner*. Чем меньше количество (*scoupe*) модулей (файлов), тем быстрее ходят тесты. Замена *enzyme* например на *react-test-renderer* даст порядка 500-700 милисек на запуск теста.

Для локальной работы, когда тесты запускаются, часто (на каждую правку кода) и их количество небольшое лучше всего их гонять с ключиками *--watch --runInBand*, либо *--watch --maxWorkers=(CPU Core -1)*.

Переход с *jest* 24 -> 26: Сильной разницы нет.
Прогон тестов в параллели: без кеша 49с (с кешем 15с)
widget.test runInBand: первый прогон 3.4c последующие 2c
