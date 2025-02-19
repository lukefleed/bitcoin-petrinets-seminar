## Slide 1

Bitcoin è stato introdotto nel 2008 come un meccanismo decentralizzato per lo scambio di valuta digitale. La caratteristica chiave del sistema è l’utilizzo della Blockchain, una struttura distribuita che registra tutte le transazioni. Questo ha portato allo sviluppo di diverse tecnologie e modelli per analizzare il comportamento della rete, tra cui quello proposto in questo paper.

Il cuore del contributo è l’adozione delle _Petri Nets_ per modellare e analizzare la Blockchain. Le Petri Nets sono un formalismo matematico ampiamente utilizzato per rappresentare sistemi distribuiti e concorrenti. In questo modello, ogni indirizzo Bitcoin è rappresentato come un _posto_, mentre ogni transazione è una _transizione_. Questo approccio permette di catturare sia le relazioni tra indirizzi sia il flusso complessivo delle transazioni all’interno della rete.

Il modello proposto si articola in due componenti principali: l’_Addresses Petri Net_ e l’_Entities Petri Net_. La prima rappresenta direttamente gli indirizzi e le transazioni della Blockchain, consentendo di raccogliere informazioni sulle interazioni tra gli utenti. La seconda raggruppa gli indirizzi associati alla stessa entità, facilitando l’identificazione di comportamenti aggregati e la costruzione di statistiche avanzate.

L’uso delle Petri Nets offre numerosi vantaggi. In primo luogo, il formalismo permette di eseguire analisi strutturali tramite algoritmi definiti, utili per identificare pattern e anomalie. Inoltre, la rappresentazione grafica nativa delle transazioni fornisce una visione alternativa e più comprensibile della rete rispetto ai metodi tradizionali. Infine, il modello consente di effettuare simulazioni dinamiche per studiare e prevedere il comportamento futuro della rete, offrendo uno strumento potente per il monitoraggio e l’analisi evolutiva del sistema.

Le sezioni successive del paper approfondiscono l’architettura del modello, descrivono nel dettaglio la costruzione delle _Petri Nets_ proposte e illustrano i risultati dell’applicazione del modello alla Blockchain. Viene inoltre mostrata l’efficacia dell’approccio nel fornire un’analisi dettagliata della rete e nel supportare simulazioni che potrebbero migliorare la comprensione dei fenomeni emergenti.

## Slide 2 - 3 - 4

Adesso vorrei illustrarle brevemente l’architettura della Bitcoin Blockchain e il suo funzionamento, elementi di base che costituiscono il contesto della nostra analisi tramite Petri Nets.

**Nella prima slide** notiamo che la Blockchain è un registro pubblico distribuito, un database globale in cui vengono memorizzate tutte le transazioni validate. Queste transazioni sono raggruppate in blocchi, formando una catena ordinata. In particolare, il modello UTXO (Unspent Transaction Outputs) è centrale: il saldo di un indirizzo corrisponde alla somma degli output non ancora spesi.

La struttura di ciascuna transazione è divisa in due sezioni:

- Gli **inputs** fanno riferimento agli UTXO derivanti da transazioni precedenti.
- Gli **outputs** indicano uno o più indirizzi (solitamente stringhe che iniziano con 1 o 4) e i relativi valori.

Gli utenti interagiscono con la rete attraverso dei portafogli digitali, che gestiscono le coppie di chiavi pubblica e privata. È importante sottolineare che, pur garantendo la tracciabilità delle transazioni, la Blockchain conserva un certo grado di anonimato in quanto registra solo gli indirizzi, senza associare informazioni personali.

**La seconda slide** ci offre una rappresentazione grafica semplificata di questo schema, evidenziando l’interazione tra transazioni (denominate con θᵢ) e indirizzi (indicati con αⱼ). Questo schema ci aiuta a visualizzare come ogni transazione influisca sul saldo degli indirizzi attraverso il meccanismo degli UTXO.

**Passando alla terza slide**, vediamo il processo di verifica delle transazioni e il mining. Le transazioni vengono trasmesse in modalità peer-to-peer e, in attesa di validazione, rimangono in uno stato “pending”. Per essere accettata, una transazione deve soddisfare regole ben definite:

- Ogni input deve fare riferimento a un UTXO valido.
- La somma degli output non può superare quella degli input, al netto di eventuali commissioni (fee).

Il processo di validazione è affidato ai miner, i quali risolvono un complesso problema computazionale noto come Proof-of-Work. In questo modo, il miner che per primo valida il nuovo blocco – il quale contiene, oltre alle transazioni, anche il riferimento al blocco precedente e altre informazioni chiave – riceve un premio in Bitcoin.

Questa panoramica sull'architettura e il funzionamento della Blockchain di Bitcoin rappresenta il fondamento su cui si sviluppa il nostro lavoro. Infatti, comprendere questi meccanismi è essenziale per apprezzare come il modello basato su **Petri Nets** ci consenta di analizzare, in modo nativo e strutturato, la dinamica delle transazioni e l’evoluzione della rete.

