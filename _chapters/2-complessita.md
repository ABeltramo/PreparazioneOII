---
layout: post
title: Complessità Computazionale
---

## Complessità computazionale

I problemi che dovrete risolvere alle olimpiadi impongono due importanti limiti sui programmi che andrete a creare:

1. **Memoria**: non si può superare un certo limite di memoria RAM occupata (ad esempio 256 MB)
2. **Tempo**: bisogna completare l'esecuzione entro un tempo limite (ad esempio 1 secondo)

In questo capitolo ci occuperemo di misurare il tempo di un algoritmo mentre nel prossimo parleremo del problema della memoria.  

### Bubble Sort

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
Innanzitutto definiamo cos'è per noi l'**istruzione**: un istruzione è una qualsiasi operazione eseguibile da un computer in un tempo costante **C**. Ad esempio `x+=1;` oppure `if(A == B)` sono istruzioni semplici.  
Nel calcolo della complessità computazionale siamo interessati a capire quanto *tempo* impiega un determinato algoritmo dato un input di dimensione **N**.
Proviamo a rifare l'analisi per `BubbleSort` partendo dalle istruzioni più interne:

```c++
    int tmp = array[i];             // *******************
    array[i] = array[i+1];          //      BLOCCO A
    array[i+1] = tmp;               // *******************
```

Queste tre istruzioni semplici impiegano ognuna tempo **C** quindi diremo che il blocco A impiega tempo **3C**. Proseguiamo verso l'esterno:

```c++
    for (int i=0; i<alto; i++){     // *******************
        if (array[i]>array[i+1]){   //
            // [... A ...]          //      BLOCCO B
        }                           //
    }                               // *******************
```

Il blocco B esegue un ciclo `for` che va da 0 ad `alto`. Questo ciclo esegue per `alto` volte il blocco `if` (che corrisponde ad una istruzione **C**). Supponiamo che nel *caso peggiore* l'array sia ordinato al contrario e quindi si entra nel blocco if ad ogni iterazione. In questo caso il blocco A (**3C**) + l'istruzione `if` (**C**) verrano eseguite per `alto` volte.  
Possiamo concludere, quindi, dicendo che il blocco B ha una complessità nel caso peggiore di **alto \* 4C**.

```c++
void BubbleSort(int *array, int elemN){
   int alto;
   for (alto = elemN; alto > 0; alto-- ){ 
         // [... B ...]
     }
 }
```

Possiamo ora considerare l'algoritmo `BubbleSort` nel suo insieme.  

1. La variabile `alto` viene inizializzata alla dimensione dell'input (**N**)
2. Viene eseguito il blocco B portando quindi la complessità a **N \* 4C**
3. `alto` assume ora il valore **N-1**.
4. Viene eseguito il blocco B portando la complessità a **(N\*4C) + [(N-1)\*4C]**

Continuando ad eseguire il ciclo si ottiene la seguente equazione:

<p align="center">
    <img src="{{site.baseurl}}/img/Compl_BubbleSort.png">
</p>

Non ci interessano molto i calcoli quanto il risultato: la notazione *Teta(N^2)* significa che l'algoritmo sia nel caso migliore che nel caso peggiore impiega il quadrato della dimensione dell'input. Mi potreste chiedere: *"Dove sono finite le C?"* e io vi risponderei: *"Grazie per avermelo chiesto!"*. In realtà lo scopo del calcolo della complessità computazionale non è definire esattamente quanto tempo impiega un programma a completare la sua esecuzione; i secondi esatti dipendono da moltissime variabili come la velocità del processore, il suo set di istruzioni macchina, la compilazione in bytecode, etc etc.   
Le **C** spariscono perchè sono insignificanti rispetto alla dimensione dell'input. Cercate sempre di immaginare un vettore di input con tante caselle quante ce ne possono stare nella RAM. Eseguire N volte un codice, 2N, 10N, 100N non è niente paragonato a **N^2** (se provate a mettere numeri grandi capirete il perchè).  
Da qui in avanti useremo la notazione **O(tempo)** (da leggersi O grande di) per indicare il *caso peggiore* dell'algoritmo.  

