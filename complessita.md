# [Preparazione OII](README.md)
## Complessità computazionale
I problemi che dovrete risolvere alle olimpiadi impongono due importanti limiti sui programmi che andrete a creare:

1. **Memoria**: non si può superare un certo limite di memoria RAM occupata (ad esempio 256 MB)
2. **Tempo**: bisogna completare l'esecuzione entro un tempo limite (ad esempio 1 secondo)

In questo capitolo ci occuperemo di misurare il tempo di un algoritmo mentre nel prossimo parleremo del problema della memoria.  

### Ordinamenti
Uno dei problemi importanti dell'informatica riguarda l'ordinamento di un insieme di oggetti. Il più semplice algoritmo di ordinamento è la [Stupid Sort](https://it.wikipedia.org/wiki/Stupid_sort):

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