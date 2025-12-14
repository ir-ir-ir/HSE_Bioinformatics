# Ссылка на ноутбук

https://colab.research.google.com/drive/1Kq9RZonUF1yzjkyo1unUF-mF1qcb1RTQ?usp=sharing

Также загрузила ноутбук в папку src

# Описание метода нормализации данных 

Так как для TPM необходимо знать длины генов, в данном анализе была применена упрощенная нормализация, CPM (Counts Per Million), которая учитывает только различия в общей глубине секвенирования между клетками

CPM = (counts / total_counts_in_cell) * 1,000,000

# Heatmap для экспрессии маркерных генов

<img width="1477" height="428" alt="image" src="https://github.com/user-attachments/assets/f9e88a3d-6b87-49d9-8ce6-72824cac5e36" />

На тепловой карте показан уровень экспрессии исследованных маркерных генов. Благодаря сортировке по кластерам, которые определили авторы статьи, клетки упорядочены по их биологическому типу или состоянию. На тепловой карте все клетки одной группы стоят рядом, образуя блок с одинаковым уровнем экспрессии.

# Полученные визуализации UMAP и PCA

## PCA

<img width="846" height="579" alt="image" src="https://github.com/user-attachments/assets/bd4220a5-ec59-4338-9eeb-ef5c81ceb7dd" />

Разные виды клеток образуют группы на графике, однако cTEC и mTEC-III не выделены также четко, как остальные группы. Распределение клеток в пространстве PCA отражает их биологические взаимосвязи.

## UMAP

<img width="838" height="577" alt="image" src="https://github.com/user-attachments/assets/91f55f36-676d-401e-b95d-1d6a27f93923" />

UMAP показывает более четкое разделение типов клеток по сравнению с PCA. Кластеры стали компактнее и лучше обособлены. Однако cTEC и mTEC-III по-прежнему остаются менее выделенными.

## Экспрессия маркерных генов на UMAP

<img width="811" height="640" alt="image" src="https://github.com/user-attachments/assets/7d2559c9-aa63-468c-b5bd-ad3349fbfaa9" />

<img width="805" height="638" alt="image" src="https://github.com/user-attachments/assets/c9513d0d-042c-4acb-aaad-6039f5548da2" />

<img width="797" height="641" alt="image" src="https://github.com/user-attachments/assets/2738e5e2-d4c1-40fd-8aa2-6e2c3de405a0" />

<img width="802" height="641" alt="image" src="https://github.com/user-attachments/assets/db653944-5452-4196-83e3-175f957b1212" />

<img width="801" height="647" alt="image" src="https://github.com/user-attachments/assets/7675d231-92ac-4c61-b1ff-624823433fa8" />

1.  Ген Ctsl: сильно экспрессированный ген, экспрессируется во всех кластерах, но наиболее сильно - в кластерах mTEC-I и cTEC

2.  Ген Psmb11: наиболее сильно экспрессирован в кластере cTEC

3.  Ген Prss16: есть экспрессия во всех кластерах, но в целом экспрессирован мало,наиболее сильно экспрессирован в кластере cTEC

4.  Ген Ascl1:  сильно экспрессированный ген, относится к кластеру mTEC-I

5.  Ген Sox4: самый экспрессированный ген из 5 представленных, экспрессируется во всех кластерах, но наиболее сильно в кластерах mTEC-I и mTEC-IV

## Сравнение уровней экспрессии генов, полученных по scRNA-seq (подгруппа  mTEC-IV) с классическим bulk RNA-seq

<img width="1134" height="853" alt="image" src="https://github.com/user-attachments/assets/8449df16-a6be-4b0f-bfde-9f81f797eb53" />

<img width="1140" height="858" alt="image" src="https://github.com/user-attachments/assets/fbe07255-8b54-4a34-b1aa-8b6675091896" />
Вывод: наблюдается расхождение между bulk RNA-seq и scRNA-seq данными для высокоэкспрессируемых генов, в то время как слабо экспрессируемые гены демонстрируют относительно неплохую корреляцию между двумя методами. Часть генов, которая находится в области высокой экспрессии, демонстрирует значительные отклонения от линии, а гены с невысокой экспрессией находятся относительно близко к x=y.
