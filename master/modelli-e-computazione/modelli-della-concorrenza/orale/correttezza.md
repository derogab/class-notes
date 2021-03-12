# Correttezza

### Definizione di Invariante
Un **invariante** è una particolare formula che gode della seguente proprietà: se è vera all'inizio di una iterazione allora sarà vera anche al termine dell'iterazione.

### Validità della Tripla di Hoare
La tripla di Hoare è una [specifica tripla formale](#tripla-di-hoare). 
È utilizzata nella specifica della correttezza di un programma che deve essere dimostrata.

Una dimostrazione è una sequenza di formule nel linguaggio della logica di Hoare che sono:
- assiomi;
- formule ricavate dalle precedenti tramite regole di derivazione. 

### Regola di derivazione per la istruzione di scelta
La regola di derivazione per l'istruzione di scelta viene applicata ogni volta in cui bisogna eseguire una scelta, solitamente rappresentata con l'`IF`.
Possiamo supporre che valga solo una tra le seguenti opzioni:
- `B` e la precondizione `{p ∧ B} C {q}`
- `¬B` e la precondizione `{p ∧ ¬B} D {q}`

```
 {p ∧ B} C {q}     {p ∧ ¬B} D {q}
----------------------------------
 {p} if B then C else D endif {q}
```

### Che proprietà deve avere il variante E nella correttezza totale
`E` è una espressione aritmetica nella quale compaiono variabili di programma, costanti numeriche e operazioni aritmetiche.  
`inv` è un invariante di ciclo per `W`.

Devono valere due proprietà:
- `inv → E ≥ 0`
- `|— { inv ∧ B ∧ E=K } C { inv ∧ E<K }`

Se valgono tali proprietà allora `|— { inv } W { inv ∧ ¬B }`

### Correttezza totale
Se si esegue `W` a partire da uno stato in cui vale `p`, l'esecuzione termina e nello stato finale vale `q`.
```
|— {p} W {q}
```

### Differenza tra correttezza totale e parziale
```
|— {p} W {q}
```
```
|— {p} while B do C endwhile {q}
```

Correttezza parziale    | Correttezza totale
----------------------- | ---------------------------
Se si esegue `W` a partire dal uno stato in cui vale `p` e l'esecuzione termina, nello stato finale vale `q`.     | Se si esegue `W` a partire da uno stato in cui vale `p`, l'esecuzione termina e nello stato finale vale `q`.

<!--
**Correttezza parziale**: se si esegue `W` a partire dal uno stato in cui vale `p` e l'esecuzione termina, nello stato finale vale `q`.

**Correttezza totale**: se si esegue `W` a partire da uno stato in cui vale `p`, l'esecuzione termina e nello stato finale vale `q`.
-->


### Correttezza e Completezza
Correttezza e Completezza sono due proprietà generali della logica di Hoare.

Correttezza    | Completezza
-------------- | ---------------------------
`\|— → \|=`      | `\|= → \|—` 
Tutto ciò che si riesce a derivare con l'apparato deduttivo è effettivamente vero. | L'apparato deduttivo è in grafo fi derivare tutte le formule vere.

In realtà la proprietà di completezza è relativa a causa dell'_incompletezza aritmetica_ di alcuni calcoli nella logica proposizionale.

### Precondizione più debole
Dati `C` e `q` un criterio per trovare la _miglior_ proposizione `p` tale che `|= {p} C {q}` è la ricerca della **precondizione più debole**, ovvero il più grande insieme di stati che garantiscono il raggiungimento di `q` con l'esecuzione di `C`.
La _weakest precondition_ (precondizione debole) è indicata con `wp(C, q)`. 
```
|= {p} C {q} sse p → wp(C, q)
```
Tale precondizione esiste sempre e qualora non fosse unica si può dimostrare che sono tutte equivalenti, ovvero si implicano a vicenda.


### Regola di derivazione della sequenza
La regola di derivazione della sequenza viene applicata ogni volta in cui è possibile suddividere il programma in istruzioni eseguite una dopo l'altra in sequenza.
```
 {p} C {q}     {q} D {r}
-------------------------
       {p} C;D {r}
```


### Tripla di Hoare
La tripla di Hoare è 
```
α P β
```
in cui 
- le formule `α` e `β` si basano sulla logica proposizionale 
  - `α` rappresenta la precondizione
  - `β` rappresenta la postcondizione
- `P` indica un programma, un frammento o una istruzione


### Se cambio gli assegnamenti iniziali l'invariante trovato resta tale?
L'invariante resta tale [per definizione](#definizione-di-invariante).  