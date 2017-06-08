# Introduzione

Per il seguente progetto si è cercato di perseguire l'idea di sviluppare una sezione di un sito che consente di visualizzare in 3D un prodotto da acquistare in modo da sviluppare correttamente non solamente la parte dedicata al rendering 3d, ma in generale tutta la struttura della pagina. Per fare ciò ci si è avvalsi del Framework Front-End [Fundation](http://foundation.zurb.com/), che consente di sviluppare in modo facile e standardizzato strutture HTML, CSS e Javascript.

![Struttura della pagina creata](media/screenshots/Main_Page.png)

In figura si può vedere la struttura creata: attraverso l'uso del layout a 12 colonne che è standard assodato del web, si è creata una barra superiore contenente il nome del sito, lo spazio per eventuali link appartenenti al menù di navigazione da inserire al momento di necessità ed infine un pulsante che si distingue grazie al colore dagli altri che consente di avviare la procedura d'acquisto del prodotto.

Infine, il resto della pagina è organizzato su due colonne distinte, la prima che occupa 2/12 dello spazio a disposizione prevede il menù che consentirà all'utente di interagire con la scena 3d, la seconda invece contiene la scena stessa. Sono state apportate poi delle brevi modifiche estetiche per far risaltare il tutto. Tali modifiche sono visibili in **css/app.css**. Va detto che nonostante l'uso di questo Framework di sviluppo il canvas è risultato non rispettare i vincoli su di esso imposti. Pertanto è stato traslato un poco a seconda delle dimensioni dello schermo l'elemento renderer dell'applicazione costruita per evitare eventuali sovrapposizioni. 

## Il Modello Usato

