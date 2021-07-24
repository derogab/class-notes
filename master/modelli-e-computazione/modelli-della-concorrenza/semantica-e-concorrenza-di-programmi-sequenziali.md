# Semantica e concorrenza di programmi sequenziali

### Logica proposizionale
La logica proposizionale è un linguaggio formale con una semplice struttura sintattica, basata fondamentalmente su proposizioni elementari (atomi) e su connettivi logici di tipo vero-funzionale, che restituiscono il valore di verità di una proposizione in base al valore di verità delle proposizioni connesse.

Sintassi                | .
----------------------- | ---------------------------
`P = {p1 ... p_i}`      | simboli
`T`, `⊥`                | costanti logiche
`¬`, `∨`, `∧`, `→`, `↔` | connettivi proposizionali
`(`, `)`                | delimitatori

Combinando correttamente i simboli del linguaggio formo leformule con cui derivare le dimostrazioni.

#### Costruzione induttiva delle FBF (_Formule Ben Formate_)
Posso definire induttivamente l'insieme delle FBF.
1. `T, ⊥, p_i ∈ FBF`
2. `A ∈ FBF, B ∈ FBF → ¬A, A∨B, A∧B, A→B, A↔B ∈ FBF`

### Logica di Hoare

#### Introduzione alla logica di Hoare

##### Stato della memoria
Definisco lo **stato della memoria** come una funzione
```
s: V → Z
```
con 
- `V` insieme di variabili del programma
- `Z` insieme dei relativi

Un **programma** è un trasformatore di stato.


##### Invariante
Definisco come **invariante** una particolare formula che gode della seguente proprietà: se è vera all'inizio di una iterazione allora sarà vera anche al termine dell'iterazione.

##### Formule della logica di Hoare
```
α P β
```
Una formula della logica di Hoare è l'intera tripla `α P β`.  

Tale logica si basano sulla logica proposizionale e le formule `α` e `β` si basano sulla logica proposizionale.

##### Linguaggio della logica di Hoare

```
C ::= X:= E
C ::= C;C
C ::= if B then C else C endif
C ::= while B do C endwhile
C ::= SKIP
```
```
B := true
B := false
B := ¬ B
B := b ∧ b
B := b ∨ b
B := E = E
B := E < E
```
con 
Lettera | Significato
------- | ----------------------
`E`     | Espressione 
`C`     | Comando
`B`     | Espressione booleana

##### Dimostrazione nella logica di Hoare
Una dimostrazione nella logica di Hoare è una sequenza di formule che sono:
- assiomi
- formule ricavate dalle precedenti tramite regole di derivazione

##### Regole di derivazione
> [Inserire qui]