Passiamo ora ad approfondire il ruolo delle Petri Nets nella modellazione di questi sistemi complessi.

## Slide 5

Passiamo ora a parlare delle **Petri Nets**, un formalismo matematico particolarmente efficace per descrivere sistemi distribuiti e concorrenti. Come potrà vedere dalle slide, le Petri Nets si basano su un grafo bipartito formato da due tipi di nodi: i **places** e le **transitions**.

In pratica, i **places** rappresentano le condizioni, le risorse o gli stati del sistema, mentre le **transitions** sono gli eventi che, scatenandosi, modificano questi stati. È importante notare che il grafo è strutturato in modo bipartito: le connessioni (gli archi) esistono solo tra nodi di tipo diverso. Questi archi si dividono in due categorie:

- I **pre-arcs**, che collegano un place a una transition, indicano quali token vengono richiesti affinché la transition possa scattare.
- I **post-arcs**, invece, partono da una transition e arrivano a un place, rappresentando la produzione di token una volta che la transition è stata eseguita.

## Slide 6

Nella slide successiva viene illustrato il formalismo algebrico che definisce una Petri Net. Formalmente, essa è descritta come una quadrupla $N = (P, T, Pre, Post)$. Qui:

- $P$ rappresenta l’insieme dei places,
- $T$ quello delle transitions,
- $Pre$ e $Post$ sono le funzioni di incidenza che, in pratica, vengono rappresentate come matrici.

Queste matrici ci dicono quanti archi collegano ciascun place a ciascuna transition (in ingresso o in uscita, rispettivamente). L'idea chiave è che questo formalismo ci permette di descrivere in modo preciso e strutturato la connettività e il flusso di informazioni all'interno del sistema.

## Slide 7

Infine, il concetto di **marking** è fondamentale per rappresentare lo stato corrente della rete. Un marking è un vettore che assegna un numero di token a ciascun place. Quando una transition scatta, essa consuma token dai places in ingresso e ne produce in quelli in uscita, aggiornando così il marking e, di conseguenza, lo stato del sistema. Nel contesto del nostro lavoro, mentre riconosciamo l'importanza dei marking per modellare dinamiche, la nostra analisi si concentra prevalentemente sulla struttura della rete, quindi non definiamo uno specifico marking.

Questa combinazione di rappresentazione grafica e formale, che integra la visione intuitiva con una descrizione algebrica rigorosa, rende le Petri Nets uno strumento molto potente per analizzare sistemi complessi, come quello della Blockchain.

Di seguito un possibile discorso, suddiviso per slide, della durata complessiva di circa 1 minuto e 30 secondi per slide, che spiega in modo approfondito il modello delle Addresses Petri Net e l’algoritmo per il raggruppamento in Entities Petri Net.

## Slide 8

L’idea alla base di questo modello è quella di mappare in maniera naturale la struttura della Blockchain, dove le transazioni spostano bitcoin tra indirizzi, su un formalismo delle Petri Nets. In questo contesto definiamo due insiemi fondamentali: da un lato abbiamo l’insieme $\mathcal{A} = \{\alpha*1, \alpha_2, \dots, \alpha_m\}$ che raccoglie tutti gli indirizzi registrati nella Blockchain – siano essi presenti come input o output – e dall’altro l’insieme $\Theta = \{\theta_1, \theta_2, \dots, \theta_n\}$ delle transazioni validate.
Per costruire la nostra rete, definiamo $N*\alpha = (P\_\alpha, T, \mathbf{PreA}, \mathbf{PostA})$ dove:

- $P\_\alpha$ è l’insieme dei places, ciascuno dei quali corrisponde a un indirizzo;
- $T$ è l’insieme delle transitions, una per ogni transazione;
- Le matrici $\mathbf{PreA}$ e $\mathbf{PostA}$ rappresentano, rispettivamente, le connessioni dai places alle transitions e viceversa.
  Questo approccio, che si basa su una scansione completa della Blockchain per identificare ogni nuovo indirizzo e transazione, permette di rappresentare in un’unica struttura sia la parte statica (gli indirizzi) che quella dinamica (le transazioni) della rete.

Passiamo ora alla slide successiva, in cui ci focalizziamo su come vengono costruite le matrici di incidenza.

## Slide 9

Approfondiamo il processo di costruzione delle matrici $\mathbf{PreA}$ e $\mathbf{PostA}$.
Consideriamo una transazione $\theta$ che viene suddivisa in due insiemi:

- $\textbf{In}(\theta)$, l’insieme degli indirizzi di input,
- $\textbf{Out}(\theta)$, l’insieme degli indirizzi di output.
  Il corrispondente evento nella nostra rete, rappresentato dalla transition $t$, viene così connesso ai places corrispondenti agli indirizzi. In pratica:
