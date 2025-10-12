**Домашнее задание 1**

1. Создала папку bioinf_hw1 и создала символические ссылки на файлы
```
mkdir bioinf_hw1 #создание папки
cd bioinf_hw1 #переход в папку
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq #создание символической ссылки
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
```
2. Случайным образом выбрала для paired-end 5 миллионов чтений и для mate-pairs 1.5 миллиона чтений (seed = 729)
```
seqtk sample -s729 oil_R1.fastq 5000000 > sub1.fastq # перенаправляю в файл sub1.fastq
seqtk sample -s729 oil_R2.fastq 5000000 > sub2.fastq
seqtk sample -s729 oilMP_S4_L001_R1_001.fastq 1500000 > mp1.fastq
seqtk sample -s729 oilMP_S4_L001_R2_001.fastq 1500000 > mp2.fastq
```
3. Анализ с помощью fastqc
```
mkdir fastqc
fastqc -o fastqc sub1.fastq # запускаю fastqc, -o указывает папку для сохранения результатов
fastqc -o fastqc sub2.fastq
fastqc -o fastqc mp1.fastq
fastqc -o fastqc mp2.fastq
```
4. Анализ с помощью multiqc
```
mkdir multiqc
multiqc -o multiqc fastqc 
```
5. **Рассмотрим результаты работы fastqc и multiqc:**

<img width="1435" height="311" alt="image" src="https://github.com/user-attachments/assets/6f30ae5f-f900-4780-9213-ecc91ffdbe9f" />

mp1, mp2: длинные риды (251 bp), низкий уровень дубликатов (~4%), GC-состав 44%.

sub1, sub2: короткие риды (101 bp), высокий уровень дубликатов (~30%), GC-состав 46%.

<img width="1438" height="756" alt="image" src="https://github.com/user-attachments/assets/bf5a5500-f3ce-4b59-918e-95f559679e7f" />

У MP-чтений качество хуже чем у PE чтений (на концах особенно)

mp1:

<img width="1073" height="725" alt="image" src="https://github.com/user-attachments/assets/4f2e917a-f2e2-4673-8c6b-d1d5fef909c4" />

mp2:

<img width="1082" height="756" alt="image" src="https://github.com/user-attachments/assets/27e7a924-ed02-42ec-932a-c7a2df98e14d" />

sub1:

<img width="1017" height="738" alt="image" src="https://github.com/user-attachments/assets/f44f8488-131e-404d-84ca-11b473566a7e" />

sub2:

<img width="1020" height="743" alt="image" src="https://github.com/user-attachments/assets/446d24cb-724b-4d81-a1af-e29752f096c5" />

Адаптеры найлены на mp1 и mp2:

<img width="1435" height="728" alt="image" src="https://github.com/user-attachments/assets/02acd184-0b5d-4e69-82a8-18b471a41ec4" />

Адаптеры на mp1:

<img width="1071" height="741" alt="image" src="https://github.com/user-attachments/assets/5369425e-ec28-45fc-abcf-10d8c8304d95" />

Адаптеры на mp2:

<img width="1050" height="752" alt="image" src="https://github.com/user-attachments/assets/4c4b4f0c-6621-4841-824b-a6133d7f9989" />

Дупликаты: графики также демонстрируют, что у PE чтений больше дупликатов

<img width="1431" height="774" alt="image" src="https://github.com/user-attachments/assets/044e09ba-9ccf-4f68-8f26-b01be0c863c3" />

<img width="1428" height="726" alt="image" src="https://github.com/user-attachments/assets/e077c2fa-4de2-4a01-b8a2-6b37d8452769" />

Status: качество PE чтений, в целом, лучше

<img width="1423" height="782" alt="image" src="https://github.com/user-attachments/assets/34d36893-28b7-45ad-821f-7de538a04d04" />

6. Подрезала чтения и удалила адаптеры:
```
platanus_trim sub1.fastq sub2.fastq
platanus_internal_trim mp1.fastq mp2.fastq
```

7. Удалила исходные файлы:
```
rm sub1.fastq 
rm sub2.fastq
rm mp1.fastq
rm mp2.fastq
```

8. Оценила подрезанные чтения с помощью fastqc и multiqc:
```
mkdir fastqc_trimmed
fastqc -o fastqc_trimmed sub1.fastq.trimmed
fastqc -o fastqc_trimmed sub2.fastq.trimmed
fastqc -o fastqc_trimmed mp1.fastq.int_trimmed
fastqc -o fastqc_trimmed mp2.fastq.int_trimmed
```
```
mkdir multiqc_trimmed
multiqc -o multiqc_trimmed fastqc_trimmed
```
9. **Рассмотрим результаты работы fastqc и multiqc:**

<img width="1456" height="298" alt="image" src="https://github.com/user-attachments/assets/c70dbbac-3e0f-47c2-9c74-d02d985f07f9" />

Теперь график с распределением качества чтений по длине показывает хорошие результаты, score везде > 30:

<img width="1425" height="732" alt="image" src="https://github.com/user-attachments/assets/a2bdb826-2437-4fab-9acc-b8b902325bd0" />

sub1:

<img width="1011" height="746" alt="image" src="https://github.com/user-attachments/assets/d29a65fe-cdcf-4529-93fd-5af769992eac" />

sub2:

<img width="1020" height="746" alt="image" src="https://github.com/user-attachments/assets/e4305bfc-675a-4743-8c13-aeeb898f60f6" />

