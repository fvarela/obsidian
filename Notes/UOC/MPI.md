MPI - Message passing interface

Dentro del código hay parte que se ejecuta secuencial y parte en paralelo
- incluye `#include <mpi.h>`

```c
// Incluir la biblioteca MPI para funciones de programación paralela
#include "mpi.h"

#include <stdio.h>
#include <unistd.h>

int main(int argc, char **argv) {
    // Declarar variables para almacenar el rango del proceso y el número total de procesos
    int rank, numprocs;
    char hostname[256];

    // Inicializar el entorno MPI
    MPI_Init(&argc, &argv);
    // Obtener el rango del proceso actual dentro del comunicador global
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    // Obtener el número total de procesos en el comunicador global
    MPI_Comm_size(MPI_COMM_WORLD, &numprocs);
    // Obtener el nombre del host donde se ejecuta el proceso
    gethostname(hostname, 255);
    printf("Hello world! I am process number %d of %d MPI processes on host %s\n", rank, numprocs, hostname);

    // Finalizar el entorno MPI
    MPI_Finalize();
    return 0;
}

```

Compilación:
```bash
$ mpicc hello.c -o hello
```

Ejecución directa (sin SGE):
```bash
mpirun −np 6
```
Con el np 6 le indicas que vas a usar 6 ranks. En el script esto se traduce en lo siguiente:
- Variable `&rank` asignada entre 0 y 5 para cada hilo de ejecución.
- Variable `&numprocs` asignada a 6 para todos los hilos de ejecución.

Ejecución del programa a través de SGE:

```
#!/bin/bash
#$ -cwd
#$ -S /bin/bash
#$ -N hello_job
#$ -o $JOB_NAME.out.$JOB_ID
#$ -e $JOB_NAME.err.$JOB_ID
#$ -pe orte 6 #Con esta línea le indicas a SGE que vas a necesitar 6 cores
mpirun −np 6 . / hello #Con -np6 le indicas a MPI que arranque 6 procesos
```

Y después llamas a SGE con qsub:
```bash
qsub .\your_script_name.sge
```


## Envío de mensajes entre procesos con bloqueo:


```c

#include "mpi.h"
#include <stdio.h>

int main(argc,argv)
int argc;
char **argv;
{
  int MyProc, tag=1;
  char msg='A', msg_recpt;
  MPI_Status status;
  MPI_Init(&argc, &argv);
  MPI_Comm_rank(MPI_COMM_WORLD, &MyProc);
  printf("Process # %d started \n", MyProc);
  MPI_Barrier(MPI_COMM_WORLD); // wait for all processes to start
  if (MyProc == 0) // Proc 0 sends to Proc 1 and receives from Proc 1
  {
    printf("Sending message to Proc #1 \n") ;
    MPI_Send(&msg, 1, MPI_CHAR, 1, tag, MPI_COMM_WORLD); // send message to Proc 1 blockingly
    MPI_Recv(&msg_recpt, 1, MPI_CHAR, 1, tag, MPI_COMM_WORLD, &status); // receive message from Proc 1 blockingly
    printf("Recv'd message from Proc #1 \n") ;
  }
  else //if (MyProc == 1) Proc 1 receives from Proc 0 and sends to Proc 0
  {
    MPI_Recv(&msg_recpt, 1, MPI_CHAR, 0, tag, MPI_COMM_WORLD, &status); // receive message from Proc 0 blockingly
    printf("Recv'd message from Proc #0 \n") ;
    printf("Sending message to Proc #0 \n") ;
    MPI_Send(&msg, 1, MPI_CHAR, 0, tag, MPI_COMM_WORLD); // send message to Proc 0 blockingly
  }
  printf("Finishing proc %d\n", MyProc);
  MPI_Barrier(MPI_COMM_WORLD); // wait for all processes to finish
  MPI_Finalize();
}
```