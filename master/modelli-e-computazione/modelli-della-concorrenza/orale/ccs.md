# CCS

### Cosa è il CCS e quali sono le sue applicazioni
**CCS** (_Calculus of Communicating Systems_ - Calcolo di
sistemi comunicanti), è un'algebra di processi inventata da Milner per 
poter studiare modelli concorrenti. 

- sistema aperto (è in grado di comunicare con l'esterno)
- è formato da processi
- si risolve il problema della composizionalità tramite l'uso di porte
- un processo è un insieme di sottoprocessi (che comunicano con l'esterno tramite porte)
- si ha equivalenza all'osservazione per poter sostituire un processo con un altro
- l'osservazione deve essere valida per ogni osservatore esterno 
- ad ogni processo ccs è associato un lts che ne rappresenta la semantica operazionale strutturale
- si ha semantica interleaving 


### Bisimulazione debole
Una relazione binaria `R ⊆ Proc_CCS x Proc_CCS` è una **bisimulazione debole** sse:

`∀ p`, `q` in `Proc_CCS` vale che `pRq` sse, `∀a ∈ Act`:
- se `p→ᵃ p'` allora esiste `q'` tale che `q ⇒ᵃ q'` e `p'Rq'`
- se `q→ᵃ q'` allora esiste `p'` tale che `q ⇒ᵃ p'` e `p'Rq'`

Si può quindi dire 
```
p ≈ᵇⁱˢ q
```
con `≈ᵇⁱˢ = ∪{R | R è una relazione di bisimulazione debole}`


### Regole attaccante/difensore
Dato un gioco `G(p,q)` per verificare se i due processi `p` e `q` sono bisimili o meno è possibile utilizzare le _regole dell'attaccante e del difensore_.

L'obiettivo dell'attaccante è quello di dimostare che non sono debolmente bisimili. Il difensore invece cerca di dimostrare che sono debolmente bisimili.

Un gioco è un insieme di partite, ciascuna definita come una sequenza di mosse che passano da una 
configurazione (`pᵢ`, `qᵢ`) ad una (`p'ᵢ`,`q'ᵢ`).
L'attaccante è sempre il primo a muovere e può scegliere ad ogni mossa su che _tavolo_ giocare. 

L'attaccante può muoversi utilizzando la transizione forte, mentre il difensore può utilizzare la transizione debole (usando però la stessa azione dell'attaccante).

Il gioco consiste nel trovare il vincitore tra i due; è inevitabile che uno tra attaccante e difensore abbia almeno una strategia vincente.

I casi finali sono due: 
- l'attaccante vince se ha una strategia per cui il difensore non può difendersi;
- il difensore ha almeno una mossa possibile per ogni mossa dell'attaccante.

In caso di partita infinita vince il difensore.


### Operatori del CCS
- restrizione `\ₐ`
- rietichettatura `[f]`
- prefisso `α*P`
- composizione parallela `|`
- somma `+`


### Definire le transizioni
###### Transizione forte
Sia `T ⊆ S x Act x S` e si indica con `p →ᵃ q` con `q ∈ S` e `a in Act`

Questa definizione può essere estesa a w in Act^*
avendo che, per p→w q:
- se `w = ε` allora p equivale a q
- se w = a\*X, a in Act e X in Act^\* allora ho che p →ᵃ r e r→X q

→ = U_(a in Act) →ᵃ
→^* = U_(w in Act^*) →w e quindi →^* ⊆ S x S


###### Transizione debole
Dato `T ⊆ S x Act x S` si indica con `p ⇒α q` con `q ∈ S` e `α ∈ A ∨ A̅ ∨ τ`

- se `α = τ` ho che `p →t^* q`
- se `α ∈ A ∨ A̅` ho `p →t^*→ᵃ→t^* q`

Questa definizione può essere estesa a `w ∈ Act*`
avendo che, per p⇒w q:
- se `w = τ` o `w = ε` ho che p ⇒t^* q
- se `w = a₁, a₂, ..., aₙ` ho che p ⇒a_1 ... ⇒a_n q

con `S = Proc_CCS`.

### Semantica interleaving
Per l'assunzione di atomicità delle azioni di Milner si ha che nel CCS vale la semantica interleaving in quanto si ha una simulazione sequenziale non deterministica.

### In CCS come si rappresenta la possibilità di interazione tra due processi
Due processi interagiscono tra loro tramite un modello hand-shacking, usando una scambio di messaggi (vedisi l'insieme delle azioni e l'insieme delle coazioni e le sincronizzazioni ad esse legate). Con la sincronizzazione, avendo `τ`, si perde l'osservabilità.

### Come rappresento la possibilità di sincronizzazione nei processi CCS
[Vedi sopra](#in-ccs-come-si-rappresenta-la-possibilità-di-interazione-tra-due-processi)

### Regole del gioco dell'attaccante/difensore e relazione tra il gioco e la bisimulazione
[Vedi sopra](#regole-attaccantedifensore)

### Equivalenza rispetto alle Tracce
###### Forte
Una relazione binaria `R ⊆ Proc_CCS x Proc_CCS` è una **equivalenza rispetto alle tracce** sse:

∀ `p`, `q ∈ Proc_CCS` vale che `pRq` sse:
tracce(p) = tracce(q) implica p ~T q
avendo che tracce(p)={w in Act^*| ∃ p' in Proc_CCS t.c. p →w p'}


###### Debole
Una relazione binaria `R ⊆ Proc_CCS x Proc_CCS` è una **equivalenza rispetto alle tracce** sse:

`∀ p, q ∈ Proc_CCS` vale che `pRq` sse
- tracce_⇒(p) = tracce_⇒(q) implica `p ≈ᵗ q`

avendo che tracce(p)_⇒={w in (A ∪ A-)^*|  p ⇒w}

### Congruenza
Una relazione di equivalenza `R` è una **congruenza** rispetto agli operatori del CCS sse:
- `∀ p, q ∈ Proc_CCS` 
- `∀ c[.] contesto Proc_CCS` 

Si ha che `p R q` implica `c[p] R c[q]`.

Noto che 
- isomorfismo LTS
- equivalenza forte/debole rispetto alle tracce
- bisimulazione forte 

sono congruenze rispetto agli operatori CCS. 

Invece la bisimulazione debole non è una congruenza rispetto alla somma e, nel dettaglio, rispetto alla ricorsione.