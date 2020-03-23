---
layout: post
title:  "Intonazione e Temperamento"
description: "In questo articolo analizzeremo nel dettaglio i diversi sistemi di intonazione che hanno dominato la musica durante i secoli a partire dall'intonazione naturale per arrivare al temperamento equabile che domina la musica al giorno d'oggi."
date:   2019-09-10 14:16:45 +0100
categories: Armonia
---
Durante il corso della storia sono stati usati diversi sistemi di intonazione e temperamento, ognuno con le sue caratteristiche.

Partiamo da un'assunzione a cui sono arrivate tutte le civiltà, da oriente a occidente: una corda lunga 1/2 di un'altra corda, nelle stesse condizioni, produrrà un suono un'ottava più in alto (viceversa una corda lunga il doppio produrrà un suono un'ottava più in basso). 

Questo, insieme all'unisono 1:1, rappresenta il nostro ratio di partenza, 2:1.

Il ratio più semplice dopo 2:1 è rappresentato da 3:2, quindi una corda lunga 2/3 di un'altra corda, nelle stesse condizioni, produrrà un suono una quinta perfetta più in alto.  
L'intervallo di quinta perfetta (3:2) è l'intervallo più consonante ed è per questo che è stato usato da Pitagora come intervallo generatore di tutta la scala.

