# [Preparazione OII](README.md)
## Complessità computazionale
I problemi che dovrete risolvere alle olimpiadi impongono due importanti limiti sui programmi che andrete a creare:

1. **Memoria**: non si può superare un certo limite di memoria RAM occupata (ad esempio 256 MB)
2. **Tempo**: bisogna completare l'esecuzione entro un tempo limite (ad esempio 1 secondo)

In questo capitolo ci occuperemo di misurare il tempo di un algoritmo mentre nel prossimo parleremo del problema della memoria.  

### Ordinamenti

Uno dei problemi noti dell'informatica riguarda l'ordinamento *efficiente* di un insieme di oggetti. Il più semplice algoritmo di ordinamento da implementare e da capire è sicuramente [Bubble Sort](https://it.wikipedia.org/wiki/Bubble_sort):

```c++
void BubbleSort(int *array, int elemN){
   int alto;
   for (alto = elemN; alto > 0; alto-- ){ 
         for (int i=0; i<alto; i++){
           if (array[i]>array[i+1]){ 
             int tmp = array[i]; 
             array[i] = array[i+1]; 
             array[i+1] = tmp;
           } 
         }
     }
 }
```

Come *dovreste* sapere `BubbleSort` non è un algoritmo efficiente per l'ordinamento ma come possiamo misurare la sua complessità?  
Innanzitutto definiamo l'unità base l'**istruzione**: un istruzione è una qualsiasi operazione eseguibile da un computer in un tempo costante **C**. Ad esempio `x+=1;` oppure `if(A == B)` sono istruzioni semplici.  
Nel calcolo della complessità computazionale siamo interessati a capire quanto *tempo* impiega un determinato algoritmo dato un input di dimensione **N**.
Proviamo a rifare l'analisi per `BubbleSort` partendo dalle istruzioni più interne:

```C++
    int tmp = array[i];             // *******************
    array[i] = array[i+1];          //      BLOCCO A
    array[i+1] = tmp;               // *******************
```

Queste tre istruzioni semplici impiegano ognuna tempo **C** quindi diremo che il blocco A impiega tempo **3C**. Proseguiamo verso l'esterno:

```C++
    for (int i=0; i<alto; i++){     // *******************
        if (array[i]>array[i+1]){   //
            // [... A ...]          //      BLOCCO B
        }                           //
    }                               // *******************
```

Il blocco B esegue un ciclo `for` che va da 0 ad `alto`. Questo ciclo esegue per `alto` volte il blocco `if` (che corrisponde ad una istruzione **C**). Supponiamo che nel *caso peggiore* l'array sia ordinato al contrario e quindi si entra nel blocco if ad ogni iterazione. In questo caso il blocco A (**3C**) + l'istruzione `if` (**C**) verrano eseguite per `alto` volte.  
Possiamo concludere, quindi, dicendo che il blocco B ha una complessità nel caso peggiore di **alto \* 4C**.

[Stupid Sort](https://it.wikipedia.org/wiki/Stupid_sort):

```language
function stupid_sort(array)
   while not is_sorted(array)
     array = random_permutation(array)
```

Dato un array da ordinare si continua ad ordinarlo a random fino a quando esso non è ordinato. La cosa buffa è che il [teorema della scimmia instancabile](https://it.wikipedia.org/wiki/Teorema_della_scimmia_instancabile) ci permette di affermare che *prima o poi* la stupid sort riuscirà ad ordinare qualsiasi array in input.  
Intuitivamente riusciamo a capire che non sia una buona soluzione ma come possiamo dimostrare questa supposizione? Ipotizziamo che l'array di Input abbia N=5 elementi al suo interno e analizziamo in dettaglio il codice precedente:

1. `is_sorted()`: questa funzione dato un array restituisce `true` se esso è ordinato, `false` altrimenti. Per poter sapere se un array è ordinato è sufficiente il seguente codice:
    ```C++
    bool is_sorted(int array[5]){
        for(int i=0;i<4;i++){           // Scorro l'array da 0 a N-1
            if(array[i] > array[i+1])   // Se a[i] > a[i+1]
                return false;           // Non è ordinato
        }
        return true;                    // Se ho passato tutto il for allora è ordinato
    }
    ```
    Nel nostro esempio dove l'array ha N=5 elementi is_sorted esegue 4 volte il ciclo `for`.  
    Possiamo concludere dicendo che `is_sorted()` impiega **N-1** passi per completare la sua esecuzione.
2. `random_permutation()`: 