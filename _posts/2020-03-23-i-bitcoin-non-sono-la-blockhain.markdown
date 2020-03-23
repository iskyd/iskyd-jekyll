---
layout: post
title:  "I Bitcoin non sono la Blockchain!"
description: "Bitcoin, blockchain, criptovalute sono diventati uno dei topic più gettonati degli ultimi anni. Sono sulla bocca di tutti. Purtroppo però molte persone non hanno ancora ben chiaro cosa siano il Bitcoin e cosa sia invece la Blockchain.
Molto spesso ci si riferisce a Blockchain e Bitcoin come se fossero sinonimi. Ma la blockchain non trova il suo utilizzo unicamente nelle criptovalute"
date:   2018-10-08 12:46:45 +0100
categories: Blockchain
---
Bitcoin, blockchain, criptovalute sono diventati uno dei topic più gettonati degli ultimi anni. Sono sulla bocca di tutti. Purtroppo però molte persone non hanno ancora ben chiaro cosa siano il Bitcoin e cosa sia invece la Blockchain.  
Molto spesso ci si riferisce a Blockchain e Bitcoin come se fossero sinonimi.  
La blockchain non trova il suo utilizzo unicamente nelle criptovalute, ma è invece una tecnologia applicabile a, più o meno, qualsiasi situazione.

In questo articolo cercheremo di capire cosa è realmente la Blockchain, come è nata e come ha cambiato, e cambierà, il mondo.

_Questo articolo è pensato per essere letto da chiunque, anche per chi non ha alcuna conoscenza pregressa ne della blockchain ne dell'informatica in generale.  
Cercherò di spiegare ogni cosa nel modo più semplice possibile._

## Le origini

La blockchain ha assunto un'importanza sempre maggiore a partire dal 2008, quando Satoshi Nakamoto (la cui identità è ancora un mistero) pubblica il documento **[Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf), **di cui consiglio vivamente la lettura (sono solo 8 pagine). Bitcoin è stato poi implementato nel 2009.

