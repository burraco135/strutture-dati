# Strutture dati

## Lista

Una lista è una sequenza di elementi di un certo tipo, in cui è possibile aggiungere o togliere elementi. Per far questo, occorre specificare la posizione relativa all'interno della sequenza nella quale il nuovo elemento va aggiunto o dalla quale il vecchio elemento va tolto.

A differenza del vettore, che è una struttura a dimensione fissa dove è possibile accedere direttamente ad ogni elemento specificandone l'indice, la lista è a dimensione variabile e si può accedere direttamente solo ad un ristretto sottoinsieme di elementi (di solito il primo o l'ultimo). Per accedere ad un generico elemento, occore scandire sequenzialmente gli elementi della lista: partendo da un elemento accessibile direttamente, ci si sposta via via da un elemento ad uno adiacente nella sequenza, fino a raggiungere l'elemento desiderato.

#### Esempio 2.1 (Liste)
Uno schedario contenente le informazioni degli impiegati di un'azienda, in cui è possibile ricercare, aggiungere e togliere schede, è un esempio di lista.

Sia L = a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> una lista. La lunghezza di L è pari ad n, il numero dei suoi elementi. Se la lista è vuota, cioè non contiene alcun elemento, allora n = 0, e la lista è indicata con &wedge;. Ogni elemento è caratterizzato da una posizione in L, indicata con pos<sub>i</sub>, e da un valore a<sub>i</sub>. Anche se viene immediato immaginare che pos<sub>i</sub> sia uguale ad i, si considera la posizione come un tipo di dato a sé stante la cui realizzazione, che varia a seconda della realizzazione adottata per il tipo di dato lista, può non essere uguale all'intero i. Per comodità, si assume inoltre l'esistenza di una posizione pos<sub>0</sub> che precede quella del primo elemento e di una posizione pos<sub>n+1</sub> che segue quella dell'ultimo elemento.

### Specifica
Un tipico insieme di operazioni per il tipo di dato lista comprende l'operazione di creazione CREALISTA, per inizializzare una lista ad un particolare vettore (di solito la sequenza vuota), quelle di selezione PRIMOLISTA ed ULTIMOLISTA, per accedere direttamente al primo o all'ultimo elemento della sequenza, e SUCCLISTA e PREDLISTA, per passare da un elemento al successivo o al precedente della sequenza, quelle di interrogazione LISTAVUOTA e FINELISTA, per verificare che la sequenza sia vuota o che sia stato oltrepassato un estremo della lista, quella di lettura LEGGILISTA per leggere il valore di un elemento, INSLISTA per inserire un nuovo elemento nella lista, e CANCLISTA per cancellare un vecchio elemento della lista.

Formalmente, la sintassi degli operatori è la seguente.
CREALISTA: () &rightarrow; lista
LISTAVUOTA: (lista) &rightarrow; booleano
PRIMOLISTA: (lista) &rightarrow; posizione
ULTIMOLISTA: (lista) &rightarrow; posizione
SUCCLISTA: (posizione, lista) &rightarrow; posizione
PREDLISTA: (posizione, lista) &rightarrow; posizione
FINELISTA: (posizione, lista) &rightarrow; booleano
LEGGILISTA: (posizione, lista) &rightarrow; tipoelem
SCRIVILISTA: (tipoelem, posizione, lista) &rightarrow; lista
INSLISTA: (tipoelem, posizione, lista) &rightarrow; lista
CANCLISTA: (posizione, lista) &rightarrow; lista

Indicando col termine lista l'insieme di tutte le sequenze di lunghezza arbitraria di elementi di tipo "tipoelem" e con L una generica lista, la semantica degli operatori è data dalle seguenti funzioni, con relative precondizioni e postcondizioni.
