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
