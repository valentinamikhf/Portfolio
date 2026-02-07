Добрый день! 


Этот проект представляет собой пайплайн по распознаванию лиц. Проект полностью написан в GoogleColab и включает в себя 6 ноутбуков ipynb:
- `1_FaceAlignment_part1_Dataset.ipynb` - в этом ноутбуке происходит отбор приблизительно 16 тысяч снимков из октрытого датасета CelebA. Для корректной работы данного ноутбука требуется открыть его в Colab и загрузить дополнительно файлы `identity_CelebA` и `list_landmarks_celeba` во временное файловое хранилище GoogleColab. Также в процессе выполнения ноутбука потребуется подключение к вашему GoogleDrive, в котором необходимо иметь около 1 Гб свободного места (для всех трех ноутбуков, не только для первого). Данный ноутбук в результате своей работы выгрузит на ваш диск архив с отобранными и обрезанными картинками в количестве 16 с небольшим тысяч, а также 3 файла csv для дальнейшей работы.
Файл `person_id.csv`, загруженный в папку проекта - это файл с image_id отобранных для обучения модели картинок.
- `1_FaceAlignment_part2_Model.ipynb` - этот ноутбук представляет собой реализацию модели Stacked Hourglass Network, к отороая используется дл япредсказания 5ти ключевых точек лица. 5 точек мы берем потому, что в исходном датасете было размечено именно 5 точек. Далее, результат модели в этом ноутбуке используется дл явыравнивания картинок методом аффинного преобразования. Целевым результатом исполнения ноутбука будет архив с выровненными картинками на вашем GoogleDrive, а также файл сохраненной модели `stacked_hourglass.pth` 
- `2_ArcFace.ipynb` - представляет собой реализацию модели распознавания лиц, созданной на основе предобученной ResNet50 с применением ArcFace # ArcFace Loss (Additive Angular Margin Loss). Модель обучается на массиве данных, используя метки класса (person_id). Целевым результатом работы данного ноутбука будет сохранение модели  `resnet_arcface.pth`
- `3_Pipeline.ipynb` - это финальный пайплайн решения. Он берет сохраненные на GoogleDrive обученные модели `stacked_hourglass.pth` и `resnet_arcface.pth` - для этого снова потребуется подключение к GoogleDrive. Этот ноутбук можно запускать также без прохода по трем подготовительным ноутбукам, если есть желание просто посмотреть на работу решения. Для этого нужно скачать модели по ссылкам: [stacked_hourglass.pth](https://drive.google.com/file/d/1uoeoOnA68nixbjWw2n4mcsQIF_mUBXhF/view?usp=sharing) и [resnet_arcface.pth](https://drive.google.com/file/d/1Iy9PeIxz0ejxIAFQUboj7KMOjpiZUmPJ/view?usp=sharing) и загрузить на свой Google drive в папку `/content/drive/MyDrive/DLS1` - после этого можно будет запускать этот ноутбук. Для него также необходимо подготовить несколько фотографий с изображенными на них людьми для проверки. В конце ноутбука есть исполняемые ячейки, каждай из которых просит загрузить 2 фото для сравнения. С результатом можно ознакомиться, не запуская ноутбук (в нем сохранены несколько примеров работы пайплайна)
- `2_dop. Triplet Loss.ipynb` - здесь сохранено дополнительное задание: реализация модели с Triplet Loss. 
- `2_dop_Pipeline_TripletLoss.ipynb` - здесь собран пайплайн для модели с Triplet Loss и сохранены примеры работы модели с метрикой без margin, обученной на 3х эпохах (она оказалась по работе лучше, чем на 5 эпохах). Файл с сохраненной моделью можно скачать по ссылке: [resnet_triplet_3epoch.pth](https://drive.google.com/file/d/1xQjuiWF1D_xwLoDvTam8OYGZglYTDDWC/view?usp=sharing) 


- Если указанные ноутбуки по какой-то причине не открываются, то их можно найти по ссылкам:
1. [1_FaceAlignment_part1_Dataset.ipynb](https://colab.research.google.com/drive/1rhzKXRdk9V3UYl2MEL_zIYiDcdeDjkMA?usp=sharing)
2. [1_FaceAlignment_part2_Model.ipynb](https://colab.research.google.com/drive/1aCEjhHlSFx9Pqi3yzaEgcsVQwgYTHfZj?usp=sharing)
3. [2_ArcFace.ipynb](https://colab.research.google.com/drive/195qS4F06H-GxkU1AiI6Voo708Gnqs0-N?usp=sharing)
4. [3_Pipeline.ipynb](https://colab.research.google.com/drive/1pxOsjuDnmjH9J3dWfiQfc2LLRVauOM5n?usp=sharing)
5. [2_dop. Triplet Loss.ipynb](https://colab.research.google.com/drive/1EWztF6eeSZI3VCiPCcX-Upt9DSe7Ilov?usp=sharing)
6. [2_dop_Pipeline_TripletLoss.ipynb](https://colab.research.google.com/drive/1r-JFSR4DJv0IZTm2uR7Q3sxG2woLOsBQ?usp=sharing)

   Спасибо за внимание!
