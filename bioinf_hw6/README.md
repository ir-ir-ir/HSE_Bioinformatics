# Домашняя работа: CpG метилирование ДНК при раннем эмбриональном развитии мыши

## Анализ QC 
Так как данные очень большие, провела FastQC анализ только для образца SRR5836473

*Какие особенности можно наблюдать по сравнению с секвенированием ДНК или РНК?*

<img width="973" height="737" alt="image" src="https://github.com/user-attachments/assets/67995060-fdd8-4036-a6eb-77e96c2179f9" />

В обычном секвенировании ДНК/РНК график GC содержания имеет один пик, распределение близко к нормальному распределению. Линия, показывающая теоретическое распределение близка к реальным результатам. В данном случае, после бисульфитной конверсии, на графике два пика, левый пик значительно больше, теоретическая линия совсем не совпадает с реальными результатами.

После бисульфитной коверсии: 

  - неметилированная ДНК: цитозины превратились в тимины - GC-состав низкий - образуется левый пик, который значительно выше по количеству ридов.
  - метилированная ДНК: метилированные цитозины сохранились - GC-состав высокий - образует правый пик, который ниже по количеству ридов.

<img width="974" height="732" alt="image" src="https://github.com/user-attachments/assets/c0de48e0-1c89-41bc-9f82-20615fbff5d0" />

На данном графике видно, что содержание C низко (около 10), в то время как содеражние T большое (около 40). Это объясняется превращением неметилированных цитозинов в тимины. В обычном секвенировании ДНК/РНК не наблюдается такого преобладания тимина над цитозином.

Качество чтений в целом хорошее. Есть небольшие ухудшения в конце:

<img width="944" height="725" alt="image" src="https://github.com/user-attachments/assets/3a392655-e644-4664-baa5-8cc7d04fcf45" />

*Отчеты html загружены в папку data. Скрины отчетов приложены в html_screens*

## Cводная таблица с числом ридов, закартированных на заданные участки 

| Образец                    | 11347700-11367700 | 40185800-40195800|
|----------------------------|-------------------|------------------|
|SRR5836473 (8 Cell)         |551                |194               |
|SRR5836475 (ICM)            |797                |274               |
|SRR3824222 (Epiblast)       |1344               |565               |

## Дедупликация файлов выравниваний

| Образец              | Уникальные прочтения | Процент уникальных | Процент дуплицированных |
|----------------------|---------------------|---------------------|-------------------------|
| SRR5836473 (8 Cell)  | 2,335,658           | 81.72%              | 18.28%                  |
| SRR5836475 (ICM)     | 3,791,973           | 90.93%              | 9.07%                   |
| SRR3824222 (Epiblast)| 6,846,444           | 97.09%              | 2.91%                   |

## Коллинг метилирования цитозинов

*Скриншоты M-bias plot:*

На M-bias графиках для всех трех образцов видно: для read1 уровень метилирования равномерен по всей длине рида, для read2 есть колебания в начале и конце последовательности. Причиной этого являются неметилированные цитозины, которые содержатся в адаптерах. Артефакты на read2 выражены сильнее из-за особенностей парноконцевого секвенирования.

Для 8 Cell:
<img width="1508" height="862" alt="image" src="https://github.com/user-attachments/assets/8676204f-c289-4576-9d18-42ed53f78abc" />
<img width="1497" height="759" alt="image" src="https://github.com/user-attachments/assets/19b024bc-e006-4fbd-a206-f6a80f784a1d" />

Для ICM:
<img width="1514" height="864" alt="image" src="https://github.com/user-attachments/assets/6b7e5f25-7c65-480b-9bea-d59b715152d8" />
<img width="1477" height="713" alt="image" src="https://github.com/user-attachments/assets/c27c656c-2553-41eb-a617-d773a0cc0783" />

Для Epiblast:
<img width="1502" height="855" alt="image" src="https://github.com/user-attachments/assets/84e84cc3-b3ec-4496-b148-252709593aa6" />
<img width="1473" height="749" alt="image" src="https://github.com/user-attachments/assets/59141314-9220-4a1f-b7f5-2b69c56c1adf" />

*Отчеты html загружены в папку data*

## Гистограммы распределения метилирования цитозинов по хромосоме

### Код построения

```python
import pandas as pd
import matplotlib.pyplot as plt
import gzip

# функция для построения гистограммы
def plot_methylation_histogram(cov_file, sample_name, coverage_threshold=10):
    """
    cov_file: путь к файлу .cov.gz
    sample_name: название образца для заголовка
    coverage_threshold: минимальная глубина покрытия для фильтрации
    """

    # чтение файла
    with gzip.open(cov_file, 'rt') as f:
        df = pd.read_csv(f, sep='\t', header=None,
                         names=['chr', 'start', 'end', 'percent', 'methylated', 'unmethylated'])

    # расчет глубины покрытия
    df['coverage'] = df['methylated'] + df['unmethylated']

    # статистика до фильтрации
    total_sites = len(df)
    print(f"\n{sample_name}:")
    print(f"всего позиций: {total_sites}")
    print(f"средняя глубина покрытия: {df['coverage'].mean():.2f}")

    # фильтрация по глубине
    filtered = df[df['coverage'] >= coverage_threshold]
    filtered_sites = len(filtered)
    print(f"позиций с покрытием >= {coverage_threshold}: {filtered_sites} ({100*filtered_sites/total_sites:.1f}%)")

    # построение гистограммы
    plt.figure(figsize=(10, 6))
    plt.hist(filtered['percent'], bins=50, edgecolor='black', alpha=0.7, color='steelblue')
    plt.xlabel('процент метилирования (%)')
    plt.ylabel('количество позиций (частота)')
    plt.title(f'{sample_name}\nРаспределение метилирования (покрытие >= {coverage_threshold}, n = {filtered_sites})')
    plt.grid(True, alpha=0.3)
    plt.show()


# вызов функции для трех образцов
plot_methylation_histogram('SRR5836473_1_dedup.deduplicated.bismark.cov.gz', '8-cell')
plot_methylation_histogram('SRR5836475_1_dedup.deduplicated.bismark.cov.gz', 'ICM')
plot_methylation_histogram('SRR3824222_1_dedup.deduplicated.bismark.cov.gz', 'Epiblast')
```

### Графики

<img width="892" height="565" alt="image" src="https://github.com/user-attachments/assets/58363a43-f38e-422f-82ba-8251597942f2" />
<img width="864" height="573" alt="image" src="https://github.com/user-attachments/assets/771f1b94-706b-4357-9260-b2ace9e68f71" />
<img width="894" height="561" alt="image" src="https://github.com/user-attachments/assets/7e942858-fdb3-4c13-9398-c057f0cdf5d6" />

 Для надежности данных был выбран порог покрытия = 10, при этом абсолютное количество ридов достаточно для анализа.
 На графиках видна четкая тенденция: уровень метилирования снижается к стадии ICM, затем возрастает к стадии Epiblast, что подтверждает результаты исходного исследования. 