- Per ogni indirizzo $\alpha \in \textbf{In}(\theta)$, aggiungiamo un arco – detto pre-arc – dal place $p\alpha$ verso la transition $t$ e impostiamo $\mathbf{PreA}(p\alpha,t)=1$;
- Per ogni indirizzo $\alpha \in \textbf{Out}(\theta)$, aggiungiamo un arco – post-arc – dalla transition $t$ al relativo place $p\alpha$, impostando $\mathbf{PostA}(p\alpha,t)=1$.
  Le matrici risultanti hanno dimensione $m \times n$ e codificano, in maniera algebrica, la struttura delle transazioni sulla Blockchain. Questo formalismo non solo offre una rappresentazione intuitiva, ma facilita anche successive analisi, ad esempio per determinare il numero di UTXO per ogni indirizzo.

Con ciò in mente, passiamo adesso a un esempio pratico che ci aiuti a visualizzare concretamente la nostra Addresses Petri Net.

## Slide 10

In questa slide osserviamo un esempio semplificato: abbiamo 6 places, corrispondenti agli indirizzi $P\_\alpha = \{p\alpha_1, p\alpha_2, \dots, p\alpha_6\}$, e 7 transitions, una per ciascuna transazione $\theta$ della nostra sequenza.
Il diagramma grafico, che potete vedere al centro della slide, mostra chiaramente come ogni transazione sia collegata agli indirizzi in ingresso e in uscita.
Questa rappresentazione ci permette di fare diverse considerazioni pratiche. Ad esempio, osservando la matrice $\mathbf{PreA}$, possiamo contare quante volte un certo indirizzo compare come input, mentre la matrice $\mathbf{PostA}$ evidenzia invece le occorrenze in output.
Un’analisi interessante consiste nel calcolare la differenza ($\mathbf{PostA} - \mathbf{PreA}$) per ogni riga: il numero di elementi non nulli corrisponde al numero di UTXO associati a quell’indirizzo. Se il risultato è zero, significa che il saldo dell’indirizzo è nullo.
Inoltre, è importante notare che transazioni con insiemi identici di input e output possono essere aggregate in un’unica transition, arricchita da un “firing clock” per rappresentare il loro comportamento dinamico.

Procediamo ora ad approfondire ulteriormente l’analisi delle matrici, esaminando nel dettaglio le informazioni che esse ci forniscono.

## Slide 11

Qui ci concentriamo sull’analisi delle matrici di incidenza.
La **Pre-incidence matrix $\mathbf{PreA}$**, mostrata nella slide successiva, ci consente di valutare la frequenza con cui un indirizzo appare come input in una transazione. Questo dato è fondamentale per comprendere la liquidità e la partecipazione degli indirizzi nella rete.
D’altra parte, la **Post-incidence matrix $\mathbf{PostA}$** fornisce una visione sui flussi in uscita: ad esempio, un indirizzo che compare frequentemente in output potrebbe essere indicativo di un elevato livello di attività o di ricezione di fondi.
Analizzando la differenza tra le due matrici per ogni riga, otteniamo un indicatore immediato della presenza o meno di UTXO per quell’indirizzo, il che, a sua volta, si traduce in informazioni sul saldo.
Queste analisi sono particolarmente utili per effettuare simulazioni dinamiche e per studiare il comportamento evolutivo della rete.

Adesso, vediamo nello specifico la rappresentazione grafica della Pre-incidence matrix per l’esempio considerato.

## Slide 12

Qui possiamo osservare la matrice $\mathbf{PreA}$ corrispondente al nostro esempio.
Ogni riga rappresenta un indirizzo, mentre ogni colonna corrisponde a una transazione.
Ad esempio, dalla prima riga vediamo che il place $p\alpha_1$ non ha alcun arco in ingresso per la maggior parte delle transazioni, mentre nella terza colonna è presente un valore pari a 1, che indica la presenza di un pre-arc collegato a quella transazione.
Questo tipo di informazione ci permette di dedurre, per ogni indirizzo, il numero di volte in cui ha partecipato come input, fondamentale per una corretta analisi dello stato dei saldi nella rete.

Infine, passiamo alla slide successiva, in cui analizziamo la Post-incidence matrix.

## Slide 13

In questa slide vediamo la matrice $\mathbf{PostA}$, che riassume le connessioni dai vari eventi (le transazioni) agli indirizzi di output.
Ogni elemento pari a 1 indica che, per quella transazione, un determinato indirizzo ha ricevuto un output.
Ad esempio, dalla prima riga si nota che l’indirizzo $p\alpha_1$ riceve un token nelle transazioni indicate, confermando così il passaggio di bitcoin a quell’indirizzo.
Analizzando insieme le due matrici, possiamo ricavare numerose statistiche sul comportamento degli indirizzi, come il numero di UTXO o la frequenza delle transazioni in ingresso e in uscita.
Questo approccio consente, in maniera integrata, di rappresentare sia la struttura che la dinamica della Blockchain.

Di seguito un possibile discorso, suddiviso per slide, della durata di circa 1 minuto e 30 secondi per slide, che spiega in modo dettagliato la sezione relativa alle Entities Petri Net e l’algoritmo ad esse associato.

---

## Slide 14

