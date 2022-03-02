# Домашнее задание к занятию " Выстраивание процесса непрерывной интеграции"
# Задание 1. Синдром 100% (обязательное к выполнению)

Вы попали в команду максималистов, которые хотят, чтобы те авто-тесты, которые вы пишете, покрывали код на 100%.

Но вот незадача:
1. Непонятно, что такое 100%
2. Непонятно, как это сделать

Вспоминаем: покрытием кода у нас занимается JaCoCo, но он просто "сигнализирует" о том, что конкретно пошло не так.

Большинство подобных плагинов помимо целей отчётности (`report`) содержат ещё цель `check`, которая обрушает сборку, если не выполнены определённые проверки.

Что вам нужно:
1. Создать мавен-проект с тестируемым кодом из листинга кода (указан ниже по условию)
1. Изучить [документацию на плагин](https://www.eclemma.org/jacoco/trunk/doc/maven.html) (а конкретно на цель `check`)
1. Внедрить эту цель в фазу `verify` (обратите внимание, что эта цель итак публикуется в эту фазу)
1. Настроить правила по покрытию на 100% (при этом нужно изучить разницу между счётчиками `INSTRUCTION`, `LINE`, `BRANCH`, `COMPLEXITY`)
1. Вникнуть в тестируемый код
1. Выбрать один из счётчиков и добиться 100% покрытия через добавление новых тестов

**Важно**: использовать можно только один из следующих: 
1. `INSTRUCTION`
1. `LINE`
1. `BRANCH`

Обратите внимание на чеклист в начале условия, он содержит подсказки по внедрению JaCoCo в ваш мавен-проект.

Тестируемый код:
```java
package ru.netology.statistic;

public class StatisticsService {
  /**
   * Calculate index of max income
   *
   * @param incomes - array of incomes
   * @return - index of first max value
   */
  public long findMax(long[] incomes) {
    long current_max_index = 0;
    long current_max = incomes[0];
    for (long income : incomes)
      if (current_max < income)
        current_max = income;
        return current_max;
  }
}
```

Класс с тестами (его надо будет расширить новыми тестами):
```java
package ru.netology.statistic;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

public class StatisticsServiceTest {

  @Test
  void findMax() {
    StatisticsService service = new StatisticsService();

    long[] incomesInBillions = {12, 5, 8, 4, 5, 3, 8, 6, 11, 11, 12};
    long expected = 12;

    long actual = service.findMax(incomesInBillions);

    assertEquals(expected, actual);
  }
}
```

Итого: отправьте на проверку ссылку на гитхаб-репозиторий с вашим проектом.
