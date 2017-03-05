---
layout: post
title: Algoritmi Greedy
---

## Algoritmi Greedy

Un algoritmo greedy è un algoritmo che ottiene una soluzione ottima globale attraverso la scelta della soluzione più golosa (Greedy in inglese) ad ogni passo locale.  
Questa tipologia di algoritmi sono semplici da implementare, efficienti e portano sempre alla soluzione migliore ma hanno un difetto: è difficile dimostrarne la correttezza in tutti i casi possibili.

**Esempio:**  
*Determinare il minor numero di monete di resto utilizzando monete da 50, 20, 10, 5, 2, 1 centesimi di Euro.*  
La soluzione di questo problema è molto semplice: ad ogni passo viene data la moneta con valore massimo possibile. Ad esempio per dare un resto di 98 centesimi verranno date in ordine: 50, 20, 20, 5, 2, 1.  

Per essere Greedy i problemi devono rispettare due proprietà:
1. **Scelta Greedy**: Ad ogni passo della soluzione viene presa una scelta *greedy* e questa è definitiva (non è possibile riconsiderare le scelte prese in precedenza).
2. **Sottostruttura ottima**: Occorre dimostrare che una soluzione ottima del problema contiene al suo interno le soluzioni ottime dei sottoproblemi.

Uno schema generale di algoritmo risolutivo per i problemi *Greedy* è il seguente:
```
Greedy(V){
    Soluzione = [];
    <Ordina gli elementi di V seguendo un criterio>
    for(i=0; i<N; i++){
        if(<Soluzione + V[i] è soluzione>)
            Soluzione += V[i];
    }
    return S;
}
```

**Esempio 2: knapsack**  
Il problema dello zaino (knapsack) nella sua versione base è formulato come segue:  

*Un ladro con il suo zaino è in grado di portare M kg prima di rompersi. Essendo in una casa piena di oggetti da rubare e dovendo scegliere come riempire il suo zaino, il ladro, ovviamente, deve cercare di mettere un insieme di oggetti che massimizzi il valore della refurtiva: ogni oggetto è caratterizzato da un peso Pi e da un valore Vi e si suppone che di ogni oggetto ce ne siano quanti esemplari si vuole.* 

In questo caso potremmo essere tentati dall'ordinare gli oggetti in base al loro valore e prendere mano a mano quelli con valore massimo fino al riempimento dello zaino.  
**ERRORE**: non si tratta di un problema *greedy* in quanto una scelta localmente ottima non si traduce necessariamente in una scelta globalmente ottima!  
*Esempio:* ho i seguenti 3 oggetti: 

* O<sub>1</sub>: peso: 10, valore: 10
* O<sub>2</sub>: peso: 5, valore: 9
* O<sub>3</sub>: peso: 4, valore: 3

Con uno zaino di capacità 10 guadagno di più prendendo gli oggetti O<sub>2</sub> e O<sub>3</sub> rispetto al solo oggetto O<sub>1</sub>.  
Vedremo nel prossimo capitolo come risolvere il problema dello zaino.