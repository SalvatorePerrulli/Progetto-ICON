# PROGETTO ICON
# 1 ROBOT WAREHOUSE – AI
Una società di e-commerce sta costruendo un nuovo magazzino e la società vorrebbe che tutte le operazioni di prelievo nel nuovo magazzino fossero eseguite da robot di magazzino. L’operazione di "prelievo" consiste nel raccogliere singoli articoli da varie posizioni del magazzino al fine di soddisfare gli ordini dei clienti. Dopo aver prelevato gli articoli dagli scaffali, i robot devono portare gli articoli in una posizione specifica all'interno del magazzino, utilizzando il percorso più breve possibile (per garantire la massima efficienza e produttività), dove gli articoli possono essere imballati per la spedizione.
## 1.1 L'ambiente 
L'ambiente è costituito da stati, azioni e ricompense. Gli stati e le azioni sono input per l'agente AI di Q-learning, mentre le azioni possibili sono gli output dell'agente AI. Gli stati nell'ambiente sono tutte le possibili posizioni all'interno del magazzino. Alcune di queste posizioni servono per riporre gli oggetti (quadrati neri), mentre altre sono corridoi che il robot può utilizzare per viaggiare in tutto il magazzino (quadrati bianchi). Il quadrato verde indica l'area di imballaggio e spedizione dell'articolo. I quadrati nero e verde sono stati terminali!![](https://github.com/SalvatorePerrulli/Progetto-ICON/blob/main/08-warehouse-map.png)

