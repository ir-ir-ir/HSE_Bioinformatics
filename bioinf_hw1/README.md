**Домашнее задание 1**

1. Создала папку bioinf_hw1 и создала символические ссылки на файлы
```
mkdir bioinf_hw1
cd bioinf_hw1
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
```
2. Случайным образом выбрала для paired-end 5 миллионов чтений и для mate-pairs 1.5 миллиона чтений (seed = 729)
```
seqtk sample -s729 oil_R1.fastq 5000000 > sub1.fastq
seqtk sample -s729 oil_R2.fastq 5000000 > sub2.fastq
seqtk sample -s729 oilMP_S4_L001_R1_001.fastq 1500000 > mp1.fastq
seqtk sample -s729 oilMP_S4_L001_R2_001.fastq 1500000 > mp2.fastq
```
3. Анализ с помощью fastqc
```
mkdir fastqc
fastqc -o fastqc sub1.fastq
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