Passiamo ora alla seconda parte del lavoro, concentrandoci sulle Entities Petri Net. Come ben sappiamo, molti utenti di Bitcoin possiedono più di un indirizzo, utilizzandoli non solo per facilitare gli scambi, ma anche per migliorare il proprio livello di anonimato. In questo contesto, definiamo un’**entity** come l’insieme di indirizzi controllati dalla stessa persona, organizzazione o gruppo. La chiave qui è che tutti gli indirizzi che compaiono nella sezione di input di una singola transazione devono necessariamente appartenere alla stessa entity, perché il trasferimento dei fondi richiede il possesso di tutte le relative chiavi private.

Questa osservazione non è solo teorica, ma ha importanti implicazioni pratiche: raggruppando gli indirizzi in entity, possiamo ottenere un’analisi a un livello più elevato della Blockchain, riducendo la complessità del sistema e mappando in maniera più naturale gli attori economici reali. In altre parole, passando dal livello degli indirizzi a quello delle entity, otteniamo una visione più coerente e semplificata delle interazioni sul network. Questo approccio ci permette di tracciare, ad esempio, i flussi di bitcoin non solo tra singoli indirizzi, ma tra utenti o organizzazioni, fornendo così uno strumento potente per analisi statistiche e simulazioni dinamiche.

Procediamo ora alla definizione formale e alla mappatura degli indirizzi nelle entity.

## Slide 15

In questa slide definiamo formalmente il passaggio dal livello degli indirizzi a quello delle entity. Partiamo definendo l’insieme degli indirizzi, $\mathcal{A}=\{\alpha_1, \alpha_2, \dots, \alpha_m\}$, e l’insieme delle transazioni, $\Theta=\{\theta_1, \theta_2, \dots, \theta_n\}$. Nel nostro modello di Addresses Petri Net, ogni indirizzo è rappresentato da un place, indicato come $p\alpha$, e ogni transazione da una transition, il tutto codificato tramite le matrici $\mathbf{PreA}$ e $\mathbf{PostA}$.

Per raggruppare gli indirizzi in entity, definiamo un’**entity** $\epsilon$ come un sottoinsieme degli indirizzi, ossia $\epsilon\subseteq \mathcal{A}$. Raggruppiamo tutte queste entity nell’insieme $E=\{\epsilon*1, \epsilon_2, \dots, \epsilon_k\}$. Successivamente, nella Entities Petri Net $N*{\epsilon}=(P\_{\epsilon}, T, \mathbf{PreE}, \mathbf{PostE})$ ogni place $p\epsilon$ corrisponde ad una entity. In questo modo, mantenendo invariato l’insieme delle transazioni $T$ (lo stesso che utilizziamo nella Addresses Petri Net), possiamo rielaborare le matrici di incidenza aggregando i dati degli indirizzi che compongono ciascuna entity.

Questa mappatura è fondamentale perché ci permette di analizzare il comportamento degli attori reali, semplificando la complessità derivante dalla presenza di numerosi indirizzi, e rendendo più evidente il flusso di bitcoin tra le varie entity.

Adesso passiamo alla parte operativa, illustrando l’algoritmo che ci consente di determinare automaticamente quali indirizzi appartengono alla stessa entity.

## Slide 16

In questa slide vediamo l’algoritmo utilizzato per calcolare l’insieme $E$ delle entity partendo dalla Addresses Petri Net.
L’algoritmo parte dall’insieme delle transazioni $T$ – indicato come $T^\*$, l’insieme delle transazioni ancora da esaminare – e procede in maniera iterativa. Per ogni transazione $t$ selezionata, inizializziamo un nuovo insieme $e$ che rappresenta la potenziale entity. In particolare, per ogni place $p_i$ tale che $\mathbf{PreA}(p_i,t)=1$, aggiungiamo $p_i$ a $e$; questi sono gli indirizzi che compaiono come input in quella transazione e, quindi, devono appartenere alla stessa entity.

Successivamente, l’algoritmo espande $e$ utilizzando un set ausiliario $e^\*$ – che rappresenta i places ancora da esplorare – per trovare ulteriori transazioni che coinvolgono uno qualsiasi degli indirizzi già inclusi in $e$. Per ogni place non ancora esaminato, si cercano tutte le transazioni in cui quel place compare come input e, per ciascuna di esse, si aggiungono ulteriori indirizzi che compaiono. In questo modo, l’algoritmo espande in maniera ricorsiva l’insieme $e$ fino a quando non è più possibile trovare nuovi indirizzi correlati. Infine, $e$ viene aggiunto all’insieme $E$ e l’algoritmo continua finché non sono state esplorate tutte le transazioni.

Questo procedimento garantisce che, per ogni transazione, gli indirizzi utilizzati in input – e quelli eventualmente connessi tramite ulteriori transazioni – vengano raggruppati correttamente in un’unica entity. Inoltre, possiamo verificare la correttezza dell’algoritmo osservando che ogni transazione viene processata una sola volta e che, alla fine, gli insiemi ottenuti sono mutuamente disgiunti e coprono tutti i places della Addresses Petri Net.

