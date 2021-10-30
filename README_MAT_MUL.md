# HPC_matrix_multi_GPU
## Задание
1 лабораторная по высокопроизводительным вычислениям.

Задача: реализовать алгоритм перемножения матриц

Язык: C++ или Python

Входные данные: 2 матрицы размером от 100х100 до 2000х2000 каждая.

Выходные данные: проверка корректности перемножения + время вычисления

Реализация должна содержать 2 функции перемножения матриц: на CPU и на GPU с применением CUDA.

Отчет о проделанной лабораторной работе - это git-репозиторий с исходным кодом реализации + описание проделанной работы там же в readme. Необходимо описать реализацию, объяснив, что конкретно было распараллелено и почему.

Провести эксперименты: перемножить матрицы разных размеров, посчитать ускорение. Результаты привести в виде таблицы/графика.


## Техническое обеспечение:
1) Графические процессоры, доступные в Colab, часто включают Nvidia K80s, T4s, P4s и P100s. Невозможно выбрать, к какому типу графического процессора вы можете подключиться в Colab в любой момент времени. 
2) Процессор Intel(R) Core(TM) i3-3110M CPU @ 2.40GHz   2.40 GHz
3) ОЗУ -  8,00 ГБ (доступно: 7,71 ГБ)
4) Система - Windows 10 (версия - 20H2) 
5) Язык реализации программы - Python 3.7.0

## Описание
На вход функцииям подается 2 матрицы, случайно сгенерированные с помощью np.random.random размеров НхН(Н - 128/256/512/1024).

Реализовано 3 функции в отдельных блоках "гугл коллаба" и в последнем блоке 2 строки показывают - что перемножение матриц было произведено без ошибок.

И был использован компилятор "numba jit", который переводит сколько возможно когда python - в машинный код, тем самым ускоряя процесс выполнения программы.

## Таблица
<table border="0" cellpadding="0" cellspacing="0" id="sheet0" class="sheet0 gridlines">
<col class="col0">
<col class="col1">
<col class="col2">
<tbody>
<tr class="row0">
<td class="column0 style2 s">Shape</td>
<td class="column1 style1 s">CPU</td>
<td class="column2 style1 s">CPU-jit</td>
<td class="column3 style1 s">GPU</td>
</tr>
<tr class="row1">
<td class="column0 style1 n">128</td>
<td class="column1 style3 n">1.339</td>
<td class="column2 style3 n">0.202</td>
<td class="column3 style3 n">0.230</td>
</tr>
<tr class="row2">
<td class="column0 style1 n">256</td>
<td class="column1 style3 n">9.711</td>
<td class="column2 style3 n">0.241</td>
<td class="column3 style3 n">0.220</td>
</tr>
<tr class="row3">
<td class="column0 style1 n">512</td>
<td class="column1 style3 n">1:18.000</td>
<td class="column2 style3 n">0.545</td>
<td class="column3 style3 n">0.237</td>
</tr>
<tr class="row4">
<td class="column0 style1 n">1024</td>
<td class="column1 style3 n">10:45.187</td>
<td class="column2 style3 n">2.862</td>
<td class="column3 style3 n">0.407</td>
</tr>
</tbody>
</table>


## Вывод
При малом размере матриц от 100 до 200 уже заметна разница по времени при вычислениях на CPU без jit и в 2х других случаях(CPU с jit и GPU).
Чем больше будет размер матрицы, тем больше будет разница по времени.
Но при использовании компилятора jit, разница времени перемножения матриц на CPU и GPU меньше.