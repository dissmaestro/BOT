**Задание на лабораторную работу**
1. С помощью неблокируемых операций точечного взаимодействия реализовать каждую из функций коллективного взаимодействия (MPI_Barrier, MPI_Bcast, MPI_Gather, MPI_Scatter, MPI_Allgather, MPI_Alltoall).
2. Произвести экспериментальное сравнение времени выполнения разработанных функций с функциями коллективного взаимодействия для разного количества передаваемых данных.
3. Реализовать алгоритм перемножения матриц с использованием функций коллективного взаимодействия.

**1. Программы реализующие коллективное взаимодействие**

**1.1. MPI_barrier**

Для компиляции программы нужно ввести команду:
```bash
mpic++ -o barrier barrier.cpp
``` 
Для запуска программы нужно ввести команду:
```bash
mpirun -np 4 barrier
```
Результат выполнения программы:
```bash
Time with barrier:
rank=1   time=5.0001
rank=0   time=5.0002
rank=2   time=5.0001
rank=3   time=5.0002
```

**1.2. MPI_Bcast**

Для компиляции программы нужно ввести команду:
```bash
mpic++ -o bcast bcast.cpp
``` 
Для запуска программы нужно ввести команду:
```bash
mpirun -np 4 bcast -r 0 -s 5
```
Результат выполнения программы:
```bash
mybcast rank=0, buffer=mmmm,  time=0.000011 
MPI_Bcast rank:0 buffer=mmmm  time:0.000003 
rank=1, buffer=mmmm 
rank=2, buffer=mmmm 
rank=3, buffer=mmmm 
```

**1.3. MPI_Gather**

Для компиляции программы нужно ввести команду:
```bash
mpic++ -o gather gather.cpp
``` 
Для запуска программы нужно ввести команду:
```bash
mpirun -np 4 gather -r 0 -s 6
```
Результат выполнения программы:
```bash
Time MY_Gather: 0.000128
recv = "MMMMMNNNNNOOOOOPPPPP"
Time MPI_Gather: 0.000018
rank=1, send: "NNNNN"
rank=2, send: "OOOOO"
rank=3, send: "PPPPP"
```

**1.4. MPI_Scatter**

Для компиляции программы нужно ввести команду:
```bash
mpic++ -o scatter scatter.cpp
``` 
Для запуска программы нужно ввести команду:
```bash
mpirun -np 4 scatter -r 0 -s 6
```
Результат выполнения программы:
```bash
rank:2, recv : "CDEFGH"
rank:3, recv : "DEFGHI"
Time MY_Scatter: 0.000222
rank:0, send: ABCDEF     BCDEFG          CDEFGH          DEFGHI
rank:0, recv : "ABCDEF"
Time MPI_Scatter: 0.000008
rank:1, recv : "BCDEFG"
```

**1.5. MPI_Allgather**

Для компиляции программы нужно ввести команду:
```bash
mpic++ -o allgather allgather.cpp
``` 
Для запуска программы нужно ввести команду:
```bash
mpirun -np 4 allgather -s 4
```
Результат выполнения программы:
```bash
rank:2, send: IJKL      recv: ABCD      recv: EFGH      recv: IJKL      recv: MNOP 
Time MY_Allgether: 0.000123
rank:3, send: MNOP      recv: ABCD      recv: EFGH      recv: IJKL      recv: MNOP 
Time MPI_Allgather: 0.000008
rank:0, send: ABCD      recv: ABCD      recv: EFGH      recv: IJKL      recv: MNOP 
rank:1, send: EFGH      recv: ABCD      recv: EFGH      recv: IJKL      recv: MNOP 
```

**1.6. MPI_Alltoall**

Для компиляции программы нужно ввести команду:
```bash
mpic++ -o alltoall alltoall.cpp
``` 
Для запуска программы нужно ввести команду:
```bash
mpirun -np 4 alltoall
```
В данном случае 1_2 исполняемый файл полученый компиляцией файла 1_2.с. 
Результат выполнения программы:
```bash
rank:0, send=[ 1 2 3 4 ]        recv:[ 1 13 9 5 ]
rank:1, send=[ 5 6 7 8 ]        recv:[ 2 10 14 6 ]
rank:2, send=[ 9 10 11 12 ]     recv:[ 3 7 11 15 ]
Time MY_Alltoall: 0.000215
rank:3, send=[ 13 14 15 16 ]    recv:[ 4 8 12 16 ]
Time MPI_Alltoall: 0.000014
```


**Вывод**
В результате выполнения лабораторной работы были получены навыки по базовым операциям MPI - получение ранга, количества процессов, имя узла. Было проведено исследование зависимости времени приема/передачи сообщения при увеличении размера сообщения. Так же было проверено,что время выполнения блокированного приема/передачи выполняется дольше чем неблокированного. Было произведено транспонирование матрицы несколькими процессами.
