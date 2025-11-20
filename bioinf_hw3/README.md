Ссылка на коллаб: https://colab.research.google.com/drive/1FgEto99DniOw6HL4zKjR2--Y8TamBppZ?usp=sharing (также загружено в src)

# **Результаты MultiQC**

Общая статистика:
<img width="1462" height="394" alt="image" src="https://github.com/user-attachments/assets/df312ecc-3ab2-4656-a8f1-c3db4e51bf8a" />

Дупликаты:
<img width="1467" height="534" alt="image" src="https://github.com/user-attachments/assets/1fee3641-5a51-46da-b8ed-92def10faf8d" />

Качество чтений хорошее, score > 30:
<img width="1455" height="753" alt="image" src="https://github.com/user-attachments/assets/0e21cfb2-b9b1-466e-826d-777344bc0e6b" />
<img width="1458" height="752" alt="image" src="https://github.com/user-attachments/assets/23069237-9932-46ec-85d5-d019b7caf892" />

Адептеры отсутствуют: 
<img width="1456" height="165" alt="image" src="https://github.com/user-attachments/assets/5986e303-78c1-44b3-b2e0-4c4c2126dcfb" />

График показывает два пика в распределении GC-состава вместо ожидаемого одного. Такое отклонение от теоретической кривой может указывать на наличие технических артефактов или биологических особенностей образцов:
<img width="1470" height="746" alt="image" src="https://github.com/user-attachments/assets/8c585c5f-eeae-4bc0-9727-5bc6883a6477" />

Практически отсутствуют неопределенные нуклеотиды (N):
<img width="1456" height="762" alt="image" src="https://github.com/user-attachments/assets/27fea5ab-817e-45da-b820-9d87b469aebd" />

Наблюдается достаточно высокое число дупликатов, что скорее всего типично для RNA-seq и показывает, что экспрессия генов неравномерна:
<img width="1456" height="759" alt="image" src="https://github.com/user-attachments/assets/b1c198ec-148f-48c2-abee-74117612e026" />

Процентное содержание каждого нуклеотида - наблюдается смещение состава нуклеотидов в первых 10-15 bp:
<img width="1456" height="629" alt="image" src="https://github.com/user-attachments/assets/bce5fe37-768c-42f1-957f-ed1472aff1a8" />
<img width="1464" height="686" alt="image" src="https://github.com/user-attachments/assets/7f01312d-d583-492f-8942-f064a7e923a2" />

Status:
<img width="1473" height="758" alt="image" src="https://github.com/user-attachments/assets/7f4b44a9-44d1-4d82-9537-58fd75e8d5d2" />

# **Статистика**
ID | Тип образца | Общее кол-во исходных чтений | Кол-во и процент чтений, которые были успешно откартированы на геном | Кол-во и процент уникально откартированных чтений | Общее кол-во чтений, которые попали на гены
-----------|-----------------------|-----------|-------------------|------------------|----------
SRR3414629 | Перепрограммированный | 21106089 | 20865479 (98.86%) | 18573565 (88.00%) | 16224313
SRR3414630 | Перепрограммированный | 15244711 | 15077019 (98.90%) | 13320505 (87.38%) | 11583775
SRR3414631 | Перепрограммированный | 24244069 | 23965262 (98.85%) | 21159606 (87.28%) | 18613501
SRR3414635 | Контрольный | 20956475 | 20715475 (98.85%) | 18637053 (88.93%) | 16463013
SRR3414636 | Контрольный | 20307147 | 20073614 (98.85%) | 18032679 (88.80%) | 15942667
SRR3414637 | Контрольный | 20385570 | 20149097 (98.84%) | 18043406 (88.51%) | 15914380

# **Бонус**

Тепловая карта:

<img width="780" height="768" alt="image" src="https://github.com/user-attachments/assets/2e182da4-2015-4bec-87d6-6d23a1aecbc8" />

Все контрольные образцы похожи между собой, а перепрограммированные образцы - между собой. Такие кластеры доказывают присутствие дифференицальной экспрессии и хорошее качество эксперимента.

MA-plot:

<img width="640" height="589" alt="image" src="https://github.com/user-attachments/assets/eff1ce65-cc0e-41c1-832f-b237d95f3178" />

Синим цветом показаны те гены, в которых значительно изменился уровень экспрессии. Серым цветом показаны гены, в которых не произошло статистически значимых измений уровня экспрессии. Из графика видно, что множество генов значимо изменили экспрессию, наблюдаются сильные изменения - log2FC до 10 (изменение в 1000+ раз)

Тепловая карта для 20 самых экспрессированных генов:

<img width="765" height="788" alt="image" src="https://github.com/user-attachments/assets/6c469a36-44ac-4e53-8fd3-c1743e36f971" />

Из графика видно, что гены равномерно экспрессированы во всех образцах, нет разделения на контроль и перепрограммирование. Это подтверждает хорошее качество данных, так как наиболее экспрессированные гены связаны с базовыми процессами, и их экспрессия отличается слабо.

Графики со значениями "Normalized counts" в контрольных и перепрограммированных образцах для генов, которые наиболее поменяли экспрессию:

<img width="755" height="750" alt="image" src="https://github.com/user-attachments/assets/9b39d3a4-2e58-4f5c-ba83-1909ccb7c815" />

<img width="795" height="794" alt="image" src="https://github.com/user-attachments/assets/b828057b-a690-42fc-b8d8-14f32797c20e" />

<img width="798" height="776" alt="image" src="https://github.com/user-attachments/assets/9d7ca7e6-d231-421d-8923-bb86ee927b85" />

На всех графиках видно четкое разделение между группами, при этом уровень экспрессии в reprogramming в несколько раз выше чем в control. Графики демонстрируют значимую разницу уровней экспрессии.




