---
layout: post
title: STL C++
---

## STL: Standard Template Library

La libreria standard del C++ si compone di quattro componenti principali:

1. *Algorithms*: Algoritmi standard come la ricerca e l'ordinamento.
2. *Containers*: Un set di contenitori pronti da usare come vettori dinamici e mappe.
3. *Functionals*: Possibilità di scrivere funzioni che ricevono diversi tipi di dati.
4. *Iterators*: Astrazione dei puntatori classici.

Alcuni componenti della libreria standard saranno fondamentali per i problemi che andrete a risolvere e per questo motivo li analizzeremo in questo capitolo.

### Functionals

Non andremo ad analizzare nel dettaglio tutte le possibilità offerte da queste classi perchè quello che ci interessa sapere è che esiste un modo per definire funzioni *generiche* (non preoccupatevi non sarà necessario che ne implementiate durante le gare). Vediamone subito un esempio concreto: si vuole creare una funzione che permetta di stampare qualsiasi variabile a schermo:

```c++
template <typename T> void stampa(T messaggio){
        std::cout << messaggio << std::endl;
}
``` 

La funzione `stampa()` riceve come parametro un tipo di dato qualsiasi come `int`, `string` o `char` e lo stampa sullo standard output. Magia? [No](http://i1.kym-cdn.com/entries/icons/facebook/000/013/034/yeahsciencebitch.jpg), in realtà viene definito un *tipo* dinamico **T** il quale può assumere qualsiasi tipo reale durante l'esecuzione del programma (e non in fase di compilazione).  
Vedremo come questa libertà verrà sfruttata da tutti i componenti della libreria standard.

### Containers

Un contenitore, nella sua forma più generale, è un oggetto dove possono essere inseriti altri oggetti. Esempi di contenitori sono i vettori, le liste, gli alberi. Tra i [contenitori](http://www.cplusplus.com/reference/stl/) presenti nella libreria standard andremo ad analizzare in particolare:

1. **Vector**: generalizzazione del classico Array che consente di avere una dimensione dinamica.
4. **Map**: array associativo del tipo <chiave,valore>
5. **Bitset**: struttura molto compatta per rappresentare un array di `bool`

#### Vector



