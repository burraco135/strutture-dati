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

* CREALISTA: () &rightarrow; lista
* LISTAVUOTA: (lista) &rightarrow; booleano
* PRIMOLISTA: (lista) &rightarrow; posizione
* ULTIMOLISTA: (lista) &rightarrow; posizione
* SUCCLISTA: (posizione, lista) &rightarrow; posizione
* PREDLISTA: (posizione, lista) &rightarrow; posizione
* FINELISTA: (posizione, lista) &rightarrow; booleano
* LEGGILISTA: (posizione, lista) &rightarrow; tipoelem
* SCRIVILISTA: (tipoelem, posizione, lista) &rightarrow; lista
* INSLISTA: (tipoelem, posizione, lista) &rightarrow; lista
* CANCLISTA: (posizione, lista) &rightarrow; lista

Indicando col termine lista l'insieme di tutte le sequenze di lunghezza arbitraria di elementi di tipo "tipoelem" e con L una generica lista, la semantica degli operatori è data dalle seguenti funzioni, con relative precondizioni e postcondizioni.

* CREALISTA() = L'
  * Post: L' = &wedge;, la sequenza vuota
* LISTAVUOTA(L) = b
  * Post: b = vero, se L = &wedge;; b = falso, altrimenti
* PRIMOLISTA(L) = p
  * Post: p = pos<sub>1</sub> (e quindi pos<sub>1</sub> = pos<sub>n+1</sub> se L = &wedge;)
* ULTIMOLISTA(L) = p
  * Post: p = pos<sub>n</sub> (e quindi pos<sub>n</sub> = pos<sub>0</sub> se L = &wedge;)
* SUCCLISTA(p, L) = q
  * Pre: L = a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> e p = pos<sub>i</sub> per un i, 1 &le; i &le; n
  * Post: q = pos<sub>i+1</sub>
* PREDLISTA(q, L) = q
  * Pre: L = a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> e p = pos<sub>i</sub> per un i, 1 &le; i &le; n
  * Post: q = pos<sub>i-1</sub>
* FINELISTA(p, L) = b
  * Pre: L = a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> e p = pos<sub>i</sub>, 0 &le; i &le; n+1
  * Post: b = vero, se p = pos<sub>0</sub> oppure se p = pos<sub>n+1</sub>; b = falso, altrimenti
* LEGGILISTA(p, L) = a
  * Pre: L = a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> e p = pos<sub>i</sub> per un i, 1 &le; i &le; n
  * Post: a = a<sub>i</sub>
* SCRIVILISTA(a, p, L) = L'
  * Pre: L = a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> e p = pos<sub>i</sub> per un i, 1 &le; i &le; n+1
  * Post: L' = a<sub>1</sub>, ..., a<sub>i-1</sub>, a, a<sub>i</sub>, a<sub>i+1</sub>, ..., a<sub>n</sub> se 1 &le; i &le; n, L' = a<sub>1</sub>, ..., a<sub>i-1</sub>, a<sub>i+1</sub>, ..., a<sub>n</sub> (e quindi L' = &wedge; se i = n = 1)

Dalla specifica emerge che per accedere ad un elemento occorre conoscerne la posizione. Ciò è possibile solo conoscendo a priori la posizione dell'elemento precedente (o seguente) ed applicando quindi l'operazione SUCCLISTA (o PREDLISTA). Le uniche operazioni che danno per risultato una posizione, senza che gliene venga fornita una in ingresso, sono le operazioni PRIMOLISTA e ULTIMOLISTA. Per accedere ad un generico elemento occorre pertanto scandire la lista in avanti a partire dal primo elemento, o a ritroso partendo dall'ultimo. Se viene oltrepassato un estremo della lista, SUCCLISTA e PREDLISTA restituiscono, rispettivamente pos<sub>n+1</sub> e pos<sub>0</sub>. È possibile accorgersi di questo fatto con l'interrogazione FINELISTA, che in tal caso restituirà il valore booleano vero.

Poichè inserzioni e cancellazioni "allungano" ed "accorciano" la lista, esse provocano la modifica di tutte le posizioni degli elementi che seguono quello inserito o cancellato. In particolare, INSLISTA(a, p, L) con p = pos<sub>i</sub> inserisce il nuovo elemento di valore a come nuovo i-esimo elemento della sequenza, mentre il vecchio i-esimo elemento diventa l'(i+1)-esimo, il vecchio (i+1)-esimo diventa l'(i+2)-esimo, ecc. Se p = pos<sub>n+1</sub>, INSLISTA inserisce il nuovo elemento in fondo alla sequenza, lasciando inalterate le posizioni dei vecchi elementi. Se la lista è vuota e p = pos<sub>1</sub> = pos<sub>n+1</sub>, il nuovo elemento diviene il primo (ed unico) elemento della lista. Invece, CANCLISTA(p, L) con p = pos<sub>i</sub> cancella il vecchio i-esimo elemento della sequenza, mentre il vecchio (i+1)-esimo elemento diventa l'i-esimo, il vecchio (i+2)-esimo diventa l'(i+1)-esimo, ecc.

Si noti infine che l'operazione LISTAVUOTA è ridondante, poichè LISTAVUOTA(L) = FINELISTA(PRIMOLISTA(L), L) = FINELISTA(ULTIMOLISTA(L), L).
