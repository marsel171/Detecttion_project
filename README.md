Классификатор нейтрального лица
=====================
Классификатор нейтрального лица. Данная задача разбивается на две:
Классификатор открытого рта
Классификатор улыбки

Задача опирается на стандартную разметку 68 ключевых антропометрических точек лица (landmark'и), которая использовалась в [MULTI-PIE](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2873597/). 

Программа по набору путей до фотографий выводит 2 списка (по одному для каждого классификатора) фотографий, проходящих соответствующий фильтр.

Обучающая выборка из landmark'ов находится в файле X.mat.

Данные с метками находятся в файлах y_om.mat (neutral = 0, open mouth = 1) и y_smile.mat (neutral = 0, smile = 1).

Соответственно, обучение происходит как для open_mouth, где в качестве меток берутся y_om, так и для smile, где в качестве меток берутся y_smile.

В качестве классификатора используется простой линейный классификатор SVM метод опорных векторов, который дает в среднем 87% точности при тестах с разделением обучающей выборки 50/50 и 80/20. Также использовался классификатор Гауссов наивный байесовский классификатор, который давал схожие результаты при тестах. В итоге был взят классификатор SVM.

Для вычисления положений landmark'ов по тестируемому изображению использовались данные shape_predictor_68_face_landmarks.dat (не представлена в репозитории) а также dlib (устновка по инструкции Marco D.G. в https://stackoverflow.com/questions/41912372/dlib-installation-on-windows-10).

Запуск производится с командной строки, например:
python Detection_project_GIT.py "img1.jpg" "img2.jpg"

На выходе получаем классификацию для каждого тестируемого изображния и каждого случая, например:

Detection image  img1.jpg
Open mouth detection:
neutral : 0.0 (3.0 %)
open mouth : 1.0 (97.0 %)
Smile detection:
neutral : 1.0 (100.0 %)
smile : 0.0 (0.0 %)

Detection image  img2.jpg
Open mouth detection:
neutral : 1.0 (99.0 %)
open mouth : 0.0 (1.0 %)
Smile detection:
neutral : 1.0 (97.0 %)
smile : 0.0 (3.0 %)