## 1.2 Obiettivo dell'agente AI
È apprendere il percorso più breve tra l'area di confezionamento degli articoli e tutte le altre posizioni del magazzino in cui il robot può viaggiare. Come mostrato nell'immagine sopra, ci sono 121 possibili stati (posizioni) all'interno del magazzino. Questi stati sono disposti in una griglia contenente 11 righe e 11 colonne. Ogni posizione può quindi essere identificata dal suo indice di riga e colonna.
## 1.3 Azioni 
Le azioni disponibili per l'agente AI consistono nel muovere il robot in una delle quattro direzioni:
[Su, Destra, Giù, Sinistra]
Ovviamente, l'agente AI deve imparare a evitare di guidare nelle posizioni di stoccaggio degli oggetti (ad esempio, scaffali).
##  1.4 Ricompense
L'ultima componente dell'ambiente che dobbiamo definire sono le ricompense. Per aiutare l'agente AI ad apprendere, a ogni stato (posizione) nel magazzino viene assegnato un valore di ricompensa. L'agente può iniziare da qualsiasi quadrato bianco, ma il suo obiettivo è sempre lo stesso: massimizzare le sue ricompense totali.
Le ricompense negative (cioè le punizioni) vengono utilizzate per tutti gli stati tranne l'obiettivo. Questo incoraggia l'IA a identificare il percorso più breve verso l'obiettivo riducendo al minimo le sue punizioni.
![](https://github.com/SalvatorePerrulli/Progetto-ICON/blob/main/08-warehouse-map-rewards.png)
Per massimizzare i suoi premi cumulativi (riducendo al minimo le sue punizioni cumulative), l'agente AI dovrà trovare i percorsi più brevi tra l'area di imballaggio dell'articolo (quadrato verde) e tutte le altre posizioni nel magazzino dove il robot è autorizzato a viaggiare (quadrati bianchi). L'agente dovrà anche imparare a evitare di schiantarsi contro le posizioni di deposito degli oggetti (quadrati neri).
##  1.5 Addestramento
Il nostro prossimo compito è che il nostro agente AI apprenda il suo ambiente implementando un modello di Q-learning. Il processo di apprendimento seguirà questi passaggi:
1. Scegli uno stato casuale, non terminale (quadrato bianco) per l'agente per iniziare questo nuovo episodio.
2. Scegli un'azione (sposta in alto, a destra, in basso o a sinistra) per lo stato corrente. Le azioni verranno scelte utilizzando un algoritmo _epsilon greedy_. Questo algoritmo solitamente sceglierà l'azione più promettente per l'agente AI, ma a volte sceglierà un'opzione meno promettente per incoraggiare l'agente a esplorare l'ambiente.
3. Esegui l'azione scelta e passa allo stato successivo (ovvero passa alla posizione successiva).
4. Ricevi la ricompensa per il passaggio al nuovo stato e calcola la differenza temporale.
5. Aggiorna il valore Q per la coppia di stato e azione precedente.
6. Se il nuovo stato (corrente) è uno stato terminale, vai al n. 1. Altrimenti, vai al n. 2.
L'intero processo verrà ripetuto in 1000 episodi. Ciò fornirà all'agente AI un'opportunità sufficiente per apprendere i percorsi più brevi tra l'area di imballaggio degli articoli e tutte le altre posizioni nel magazzino in cui il robot può viaggiare, evitando allo stesso tempo di schiantarsi in qualsiasi posizione di stoccaggio degli articoli.
##  1. 6 Ottieni percorsi più brevi
Ora che l'agente AI è stato completamente addestrato, possiamo vedere cosa ha imparato visualizzando il percorso più breve tra qualsiasi posizione nel magazzino in cui il robot può viaggiare e l'area di imballaggio degli articoli.

#  2 Q-learning
E' un paradigma di machine learning noto per l’apprendimento tramite rinforzo.
Il quale coinvolge un agente ai che opera in modo casuale nell’ambiente imparando una policy ottimale tramite osservazione, utilizzando stati e ricompense come input e le azioni come l’output sono conosciuti come model-free cioè l’agente ai non ha come obiettivo di conoscere un modello matematico o una distribuzione di probabilità come per il campionamento di Thompson, ma tenta di costruire una policy ottimale interagendo con l’ambiente dell’agente ai. Usa un approccio trial-and-error-based approach aggiornando la sua policy per ogni tentativo ed errore. Cioè tramite ricompense negative e positive l‘agente cerca di ridurre le punizioni totali(ricompense negative) e quindi la loro capacita di apprendimento sta nel rinforzo(sia positivo che negativo).
È importante specificare:  
1. Il numero di stati possibili (deve essere finito)
2. Il numero possibili di azioni (deve essere finito)
## 2.1 Q-Value
Il Q-value e' la qualita' di una azione per un particolare stato. Il Q-Value ottimale per la coppia stato-azione (s,a), indicato come Q*(s,a) è la somma delle future ricompense scontate, rappresentano una stima delle somme di futuri guadagni se dovessimo intraprendere una particolare azione in uno stato specifico, i valori stimano la quantità di ricompensa aggiuntiva che possiamo aspettarci di accumulare attraverso tutti i passaggi rimanenti negli episodi correnti se l’agente ai e attualmente nello stato s e prende azione a.
E il Q-values, pertanto, aumenta man mano che l'agente ai si avvicina sempre più alla ricompensa più alta e quindi una volta ottenuti Q-values ottimale, definire la policy ottimale e’ banale cioè quando si trova nello stato s basterà scegliere il Q-Values più alto per lo stato corrente: π* (s) = argmax (a) Q*(s, a) .![](https://github.com/SalvatorePerrulli/Progetto-ICON/blob/main/qvalues.PNG)
Si può dedurre che il Q-values e ‘una matrice tridimensionale data dallo stato (colonne e righe dell’ambiente) e dall’azione (up, down, right, left). E quindi nel nostro caso 11x11x4.
Il ruolo della Temporal Difference Learning è fondamentale permette di assicurare la convergenza dell’algoritmo, calcolando per ogni stato s una media mobile (running average) delle ricompense immediatamente ottenute lasciando lo stato.
## 2.2 Q-Table
Q-values sono memorizzati in Q-table dove la riga indica un possibile stato e la colonna una possibile azione.![](https://github.com/SalvatorePerrulli/Progetto-ICON/blob/main/qtable.PNG)
Un ottimale q table corrisponde a q-values ottimali, cioè contiene i valori che permettono all’agente di ai di prendere la migliore azioni in ogni possibile stato permettendo di percorrere il miglior percorso per il guadagno più alto. E quindi la q table rappresenta la policy dell’agente di ai per muoversi nell’ambiente.