Inoltre questi ratio semplici (generatori) rappresentano la tetractys (A dimostrazione dell'importanza che il simbolo aveva per Pitagora, la scuola portava questo nome e i suoi discepoli prestavano giuramento sulla tetraktys): 1:1 (unisono), 2:1 (ottava), 3:2 (quinta perfetta), 4:3 (quarta perfetta).

**La scala pitagorica **nasceva quindi dalla successione di intervalli di quinta perfetta. Ipotizzando che la nostra nota di partenza abbia una frequenza di 220hz (A) generiamo la scala pitagorica: 

*   220 * 3/2 = 330 (questa frequenza rappresenta il E, quinta perfetta della nostra nota di partenza A)
*   330 * 3/2 = 495 (essendo una frequenza superiore all'ottava lo dividiamo per due in modo da ottenere la stessa nota un'ottava più in basso, seguendo come abbiamo visto il ratio dell'ottava 2:1). 495/2 = 247,5

e così via, ottenendo le seguenti frequenze:

220, 234.931640625, 247.5, 264.298095703125, 278.4375, 297.3353576660156, 313.2421875, 330.0, 352.3974609375, 371.25, 396.4471435546875, 417.65625

Ogni 12 intervalli di quinta ritorniamo all'ottava di partenza, quindi a una frequenza di 440hz ma in realtà seguendo la scala pitagorica non arriviamo esattamente a 440hz.  
Questa discrepanza è detta comma pitagorica.

**L'intonazione pura **(o **just intonation**) è un'intonazione che si basa sulla successione naturale degli armonici. In questo modo quando due intervalli ad intonazione pura vengono suonati non si crea nessuna interferenza tra di loro.  
A differenza della scala pitagorica vengono definiti i ratio di altri due intervallo, la terza maggiore a 5/4 e la terza minore a 6/5\. Le altre note vengono trovate dalla differenza con questi ratio già definiti ottenendo:

*   unisono: 1
*   seconda maggiore: 9/8
*   terza maggiore: 5/4
*   quarta giusta: 4/3
*   quinta giusta: 3/2
*   sesta maggiore: 5/3
*   settima maggiore: 15/8
*   ottava: 2/1

Prendendo come fondamentale sempre la frequenza di 220 (A) queste sono le frequenze che formano gli intervalli sopra indicati:

[220.0, 247.5, 275.0, 293.3333333333333, 330.0, 366.6666666666667, 412.5, 440.0]

In musica la distanza tra due intervalli si misura in **cent**. Il cent è la 1200esima parte di un'ottava. Questa misura deriva dal temperamento equabile in cui ci sono 12 semitoni con la stessa distanza, una distanza di 100 cent (1200 / 12).  
Per trovare la distanza in cent tra due intervalli possiamo applicare la seguente formula: 1200 * log2(f2 / f1), dove f2 e f1 sono le due frequenze e f2 > f1.

Proviamo a calcolare ora la differenza in cent tra le frequenze della scala pitagorica e dell'intonazione pura.

*   intonazione pura 220.0 - scala pitagorica 220 = 0.0 cents
*   intonazione pura 247.5 - scala pitagorica 247.5 = 0.0 cents
*   intonazione pura 275.0 - scala pitagorica 278.4375 = 21.50628959671478 cents
*   intonazione pura 293.3333333333333 - scala pitagorica 297.3353576660156 = 23.460010384649014 cents
*   intonazione pura 330.0 - scala pitagorica 330.0 = 0.0 cents
*   intonazione pura 366.6666666666667 - scala pitagorica 371.25 = 21.50628959671478 cents
*   intonazione pura 412.5 - scala pitagorica 417.65625 = 21.50628959671478 cents
*   intonazione pura 440.0 - scala pitagorica 440 = 0.0 cents

In questo modo possiamo vedere le differenze e le analogie tra i due tipi di intonazione.  
In particolare la terza maggiore risulta essere più larga nella scala pitagorica rispetto all'intonazione pura. Questo viene spesso sottolineato come problema in quanto l'intervallo di terza maggiore è un intervallo fondamentale e non può essere dissonante (una dissonanza che ormai siamo abituati a sentire visto che anche nel temepramento equabile la terza risulta più grande).

Andiamo più nel dettaglio, analizziamo la distanza di tono che troviamo tra tutti gli intervalli di seconda maggiore nella just intonation (A-B, B-C#, D-E....):

*   root - 2nd: 1.125 = 203.91000173077484 cents
*   2nd - 3rd: 1.1111111111111112 = 182.40371213406007 cents
*   4th - 5th: 1.125 = 203.91000173077484 cents
*   5th - 6th: 1.1111111111111112 = 182.40371213406007 cents
*   6th - 7th: 1.125 = 203.91000173077484 cents

Come possiamo vedere abbiamo due diversi tipi di tono, uno con distanza 203.9 cents e uno con una distanza di 182.4 cents.  
Questo è il motivo per cui l'intonazione pura è limitato a una sola tonalità (e neanche all'interno della stessa tonalità, ma lo vedremo più avanti). Prendiamo ad esempio il 5 grado della scala (E) che ha una frequenza di 330hz e calcoliamo il suo secondo grado (F#) attraverso il ratio visto precedentemente: 371.25hz.  
Possiamo quindi notare che il F# come sesto grado di A ha una frequenza di 366.6hz mentre come secondo gradi di A ha una frequenza di 371.25hz.

Questo è un grosso problema per gli strumenti ad intonazione fissa come il pianoforte, che dovrebbe riaccordarsi ad ogni cambio di tonalità. Un discorso a parte va invece fatto per gli strumenti senza intonazione fissa come ad esempio gli archi (violino ecc..) o la voce. Loro possono mantenere la corretta intonazione in base alla tonalità senza doversi riaccordare, e potrebbero anche variare l'intonazione all'interno dello stesso brano nel caso di più tonalità.

A questo punto possiamo affermare che abbiamo due tipi di tono:

*   Tono maggiore: 9/8
*   Tono minore: 10/9

Per quanto riguarda i semitoni invece si trovano alla stessa distanza:

*   3rd - 4th: 1.0666666666666667 = 111.73128526977776 cents
*   7th - 8th: 1.0666666666666667 = 111.73128526977776 cents

Come anticipato precedentemente con l'intonazione pura non possiamo neanche ottenere tutti gli accordi con intervalli puri neanche all'interno della stessa tonalità.  
Prendiamo ad esempio il D (293.3333333333333hz) e il F (352hz). Dovrebbero avere un ratio di 6/5 come abbiamo visto precedentemente mentre vediamo che differisce da una terza minore pura di 21,51 cents:

1200 *  log2(352 / 293.3333333333333) = 294.13499740383764  
1200 *  log2(6/5) = 294.13499740383764 = 21,51

Analizziamo ora la distanza tra gli intervalli di tono e semitono per la scala pitagorica come fatto per la scala pura:

*   root - 2nd: 1.125 = 203.91000173077484 cents
*   2nd - 3rd: 1.125 = 203.91000173077484 cents
*   4th - 5th: 1.1098579146132872 = 180.44999134612573 cents
*   5th - 6th: 1.125 = 203.91000173077484 cents
*   6th - 7th: 1.125 = 203.91000173077484 cents

Tutti gli intervalli di seconda maggiore hanno la stessa distanza ad eccenzione dell'intervallo che si forma tra il quarto e il quinto grado che è più piccolo di 23cents.  

Anche gli intervalli di semitono risultano differenti:

*   3rd - 4th: 1.06787109375 = 113.68500605771193 cents
*   7th - 8th: 1.0534979423868314 = 90.22499567306306 cents

Per ovviare ai problemi visti con l'intonazione pura (dover riaccordare per ogni differente tonalità e impossibilità di avere accordi puri anche all'interno della stessa tonalità) e con la scala pitagorica (wolf fifth e terza maggiore più grande dell'intervallo puro) sono stati adottati dei **temperamenti**.

Il **temperamento **è un sistema usato per modificare gli intervalli in modo da ottenere un'intonazione "migliore", come ad esempio il **temperamento equabile **o il **meantone temperament.**

Il **temperamento meantone **è un temperamento in cui vengono modificate le quinte per migliorare le terze (per risolvere il problema della scala pitagorica).  
Il temperamento meantone più famoso è il quarter comma meantone in cui le quinte vengono modificate di 1/4 del syntonic comma (differenza tra l'intervallo di terza puro e quello della scala pitagorica). Il syntonic comma corrisponde  a 21,5 cents.

Quattro intervalli di quinta formano un intervallo di terza maggiore: **A** - E - B - F# - **C#**  
Ma come abbiamo visto prima nella scala pitagorica questo intervallo non è puro, ma modificando ogni quinta di 1/4 del syntonic comma (in modo da "spalmare" questa differenza su tutte le quinte e non su una soltanto, rendendola inutilizzabile), otteniamo un intervallo di terza maggiore puro.

A questo punto l'intervallo di quinta non sarà più puro ma sarà più piccolo, infatti sottraiamo da ogni quinta 1/4 del syntonic comma:

*   Intervallo di quinta nell'intonazione pura: 701.9 cents
*   intervallo di quinta nel quarter comma meantone: 696.5

Vediamo ora tutte e 12 le note che formano la scala cromatica con il quarter comma meantone partendo da una frequenza di 220hz (A)

220, 229.87947983564504, 245.96747752497689, 257.0130717723972, 275.0, 287.34934979455625, 307.45934690622107, 328.97673186866854, 343.74999999999994, 367.80716773703216, 384.3241836327762, 411.22091483583563, 440

Il calcolo per ottenerle è molto semplice, come per la scala pitagorica procediamo per una successione di quinte a cui sottraiamo 1/4 del syntonic comma:  
220 x ((3/2) / ((81/80) ^ 1/4) dove:

*   220 rappresenta la frequenza di partenza
*   81/80 rappresenta il syntonic comma

Questa è la distanza in cents di tutte le note della scala cromatica nel meantone temperament:

*   minor second: 76.04899926346074 cents
*   major second: 193.15685693241682 cents
*   minor third: 269.20585619587797 cents
*   major third: 386.3137138648348 cents
*   perfect fourth: 462.36271312829524 cents
*   augmented fourth / diminished fifth: 579.4705707972521 cents
*   perfect fifth: 696.578428466209 cents
*   minor sixth: 772.6274277296694 cents
*   major sixth: 889.7352853986264 cents
*   minor seventh: 965.7842846620863 cents
*   major seventh: 1082.8921423310435 cents
*   octave: 1200.0 cents

La distanza di tono in tutti i meantone temperament (da qui il nome meantone, mean = media) è esattamente la metà di una terza maggiore.  
Inoltre, solo per il quarter comma meantone, il tono corrisponde alla media tra il tono maggiore è il tono minore dell'intonazione pura.

Come per la scala pitagorica anche in questo caso ogni 12 quinte non ritorniamo perfettamente sull'ottava e si crea quindi l'intervallo chiamato **wolf fifth** tra il quarto e l'ottavo grado. La distanza di tutte le quinte è di 696 cents tranne tra il quarto e l'ottavo grado che corrisponde a 737.6 cents, troppo ampio per essere utilizzato.

Per migliorare l'intervallo di quinta esistono altri temperamenti in cui il syntonic comma viene suddiviso su 5 o 6 quinte (invece che su 4 come nel meantone), senza però più avere una terza maggiore completamente pura, ma comunque accettabile. Esistono infatti altri temperamenti come il **1/5 comma meantone** e **1/6 comma meantone**.

Il sistema è identico al precendete, ma la suddivisione avviene su più quinte, vediamo velocemente come sarebbe il 1/6 comma meantone:

220, 231.55134483348976, 246.47726106064405, 259.41882395212394, 276.1410919088949, 290.64018725133144, 309.37499999999994, 329.31746820763, 346.6086483665306, 368.9512162874653, 388.32341049688335, 413.35493297967145, 440

Come vediamo la terza maggiore non è più pura (275) ma molto vicino (276,1), mentre l'intervallo di quinta (329.3) è molto più vicino all'intervallo di quinta puro (330).

Tutti questi temperamenti sono detti temperamenti regolari in quanto tutte le quinte vengono temperate nello stesso modo.  
Esistono altri temperamenti detti irregolari in cui le quinte vengono modificate di un valore differente. Questo veniva fatto ad esempio per evitare il wolf fifth che si crea nel quarter comma meantone. Un esempio di temperamento irregolare è il temperamento di Vallotti che vedremo magari in un altro articolo.

Il **temperamento equabile **è un temperamento che si bassa sulla divisione dell'ottava in 12 intervalli uguali tra loro. Questo è il temperamento senza dubbio più utilizzato e conosciuto al giorno d'oggi (ma non nel passato! molti musicisti, tra cui Mozart, utilizzavano altri sistemi di intonazione nonostante il temperamento equabile fosse conosciuto anche all'epoca).

Nel temperamento equabile abbiamo quindi 12 note a distanza di 100 cents l'una dall'altra.  
Vediamo le frequenze partendo come sempre dalla fondamentale a 220hz (A):

220.00, 233.08, 246.94, 261.63, 277.18, 293.66, 311.13, 329.63, 349.23, 369.99, 392.00, 415.30, 440.00

Vediamo subito le due note principali, la terza maggiore che ha una frequenza di 277,1 hz a differenza dell'intervallo puro a 275hz e la quinta giusta he ha una frequenza di 329,62hz a differenza dell'intervallo puro a 330hz.

Il principale vantaggio, che ha portato il temperamento equabile ad essere il più usato, è che può essere utilizzato in tutte le tonalità senza doversi riaccordare (intonazione pura) e senza avere problemi di intervalli inutilizzabili, come il wolf fifth (scala pitagorica e meantone temperament).

In tutti i sistemi precedentemente visti abbiamo sempre parlato di una divisione dell'ottava in 12 note, ma non sempre è così.  
Come abbiamo visto all'interno del meantone temperament abbiamo due differenze distanze di semitono.  
Il sistema del meantone temperament esteso consente di avere entrambi i semitoni, quindi gli equivalenti armonici A# e Bb risultano essere due note differenti.  
Queste intonazioni sono però possibili su strumenti che possono modificare l'intonazione in base all'armonia (come il violino).  
Nel corso della storia abbiamo evidenza che questi intervalli venivano considerati come due note differenti, infatti in molte diteggiature per violino vediamo indicate entrambe le note. Anche Mozart, nei suoi scritti, fa riferimento al "mezzo tuono grande" (semitono maggiore) e al "mezzo tuono piccolo" (semitono minore).  
Questi sono anche chiamati semitono cromatico (G - G#) e semitono diatonico (A - Ab).

Una divisione particolarmente famosa è la **divisione di Tosi** in cui l'ottava viene divisa in 55 parti. Ogni tono è formato da 9 parti (comma). 5 parti formano il semitono maggiore, mentre 4 parti il semitono minore.

Quelli che abbiamo visto oggi sono i principali temperamenti (intonazione pura e scala pitagorica non sono considerati temperamenti in quanto non modificano nessuna nota) utilizzati nel corso della storia fino ad oggi. Ne esistono ovviamente altri, come ad esempio il citato temperamento di Vallotti.  
E' importante capire come funzionano e sentire le differenze tra loro in modo da fare una scelta su quale si adatta meglio alle nostre esigenze.  
Al giorno d'oggi sembra non esserci neanche la considerazione di cosa ci sia al di fuori del temperamenti equabile, ma è proprio oggi che possiamo utilizzare senza sforzo molti altri sistemi. Infatti grazie alla tecnologia possiamo riaccordare il pianoforte digitale con un solo click, o possiamo direttamente specificare la frequenza che vogliamo per un singolo suono, creando un temperamento irregolare in base alle nostre esigenze.

Vi consiglio molto il libro "How Equal Temperament Ruined Harmony: And Why You Should Care" di Ross W. Duffin in cui, oltre a spiegare i vari temperamenti, spiega anche il loro uso nel corso della storia, secondo me molto interessante e illuminante.

Per qualsiasi dubbio, curiosità, suggerimenti, correzioni o per farmi sapere cosa ne pensate non esitate a **commentare qua sotto**!