Con l’algoritmo in mente, vediamo ora come vengono costruite le matrici aggregate e la rappresentazione grafica della Entities Petri Net.

## Slide 17

In questa ultima slide, esaminiamo la fase di aggregazione delle matrici di incidenza per la Entities Petri Net.
Una volta ottenuto l’insieme $E$ delle entity, per ciascuna entity $e \in E$ identifichiamo i places $p\alpha$ della Addresses Petri Net che la compongono. Le matrici $\mathbf{PreE}$ e $\mathbf{PostE}$ vengono quindi generate sommando le righe corrispondenti agli indirizzi in $e$ delle matrici originali $\mathbf{PreA}$ e $\mathbf{PostA}$. In questo modo, ogni riga nelle nuove matrici rappresenta il comportamento aggregato di una entity: si ottiene una visione unificata degli input e degli output relativi a quell’insieme di indirizzi.

Ad esempio, se nella nostra analisi semplificata notiamo che i places $p\alpha_2$, $p\alpha_3$ e $p\alpha_6$ appaiono insieme nelle transazioni, l’algoritmo li raggruppa in una unica entity, che viene poi rappresentata da un singolo place $p\epsilon$ nella Entities Petri Net. Le matrici risultanti, $\mathbf{PreE}$ e $\mathbf{PostE}$, ci consentono di estrarre informazioni aggregate, come il numero complessivo di UTXO associati a quell’entity, o la frequenza delle transazioni in cui essa ha partecipato.

Questo processo di aggregazione non solo semplifica l’analisi, riducendo la complessità della rete, ma fornisce anche una rappresentazione più aderente alla realtà, dove un singolo utente o organizzazione opera attraverso molteplici indirizzi. La grafica che vedete nella slide finale mostra esattamente come le entity, una volta aggregate, si colleghino alle stesse transazioni del modello originale, offrendo una visione unificata e dinamica del sistema.

## Slide 18

Questa slide descrive il processo di acquisizione ed elaborazione dei dati della Blockchain utilizzato in questo studio.

Per analizzare la Blockchain, gli autori hanno scelto di scaricare i blocchi formattati in JSON dal sito _blockchain.info_, evitando di dover elaborare direttamente i dati grezzi dal network peer-to-peer. L'analisi si è concentrata sui primi 180.000 blocchi, che coprono un periodo di circa tre anni e mezzo, da gennaio 2009 a marzo 2012, permettendo un confronto con studi precedenti, come quello di Ron e Shamir.

L'elaborazione è stata realizzata interamente in R, utilizzando RStudio. Il tempo totale di elaborazione è stato di circa 250 ore, con un tempo medio di 5 secondi per blocco. Questo valore dipende dal numero di indirizzi presenti in ogni blocco, poiché il modello basato su reti di Petri deve considerare ogni indirizzo coinvolto nelle transazioni.

Il diagramma mostra il flusso di elaborazione dei dati. I file JSON scaricati occupano circa 2.8GB, mentre la rappresentazione finale della rete di indirizzi in R richiede circa 800MB in RAM. Tuttavia, salvando i dati elaborati in formato _RData_, lo spazio si riduce a 40MB.

Questo approccio ha permesso agli autori di esaminare le dinamiche delle transazioni e di costruire un modello per l'analisi della Blockchain in un periodo storico significativo.

Di seguito un possibile discorso, suddiviso per slide, che spiega in dettaglio i risultati ottenuti con il modello basato sulle Addresses Petri Net. Ricorda che sto presentando il lavoro degli autori, non il mio.

## Slide 19

In questa prima slide vengono presentate le statistiche globali ottenute dall’analisi della Blockchain utilizzando il modello basato sulle Addresses Petri Net. Gli autori hanno individuato 3.730.480 indirizzi distinti e 3.142.019 transazioni, che corrispondono rispettivamente al numero di righe e colonne delle matrici \(\mathbf{PreA}\) e \(\mathbf{PostA}\). Ogni indirizzo è stato associato al proprio place all’interno della rete, mentre ogni transazione corrisponde a una transition.

Esaminando le matrici, si è rilevato che ci sono in totale 4.575.888 pre-arcs e 7.352.494 post-arcs, il che significa che, per ogni indirizzo, il numero di elementi non nulli nella riga di \(\mathbf{PreA}\) indica quante transazioni in ingresso ha ricevuto, mentre quella in \(\mathbf{PostA}\) mostra quante transazioni in uscita sono state effettuate.

Le curve CCDF, che trovate a destra e a sinistra della slide, evidenziano una distribuzione in legge di potenza: la maggior parte degli indirizzi registra poche transazioni, mentre soltanto un numero ridotto di indirizzi ha un’attività molto elevata. Questo tipo di distribuzione è tipico dei sistemi complessi e conferma l’efficacia del formalismo delle Petri Net nel catturare le dinamiche della Blockchain. In altre parole, il modello permette di ottenere in maniera semplice informazioni cruciali, quali il numero di transazioni in ingresso e in uscita per ciascun indirizzo.