Ma ahimè il concetto di blockchain è molto più antico.  
I primi a parlare di un sistema molto simile a quello della blockchain che oggi conosciamo sono Stuart Haber e W. Scott Stornetta che nel lontano 1991 pubblicano un documento: **[How to Time-Stamp a Digital Document](https://www.anf.es/pdf/Haber_Stornetta.pdf).**

Nella soluzione proposta da Haber e Stornetta per applicare il time-stamp a un documento digitale troviamo moltissimi dei concetti che rendono oggi la blockchain quello che è.  
_Vi consiglio di leggere prima questo articolo e poi leggere il documento di Haber e Stornetta._

> La blockchain è un insieme in continua crescita di record immutabili, chiamati blocchi, collegati tra loro.

Partiamo da questa defnizione e cerchiamo di capire meglio il concetto base della blockchain.

Che dati contengono i blocchi?

_In questa prima parte vedremo solamente una parte di quello che contengono i blocchi._

*   **Data**: contiene tutti i dati che si vogliono salvare, nel caso delle criptovalute, ad esempio, contiene le transazioni. Può contenere comunque qualsiasi tipo di informazioni in quanto al blockchain, come abbiamo detto, non trova la sua unica applicazione nelle criptovalute.
*   **Hash**: stringa di 64 caratteri che identifica un blocco
*   **Previous Hash**: stringa di 64 caratteri che è uguale al campo hash del blocco precedente. In questo modo tutti i blocchi sono collegati in una blockchain.

![](/files//Blockchain-300x131.jpg)

Nell'immagine vediamo come avviene il collegamento tra un blocco e il blocco precedente.

Un altro concetto importante, che è bene chiarire sin da subito, è il **genesis block**.  
Essendo la blockchain una catena ha bisogno di un inizio. Questo inizio è proprio il genesis block. Ciò che differenzia il genesis block da tutti gli altri blocchi è il previous hash in quanto il blocco iniziale non avrà nessun blocco precedente.

Ora che abbiamo visto in modo generico e basilare come è fatta la blockchain, cerchiamo di vedere in dettaglio quali sono i concetti su cui la blockchain è costruita.

*   **Hash**
*   **Immutable Ledger**
*   **Distrubuted P2P**
*   **Mining**
*   **Consensus Protocol**

### Hash

> E' una funzione non invertibile che mappa una stringa di qualsiasi lunghezza ad una stringa univoca di lunghezza fissa

Prendiamo per esempio l'impronta digitale.  
La nostra impronta digitale è il modo attraverso cui veniamo identificati.  
Possiamo dire che l'hash è per una stringa, un file, una qualsiasi cosa digitale, quello che è per noi l'impronta digitale.

Ci sono vari algoritmi di hash, bitcoin ad esempio utilizza lo [sha256](https://it.wikipedia.org/wiki/Secure_Hash_Algorithm).

Tutti gli algoritmi devono rispettare 5 requisiti per essere una funzione di hash:

*   **One way: **deve essere una funzione non invertibile ovvero partendo dal risultato non possiamo in alcun modo trovare il dato iniziale
*   **Deterministic: **la stessa funzione applicata allo stesso input di dati deve dare sempre lo stesso risultato
*   **Fast computation: **deve essere veloce da eseguire
*   **Avalanche effect: **se il dato in input viene cambiato leggermente, come ad esempio un solo bit, il risultato deve cambiare drasticamente
*   **Must withstand collision: **deve essere estremamente raro ottenere lo stesso risultato dati due diversi input.  
    E' bene chiarire un pò questo punto. Torniamo all'esempio precedente delle impronte digitali. Esiste una possibilità su 60 milioni che due persone abbiano le stesse impronte digitali. La stessa cosa accade per le funzioni di hash.  
    E' un problema? No.  
    Allora cosa è un problema? E' un problema se qualcuno riesce, partendo dall'hash desiderata, a generare una stringa un file ecc.. che diano quella specifica hash come risultato. Facciamo un esempio pratico. Voi avete un file e il risultato dell'hash del vostir file è (per esempio):  0061531F3FAE30FF99F9CFA2B026BCD012E345BAA1156650BA797132C2BDC15A  
    Voi quindi sapete che quello è il vostro file, ne siete certi. Ma cosa succede se qualcuno riesce **VOLONTARIAMENTE **a creare un file con un contenuto diverso ma che come hash abbia il vostro stesso? A questo punto sarebbe molto semplice sostituire i due documenti in modo che nessuno se ne accorga.  
    Questo è quello che non deve succedere.Nel 2017 google ha annunciato di aver ottenuto la prima collisione per l'algoritmo sha1\. Se siete interessati [qua](https://security.googleblog.com/2017/02/announcing-first-sha1-collision.html) il post di google.

Torniamo ora alla blockchain. In che modo il concetto di hash si applica?

Ogni blocco viene sottoposto a una funzione di hash e il risultato diventa il suo identificativo.

## Immutable ledger

Proviamo a immaginare una situazione reale dove il Libro mastro contiene gli immobili e a chi appartengono.  
Nei paesi del terzo mondo questi "ledger" sono ancora dei veri e propri libri scritti a mano, mentre nei paesi più sviluppati sono in forma digitale.  
Pensiamo a un file excel dove in ogni riga è specificato l'immobile e il proprietario.  
Cosa succede se qualcuno cancella una riga? Niente.  
Come c'è ne accorgiamo se qualcuno cancella una riga? Non possiamo.  
Allo stesso modo non possiamo accorgerci se qualcuno modifica una riga. Anche solo per errore.

Vediamo ora di applicare lo stesso concetto con la blockchain. All'interno del nostro campo "Data" abbiamo l'immobile e la sua proprietà.

![](/files//Blockchain-300x131.jpg)

_Prendiamo in riferimento di nuovo questa immagine._

Supponiamo che qualcuno voglia cambiare il contenuto del blocco numero 2\. Il suo identificativo (l'hash) cambierebbe. In questo modo la chain si romperebbe perchè il blocco numero 3 avrebbe un valore del campo previous hash diverso dal valore dell'hash del blocco numero 2.

Allo stesso modo se qualcuno vuole rimuovere il blocco numero 2 la chain si romperebbe.

Un malintenzionato per cambiare il contenuto del blocco numero 2 dovrebbe poi successivamente cambiare anche il contenuto di **tutti i blocchi successivi **in modo che il previous hash sia sempre integro e corrisponda all'hash del blocco precedente.  
Una volta cambiato il blocco numero 2 deve di conseguenza cambiare il previous hash del blocco numero 3\. Cambiando il previous hash anche l'hash del blocco numero 3 cambierebbe e quindi bisognerebbe cambiare anche il previous hash del blocco numero 4 e così via fino alla fine della chain.

## Distrubuted P2P

La blockchain è un sistema distribuito e decentralizzato, ovvero non esiste un master che "decide". Tutti i nodi della rete distribuita della blockchain hanno lo stesso ruolo.

**La blockchain è copiata e salvata su tutti i nodi della rete che si occuperanno di verificarne l'integrità.**

Torniamo all'esempio di prima. Un malintenzionato vuole cambiare il contenuto del blocco numero 2.  
Supponiamo che il malintenzionato riesca a cambiare anche tutti i blocchi successivi e quindi ad avere una chain integra. Cosa succede?  
Gli altri nodi della rete si accorgeranno che la blockchain di quel nodo è diversa dalla loro e quindi, attraverso un protocollo di consenso che vedremo successivamente, il nodo con la chain sbagliata la correggerà.

Il malintenzionato non dovrà quindi solo modificare tutti i blocchi della chain in modo da avere una chain integra ma **dovrà anche cambiarla sugli altri nodi**.

Risulta quindi abbastanza evidente di come non sia possibile manomettere la blockchain.

## Mining

Ecco che arriviamo al concetto di cui tutti parlano ma che in pochi conoscono davvero.  
Quante volte avete sentito di persone che usano il loro PC per fare mining e guadagnare soldi?

Il mining è un concetto importantissimo ed è alla base della blockchain. Vediamo quindi in cosa consiste.  
**plot twist: non vi farà diventare ricchi come in molti vi dicono.**

Come abbiamo visto prima il risultato di una funziona di hash è un insieme di numeri e lettere. Ma cosa rappresenta? E' un semplice numero in esadecimale.  
Nel sistema decimale che usiamo tutti i giorni ci sono 10 diversi numeri, dallo 0 al 9.  
Nel sistema esadecimale ne abbiamo 16, 10 numeri dallo 0 al 9 e 5 lettere A - B - C - D - E - F.

Quando un blocco deve essere aggiunto bisogna fare in modo che il risultato della funzione di hash sia inferiore a un determinato numero.  
Come possiamo controllare l'hash di un blocco senza cambiare i dati contenuti?  
All'interno di ogni blocco c'è un altro campo di cui non abbiamo ancora parlato, il nonce (number used only once).  
Questo campo non serve a niente se non a modificare l'hash del blocco.  
**Cambiando il valore del nonce l'hash del blocco cambierà.**

**Un miner quindi dovrà continuare a cambiare il valore del nonce finchè l'hash del blocco non sarà un numero inferiore a un numero scelto.**

Questo ci porta ad un altro concetto, i **leading zeros**.  
Non è nulla di diversod a quanto spiegato prima.  
Ricordiamo che il risultato di una funziona di hash sono sempre 64 caratteri. Pensiamo per semplicità di essere in un sistema decimale e che il numero di caratteri sia 4.  
Per avere un numero inferiore a 0100 dovremo avere come primi due numeri due zeri.

0099 < 0100

Se vogliamo avere un numero inferiore a 10 dovremo avere tre leading zeros.

0009 < 0010

Questo concetto viene applicato alla funzione di hash nel sistema esadecimale (niente di diverso rispetto a quanto detto prima, per essere aggiunto il risultato dell'hash di un blocco dovrà essere inferiore a un numero scelto, che quindi dovrà avere almeno n leading zeros).

Torniamo al concetto di mining.  
Prima di aggiungere un blocco i miner dovranno trovare il corretto nonce.  
Più sono i leading zeros più tempo ci vorrà a trovare il nonce corretto.  
Siccome trovare il nonce richiede molto tempo e molta potenza computazionale quando un nodo risolve il "puzzle" riceve una ricompensa.

Vediamo cosa succede con i bitcoin ad esempio. Quando un miner trova il nonce corretto e quindi aggiunge il blocco alla chain riceve una ricompensa di 12,50 bitcoin (ogni tot blocchi aggiunti il reward viene dimezzato, ma questo lo vedremo in un altro articolo).  
Sempre nel protocollo bitcoin, ad esempio, mediamente viene aggiunto un blocco ogni 10 minuti.  
Come è possibile questo? In caso la media con cui vengono aggiunti i blocchi fosse inferiore ai 10 minuti cambierebbe il numero rispetto al quale bisogna trovare un hash inferiore in modo da rendere più difficile risolvere il puzzle, ma anche questo lo vedremo in dettaglio in un altro articolo riferito ai bitcoin.

Un concetto fondamentale del mining è che deve essere **difficile da trovare ma facile da verificare**.

Ovviamente abbiamo capito che trovare un nonce corretto richiede molto tempo.  
Una volta trovato il nonce però è molto facile verificare che esso sia corretto. Basta effettuare la funzione di hash sul blocco e controllare che esso abbiamo un valore inferiore del famoso numero scelto (ricordatevi che uno dei requisiti di una funzione è hashing è che deve essere veloce da calcolare).

**Consensus Protocol**

Cosa succede quando un nodo trova il nonce corretto?  
Il blocco viene aggiunto alla chain e tutti gli altri nodi verificheranno il risultato proposto dal "vincitore".  
Una volta raggiunto il consenso il blocco viene propagato su tutti i nodi.

Cosa succede se uno o più nodi prova a imbrogliare e aggiunge un blocco non valido? Tutti gli altri nodi rifiuteranno il nuovo blocco e le chain verranno corrette.

Cosa succede invece se due nodi trovano contemporaneamente il nonce?  
Il blocco verrà aggiunto in primo luogo a entrambi i nodi che poi lo propagheranno al resto della rete. Supponiamo di avere una rete con 5 nodi. Ovviamente tra i vari nodi potrebbe esserci una velocità di connessione diversa, quindi il primo nodo che ha trovato il nonce propaga il blocco ad altri due nodi che lo aggiungeranno alla loro chain (essendo il blocco valido). L'altro nodo vincitore invece lo propagherà solo ad un altro nodo (l'unico restante), che anche lui come gli altri nodi lo aggiungerà alla sua blockchain.

Quale delle due sarà considerata corretta?  
In quel momento nessuna, entrambe vengono aggiunte e considerate valide.  
Si aspetta il prossimo blocco. La prima delle due blockchain che avrà un nuovo blocco sarà la blockchain che vincerà.  
**La blockchain più lunga è quella considerata corretta.**

Quando verrà aggiunto un nuovo blocco la blockchain corretta verrà quindi copiata sui nodi che precedentemente avevano aggiunto un blocco differente.  
**Il reward viene quindi dato solo a chi ha aggiunto il blocco alla chain corretta.**

A questo punto ci siamo fatti un idea su come la tecnologia della blockchain funziona.  
E' facile intuire perchè viene considerata una tecnologia con un grandissimo potenziale e applicabile a quasi qualsiasi situazione.  
Vedremo nei prossimi articoli di approfondire quanto visto a grandi linee in questo articolo.

Per qualsiasi dubbio, curiosità, suggerimenti, correzioni o per farmi sapere cosa ne pensate non esitate a **commentare qua sotto**!
