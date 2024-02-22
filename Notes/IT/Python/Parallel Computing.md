GIL - Global Interpreter Lock
The GIL locks the non-running threads. Only one can run at the time

CPU bound vs IO Bound
There is no point in making threads in python if the program is CPU bound because of the GIL
If the program is CPU bound you  can make processes. Up to one for each processor in your computer

Threads vs Process
Threads are lightweight and share memory. No isolation. GIL limitation
Process use separate memory and are resource heavy. Isolated. No GIL limitation

Memory Sharing
Two choices:
	IPC - Inter-Process communication
		Message Passing
	Shared Memory

Race Condition
Ocurre cuando dos threads acceden a la misma memoria y la modifican provocando inconsistencias.
Se corrige con Mutex.

Mutex ( Locks)
Cacho de código que fuerzas a que solo un hilo acceda simultáneamente.
from threading import Thread, Lock
            self.mutex.acquire()
            self.money += 10
            self.mutex.release()
Cuando se adquiere el lock estás provocando que otros threads no puedan acceder a ese pedazo de código hasta que el lock se libera
Hay además que intentar no llamar a .acquire y .release muy a menudo porque son funciones que tardan en ejecutarse. Mejor agrupar todo en un bloque y encapsular todo el bloque en las claúsulas .acquire y .release.

Condition Variables
Tiene las mismas propiedas de los Locks más otras extra:
	acquire (igual que lock)
	release (igual que lock)
	wait -> If the condition is not what you want you make the thread wait
	notify -> Notify the threads to check the condition again
	notify_all

```
class StingySpendy:

    money = 100

    cv = Condition()

  

    def stingy(self):

        for i in range(1000000):

            self.cv.acquire()

            self.money += 10

            self.cv.notify()

            self.cv.release()

        print("Stingy Done")

  

    def spendy(self):

        for i in range(1000000):

            self.cv.acquire()

            while self.money < 20:

                self.cv.wait()

            self.money -= 20

            if self.money < 0:

                print("Money in the end of the day: ", self.money)

            self.cv.release()

        print("Spendy Done")

  
  

ss = StingySpendy()

t1 = Thread(target=ss.stingy).start()

t2 = Thread(target=ss.spendy).start()
```



Barriers
Para la sincronizar la ejecución de varios threads. 
Detiene la ejecución de threads hasta que pasa algo.
Las barreras se inician así 
```
barrier = Barrier(4)
```
Cada hilo que llame a barrier con `barrier.wait()` detendrá su ejecución.
Caundo haya 4 llamadas a `barrier.wait()` todos los hilos arrancarán simultáneamente.
Si tienes tres hilos que hacen cosas y el hilo principal hace un trabajo previo puedes usar `barrier = Barrier(4)`. Primero haces que cada uno de los tres hilos hagan `barrier.wait()`. Después el hilo principal hace sus cosas y al acabar llama también a `barrier.wait()` desbloqueando la ejecución de los otros hilos.


Processes sharing memory
En la librería multiprocessing tienes objectos que puedes compartir entre procesos de manera segura.
En la implementación de abajo el proceso principal modifica un array y el proceso secundario muestra el valor actualizado.
Si usases un array normal esto no pasaría. Cada proceso (el principal y el secundario) trabajarían con una copia del array.

```
import multiprocessing
from multiprocessing.context import Process
import time

def print_array_contents(array):
    while True:
        print(*array, sep=", ")
        time.sleep(1)

if __name__ == "__main__":
    arr = multiprocessing.Array("i", [-1] * 10, lock=True)
    p = Process(target=print_array_contents, args=(arr,))
    p.start()
    for j in range(10):
        time.sleep(1)
        for i in range(10):
            arr[i] = j
```

