[![DOI](https://zenodo.org/badge/1016023671.svg)](https://doi.org/10.5281/zenodo.16307596)

# 1. Организация файлов

```

├── code/
│   ├── dataset.py    # Загрузчик датасета
│   ├── model.py      # Определение модели
│   └── main.py       # Пайплайн обучения
├── im_train/         # Обучающие изображения (.png)
├── mask_train/       # Маски для обучения (0 - 255(нормализованные))
├── im_val/           # Валидационные изображения
├── mask_val/         # Валидационные маски
├── im_test/          # Тестовые изображения
└── mask_test/        # Тестовые маски

```
# 2. Команда "train" или старт обучения модели
```cmd
python main.py train
```
 Для начала обучения модели при запуске программы следует написать в консоль **train**. В модели есть следующие изменяемые параметры

```python
epochs_max = 5             # Количество эпох обучения
batch_size = 8             # Настройка в зависимости от памяти GPU
input_image_reshape = (128, 128)  # Размер входных изображений
foreground_class = 255     # Значение пикселя объекта на маске
adam_lr = 2e-4             # Скорость обучения
```

### Также есть возможность изменять исходные директории
``` python
main_dir = Path(__file__).parent.parent # Корневая папка
val_dir = os.path.join(main_dir, "im_val") # Изображения для валидационной выборки
mask_val_dir = os.path.join(main_dir, "mask_val") # Маски для валидационной выборки
mask_train_dir = os.path.join(main_dir, "mask_train") # Маски для обучающей выборки
train_dir = os.path.join(main_dir, "im_train") # Изображения для обучающей выборки
mask_test_dir = os.path.join(main_dir, "mask_test") # Маски для тестовой выборки
test_dir = os.path.join(main_dir, "im_test") # Изображения для тестовой выборки (будут видны в конце)
```
### Выходные данные будут находится в следующих директориях

```

└── output_images/
    ├── train_val_losses.png     # Графики потерь
    ├── output_0.png             # Примеры предсказаний
    ├── output_1.png             # (вход + маски)
    └── ...
```

### Консоль выводит метрики:

```log
Test Loss: 0.123, IoU Score: 0.85, Accuracy: 0.92, F1 score: 0.88
Trained model saved as: modellll.bin(название вашей модели)
```

# 3. Команда "run" или старт модели из загруженного файла
```cmd
python main.py run
```
При запуске команды **run**, то код запустит уже обученную модель и единственное что вы можете сделать это поменять файлы в mask_test или в im_test (см. выше)
Если у вас нет маски к тестовому изображению, то в папку mask_test положите то же изображение что и im_test. Выходные изображения будут находиться в output_dir.

# 4. Команда "GUI" или запуск графического интерфейса
```cmd
python main.py GUI
```
## Ссылка на документаци графического интерфейса: [GUI](https://github.com/AnDrEUs35/APP_for_seeking_oil/blob/main/GUI.md)