### Stupid Sort

[Stupid Sort](https://it.wikipedia.org/wiki/Stupid_sort) è un algoritmo di ordinamento pessimo (basta leggerne il nome) eppure la prima cosa che salta all'occhio è il codice. Sono solo tre righe, [un solo ciclo](https://media.giphy.com/media/8McNH1aXZnVyE/giphy.gif) com'è possibile che sia così pessimo?

```c++
function stupid_sort(array)
   while not is_sorted(array)
     array = random_permutation(array)
```

Dato un array da ordinare si continua a permutarlo a random fino a quando non è ordinato. La cosa buffa è che il [teorema della scimmia instancabile](https://it.wikipedia.org/wiki/Teorema_della_scimmia_instancabile) ci permette di affermare che *prima o poi* la stupid sort riuscirà ad ordinare qualsiasi array in input.  
Intuitivamente riusciamo a capire che non sia una buona soluzione ma come possiamo dimostrare questa supposizione? Ipotizziamo che l'array di Input abbia **N** elementi al suo interno e analizziamo in dettaglio il codice precedente:  
`is_sorted()`: questa funzione dato un array restituisce `true` se esso è ordinato, `false` altrimenti. Per poter sapere se un array è ordinato è sufficiente il seguente codice:

```c++
bool is_sorted(int array[N]){
    for(int i=0;i<4;i++){           // Scorro l'array da 0 a N-1
        if(array[i] > array[i+1])   // Se a[i] > a[i+1]
            return false;           // Non è ordinato
    }
    return true;                    // Se ho passato tutto il for allora è ordinato
}
```

Quì si nasconde il primo ciclo che aumenta il tempo di esecuzione. Per quanto sia una funzione semplice un ciclo sulla dimensione dell'input è sempre da evitare. `is_sorted()` impiega **N-1** passi per completare la sua esecuzione.  

`random_permutation()`: Anche quì si nasconde una complessità ulteriore. Intuitivamente, come minimo, per spostare casualmente gli elementi di un array bisogna scorrerli tutti. [Esempi reali](http://www.cplusplus.com/reference/algorithm/random_shuffle/) di algoritmi di permutazione indica una complessità lineare con la dimensione dell'input. Concludiamo, quindi, assumendo che `random_permutation()` ha una complessità **O(N)**.  

Riguardiamo ora il codice della `stupid_sort` alla luce di quanto affermato:

```c++
function stupid_sort(array)
   while not is_sorted(array)           // TEMPO O(N)
     array = random_permutation(array)  // TEMPO O(N)
```

**N.B.** : potreste essere invogliati a dire che ad ogni passo del ciclo while l'algoritmo impiega *O(N^2)* facendo, in realtà, un grande errore. In realtà, ogni passo del ciclo impiega **O(N + N)** in quanto prima scorre il vettore *(N)* per vedere se è ordinato e, successivamente, lo riscorre per ordinarlo casualmente *(N)*. I due cicli non sono innestati!!!  

Quindi? Qual'è la complessità computazionale di `stupid_sort`? Possiamo distinguere due casi:
1. Caso migliore: il vettore in input è già ordinato. In questo caso abbiamo il miglior algoritmo del mondo per ordinare un vettore perchè impiega solo **N** passi ad accorgersi che è già ordinato!
2. Caso peggiore: il ciclo `while` non ha un limite fissato (come per i `for` precedenti) non abbiamo quindi modo di dare una stima del tempo necessario perchè dipende dal caso. Per lo studio delle probabilità arriverà ad una conclusione ma con [tempi catastrofici](https://it.wikipedia.org/wiki/Stupid_sort#Tempo_di_esecuzione)

### **TL;DR**

Cicli sulla lunghezza dell'input = **MALE**.  
Dato un vettore in input di dimensione **N** cercate di evitare codici del tipo:

```C++
    for(int i=0;i<N; i++)                           // MALE
        for(int j=0;j<N; j++)                       // MALISSIMO
            for(int k=0;k<N; k++)                   // ¯\_(ツ)_/¯
                for(int devil=0; devil<N; devil++)  // (╯°□°）╯︵ ┻━┻
```