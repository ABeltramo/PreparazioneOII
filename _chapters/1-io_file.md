---
layout: post
title: I/O da file
---

## I/O da file

Il correttore automatico delle olimpiadi prevede che il vostro programma legga un input dal file *input.txt*, computi un risultato e lo restituisca nel file *output.txt*. Ne segue che una parte fondamentale del vostro lavoro riguarda la lettura e la scrittura da file testuali.  
In C++ la manipolazione dei file avviene tramite la classe `fstream`; in particolare: 
1. `ifstream`: (input file stream) permette di aprire un file per la lettura. (nel nostro caso sarà sempre *input.txt*).
2. `ofstream`: (output file stream) permette di aprire un file per la scrittura (nel nostro caso sarà sempre *output.txt*). 

L'esempio che segue legge dal file input.txt, una riga alla volta, tutti i numeri presenti, li somma ed infine stampa il risultato sul file output.txt.  
**Input.txt**: la prima riga contiene N: il numero di righe del file successive alla prima riga. Le seguenti N righe contengono un numero.

```
1  
2  
3  
-1  
16  
```

```c++
#include <iostream>             // Input/Output stream library
#include <fstream>              // File stream library
using namespace std;            // Evito di dover specificare std::

int N, caramelle, input;        // Variabili locali

int main() {
    ifstream in("input.txt");   // Apro il file input.txt come input
    ofstream out("output.txt"); // Apro il file output.txt come output
    in >> N;                    // Leggo il primo intero e lo salvo nella variabile N
    caramelle = 0;              // Inizializzo la variabile caramelle a 0
    for (int i=0; i<N; i++){    // Per ogni riga N del file in input
        in >> input;            // Salvo nella variabile input il prossimo intero
        caramelle += input;     // Sommo l'input al valore corrente di caramelle
    }
    out << caramelle << endl ;  // Scrivo sul file di output il risultato della somma
    return 0;
}
```

**Output.txt**: viene restituita la somma dei numeri letti

```
21  
```

La lettura/scrittura di tipi diversi dall'`int` avviene allo stesso modo. Il tipo di dato (e come interpretarlo dall'input) viene automaticamente dedotto dal tipo di variabile che viene usata per salvare/leggere i dati.  
Ad esempio `in >> Carattere` se Carattere è una variabile di tipo `Char` consentirà di leggere dal file di input un singolo carattere.