## Slide 20

Passando alla seconda slide, qui gli autori si concentrano sull’identificazione delle tipologie di indirizzi in base al loro utilizzo. Per valutare l’attività di ciascun indirizzo, essi hanno sommato il numero di elementi non nulli presenti nelle righe di \(\mathbf{PreA}\) e \(\mathbf{PostA}\). In questo modo è possibile identificare le ‘address’ maggiormente utilizzate.

Un risultato particolarmente interessante è l’identificazione di 609.295 indirizzi che presentano righe completamente vuote in \(\mathbf{PreA}\) – cioè, mai utilizzati per spendere bitcoin – ma almeno un elemento non nullo in \(\mathbf{PostA}\). Questi indirizzi, che non hanno mai effettuato spese, sono usati unicamente per accumulare fondi; alcuni di essi risultano addirittura ‘dormienti’, ovvero, una volta ricevuti i bitcoin, non vengono più utilizzati. Nella tabella riportata in questa slide, vengono mostrati i primi cinque indirizzi in ordine di numero di transazioni in ingresso, insieme al saldo corrente verificato su blockchain.info. Tale analisi evidenzia come alcuni indirizzi, pur essendo molto attivi nel ricevere bitcoin, non partecipino alle operazioni di spesa, offrendo così un’interessante prospettiva sulle strategie di accumulo adottate dagli utenti.

## Slide 21

Nella terza slide gli autori approfondiscono il fenomeno delle ‘disposable addresses’. Questi sono indirizzi caratterizzati dall’utilizzo estremamente limitato: in pratica, vengono usati esattamente due volte, una volta per ricevere bitcoin e una volta per trasferirli completamente ad altri indirizzi. Dal punto di vista del modello, tali transazioni si riconoscono perché il corrispondente vettore colonna della matrice \(\mathbf{PreA}\) presenta un solo elemento non nullo, mentre quello di \(\mathbf{PostA}\) ne mostra due, in righe differenti.

Utilizzando questo criterio, il modello è stato in grado di identificare automaticamente le catene di transazioni che coinvolgono indirizzi usa e getta. I risultati sono significativi: sono state rilevate 122.155 catene di indirizzi disposable, che hanno coinvolto 1.350.010 indirizzi e transazioni. Il diagramma a destra della slide, che mostra la CCDF della lunghezza delle catene, evidenzia come la distribuzione sia molto eterogenea, con alcune catene particolarmente lunghe – la più estesa contiene ben 3.658 transazioni. Questo comportamento suggerisce che molti utenti adottino questa strategia per ragioni di anonimato o per ottimizzare la gestione dei fondi.

## Slide 22

Nell’ultima slide vengono presentati i risultati relativi ai modelli di transazioni ripetute. Gli autori hanno esaminato quante volte gli utenti eseguono transazioni con insiemi identici di indirizzi in input e output. Nel modello delle Petri Net, ciò si traduce in transitions con configurazioni identiche nei pre- e post-arcs.

I dati evidenziano che circa l’11% delle transazioni sono ripetizioni di altre, ovvero transazioni che coinvolgono esattamente lo stesso gruppo di indirizzi per l’input e per l’output. Questo fenomeno è indicativo di flussi di bitcoin costanti tra specifici gruppi di indirizzi, probabilmente legati a comportamenti abituali o a particolari strategie di trasferimento. La figura a destra della slide, che mostra la CCDF delle dimensioni dei gruppi di transazioni ripetute, illustra chiaramente come queste ripetizioni varino in grande misura, confermando la presenza di flussi stabili e significativi all’interno della rete.

In sintesi, questi risultati dimostrano come il formalismo delle Petri Net consenta non solo di rappresentare la struttura della Blockchain, ma anche di estrarre informazioni molto dettagliate sulle pratiche degli utenti, dalla frequenza delle transazioni alla gestione degli indirizzi disposable, fino all’identificazione di trasferimenti ripetuti.

## Slide 23

In questa prima slide vengono mostrati i risultati relativi alla distribuzione degli indirizzi tra le entity. Gli autori hanno applicato l’algoritmo di riduzione descritto in precedenza alla Addresses Petri Net, ottenendo così la Entities Petri Net. Il modello ha evidenziato che 2.461.010 entity controllano in totale 3.730.480 indirizzi.

È interessante notare come la distribuzione degli indirizzi tra le entity sia estremamente non uniforme e segua un andamento in legge di potenza. Cioè, molte entity possiedono un solo indirizzo, mentre soltanto poche entity controllano un numero elevato di indirizzi. Questa caratteristica è importante perché le entity che possiedono numerosi indirizzi hanno la capacità di influenzare una frazione significativa del flusso di transazioni bitcoin.

Il grafico CCDF che vedete in questa slide mostra precisamente questa distribuzione: sull’asse delle ascisse abbiamo il numero di indirizzi posseduti per entity, mentre sull’asse delle ordinate la probabilità complementare che un’entity possieda più di quel numero di indirizzi. Tale comportamento a coda pesante evidenzia la forte disparità nella distribuzione.