Il modello usato per questa applicazione è stato ottenuto dal sito web [Free3D](https://free3d.com) ed il file usato è il [Thor Hammer](https://free3d.com/3d-model/thor-hammer--62945.html) che è disponibile con licenza **Non-commercial use License**. Il modello è stato scaricato nella sua versione **.obj** e non sono state applicate le sue texture predefinite, in quanto si è preferito adottarne delle versioni ad hoc creando dei materiali personalizzati. Nello specifico si è cercato di creare:
- Una versione in cui sono presenti materiali metallici e più texture;
- Una versione prettamente metallica del martello;
- Una versione giocattolo composta da materiali gommosi.
- Una versione che subisce un effetto di rifrazione dalla luce ricevuta, da vedere nel contesto come versione "invisibile" o "mimetica".

Ciascuna delle versioni sopra elencate è stata sviluppata estendendo e modificando gli shader visti a lezione. L'idea globale è quella di consentire all'utente di visionare l'oggetto nelle sue varianti, così da consentire l'acquisto di quella ritenuta più adeguata.

## Luci

Le luci previste per questa applicazione sono diverse, come si sarà capito al punto precedente, a seconda del contesto d'uso. Il martello verrà illuminato da 4 luci puntuali usate per illuminare in modo completo i materiali metallici e plastici. Tali luci sono poste una di fronte ad esso, due ai lati ed infine una verrà posta sopra. L'idea è di consentire una illuminazione artificiale e completa dell'oggetto, mantenendo comunque alcune zone in ombra, ma esaltando alcuni particolari degni di nota, come i glifi posizionati sulla sua testa o le sue irregolarità. Questa idea è accentuata dalla assenza di sfondo e dall'uso per esso di un colore tenue. L'uso di 4 luci in questo caso è funzionale all'idea di illuminare in modo soddisfacente l'intera testa del martello. Per gli shader che invece sfruttano le texture si è invece deciso di usare solamente 3 luci, due laterali ed una superiore. Questo perchè l'inclinazione a cui è posto il martello rende superfluo l'aggiunta di una quarta luce ed inoltre si è deciso di non illuminare la parte sottostante del prodotto.

Infine la versione che prevede la rifrazione della luce sfrutterà ovviamente una CubeMap (visibile in figura) per generare luce attraverso una Enviroment Map. Le immagini usate per generarla sono disponibili attraverso licenza **Creative Commons Attribution 3.0** e quindi è utilizzabile per questo progetto gratuitamente. 

![Cubemap Usata](media/screenshots/cube_map.png)



## Materiali
I materiali metallici sono stati creati attraverso l'uso di uno Shader nella sua versione Microfacet, poichè tale versione consentiva risultati visivamente perfetti e con colori più vivi rispetto all'uso di un combined shader (cdiff + cspec). I colori vivi rendono bene l'idea di un martello appartenente ad una divinità e quindi senza alcun segno di usura data dal tempo e dall'utilizzo. Si è deciso in questo caso di usare due materiali distinti, uno dorato usato per gli intarsi del manico e le decorazioni della testa ed infine uno argentato che verrà applicato alla testa stessa. Le 4 luci puntuali integrate negli shader consentono, con questo tipo di materiale, un risultato visivamente pieno, consentendo di vedere il riflesso delle luci quasi da ogni angolazione e mantenendo in ombra alcuni elementi come la parte sottostante della testa del martello. Particolar risalto hanno in questo caso le incisioni sulla testa, che sembrano quasi brillare di luce propria grazie al posizionamento delle luci. Per dare una sensazione di microvariazione geometrica per il manico è stata usata una texture rappresentante il legno il cui shader come detto sopra è composto da 3 luci puntuali. 

![Versione Metallica](media/screenshots/metallic_mj.png)

![Texture Legno](media/screenshots/textures.png)

I materiali plastici invece sono stati creati ovviamente attraverso un combined shader integrando le informazioni inerenti a cdiff e cspec. Anche tali shader sono stati adottati nella versione vista a lezione ed integrati con le luci aggiuntive previste. I materiali usati in questo caso sono 3, tutti plastici e a far la differenza sono solamente i colori: rosso per la testa del martello, blu per il manico ed i glifi presenti sulla testa ed infine un materiale grigio per gli intarsi del manico.

![Versione Giocattolo](media/screenshots/toy_mj.png)

Una ulteriore versione è stata integrata in seguito e si avvale di una ulteriore texture ed un ulteriore materiale metallico. Questa versione integra tra l'altro i materiali dorati e argentati utilizzati precedentemente. Per il manico è stata usata una texture rappresentante la pietra. Per quanto questa scelta di texture sia poco verosimile nella realtà essa aggiunge delle microvariazioni gradevoli all'occhio all'interno del manico stesso. Agli intarsi questa volta è stato applicato il materiale legnoso che prima nella versione metallica era stata applicata al manico. La texture, unita alla forma e ai valori di repeat scelti fornisce l'aspetto di fasci di legno con le venature efficacemente messe in risalto grazie alla luce. Il giunto che si posa sulla testa è argentato, gli intarsi della stessa sono dorati e risaltano ancora una volta in modo netto rispetto al materiale scelto per la testa del martello. Su di essa questa volta è stato applicato un materiale metallico volutamente di un blu sovvranaturale.

![Versione Used](media/screenshots/used_mj.png)

Infine la versione degli shader che implementa il fenomeno di rifrazione è stata creata partendo dallo shader visto a lezione che consente il reflection mapping e modificando il codice adeguatamente usando la funzione refract. Il rapporto dell'indice di rifrazione usato (1.0/2.0) è stato scelto dopo alcuni test poichè consentiva un risultato visivamente appagante. 

![Rifrazione](media/screenshots/refract_mj.png)

Per quanto riguarda infine la base d'appoggio, essa è stata creata usando un cilindro con una altezza estremamente ridotta ed applicandovi una texture tramite shader. Tale texture è il prodotto delle informazioni di una Specular Map, una Diffuse Map ed una Roughness Map che, combinate, garantiscono un risultato visivamente soddisfacente. Tali texture sono state ottenute gratuitamente dal sito web [GameTextures] (https://www.gametextures.com/free-materials/) e poi create ed esportate singolarmente attraverso il software Substance Player. Quelle usate sono visibili in figura. 

## Il Particle System

Come piccola aggiunta si è deciso inoltre di implementare un semplice particle system statico composto da 2000 punti a cui è applicata la texture snowflake.png pe simulare delle stelle. Tale opzione di visualizzazione è attivabile attraverso lo switch posto in fondo alla colonna di UI a sinistra del canvas. L'attivazione di tale elemento dell'interfaccia comporta lo scurimento dello sfondo e la comparsa delle stelle in posizioni pseudocasuali. Tale particle system è visibile per ogni tipo di martello eccezion fatta ovviamente per quella basata sull'effetto di riflessione in quanto essa per essere credibile necessita del proprio sfondo. Nel caso in cui l'utente tentasse di passare dalla visualizzazione del particle system a quella dello scenario di rifrazione quindi viene proposto un messaggio d'errore che invita a disattivare prima il particle system stesso.

![Texture](media/snowflake.png)

![Particle System](media/screenshots/simple_particle.png)

![Error](media/screenshots/error.png)

## Struttura del codice

Avendo previsto 3 scene totalmente diverse ed usato degli elementi di UI esterni, si è rivelato necessario utilizzare dei pattern di programmazione particolari. Al click di un pulsante dell'interfaccia che attiva la visualizzazione di un particolare elemento della scena viene avviato un metodo che setta a true una apposita variabile Booleana. Questa modifica verrà vista grazie ad un if durante il successivo ciclo di render (e quindi comporterà delle differenze a partire dal frame successivo), consentendo di chiamare il rispettivo metodo che costruisce l'oggetto con  i materiali desiderati. Infine tale variabile viene ri-settata a false per evitare la costruzione ciclica dell'oggetto ad ogni frame e consentendo di avere un frame rate migliore. Per favorire inoltre la migrazione della scena da un oggetto con dei materiali alla visualizzazione di un altro con materiali diversi, è stata prevista la variabile selected_object alla quale, in ciascuna funzione di creazione degli oggetti sviluppata, viene passato l'oggetto costruito. Questo consente di verificare, prima di costruire un ulteriore oggetto se nella scena ne sono già presenti altri. Se si, l'oggetto attuale viene eliminato così da consentire la creazione di quello nuovo desiderato evitando sovrapposizioni ed ancora cali in termini di prestazioni. Infine la variabile is_refract serve ad evitare che l'utente visualizzi la base d'appoggio all'interno dell'enviroment map e quindi ottenendo un risultato poco consono. Questo tipo di transizione farà tornare l'utente ad una situazione in cui viene visualizzata la base e l'oggetto viene istanziato come da default con i materiali metallici. Inoltre, dato che per la rifrazione il background della scena diventerà la cubemap, in ogni metodo di creazione come prima cosa il background verrà ripristinato con il suo colore di default. 

In sintesi, il codice è così strutturato:
- All'interno dello script ma non all'interno di una funzione specifica vengono definite le informazioni in merito alla scena, alle variabili necessarie, alla camera, ai materiali metallici, alle luci da usare e alla texture della base;
- La funzione **SetupOrbitControls()** contiene le istruzioni che consentono di vincolare la navigazione della scena da parte dell'utente, evitando attraversamenti di mesh, rotazioni eccessive, allontanamenti dall'oggetto infiniti o avvicinamenti ancora eccessivi;
- La funzione **Update()** consente di richiamare il corretto metodo per costruire l'oggetto con i materiali desiderati a seconda del click effettuato;
- La funzione **showBase()** e la **hideBase()** consentono di visualizzare e nascondere la base con la texture applicata. La variabile mesh_base viene impostata a null dopo la rimozione e verificata prima dell'inserimento per evitare duplicati della base stessa;
- **OnWindowResize()** trasla la posizione del canvas in modo che non venga sovrapposto al menù laterale poichè, come detto prima il canvas stesso è risultato non rispettare le regole strutturali imposte da Foundation;
- Le funzioni **click_show_base(), click_hide(), click_show_toy(), click_show_metallic() e click_show_enviroment()** hanno il solo scopo di ascoltare il click del pulsante e settare a true la variabile corrispondente consentendo l'avvio della procedura specificata precedentemente per visualizzare gli oggetti desiderati;
- La funzione **Metallic_Hammer** crea il martello con i materiali metallici. I figli del file obj vengono scanditi uno alla volta in modo che ciascuno abbia il materiale desiderato;
- **SetupToyHammer** contiene la definizione delle variabili uniform per i suoi materiali e la creazione del martello apposito seguendo la stessa modalità del precedente. Le luci usate in questo caso sono le stesse descritte per il materiale metallico;
- Infine la funzione **ShowEnviroment** setta come background la cube map, calcola le uniforms apposite e crea un mjolnir il cui unico materiale rispetta la proprietà desiderata. 

