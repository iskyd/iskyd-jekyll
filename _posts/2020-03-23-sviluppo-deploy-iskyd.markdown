---
layout: post
title:  "iskyd.it - Dallo Sviluppo al Deploy"
description: "Che tecnologia c'è dietro a questo sito web? Qual è il linguaggio di programmazione scelto? Che database utilizza? Che webserver? Come è gestito il deploy?"
date:   2019-05-09 11:00:41 +0100
categories: Programmazione
---
Che tecnologia c'è dietro a questo sito web? Qual è il linguaggio di programmazione scelto? Che database utilizza? Che webserver? Come è gestito il deploy?

Possiamo scomporre tutto in tre macro categorie: **Applicazione**, **Database**, **Deploy**.

## **Applicazione**

L'applicazione è scritta in **python** utilzzando il web framework **Flask**. Di conseguenza il template engine utilizzato è **Jinja** e il WSGI è **Werkzeug**. Flask, Jinja e Werkzeug condividono lo stesso autore: Armin Ronacher.  
Ulteriori estensioni utilizzate sono:

*   Flask-Admin: per tutta la gestione CRUD delle entità (articoli, categorie, tag...)
*   Flask-Login: per gestire il security della parte admin
*   Flask-WTF: per gestire i form
*   Flask-SQLAlchemy: integrazione di SQL-Alchemy in flask
*   click: per i comandi (inizializzazione database, generazione sitemap, generazione feedRss, creazione utenti ecc...)

La scelta dell'ORM è ricaduta su SQLAlchemy per varie ragioni tra cui, le sue potenzialità, la community, il supporto ai principali database (nella fase di sviluppo non avevo ancora deciso che database utilizzare) e l'integrazione immediata con Flask. 

Per quanto riguarda la parte frontend è stato utilizzato, come dicevo precedentemente, Jinja come template engine, jquery come utilities javascript e bootstrap come framework css.

JQuery è stato utilizzato solo perchè è una dipendenza di altre librerie che ho utilizzato (bootstrap ad esempio). Essendo molto limitato, nel mio caso, l'utilizzo di javascript avrei evitato l'utilizzo di JQuery.

I file statici sono gestiti tramite gulp in modo da avere un unico file css e un unico file js.  
Tutti gli assets infatti (css e js) vengono concatenati e successivamente minificati tramite gulp, in modo da ridurre il numero e la dimensione dei file statici.

## **Database**

Inizialmente la scelta del database era ricaduta su un database NoSQL (mongodb molto probabilmente) in quanto pensavo di gestire anche i commenti degli articoli.  
Sarebbe stato molto comodo infatti estrarre direttamente l'articolo e i commenti ad esso associati evitando JOIN.   
Successivamente ho deciso di appoggiarmi a disqus per la gestione dei commenti e per cui, non avendo più necissità di un database NoSQL la scelta è ricaduta su un database relazionale.  
Non ho scelto da subito mysql, anzi il sito è stato sviluppato con sqlite per poi passare a mysql solamente in produzione, grazie a SQLAlchemy.

Ho scelto mysql per comodità, performance, facilità di gestione. Non avevo inoltre necessità di portabilità, grande punto a favore di sqlite.  

## **Deploy**

L'applicativo è eseguito all'interno di un container docker. Ormai docker è un mio MUST per ogni applicativo, indipendentemente dalla tecnologia scelta. I vantaggi sono infiniti: utilizzo dello stesso ambiente in sviluppo e in produzione, possibilità di deployare più container senza doversi preoccupare di niente, lanciare l'applicativo in maniere automatica, CI ecc..

Il progetto utilizza, ovviamente, GIT (versionamento) ed è hostato su Github (da quando mamma Microsoft ha acquistato github il numero di repository privati senza pagare è diventato illimitato <3).   
L'immagine docker è invece pushata sul docker hub.  
Ed è proprio qui che la magia inizia. Docker hub consente di effettuare build dell'immagine in maniera automatica quando viene rilevato un nuovo commit su Github.   
Tramite watchtower inoltre è possibile redeployare il container (pull della nuova immagine e run del container) in maniera automatica, quando viene rilevata un aggiornamento dell'immagine sul registry.   
In questo modo la mia unica preoccupazione è quella di fare un push su github, tutto il resto è automatico. Docker hub si occuperà di creare la nuova immagine e watchtower (che gira in un container sulla stessa macchina dell'applicativo) si occuperà di fare redeploy. Fantastic!

All'interno del container il nostro http server è gunicorn mentre sulla macchina è apache che riceve la richiesta e fa proxy pass sulla porta esposta dal container, su cui è in ascolto gunicorn.  
La parte più complessa, di caching, è su apache.  
Apache si occupa infatti di cachare (tramite mod_cache_disk) tutte le richieste tranne quelle alle pagine di admin.   
Inoltre per tutte le pagine ho scelto un expire di 1 giorno mentre per le immagini di 1 mese. Questa scelta è indicativa per le mie necessità.  
Apache oltre al caching si occupa anche di gestire la sicurezza delle richieste attraverso il protocollo https. Tutte le richieste infatti faranno redirect ad https e solo in quel caso verranno servite. I certificati SSL utilizzati sono quelli di Let's Encrypt.

## **Conclusione**

Le scelte principali che ho fatto, quindi, riguardano il linguaggio di programmazione (e di conseguenza un web framework relativo), il database, l'utilizzo di docker (e tutta l'automazione del deploy) e di apache (principalmente del caching).  
Tutte queste scelte sono fatte in base alle mie necessità che quindi potrebbero essere diverse dalle vostre.  
Indubbiamente l'utilizzo di docker è un MUST nel 2019.  
Un'ORM come SQLAlchemy lo è altrettanto.  
Automatizzare il deploy forse lo è ancora di più!

Per qualsiasi dubbio, curiosità, suggerimenti, correzioni o per farmi sapere cosa ne pensate non esitate a **commentare qua sotto**!