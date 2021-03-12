# Logica Temporale

### Differenza tra proprietà e formula
proprietà → linguaggio naturale, esprimo comportamenti
formula → connettivi logici e temporali
(???)

### Induzione LTL e Induzione CTL
Definire induttivamente la sintassi delle due.

### Relazione tra LTL e CTL
Alcune proprietà possono essere espresse sia attraverso formule di LTL che di CTL.
Proprietà  | LTC          | CTL
---------- | ------------ | ----------------------
Invariante | `G ¬p`       | `AG ¬p`
Reattività | `G(p → Fq)` | `AG(p → Fq)` 

Ci sono formule esprimibili solo in LTL (ad esempio "in ogni cammino, prima o poi,
 si raggiungerà uno stato a partire dal quale una formula è sempre vera")

Ci sono formule esprimibili solo in CTL (ad esempio la reset property "da ogni stato raggiungibile in ogni cammino
è sempre possibile raggiungere uno stato dove vale una formula", AGEFa)

Posso estendere CTL e LTL con CTL^* dove un operatore temporale può anche non essere
preceduto da un quantificatore

### Introduzione all'LTL
Si aggiunge alla logica proposizionale il concetto di tempo, lineare e discreto,
che con la sola logica proposizionale sarebbe esprimibile solo usando infinite variabili.
Si usa per il model checking e per studiare sistemi reattivi.

### Reticolo e Reticolo Completo
Un **reticolo** è un insieme parzialmente ordinato `(L, <=)` per cui
```
∀ x,y ∈ L | ∃ x join y , x meet y
```

Il reticolo è un **reticolo completo** sse 
```
∀B ⊆ L ∃ join B e meet B
```
### Equivalenza tra Formule
a equivale a b sse `∀ π:(π ⊧ a <→ π ⊧ b)`

### Equivalenza di Modelli rispetto a una Logica
Dati due modelli M1 (con stato iniziale s0) e M2 (con stato iniziale p0) essi 
sono quivalenti sse, per ogni formula a ben formata:
`M1,s0 ⊧ a <→ M2,p0 ⊧ a `

### Modello di Kripke
Siano
- `Z` insieme delle proposizioni atomiche
- `A = (Q, T)` un sistema di transizioni, con
  - `Q` insieme di stati
  - `T` insieme delle transizioni
- `I : Q → 2^Z` una funzione (detta _funzione di interpretazione_) che associa ad ogni stato `q ∈ Q` tutte le proposizioni atomiche che sono vere in quello determinato stato.

Un modello di Kripke è `A = (Q, T, I)`.

### Costruire un modello di Kripke a partire da una rete
A partire da una rete posso ricavare il modello di Kripke a partire dal grafo dei casi sequenziali,
dove le etichette delle transizioni sono trascurabili.

### CTL in generale
Si introduce l'uso dei quantificatori `A` ed `E` e si studia l'albero di computazione
di un modello di Kripke, definendo computazione un cammino che parte dalla radice 
dell'albero.

### Calcolo μ e relazione tra calcolo μ e altre logiche
Sappiamo che `CTL* ⊂ μ-calcolo` e quindi è più espressivo di tutte le logiche
trattate nel corso a costo di un'elevata complessità computazionale di studio e 
una scarsa leggibilità delle formule. Anche la semantica del μ-calcolo è esprimibile
tramite modelli di Kripke.

### Significato dell'UNTIL
L'until (forte) `α U β` indica che la formula `α` deve essere vera fino a quando non diventa vera `β`. Una volta che `α` diventa vera, la `β` può assumere qualunque valore.
Un caso particolare può essere quando `β` è vera fin da subito; in questo caso `α` potrebbe non essere mai vera, ma l'until comunque verificato.
```
∃ k ≥ 0 t.c. πᵏ ⊧ β ∧ ∀h 0 ≤ h < k πʰ ⊧ α 
```
### UNTIL DEBOLE (W) and RELEASE (R)
###### UNTIL DEBOLE
L'until debole `α W β` indica che la formula α è sempre vera o è vera α U β.
Si può riscrivere come `Gα v (α U β)`.
###### RELEASE
La release `α R β` indica che la formula `β` deve essere sempre vera fin quando non diventa vera `α`; quando `α` diventa vera, la `β` può assumere qualunque valore.
Si può riscrivere come `β W (α ∧ β)`
```
∀ k ≥ 0 πᵏ ⊧ β  or ∃ h < k t.c. πʰ ⊧ α 
```

### Costruzione di F(Future) e G(Globally) partendo da UNTIL
###### Future
Per il future basta dire che `Fa` equivale a `T U a` per costruzione dell'until.
###### Globally
Per il globally si ha che `Ga` diciamo che `Ga` equivale a `¬F(¬a)` e quindi equivale a `¬(T U ¬a)`.
### Criterio di validità di una formula LTL nel modello di Kripke
Guardare lista di definizioni.

### Formule non traducibili tra CTL e LTL
Vedi [sopra](#relazione-tra-ltl-e-ctl).

### CLT*
`CLT*` è una logica che estende sia `LTL` che `CTL`.
Anche in `CTL*` compaiono i quantificatori `A` e `E` ma non ho più il vincolo di `CTL` per cui non era possibile avere un operatore temporale non preceduto da un quantificatore.

### Punto Fisso/Kleene/Knaster-tarski
###### Punto fisso
Presa una funzione `f:X→X` si ha che `x∈X` è un punto fisso sse `f(x)=x`
###### Knaster-tarski
Preso un reticolo completo `(L, <=)` e una funzione monotona `f:L->L` si ha che 
`f` ha sempre un minimo punto fisso e un massimo punto fisso, quindi l'insieme
dei punti fissi di `f` è a sua volta un reticolo completo.

Un caso particolare è `L=2^A`, l'_insieme delle parti_ di un insieme.

Dim:
Costruiamo l'insieme (non vuoto) `Z={ T ⊆ A | f(T) ⊆ T}`, insieme dei _punti pre-fissi_.
Poniamo `m = ∩Z`.
`∀ S ∈ Z`, `m ⊆ S`, quindi, visto che f è monotona ho che:
```
f(m) ⊆ f(S)
```
Ma sappiamo anche che, per definizione di `Z`:
```
f(S) ⊆ S
```
Quindi per transitività di ⊆:
```
f(m) ⊆ S
```
Sappiamo che:
```
f(m) ⊆ ∩Z = m
```
Ma abbiamo così dimostrato che:
```
f(m) ⊆ m
```
Quindi `m ∈ Z` ma quindi `m=min Z`.

Sappiamo che:
```
f(m) ⊆ m
```
Ma quindi, essendo `f` monotona:
```
f(f(m)) ⊆ f(m)
```
Quindi `f(m) ∈ Z`. 

D'altro canto `m=min Z` quindi `m ⊆ f(m)`.
Ma quindi contemporaneamente ho che:
- `m ⊆ f(m)`
- `f(m) ⊆ m`

Quindi `f(m) = m` e quindi `m` è un punto fisso. Essendo anche il minimo è il
minimo punto fisso. 
###### Kleene
Presa una funzione monotona `f:2^A->2^A` possiamo dire che è continua se, con `Xi ⊆ A`:
`f(U Xi) = U f(Xi)`
ovvero se `X1 ⊆ X2 ⊆ ... ⊆ Xn` e `f(X1) ⊆ f(X2) ⊆ ... ⊆ f(Xn)` 
- minimo punto fisso: `f(∅), f(f(∅)), f(f(f(∅)))` finché non lo trovo.
- massimo punto fisso: `f(A), f(f(A)), f(f(f(A)))` finché non lo trovo.

### Dove può essere utile/ dove usiamo il concetto di punto fisso.
Lo usiamo per fare model checking su modelli di kripke, usando il teorema di 
Kleene per fare model checking globale di una data formula, verificando i
stati in cui vale. Nel dettaglio, pensando ad un future, ho un algoritmo che cerca
i minimi punti fissi (aumentando di volta in volta gli stati), partendo dall'insieme vuoto. 
Per un globally i massimi punti fissi (escludo di volta in volta stati), partendo da tutti gli stati dove non vale la formula.