## Slide 24

Passando alla seconda slide, gli autori hanno analizzato il coinvolgimento delle entity nelle transazioni. In questo caso, l’analisi si basa sul numero di elementi non nulli nelle righe delle matrici \(\mathbf{PreE}\) e \(\mathbf{PostE}\), che rappresentano rispettivamente il numero di transazioni in ingresso e in uscita per ciascuna entity.

Anche qui si riscontra un andamento in legge di potenza: la maggior parte delle entity è coinvolta in un numero ridotto di transazioni, mentre poche entity partecipano a moltissime operazioni. Le due CCDF mostrate, una per \(\mathbf{PreE}\) e l’altra per \(\mathbf{PostE}\), confermano questa osservazione. Questi risultati evidenziano che, a livello di entity, il modello cattura efficacemente la forte eterogeneità nell’attività transazionale, fornendo così un quadro dettagliato su come il flusso di bitcoin sia concentrato in pochi attori molto attivi.

## Slide 25

La terza slide si concentra sull’identificazione delle entity più attive. Gli autori hanno determinato la 'popolarità' di un’entity sommando il numero di transazioni in ingresso e in uscita, cioè la somma degli elementi non nulli nelle righe di \(\mathbf{PreE}\) e \(\mathbf{PostE}\).

Dalla tabella presentata si evince che le entity più attive, ad esempio quella identificata come '95237', registrano valori molto elevati per le transazioni sia in ingresso che in uscita, pur essendo composte da un numero variabile di indirizzi. Alcuni di questi top entity sono associati a tag noti, come 'deepbit.net' o 'ilovethebtc', il che permette di collegare il modello a realtà del mercato e a specifici operatori. Inoltre, i saldi di ciascuna entity vengono calcolati sommando i saldi di tutti gli indirizzi che la compongono, evidenziando così come il controllo su numerosi indirizzi possa tradursi in un’influenza notevole sui flussi di bitcoin.

## Slide 26

Nell’ultima slide vengono presentati i risultati relativi ai pattern di transazioni ripetute tra le entity. Gli autori hanno rilevato che circa il 22,6% delle transazioni sono ripetizioni: ovvero, si verificano transazioni identiche in termini di set di indirizzi in input e in output tra le stesse entity.

Questa osservazione indica che esistono flussi stabili di bitcoin tra determinati attori, il che può essere interpretato come un comportamento tipico di trasferimenti regolari o di operazioni automatiche. Il grafico CCDF che vedete mostra la distribuzione delle dimensioni dei gruppi di transazioni ripetute, fornendo una chiara rappresentazione di quanto spesso queste ripetizioni si verifichino.

In sintesi, questi risultati evidenziano come il modello basato sulle Entities Petri Net permetta di analizzare non solo la distribuzione degli indirizzi tra gli attori, ma anche le dinamiche transazionali a un livello aggregato, fornendo spunti interessanti sulle strategie e sulle pratiche adottate dagli utenti della rete Bitcoin.

Di seguito vi propongo un discorso strutturato per presentare la sezione Analysis, in cui illustrerò sia i risultati dell'analisi degli utenti Bitcoin tramite Petri Nets sia i vantaggi del formalismo PT, ricordando che sto esponendo il lavoro degli autori e non il mio.

## Slide 27

In questa parte dello studio, gli autori hanno utilizzato il modello basato sulle Petri Nets per estrarre informazioni dettagliate sugli utenti della Blockchain. Il modello consente di raggruppare gli indirizzi Bitcoin in 'entity' o, in alcuni casi, in catene di indirizzi disposable, cercando di associare un'identità a ciascun gruppo.

Ad esempio, analizzando la Entities Petri Net, gli autori hanno evidenziato che 246.660 proprietari controllano circa 1,5 milioni di indirizzi. In aggiunta, studiando le catene di transazioni che coinvolgono indirizzi disposable – cioè indirizzi utilizzati esclusivamente per ricevere e poi trasferire bitcoin – si è arrivati a stimare che circa 122.155 proprietari controllano fino a 1,35 milioni di indirizzi coinvolti in queste catene.

La classificazione degli utenti è molto interessante. In particolare, il lavoro distingue tra:

- 368.815 'engaged' o utenti esperti, che adottano pratiche come l’uso di indirizzi disposable o l’impiego di più indirizzi nelle proprie operazioni – questi sono responsabili del 72,6% delle transazioni.
- 609.295 indirizzi che compaiono solo come output nelle transazioni e che probabilmente funzionano come indirizzi deposito per questi utenti attivi.
- Infine, i restanti 255.045 indirizzi sono associati a utenti occasionali.

Un ulteriore approfondimento è offerto dai casi di studio. Ad esempio, l'indirizzo più utilizzato in input, che appare in circa 270.000 transazioni, è stato identificato come appartenente a un noto mining pool – il DeepBit – ormai chiuso. D'altro canto, la più grande entity in output, composta da 156.725 indirizzi e raggruppante circa il 4,2% del totale degli indirizzi, è stata associata a diversi tag, tra cui 'ilovethebtc', 'mikeo' e altri, alcuni dei quali sono reperibili anche su risorse online, anche se alcune informazioni risultano oggi non più accessibili.

