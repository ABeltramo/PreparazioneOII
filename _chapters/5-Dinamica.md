---
layout: post
title: Programmazione dinamica - Fibonacci
---

## Programmazione dinamica

### Fibonacci ricorsivo ###
*La successione di Fibonacci è una successione di numeri in cui ciascun numero è la somma dei due precedenti e i primi due elementi della successione sono, per definizione, 1 e 1*.  
La versione ricorsiva di Fibonacci è la seguente:

```c++
int Fibonacci(int i){
    if (i == 0) return 0;
    else if (i == 1) return 1;
    else return Fibonacci(i-1) + Fibonacci(i-2); 
}
```
Semplice no? Proviamo a calcolare la complessità di questo algoritmo. Ad ogni chiamata ricorsiva il problema si divide in 2 sottoproblemi più semplici. La figura che segue rappresenta le chiamate necessarie a computare Fibonacci(7).

<p align="center">
    <img src="{{site.baseurl}}/img/Fib_Ricorsivo.png">
</p>

Il calcolo della complessità computazionale è più complesso di quelli visti in precedenza. Guardando l'albero ci si può accorgere che mentre la crescita in altezza è lineare la crescita in *ampiezza* è esponenziale, più precisamente: ad ogni passo raddoppia.  
Possiamo quindi supporre che Fibonacci ricorsivo impiega **O(2<sup>N</sup>)**? La dimostrazione avviene per induzione:

1. *Base*: per N=1 il tempo T è costante.
2. *Assumiamo* T(N-1) = O(2<sup>N-1</sup>)
3. *Ne segue che* T(N) = T(N-1) + T(N-2) = O(2<sup>N-1</sup>) + O(2<sup>N-2</sup>) =
O(2<sup>N-1</sup>) asintoticamente.

Abbiamo dimostrato che Fibonacci ricorsivo impiega **O(2<sup>N</sup>)** guardando ad occhio l'immagine precedente è facile vedere come Fib(4), ad esempio, venga calcolato 3 volte. Come possiamo evitare questa ripetizione di calcoli?

### Fibonacci dinamico ###

L'idea alla base della versione di Fibonacci utilizzando la programmazione dinamica è molto semplice: ogni volta che calcoliamo l'i-esimo valore della successione di Fibonacci salviamo questo risultato parziale in un vettore.

```c++
int fib[100];

int Fibonacci(int n) {
    fib[0] = 0; 
    fib[1] = 1;
    for (int i=2; i<=n; i++)
        fib[i] = fib[i-1] + fib[i-2]; 
    return fib[n];
}
```

Ottenendo una molto più efficiente soluzione lineare **O(N)**. Potreste notare che il vettore è superfluo per questo algoritmo in quanto sono necessarie solo due variabili (i due risultati precedenti) per calcolare Fibonacci.