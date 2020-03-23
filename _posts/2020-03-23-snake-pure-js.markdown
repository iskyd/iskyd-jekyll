---
layout: post
title:  "Snake in pure Javascript!"
description: "Oggi vedremo step-by-step come possiamo creare Snake usando solo e soltanto Javascript, nessuna libreria esterna"
date:   2018-10-10 12:48:04 +0100
categories: Programmazione
---
Oggi vedremo step-by-step come possiamo fare un semplice giochino, come Snake, usando solo e soltanto Javascript, nessuna libreria esterna o altro.

Potete trovare il codice completo [qua](https://github.com/iskyd/snakejs) e potete provare la demo su [codepen](https://codepen.io/isky/full/mmGVXO).

Iniziamo creando due file, index.html (che sarà la nostra pagina) e snake.js che sarà il nostro codice js.

index.html

<pre><html>
<head>
    <title>Snake</title>
    <style>canvas { background: #000; display: block; margin: 0 auto; }</style>
</head>
<body>
    <canvas id="snake" width="480" height="320"></canvas>
</body>
<script src="./snake.js"></script>
<script>
</script>
</html></pre>

Il canvas è il nostro elemento grafico su cui andremo a "disegnare" i nostri elementi.  
Tramite css impostiamo lo sfondo del canvas nero e centriamo il canvas nella pagina.  
Alla fine includiamo il file snake.js.

Ora che nel DOM abbiamo l'elemento canvas per scriverci sopra dobbiamo prenderlo nel nostro script js e creare una variabile ctx, che useremo per aggiungere il render 2D.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");</pre>

_Vi consiglio di provare voi stessi step-by-step in modo da capire quello che veramente succede._

Per prima cosa vogliamo disegnare il serpente, che all'inizio si troverà in basso al centro del canvas. Inizialmente sarà un quadrato di dimensioni 10x10 quindi definiamo qualche variabile.

<pre>var x = canvas.width/2;
var y = canvas.height-30;
var snakeHeight = 10;
var snakeWidth = 10;</pre>

x e y rappresentano la posizione del serpente mentre snakeHeight e snakeWidth la sua altezza e larghezza.  
Ora ci serve una funzione che disegna il serpente sul canvas in base alla sua posizione (x e y) e alle sue dimensioni (snakeHeight e snakeWidth).

_Creiamo una funzione perchè questa dovrà continuamente essere chiamata durante tutto il gioco._

<pre>function drawSnake() {
    ctx.beginPath();
    ctx.rect(x, y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}</pre>

Tutte le nostre modifiche a ctx (il contesto 2D del canvas) devono essere contenute tra beginPath(), che si occupa di inizializzare il path o di resettare quello attuale, e closePath() che si occupa di creare un path tra il punto attuale e il punto iniziale.

Cos'è un path? Un canvas path è semplicemente una serie di punti con le istruzioni su come unire questi punti.

La funzione rect si occupa di creare appunto un rettangolo (che inizialmente sarà un quadrato) delle dimensioni e nella posizione indicata.

La funzione fill si occupa di "riempire" il rettangolo disegnato con il colore specificato da fillStyle (nel nostro caso bianco).

_Attenzione! A questo punto nel vostro canvas non vedrete niente perchè la funzione drawSnake non è ancora mai stata chiamata! Provate ad aggiungerla alla fine e vedrete che il quadrato che rappresenta il serpente comparirà._

Una volta disegnato il serpente vogliamo disegnare il cibo. Il cibo comparirà sempre in una posizione casuale del canvas e sarà sempre di dimensioni 10x10\. Applichiamo quindi lo stesso concetto visto per il cibo.

<pre>var foodHeight = 10;
var foodWidth = 10;
var foodX = Math.floor(Math.random() * canvas.width) + 1;
var foodY = Math.floor(Math.random() * canvas.height) + 1;</pre>

<pre>function drawFood() {
    ctx.beginPath();
    ctx.rect(foodX, foodY, foodWidth, foodHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}</pre>

Come vedete abbiamo fatto la stessa identica cosa di prima.  
La posizione del cibo foodX e foodY sono due posizioni casuali, li moltiplichiamo rispettivamente per canvas.width e canvas.height in modo che essi non vengano disegnati "fuori" dal canvas che vediamo sulla pagina.

Mettiamo ora tutto insieme quello che abbiamo fatto.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var x = canvas.width/2;
var y = canvas.height-30;
var snakeHeight = 10;
var snakeWidth = 10;
var foodHeight = 10;
var foodWidth = 10;
var foodX = Math.floor(Math.random() * canvas.width) + 1;
var foodY = Math.floor(Math.random() * canvas.height) + 1;
function drawSnake() {
    ctx.beginPath();
    ctx.rect(x, y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}
function drawFood() {
    ctx.beginPath();
    ctx.rect(foodX, foodY, foodWidth, foodHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

drawSnake();
drawFood();</pre>

Se adesso aprite la pagina index.html nel browser vedrete che compariranno i due quadrati che rappresentano il nostro serpente (in basso al centro) e il cibo in una posizione casuale.  
Quello che può succedere però è che il cibo venga stampato fuori dal canvas per metà della sua grandezza (se continuatate a refreshare la pagina prima o poi vi troverete in questa situazione, ma se non avete voglia di sfidare il Math.random riponete in me la vostra fiducia).

Perchè questo succede? Succede perchè come x e y del cibo abbiamo messo al massimo la dimensione del canvas. Se quindi ci esce quella come posizione il punto centrale del cibo sarebbe sull'estremo della x o della y e quindi metà verrebbe disegnato dentro e l'altra metà fuori. Per correggere questo problema sottraiamo metà della dimensione del cibo dalla posizione massima della x e della y.

<pre>Math.floor(Math.random() * canvas.width - (foodWidth / 2)) + 1;
Math.floor(Math.random() * canvas.height - (foodHeight / 2)) + 1;</pre>

Il prossimo passo sarà far muovere il serpente. Quello che faremo sarà chiamare una funziona draw() ogni 10 millisecondi che si occuperà di disegnare il serpente e il cibo.

<pre>function draw() {
    drawSnake();
    drawFood();
    y--;
}

var interval = setInterval(draw, 10);</pre>

Come vedete diminuiamo ogni volta la posizione della y del serpente in modo che esso si sposti verso l'alto.  
Provate ad aggiornare la pagina con il nuovo codice inserito, vedrete che ogni 10 millisecondi viene disegnato un nuovo quadrato che rappresenta il serpente ma il vecchio quadrato non viene cancellato.  
Aggiungiamo quindi all'inizio della funziona draw() il clear del canvas in modo che tutto quello disegnato sopra venga rimosso.

<pre>function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    drawSnake();
    drawFood();
    y--;
}

var interval = setInterval(draw, 10);

</pre>

La funzione clearRect si occuperà, come abbiamo detto, di rimuovere dal canvas tutti gli oggetti disegnati nella parte che gli specifichiamo (nel nostro caso tutto visto che gli passiamo la grandezza e l'altezza massima).

Anche se non si muove e non si vede, visto che foodX e foodY rimangono sempre uguali, anche il cibo viene rimosso e ridisegnato, nello stesso punto, ogni 10 millisecondi.

Come avrete notato il serpente si sposterà verso l'alto finchè non supera l'altezza massimo del canvas e scompare. Penseremo a questo dopo, per ora vogliamo fare in modo che il serpente cambi direzione in base a che tasto sulla tastiera schiacciamo (freccia sinistra, freccia destra, freccia in alto e freccia in basso).

Per fare ciò dobbiamo aggiungere un evento che verrà eseguito ogni volta che viene schiacciato un tasti sulla tastiera. Filtreremo poi i tasti che ci interessano.

<pre>function keyDownHandler(e) {
    if(e.keyCode == 37) {
    //left
    } 
    else if(e.keyCode == 38) {
    //up
    } 
    else if(e.keyCode == 39) {
        //rigth
    } 
    else if(e.keyCode == 40) {
        //down
    }
}</pre>

Il keyCode 37 corrisponde alla freccia a sinistra e così via come indicato dai commenti nel codice sopra.  
Quello che vogliamo fare ora è salvare la direzione scelta in una variabile in modo da usarla successivamente nella funziona draw(), invece che fare y-- come facciamo ora.

<pre>var direction = 1;
function keyDownHandler(e) {
    if(e.keyCode == 37) {
    direction = 3;
    } 
    else if(e.keyCode == 38) {
    direction = 1;
    } 
    else if(e.keyCode == 39) {
        direction = 4;
    } 
    else if(e.keyCode == 40) {
        direction = 2;
    }
}</pre>

Ora creiamo una funzione changePosition() che si occuperà di modificare la posizione del serpente in base alla direzione scelta. Se per esempio viene schiacciata la freccia in giù sappiamo che il valore dell'ordinata (ovvero y). Sappiamo inoltre che dovendo muoversi verso il basso il valore dell'ordinata deve aumentare.

<pre>function changePosition() {
    if(direction == 1) {
        y--;
    }
    else if(direction == 2) {
        y++;
    } 
    else if(direction == 3) {
        x--;
    }
    else if(direction == 4) {
        x++;
    }
}</pre>

Mettiamo ora tutto insieme e vediamo cosa succede.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var x = canvas.width/2;
var y = canvas.height-30;
var snakeHeight = 10;
var snakeWidth = 10;
var foodHeight = 10;
var foodWidth = 10;
var foodX = Math.floor(Math.random() * canvas.width - (foodWidth / 2)) + 1;
var foodY = Math.floor(Math.random() * canvas.height - (foodHeight / 2)) + 1;
var direction = 1

function keyDownHandler(e) {
    if(e.keyCode == 37) {
        direction = 3;
    } 
    else if(e.keyCode == 38) {
        direction = 1;
    } 
    else if(e.keyCode == 39) {
        direction = 4;
    } 
    else if(e.keyCode == 40) {
        direction = 2;
    }
}

function drawSnake() {
    ctx.beginPath();
    ctx.rect(x, y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}
function drawFood() {
    ctx.beginPath();
    ctx.rect(foodX, foodY, foodWidth, foodHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    drawSnake();
    drawFood();
    changePosition();
}

function changePosition() {
    if(direction == 1) {
        y--;
    }
    else if(direction == 2) {
        y++;
    } 
    else if(direction == 3) {
        x--;
    }
    else if(direction == 4) {
        x++;
    }
}

document.addEventListener("keydown", keyDownHandler, false);

var interval = setInterval(draw, 10);</pre>

Il serpente inizierà a muoversi verso l'alto (la variabile direction viene inizializzata di default a 1 che corrisponde a un movimento verso l'alto).  
Adesso attraverso le frecce direzionali possiamo decidere in che direzione il serpente si deve muovere.  
Abbiamo però ancora un enorme problema, il serpente quando raggiunge la dimensione massima del canvas esce da esso.  
Quello che vogliamo fare invece è che in caso di collisione con gli estremi del canvas il giocatore perde la partita e tutto rinizia da capo.  
Creiamo quindi una funzione checkCollision() che ad ogni iterazione (nella funzione draw()) si occuperà di controllare se il serpente è al di fuori della dimensione massima, e quindi la partita viene persa, o all'interno, e quindi il serpente continua a muoversi.

<pre>function checkCollision() {
    if(y > canvas.height || y < 0 || x < 0 || x > canvas.width) {
        //collision detect call restart function
    }
}</pre>

E' molto semplice verificare se il serpente è fuori dal canvas, basta controllare se la sua posizione sia fuori dall'altezza / larghezza massima (canvas.height / canvas.width) o sia fuori dall'altezza / larghezza minima (0 / 0).

Quello che vogliamo fare quando troviamo una collisione è chiamare una funzione restart() che si occuperà di cambiare la posizione del serpente alla posizione iniziale e rimettere la sua direzione a 1.

<pre>function restart() {
    x = canvas.width/2;
    y = canvas.height-30;
    direction = 1;
}</pre>

Mettiamo ora tutto insieme e proviamo.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var x = canvas.width/2;
var y = canvas.height-30;
var snakeHeight = 10;
var snakeWidth = 10;
var foodHeight = 10;
var foodWidth = 10;
var foodX = Math.floor(Math.random() * canvas.width - (foodWidth / 2)) + 1;
var foodY = Math.floor(Math.random() * canvas.height - (foodHeight / 2)) + 1;
var direction = 1

function keyDownHandler(e) {
    if(e.keyCode == 37) {
        direction = 3;
    } 
    else if(e.keyCode == 38) {
        direction = 1;
    } 
    else if(e.keyCode == 39) {
        direction = 4;
    } 
    else if(e.keyCode == 40) {
        direction = 2;
    }
}

function drawSnake() {
    ctx.beginPath();
    ctx.rect(x, y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}
function drawFood() {
    ctx.beginPath();
    ctx.rect(foodX, foodY, foodWidth, foodHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    drawSnake();
    drawFood();
    checkCollision();
    changePosition();
}

function changePosition() {
    if(direction == 1) {
        y--;
    }
    else if(direction == 2) {
        y++;
    } 
    else if(direction == 3) {
        x--;
    }
    else if(direction == 4) {
        x++;
    }
}

function checkCollision() {
    if(y > canvas.height || y < 0 || x < 0 || x > canvas.width) {
        restart();
    }
}

function restart() {
    x = canvas.width/2;
    y = canvas.height-30;
    direction = 1;
}

document.addEventListener("keydown", keyDownHandler, false);

var interval = setInterval(draw, 10);</pre>

Se provate ora ad uscire dal canvas vedrete che la posizione del serpente e la sua direzione ritorneranno ad essere quelle iniziali.

Tutto molto bello. Cerchiamo ora di rendere il nostro gioco almeno un pò divertente.  
Quando il serpente collide con il cibo dobbiamo fare in modo di aumentare la sua dimensione e cambiare la posizione del cibo in un altra posizione casuale.

Creiamo quindi una funzione checkCollisionWithFood() che si occuperà di verificare se il serpente ha colliso con il cibo, allo stesso modo in cui abbiamo fatto per la collisione con i bordi del canvas.

<pre>var precision = 5;
function checkCollisionWithFood() {
if((x - precision < foodX  && foodX < x + precision) && (y - precision < foodY && foodY < y + precision)) {
        //collision detect
    }
}</pre>

La variabile precision ci serve per fare in modo che il serpente non sia esattamente nella stessa posizione del cibo, sarebbe impossibile, ma che sia a un massimo di "precision" distante.  
Provate ad aumentare o diminuire la precision per vedere cosa succede.

Il prossimo step sarà quello di spostare il cibo in una nuova posizione quando si verifica la collisione.

<pre>function checkCollisionWithFood() {
    if((x - precision < foodX  && foodX < x + precision) && (y - precision < foodY && foodY < y + precision)) {
        foodX = Math.floor(Math.random() * canvas.width) + 1;
        foodY = Math.floor(Math.random() * canvas.height) + 1;
    }
}</pre>

In questo modo ogni volta che il serpente avrà una collisione con il cibo, quest'ultimo si sposterà in un nuovo punto casuale della mappa.  
Un'altra cosa che vogliamo fare a mostrare sul canvas lo score attuale del giocatore.  
Lo score aumenterà di 1 ogni volta che il cibo verrà "preso".  
Per questo definiamo una funzione drawScore() che chiameremo all'interno di draw() che scriverà il score sul canvas.

<pre>function drawScore() {
    ctx.font = "16px Arial";
    ctx.fillStyle = "#b6b3b3";
    ctx.fillText("Score: "+score, 8, 20);
}</pre>

Impostiamo al contesto il font e il colore che vogliamo abbia la nostra scritta e lo scriviamo sul canvas nella posizione 8,20.

Quello che dobbiamo fare è definire una variabile score e incrementarla ogni volta che troviamo una collisione con il cibo.  
Aggiungiamo anche che al restart() lo score ritorna a 0.  
Mettiamo tutto insieme.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var x = canvas.width/2;
var y = canvas.height-30;
var snakeHeight = 10;
var snakeWidth = 10;
var foodHeight = 10;
var foodWidth = 10;
var foodX = Math.floor(Math.random() * canvas.width - (foodWidth / 2)) + 1;
var foodY = Math.floor(Math.random() * canvas.height - (foodHeight / 2)) + 1;
var direction = 1
var score = 0
var precision = 5

function keyDownHandler(e) {
    if(e.keyCode == 37) {
        direction = 3;
    } 
    else if(e.keyCode == 38) {
        direction = 1;
    } 
    else if(e.keyCode == 39) {
        direction = 4;
    } 
    else if(e.keyCode == 40) {
        direction = 2;
    }
}

function drawSnake() {
    ctx.beginPath();
    ctx.rect(x, y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}
function drawFood() {
    ctx.beginPath();
    ctx.rect(foodX, foodY, foodWidth, foodHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function drawScore() {
    ctx.font = "16px Arial";
    ctx.fillStyle = "#b6b3b3";
    ctx.fillText("Score: "+score, 8, 20);
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    drawSnake();
    drawFood();
    drawScore();
    checkCollisionWithFood();
    checkCollision();
    changePosition();
}

function changePosition() {
    if(direction == 1) {
        y--;
    }
    else if(direction == 2) {
        y++;
    } 
    else if(direction == 3) {
        x--;
    }
    else if(direction == 4) {
        x++;
    }
}

function checkCollision() {
    if(y > canvas.height || y < 0 || x < 0 || x > canvas.width) {
        restart();
    }
}

function checkCollisionWithFood() {
    if((x - precision < foodX  && foodX < x + precision) && (y - precision < foodY && foodY < y + precision)) {
        foodX = Math.floor(Math.random() * canvas.width) + 1;
        foodY = Math.floor(Math.random() * canvas.height) + 1;
        score++
    }
}

function restart() {
    x = canvas.width/2;
    y = canvas.height-30;
    direction = 1;
    score = 0
}

document.addEventListener("keydown", keyDownHandler, false);

var interval = setInterval(draw, 10);</pre>

A questo punto il gioco funziona. Abbiamo aggiunto le collisioni con i bordi, possiamo prendere il cibo e il nostro score aumenta.  
Manca ancora qualcosa. Il serpente non si ingrandisce quando mangia.  
Vediamo di risolvere subito il problema!

Dimentichiamo per un momento quello fatto prima e cerchiamo di capire come fare ad avere un serpente diventa sempre più grosso. Ovviamente avere solo una x e una y che descrivono la posizione del singolo quadrato non ci basta, ma dobbiamo avere un array di posizioni in modo che ognuna descriva quella del quadrato corrispondente.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var snake = [ {x: canvas.width/2, y: canvas.height-30} ]
var snakeHeight = 10;
var snakeWidth = 10;

function drawSnake(element) {
    ctx.beginPath();
    ctx.rect(element.x, element.y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    snake.forEach(function(element){
        drawSnake(element)
    })
}

draw();</pre>

Abbiamo usato la variabile snake che al suo interno contiene un array di oggetti. Ogni oggetto ha una x a una y che definiscono la posizione di quel quadrato.  
Per disegnare tutto il serpente a questo punto usiamo un ciclo forEach in modo da disegnare ogni singolo quadrato.  
Create un nuovo file snake2.js in cui incollate il codice qui sopra e modificate lo script che includete nell'index.html da snake.js a snake2.js.

Provate ora a modificare la variabile snake in modo da aggiungere altri quadrati, ad esempio:

<pre>var snake = [ {x: canvas.width/2, y: canvas.height-30}, {x: canvas.width/2 - 10, y: canvas.height-30} ]</pre>

Riaggiungiamo parte del codice già scritta prima in modo da integrarla con questa nuova struttura.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var snake = [ {x: canvas.width/2, y: canvas.height-30} ]
var snakeHeight = 10;
var snakeWidth = 10;
var direction = 1;

function keyDownHandler(e) {
    if(e.keyCode == 37) {
        direction = 3;
    } 
    else if(e.keyCode == 38) {
        direction = 1;
    } 
    else if(e.keyCode == 39) {
        direction = 4;
    } 
    else if(e.keyCode == 40) {
        direction = 2;
    }
}

function drawSnake(element) {
    ctx.beginPath();
    ctx.rect(element.x, element.y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    snake.forEach(function(element){
        changePosition(element);
        drawSnake(element);
    })
}

function changePosition(element) {
    if(direction == 1) {
        element.y--;
    }
    else if(direction == 2) {
        element.y++;
    } 
    else if(direction == 3) {
        element.x--;
    }
    else if(direction == 4) {
        element.x++;
    }
}

document.addEventListener("keydown", keyDownHandler, false);

var interval = setInterval(draw, 10);</pre>

Come vedete non è cambiato nulla se non l'utilizzo di un array per la posizione di ogni singolo pezzo del serpente.  
Ora possiamo muovere il nostro serpente come prima ma con la nuova struttura dati.

Proviamo adesso a cambiare il nostro snake aggiungedogli un pezzo.

<pre>var snake = [ {x: canvas.width/2, y: canvas.height-30}, {x: canvas.width/2, y: canvas.height-40} ]</pre>

In questo muovo tutti i pezzi si muovono.... ma non come volevamo.  
Ovviamente non possiamo muovere ogni pezzo nella direzione scelta ma una volta scelta una nuova direzione dobbiamo muoverli uno per volta nella nuova direzione.  
Come facciamo? Alla nostra struttura dati, oltre che alla x e alla y, aggiungiamo anche la direzione in modo che ogni singolo pezzo del serpente sia autonomo.

<pre>var snake = [ {x: canvas.width/2, y: canvas.height-30, direction: 1} ]</pre>

Quello che dobbiamo fare è quindi far si che quando la direzioni cambi solo il primo pezzo cambi la sua direzione, dopodichè, uno dopo l'altro, tutti gli altri pezzi cambieranno la loro direzione in base al pezzo precedente.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var snake = [ {x: canvas.width/2, y: canvas.height-30, direction: 1} ]
var snakeHeight = 10;
var snakeWidth = 10;

function keyDownHandler(e) {
    if(e.keyCode == 37) {
    snake[0].direction =  3;
    } 
    else if(e.keyCode == 38) {
    snake[0].direction = 1;
    } 
    else if(e.keyCode == 39) {
        snake[0].direction = 4;
    } 
    else if(e.keyCode == 40) {
        snake[0].direction = 2;
    }
}

function drawSnake(element) {
    ctx.beginPath();
    ctx.rect(element.x, element.y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    snake.forEach(function(element){
        changePosition(element);
        drawSnake(element);
    })
}

function changePosition(element) {
    if(element.direction == 1) {
        element.y--;
    }
    else if(element.direction == 2) {
        element.y++;
    } 
    else if(element.direction == 3) {
        element.x--;
    }
    else if(element.direction == 4) {
        element.x++;
    }
}

document.addEventListener("keydown", keyDownHandler, false);

var interval = setInterval(draw, 10);</pre>

A questo punto soltanto il primo pezzo cambierà direzione. Dobbiamo ora fare in modo che tutti i pezzi che seguono cambino la propria direzione in base al pezzo precedente.

Per prima cosa modifichiamo la funzione changePosition() in modo che il pezzo si muova nella direzione specificata di una distanza pari alla sua dimensione.

<pre>function changePosition(element) {
    if(element.direction == 1) {
        element.y -= snakeWidth;
    }
    else if(element.direction == 2) {
        element.y += snakeWidth;
    } 
    else if(element.direction == 3) {
        element.x -= snakeHeight;
    }
    else if(element.direction == 4) {
        element.x += snakeHeight;
    }
}</pre>

A questo punto ci serve una nuova funzione, changeDirection() che a ogni loop (all'interno della funzione draw()) modificherà la direzione del singolo pezzo in base che la sua direzione diventi uguale a quella del pezzo precedente.

<pre>function changeDirection(element, index) {
    if(index != 0) {
        var previousElement = snake[index - 1];
        element.direction = previousElement.direction;
    }
}</pre>

Rimettiamo tutto insieme e usiamo un serpente composto da 3 pezzi.

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var snake = [ {x: canvas.width/2, y: canvas.height-30, direction: 1}, {x: canvas.width/2, y: canvas.height-20, direction: 1}, {x: canvas.width/2, y: canvas.height-10, direction: 1} ]
var snakeHeight = 10;
var snakeWidth = 10;

function keyDownHandler(e) {
    if(e.keyCode == 37) {
        snake[0].direction =  3;
    } 
    else if(e.keyCode == 38) {
        snake[0].direction = 1;
    } 
    else if(e.keyCode == 39) {
        snake[0].direction = 4;
    } 
    else if(e.keyCode == 40) {
        snake[0].direction = 2;
    }
}

function drawSnake(element) {
    ctx.beginPath();
    ctx.rect(element.x, element.y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    snake.forEach(function(element, index){
        changePosition(element);
        drawSnake(element);
    })
    for(var i = snake.length - 1; i >= 0; i--) {
        changeDirection(snake[i], i);
    }
}

function changePosition(element) {
    if(element.direction == 1) {
        element.y -= snakeWidth;
    }
    else if(element.direction == 2) {
        element.y += snakeWidth;
    } 
    else if(element.direction == 3) {
        element.x -= snakeHeight;
    }
    else if(element.direction == 4) {
        element.x += snakeHeight;
    }
}

function changeDirection(element, index) {
    if(index != 0) {
        var previousElement = snake[index - 1];
        element.direction = previousElement.direction;
    }
}

document.addEventListener("keydown", keyDownHandler, false);

var interval = setInterval(draw, 100);
</pre>

A questo punto potete vedere che abbiamo raggiunto il nostro obbiettivo.

Quello che ci rimane da fare è fare in modo che la collision con il cibo sia considerata solo quando è la testa (in ogni caso non sarebbe possibile che collida con un altro pezzo) collida con il cibo.

<pre>function checkCollisionWithFood() {
    if((snake[0].x - precision < foodX  && foodX < snake[0].x + precision) && (snake[0].y - precision < foodY && foodY < snake[0].y + precision)) {
        foodX = Math.floor(Math.random() * canvas.width - 5) + 1;
        foodY = Math.floor(Math.random() * canvas.height - 5) + 1;
        score++;
    }
}</pre>

A questo punto ci resta solo da aggiungere un pezzo al nostro serpente ogni qualvolta mangi il cibo. Per fare questo aggiungiamo un oggetto alla fine dell'array che identifica il serpente.

<pre>function checkCollisionWithFood() {
    if((snake[0].x - precision < foodX  && foodX < snake[0].x + precision) && (snake[0].y - precision < foodY && foodY < snake[0].y + precision)) {
        foodX = Math.floor(Math.random() * canvas.width - 5) + 1;
        foodY = Math.floor(Math.random() * canvas.height - 5) + 1;
        var lastElement = snake[snake.length - 1];
        switch(lastElement.direction) {
            case 1:
                snake.push({x: lastElement.x, y: lastElement.y + snakeHeight, direction: lastElement.direction});
                break;
            case 2:
                snake.push({x: lastElement.x, y: lastElement.y - snakeHeight, direction: lastElement.direction});
                break;
            case 3:
                snake.push({x: lastElement.x + snakeWidth, y: lastElement.y, direction: lastElement.direction});
                break;
            case 4:
                snake.push({x: lastElement.x - snakeWidth, y: lastElement.y, direction: lastElement.direction});
                break;
        }
        score++;
    }
}</pre>

Lo switch serve per fare in modo di aggiungere il pezzo del serpente nella posizione giusta in base a quale sia la sua attuale direzione. Se l'ultimo pezzo del serpente si muove da sinistra verso destra dovremo aggiungere il pezzo in fondo a sinistra, e così via.

Pensate che siamo arrivati alla fine? E invece no.  
Abbiamo ancora due problemi. Se stiamo andando da sinistra verso destra, al momento, possiamo muoverci verso sinistra e andare nella direzione opposta, ottenendo così la sovrapposizione di alcuni pezzi.  
Il secondo problema è verificare oltre che la collisione con in bordi anche la collisione con il serpente stesso in modo da fare il restart() della partita anche in questo caso.

Partiamo con il primo problema.  
Per questo aggiungiamo semplicemente una funzione canChangeDirection() in modo che se il serpente sta andando verso l'alto (1) non potrà cambiare la sua posizione verso il basso (2).

<pre>function canChangeDirection(newDirection) {
    if(newDirection === false) {
        return false;
    }

    if((newDirection == 1 && snake[0].direction != 2) || (newDirection == 2 && snake[0].direction != 1) || (newDirection == 3 && snake[0].direction != 4) || (newDirection == 4 && snake[0].direction != 3)) {
        return true;
    }

    return false;
}</pre>

Ci basta a questo punto integrare questa funzione dove cambiamo la direzione del serpente, ovvero nella funzione keyDownHandler (il nostro evento di click dei tasti della tastiera).

<pre>function keyDownHandler(e) {
    var newDirection = false;
    if(e.keyCode == 37) {
        newDirection = 3;
    } 
    else if(e.keyCode == 38) {
        newDirection = 1;
    } 
    else if(e.keyCode == 39) {
        newDirection = 4;
    } 
    else if(e.keyCode == 40) {
        newDirection = 2;
    }
    if(canChangeDirection(newDirection)) {
        snake[0].direction = newDirection;
    }
}</pre>

In questo modo cambiamo la direzione al primo pezzo del serpente (i successivi verranno modificati in base alla direzione del precedente pezzo) solo se questo può farlo.

A questo punto per risolvere il problema numero 2 ci basta creare una funzione checkCollisionWithSnake() per verificare se la testa del serpente sta collidendo con un suo qualsiasi altro pezzo.

<pre>function checkCollisionWithSnake() {
    var x = snake[0].x;
    var y = snake[0].y;
    var collision = false;

    snake.forEach(function(element, index){
        if(index != 0) {
            if(element.x == x && element.y == y) {
                collision = true;
            }
        }
    })

    if(collision) {
        restart();
    }
}</pre>

Semplicemente cicliamo su tutti i pezzi del serpente e verifichiamo che nessuno stia collidendo con la testa.  
In caso di collisione chiamiamo la funzione restart() in quanto abbiamo perso!

Questo è tutto, finalmente abbiamo finito.  
Qui sotto c'è il codice finale che potete trovare anche su [github](https://github.com/iskyd/snakejs).

<pre>var canvas = document.getElementById("snake");
var ctx = canvas.getContext("2d");
var snake = [ {x: canvas.width/2, y: canvas.height-30, direction: 1}, {x: canvas.width/2, y: canvas.height-20, direction: 1}, {x: canvas.width/2, y: canvas.height-10, direction: 1} ]
var snakeHeight = 10;
var snakeWidth = 10;
var foodHeight = 10;
var foodWidth = 10;
var foodX = Math.floor(Math.random() * canvas.width - foodWidth) + 1;
var foodY = Math.floor(Math.random() * canvas.height - foodHeight) + 1;
var score = 0;
var precision = 10;

function keyDownHandler(e) {
    var newDirection = false;
    if(e.keyCode == 37) {
        newDirection = 3;
    } 
    else if(e.keyCode == 38) {
        newDirection = 1;
    } 
    else if(e.keyCode == 39) {
        newDirection = 4;
    } 
    else if(e.keyCode == 40) {
        newDirection = 2;
    }
    if(canChangeDirection(newDirection)) {
        snake[0].direction = newDirection;
    }
}

function drawSnake(element) {
    ctx.beginPath();
    ctx.rect(element.x, element.y, snakeWidth, snakeHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function drawFood() {
    ctx.beginPath();
    ctx.rect(foodX, foodY, foodWidth, foodHeight);
    ctx.fillStyle = "#fff";
    ctx.fill();
    ctx.closePath();
}

function drawScore() {
    ctx.font = "16px Arial";
    ctx.fillStyle = "#b6b3b3";
    ctx.fillText("Score: "+score, 8, 20);
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    snake.forEach(function(element, index){
        changePosition(element);
        drawSnake(element);
    })
    checkCollision();
    checkCollisionWithFood();
    checkCollisionWithSnake();
    drawFood();
    drawScore();
    for(var i = snake.length - 1; i >= 0; i--) {
        changeDirection(snake[i], i);
    }
}

function changePosition(element) {
    if(element.direction == 1) {
        element.y -= snakeWidth;
    }
    else if(element.direction == 2) {
        element.y += snakeWidth;
    } 
    else if(element.direction == 3) {
        element.x -= snakeHeight;
    }
    else if(element.direction == 4) {
        element.x += snakeHeight;
    }
}

function changeDirection(element, index) {
    if(index != 0) {
        var previousElement = snake[index - 1];
        element.direction = previousElement.direction;
    }
}

function canChangeDirection(newDirection) {
    if(newDirection === false) {
        return false;
    }

    if((newDirection == 1 && snake[0].direction != 2) || (newDirection == 2 && snake[0].direction != 1) || (newDirection == 3 && snake[0].direction != 4) || (newDirection == 4 && snake[0].direction != 3)) {
        return true;
    }

    return false;
}

function checkCollision() {
    if(snake[0].y > canvas.height || snake[0].y < 0 || snake[0].x < 0 || snake[0].x > canvas.width) {
        restart();
    }
}

function checkCollisionWithFood() {
    if((snake[0].x - precision < foodX  && foodX < snake[0].x + precision) && (snake[0].y - precision < foodY && foodY < snake[0].y + precision)) {
        foodX = Math.floor(Math.random() * canvas.width - 5) + 1;
        foodY = Math.floor(Math.random() * canvas.height - 5) + 1;
        var lastElement = snake[snake.length - 1];
        switch(lastElement.direction) {
            case 1:
                snake.push({x: lastElement.x, y: lastElement.y + snakeHeight, direction: lastElement.direction});
                break;
            case 2:
                snake.push({x: lastElement.x, y: lastElement.y - snakeHeight, direction: lastElement.direction});
                break;
            case 3:
                snake.push({x: lastElement.x + snakeWidth, y: lastElement.y, direction: lastElement.direction});
                break;
            case 4:
                snake.push({x: lastElement.x - snakeWidth, y: lastElement.y, direction: lastElement.direction});
                break;
        }
        console.log(snake.length);
        score++;
    }
}

function checkCollisionWithSnake() {
    var x = snake[0].x;
    var y = snake[0].y;
    var collision = false;

    snake.forEach(function(element, index){
        if(index != 0) {
            if(element.x == x && element.y == y) {
                collision = true;
            }
        }
    })

    if(collision) {
        restart();
    }
}

function restart() {
    snake = [ {x: canvas.width/2, y: canvas.height-30, direction: 1}, {x: canvas.width/2, y: canvas.height-20, direction: 1}, {x: canvas.width/2, y: canvas.height-10, direction: 1} ];
    foodX = Math.floor(Math.random() * canvas.width - foodWidth) + 1;
    foodY = Math.floor(Math.random() * canvas.height - foodHeight) + 1;
    score = 0;
}

document.addEventListener("keydown", keyDownHandler, false);

var interval = setInterval(draw, 100);</pre>

In sole 161 righe abbiamo scritto, in modo semplice, snake.  
Vi invito a modificare il codice in modo da prendere più confidenza con quello che abbiamo fatto.  
Vi consiglio anche di aggiungere qualche abbellimento all'interno del gioco in modo da capire in modo più approfondito come il tutto funziona.  

_Potete ad esempio fare in modo che il cibo resti in quella posizione solo per 10 secondi, dopodichè si sposterà in un altro posto random._

Per qualsiasi dubbio, curiosità, suggerimenti, correzioni o per farmi sapere cosa ne pensate non esitate a **commentare qua sotto**!