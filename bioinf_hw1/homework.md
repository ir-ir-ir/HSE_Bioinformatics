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
5. Итоговые файлы находятся в bioinf_hw1/analusis_before_сutting
*Рассмотрим результаты работы fastqc и multiqc:*