mp1:

<img width="1073" height="755" alt="image" src="https://github.com/user-attachments/assets/665d0916-488b-4bb6-82bf-e7fc3fd8891d" />

mp2:

<img width="1077" height="755" alt="image" src="https://github.com/user-attachments/assets/3afd80af-a2e3-43cd-af0d-39410da98444" />

Адаптеры теперь отсутствуют:

mp1:

<img width="1070" height="746" alt="image" src="https://github.com/user-attachments/assets/0f4a80c0-ec26-4e52-b4dc-cae639a10dd3" />

mp2:

<img width="1067" height="747" alt="image" src="https://github.com/user-attachments/assets/780ba00a-08b2-4fb4-8ba1-d224fb5c28ca" />

Status:

<img width="1437" height="761" alt="image" src="https://github.com/user-attachments/assets/77f0e386-4c04-4c97-97ef-2e290a7d718d" />

10. С помощью platanus assemble собираю контиги из подрезанных чтений (PE чтения)
```
# -o: выходные файлы получат префикс Contigi
# -f: указывает, что следующие аргументы - файлы для сборки
# 2> assemble.log: перенаправляет ошибки, служебные сообщения, предупреждения в файл assemble.log
platanus assemble -o Contigi -f sub1.fastq.trimmed sub2.fastq.trimmed 2> assemble.log
```

11. Проанализировала контиги, результаты:
```
Общее количество контигов:  610
Общая длина:  3924957
Длина самого длинного контига:  179307
Длина самого короткого контига:  87
Средняя длина контига:  6434.355737704918
N50:  53970
```

Ссылка на гугл коллаб: https://colab.research.google.com/drive/1Fgj0wJ1O1yryR37DPXxKnSTvFmNhtfl7?usp=sharing

Также загрузила файл ipynb в src 

12. С помощью программы “ platanus scaffold” собираю скаффолды из контигов, а также из подрезанных чтений:
```
# -o указывает префикс для выходных файлов
# -c указывает файл с контигами
# -IP1 указывает чтения PE
# -OP2 указывает чтения MP
# 2> scaffold.log - сохранение логов в файл
platanus scaffold -o scaffolds -c Contigi_contig.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 mp1.fastq.int_trimmed mp2.fastq.int_trimmed 2> scaffold.log
```

13. Проанализировала скаффолды, результаты:
```
Общее количество скаффолдов:  64
Общая длина:  3873859
Длина самого длинного скаффолда:  3838161
Длина самого короткого скаффолда:  102
Средняя длина скаффолда:  60529.046875
N50:  3838161
```
**Весь код находится в одном блокноте, ссылка в п.11**

14. Для самого длинного скаффолда посчитала количество гэпов и их общую длину, результаты:
```
Длина самого длинного скаффолда:  3838161
Количество гэпов:  64
Общая длина гэпов:  6638
```
15. С помощью программы platanus gap_close уменьшила кол-во гэпов с помощью подрезанных чтений:
```
# флаги как в п.12
platanus gap_close -o scaffolds_closed -c scaffolds_scaffold.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 mp1.fastq.int_trimmed mp2.fastq.int_trimmed 2> gap_close.log
```
16. Удалила  .fastq файлы, содержащие подрезанные чтения:
```
rm sub1.fastq.trimmed sub2.fastq.trimmed mp1.fastq.int_trimmed mp2.fastq.int_trimmed
```
17. После уменьшения гэпов для самого длинного скаффолда посчитала количество гэпов и их общую длину, результаты:
```
Длина самого длинного скаффолда:  3871074
Количество гэпов:  8
Общая длина гэпов:  2225
```
18. Бонусная часть
```
mkdir bonus #создание папки внутри bioinf_hw1
cd bonus #переход в папку
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq #создание символической ссылки
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
```
Случайным образом выбрала для paired-end 1 миллион чтений и для mate-pairs 0.5 миллиона чтений (seed = 729)
```
seqtk sample -s729 oil_R1.fastq 1000000 > sub1.fastq # перенаправляю в файл sub1.fastq
seqtk sample -s729 oil_R2.fastq 1000000 > sub2.fastq
seqtk sample -s729 oilMP_S4_L001_R1_001.fastq 500000 > mp1.fastq
seqtk sample -s729 oilMP_S4_L001_R2_001.fastq 500000 > mp2.fastq
```
Выполняю все команды, аналогично основной части задания

Результаты:
| | 5 миллионов чтений paired-end и 1.5 миллиона чтений mate-pairs|1 миллион чтений paired-end и 0.5 миллиона чтений mate-pairs |
|-|---------------------------------------------------------------|-------------------------------------------------------------|
| количество контигов| 610 | 1277 |
| количество скаффолдов| 64 | 154 |
| N50 для контигов| 53970 | 60218 |
| N50 для скаффолдов| 3871074 | 2912174 |
| длина самого длинного контига| 179307 | 187087|
| длина самого длинного скаффолда| 3871074 | 2912174 |
| количество гэпов в самом длинном скаффолде| 8 | 23 |
-----------------------------------------------------

При уменьшении данных наблюдаются ожидаемые изменения:

1) Контиги: увеличение количества
2) Скаффолды: увеличение количества, снижение N50 
3) Гэпы: увеличение количества

Небольшой рост N50 для контигов может быть связан со случайностью выборки