Infine, l'analisi delle curve CCDF dimostra come la distribuzione delle transazioni sia fortemente eterogenea: si osserva una coda pesante, che indica che mentre la maggior parte degli indirizzi e delle entity gestisce poche transazioni, alcuni attori – come i miner pool – sono coinvolti in un numero molto elevato di transazioni, probabilmente a causa del meccanismo di redistribuzione delle ricompense.

## Slide 28

Passando ora ai vantaggi del formalismo delle Petri Nets, gli autori evidenziano numerosi punti di forza che rendono questo approccio particolarmente adatto all'analisi delle transazioni Bitcoin.

In primo luogo, il formalismo PT permette di modellare dinamiche non deterministiche. Ciò significa che le transazioni abilitate – cioè quelle associate a UTXO non nulli – possono essere considerate eventi indipendenti, il cui verificarsi dipende da vari fattori, come la decisione dell'utente, il pagamento delle fee o il successo nella competizione per la validazione da parte dei miner. Questo rispecchia perfettamente la natura della Blockchain, in cui la validazione dei blocchi avviene in maniera probabilistica.

In secondo luogo, la potenza del modello PT risiede anche nella sua capacità di simulare dinamiche di sistema. A differenza dei semplici grafi bipartiti, che forniscono solo una visione statica, le Petri Nets consentono di modellare transazioni concorrenti e non in conflitto – ad esempio, più transazioni che vengono confermate nello stesso blocco. Inoltre, il formalismo permette di definire equazioni di stato, che possono essere usate per prevedere, in maniera probabilistica, gli stati futuri della rete, come ad esempio l'evoluzione dei flussi di bitcoin tra exchange, miner pool o altri attori.

Un terzo aspetto è la capacità di effettuare analisi sequenziali. Le Petri Nets, infatti, identificano automaticamente le catene di transazioni, come quelle composte da indirizzi disposable che vengono usate per preservare l'anonimato. Questo consente agli autori di studiare i flussi di bitcoin a livello di singolo utente o gruppo, offrendo così un'analisi molto dettagliata delle strategie adottate dagli utenti.

Infine, grazie all’uso delle matrici pre e post, il modello fornisce numerosi insight in maniera diretta: ad esempio, è possibile individuare facilmente gli indirizzi mai utilizzati per spendere bitcoin o rilevare transazioni ripetute, semplicemente effettuando operazioni standard sui dati. Questi risultati, ottenuti in maniera 'nativa' dal formalismo PT, sarebbero difficili da raggiungere con altri modelli, che sono solitamente limitati ad un’analisi statica.

In sintesi, il formalismo delle Petri Nets non solo consente di rappresentare accuratamente la struttura e le dinamiche della Blockchain, ma offre anche strumenti potenti per la simulazione e la previsione dei flussi di bitcoin, aprendo nuove prospettive per lo studio dell'economia digitale.

Questa conclusione evidenzia come l'approccio basato sulle Petri Nets, adottato dagli autori, offra una visione integrata e dinamica della Blockchain, capace di rivelare comportamenti complessi e di supportare simulazioni statistiche per futuri scenari di sviluppo. Se avete domande o volete approfondire alcuni aspetti, sono a disposizione per ulteriori chiarimenti. Grazie per l'attenzione.

## Slide 29

"Per concludere, questo lavoro ha introdotto un nuovo approccio per modellare la Blockchain attraverso le Reti di Petri.

Partendo dai primi 180.000 blocchi, che coprono circa 3 anni e mezzo di storia di Bitcoin, gli autori hanno costruito una rappresentazione formale in cui ogni indirizzo è modellato come un 'place' e ogni transazione come una 'transition'. L'intero sistema è descritto tramite matrici di incidenza, che catturano le relazioni tra input e output.

Questa formalizzazione ha permesso di identificare strutture interessanti nei dati. In particolare, sono emerse distribuzioni di tipo power-law in diversi aspetti della rete: nel numero di connessioni per transazione, nelle catene di indirizzi usa-e-getta e nei gruppi di transazioni che coinvolgono gli stessi indirizzi in input e output. Inoltre, analizzando la matrice di pre-incidenza, è stato possibile costruire una seconda Rete di Petri che rappresenta le entità reali dietro agli indirizzi, fornendo un livello di astrazione più alto.

Dal punto di vista computazionale, il lavoro ha dimostrato che, sebbene la dimensione attuale della Blockchain renda difficile un’analisi completa, è comunque possibile effettuare studi mirati su sottoinsiemi specifici, per esempio partendo da un gruppo di indirizzi di interesse.

Infine, gli autori suggeriscono che questo stesso modello potrebbe essere applicato ad altre blockchain, come Ethereum, che è diventata un punto di crescente interesse e rappresenta un possibile sviluppo futuro della ricerca.
