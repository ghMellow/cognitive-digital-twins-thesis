# Chiamata — [DATA: YYYY-MM-DD]

**Partecipanti:** Andrea, Mario (Prof. Università di Lorena), Raffaele (FUB), Francesco, Nicolò (studente)
**Durata:** 1 h

---
### Punti chiave

**Obiettivo della tesi** La tesi si intitola provvisoriamente "Cognitive Digital Twin per il 5G" e mira a sviluppare un Digital Twin avanzato con capacità cognitive, applicato a reti 5G. Il sistema dovrà osservare, ragionare, pianificare e proporre azioni in modo autonomo, con comunicazione bidirezionale tra ambiente fisico simulato e componente cognitiva.

**Roadmap della tesi (proposta da Mario)** Mario ha delineato un approccio incrementale in tre fasi:

1. Implementare un Digital Twin "pulito", senza componente cognitiva, usando LLM con semantica implicita
2. Aggiungere strutture formali di conoscenza (knowledge graph, ontologie) e confrontare i risultati tramite benchmark
3. Integrare un'architettura cognitiva esistente (in Python) e misurare l'impatto sulla comprensione della realtà rispetto ai modelli digitali

**Use case 5G (Francesco)** Il caso d'uso riguarda la gestione di anomalie e comportamenti anomali in reti 5G (antenne gNB, user equipment). Si parla di un sistema simile a un intrusion detection system, capace di rilevare deviazioni da comportamenti attesi. Francesco ha sottolineato di partire semplice: un server "black box" con poche API, input/output elementari, prima di passare a uno scenario più complesso con emulatore 5G completo.

**Strumento presentato da Nicolò (Obsidian + LLM Wiki)** Nicolò ha mostrato un flusso di lavoro basato su Obsidian (gestore di file Markdown, open source) ispirato al concetto "LLM Wiki" di Karpathy. La struttura prevede due cartelle: Raw (materiale grezzo personale) e Wiki (gestita automaticamente dall'AI tramite Claude Code). Il sistema automatizza l'ingestione, il riassunto e la correlazione dei paper con gli obiettivi della tesi, senza necessità di infrastruttura RAG.

---

### Decisioni prese

- Nicolò **continua i corsi** assegnati (inclusi quelli di Berkeley su agenti e multi-agent) prima di passare alla fase implementativa
- Mario **condividerà il video della presentazione della tesi di dottorato** (in inglese) con tutto il gruppo
- Francesco **elaborerà un caso d'uso semplificato** ("scatolotto" con 1 antenna, 1 utente, poche azioni) come punto di partenza
- Nicolò **preparerà una presentazione a slide** entro circa 10 giorni su Obsidian/LLM Wiki: cosa fa, come funziona, come potrebbe integrarsi nel lavoro della tesi
- Il gruppo si aggiornerà **in chat** per fissare la prossima riunione
- Mario verrà **aggiunto ai contatti di gruppo** (numero di telefono da condividere)
---

## Trascrizione / Appunti

Prova, prova un tre Col del 15 aprile ci dovrebbero essere tutte e quattro i membri, quindi Francesco, Raffaele Andrea e io. Degli spogli, pensa Raffaele mi sembra che Mario sia la tua stessa postazione.

  

È una tesi quella fingere di stare in ufficio senza stare in ufficio.

  

Si vede però sempre dai bordini laterali Qual è la qualità della webcam?

  

Allora intanto presentate che io scrivo a Francesco Io sono Mi senti bene perché sto utilizzando il microfono di Andrea.

  

Eh no, infatti sì, ti sento solo un po' più basso, però sì, sì.

  

Se no invertiamo adesso dovresti sentirmi bene.

  

Perfetto, allora sono Mario Lesos, sono professore all'Università di Lorena in Francia e quest'anno sono visite il professor qui a Roma tra la FUB e la Sapienza.

  

I miei interessi di ricerca sono su estrazione e formalizzazione della conoscenza. Fondamentalmente utilizzo ontologie utilizzo knowledge graph e più qualche tool matematico, come per esempio format concept analysis per estrarre conoscenza e formalizzarla su strutture che seguono la logica del primo ordine.

  

In più faccio tutta la parte relativa ai cyber physical system o di E ai dital Twin. Cercando di introdurre la cognizione all'interno di questi strumenti che replicano la realtà in maniera digitale per poi poterla emulare o simulare. Che sia tutto per il Ciao Nicolò, io sono Raffaele sono un ingegnere della fondazione Ugo Bordoni Allora il mondo dell'intelligenza artificiale per me è abbastanza recente, quindi diciamo.

  

Sostanzialmente cercando di mettermi in pari con i colleghi Mario e Andrea. Diciamo che fino a qualche mese fa mi sono occupato di trasformazione digitale per la pubblica amministrazione, quindi. Sostanzialmente progetti più operativi che riguardavano appunto la chiamiamo digitalizzazionezzazione dei processi in essere nella nella pubblica amministrazione. Quindi la mia presenza qui diciamo è un po'' per continuare la mia formazione nell'ambito delle AI e cercare di dare un contributo da un punto di vista di pensiero, diciamo le tue attività e con l'occasione di approfittare per studiare anche insieme a te quelle tematiche insomma che riguarderanno la tua tesi.

  

Vabbè, Raffaele fa il modesto fatto molto di più, ma poi glielo tireremo fuori un po' alla volta.

  

Allora intanto, grazie a tutti.

  

Nicolò ha cominciato la tesi da due settimane 10 giorni.

  

Sì, qualcosina del genere.

  

Qualcosina del genere.

  

Allora, qual era l'obiettivo della tesi?

  

Rivediamo il titolo adesso l'avevamo messo come cognitive Digital Twin per il FiG.

  

Il nome cambierà a lungo nel tempo, piano piano che andremo poi a delineare meglio gli obiettivi e vedere i risultati.

  

L'idea è quella comunque di sperimentare un Digital Twin avanzato cognitivo.

  

Che già abbiamo iniziato a studiarlo attraverso la tesi di dottorato seguita da Mario applicato a un contesto. Realistico legato al 5G su cui è Francesco che diciamo guida un po' quella parte perché ne stavamo ragionando anche ieri non ti mettiamo ancora in tutte le e-mail perché ancora l'oggetto.

  

Però fondamentalmente noi vorremmo creare un rapporto tra un ambiente fisico simulato.

  

Uno strato di di mezzo che eravamo nel nella proposta di tesi poteva essereclipse ditto, ma un qualunque framework di mezzo che cura la comunicazione con il la parte cognitiva del Digital Twin.

  

Digital si dovrebbe arricchire, quindi da tutto quello che succede nello nell'oggetto simulato Osservare ragionare e pianificare e eventualmente proporre azioni, quindi c'è una comunicazione bidirezionale.

  

L'esempio banale potrebbe essere che il sistema si accorge stiamo parlando prima con Mario. Immaginiamo che è un sistema che gestisce può gestire la banda, quindi c'è la funzionalità di uno quanti utenti sono collegati due quali sono la banda a disposizione.

  

Si identifica il sistema identifica il sistema simulato poca banda troppi utenti lo comunica al Digital pin che decide in modo autonomo poi di fare una modifica sul sistema e quindi aumentare la b banda, buttare fuori gli utenti, non ne ho idea adesso stiamo giocando però concettualmente è questa comunicazione in cui il digital p diventa attivo E osserva anche i risultati delle proprie azioni.

  

Per fare questo, ovviamente se viene una parte di intelligenza nel digital Twin, dovremmo andare a capire come strutturare.

  

C'è l'approccio appunto quello di CDT che abbiamo visto nella tesi di Mario, che adesso Mario poi se ci vuoi raccontare qualcosa in più per quello diciamo è quasi uno stato dell'anno.

  

Ci sarà una parte, quindi sia teorica, ma poi dovremmo andare a capire come andarlo a implementare.

  

Con sistema sicuramente ad agenti, ma poi dovremmo capire come farli comunicare tra loro, come se come avere eventualmente un coordinatoretore, come e questo l'ho detto l'altra volta che mi ha messo a giocare con open clow, quindi certe azioni di basso livello si potrebbero delegare a ad altri sistemi ecco questo è sarà l'obiettivo.

  

E quindi adesso è facile dirlo, ma appunto diciamo ci sono varie cose complicate lungo la strada, vabbè l'usa di LLM non è più compli complicato coordinarne fra loro tanti capire come gestire il contesto, la memoria, cioè il sistema di mettere da parte delle informazioni ecco quelle saranno le le sfide da fare.

  

Tra cui anche capire il protocollo di comunicazione, ma quello poi lo definiremo piano piano.

  

Detto questo, poi stavo parlando con Mario sarà interessante anche vedere prima di arrivare poi all'oggetto 5G che sia un oggetto complesso è anche magari trovare qualcosa lungo la strada Qualche primo esempio più semplice in cui sistema magari ha.

  

Comunica cinque informazioni in uscita la gente può attivare tre azioni e quindi inizia a giocare vediamo come evolve però questo c'è tempo unica cosa poi Nicolò fortunatamente non finirà la tesi a luglio perché deve fare ancora degli esami, ma anche per la nostra perché dico.

  

Diciamo non sarei da solo, cioè ci lavoriamo anche noi perché siamo interessati e quindi cercheremo di starti dietro, però è qualcosa che si parla probabilmente per ottobre, cioè consegna un fine settembre discussione ottobre poi . I tempi si vedono, però diciamo c'è c'è tutto il tempo giusto vedere che poi ci sono momenti in cui Nicolò ci lascerà non per andare in vacanza, ma per fare gli esami che mi mancano. Mi rimane sicurezza e machine learning pattern Recognition, che sono due esami molto teorici, diciamo come. Poi invece ho seguito anche il corso di machine learning for vision e multime Che diciamo già sui deep learning e lì mi manca solo il progetto che devo consegnare. Invece tutti gli altri esami del corso del poli li ho dati. Ultimo aggiornamento per lasciare la parola a Mario allora le cose che ho lasciato a Nicolò da fare nel nei primi 10 giorni.

  

Si è letto la tesi e aveva iniziato a fare anche dei corsi.

  

Io faccio riferimento ai corsi tendenzialmente quelle di deparning Nicolò.

  

Sì, no pensavo dicesse più quelli anche di Berkeley che ho guardato anche un po' di quella.

  

Ci sono anche quelli di c'è una lista sul file e poi qualcosa ho mandato nella chat perché ci stanno c'è vari corsi che si possono seguire poi appunto siete già finiti fai finito pure Berkeley?

  

No, allora quelli di Berkeley li ho un po' selezionati nel senso che appunto comunque anche loro avevano un loro percorso di spiegare gli argomenti, quindi.

  

Alcuni li ho guardati tutti, soprattutto quello che poi era su il problema della comunicazione tra i genti e come validarli.

  

Ce n'era uno specifico che parlava proprio su quell'argomento, quindi ho guardato quello più specifico.

  

Va bene, sì, allora.

  

C'è una parte teorica sul CDT e ci sarà una parte teorica anche sul discorso degli agenti che ci sono vari corsi che. Qualcosa sono più recenti, qualcosa è più recente vecchio vuol dire di del ottobre 2025 roba del genere, però fra deep learning hai ed altre fonti ecco quelli servono almeno a capire quali sono le architetture.

  

E su quelle ci sarà anche un problema di validazione in questa forma di metriche che ne stanno uscendo anche nuove farà parte del del di quello che probabilmente servirà nella prima fase, tanto per capire quali sono tutte gli strumenti a disposizione prima di passare poi un'implementazione. E ok. Comunque allora per tutti dovreste essere tutti invitati c'è una cartella condivisa e su cui c'era un primo file con Una una bibliografia i primi corsi, poi su quello possiamo andare poi aggiungere altre cose via via che emergono Mario.

  

Una cosa che mi piacerebbe condividere con voi metterò il link per lo scarico che è una cosa che avevo detto ad Andrea qualche tempo fa era la presentazione della tesi che dicono tu hai letto della tesi di dottorato che tu hai letto perché Gianna ha fatto fatto la def settimana fa e quindi poi adesso mi hanno dato la possibilità di condividere il il file video è in inglese, quindi non c'è nessun problema e così che c'è anche diciamo un primo un primo approccio di risposte a quelle che la tesi stessa ha lasciato un po'' come Come prospettive sia di lavoro, ma anche come possibilità di comprendere meglio qual è la procedura per attivare un reale cognitive Digital Twin.

  

Fondamentalmente, Io penso, ma dimmi tu Andrea e anche Raffaele e Francesco che Un primo step prima di inserire la parte di cognizione è di vedere un po'' se si riesce a mettere in pratica in maniera digitale un Digital Twin, perché Ci sono tantissime persone che parlano di Digital Twin senza che poi la sua definizione formale venga applicata e quindi poi fanno degli esperimenti che non c'è che non hanno una validità scientifica.

  

Come abbiamo letto, cioè come hai letto Nicolò e Il Digital Twin fondamentalmente ha delle caratteristiche di bidirezionalità. Di insieme tempo reale della del controllo di questa bidirezionalità con il tempo reale che però è una misura estremamente variabile e poi c'è questa cosa che Sia i sensori sia i gli attuatori abbiano all'interno quelle che sono delle caratteristiche di pseudo intelligenza, ovvero ci sono all'interno delle possibili dei possibili trattamenti dati, quindi se il dato arriva al sensore, questo non viene inviato direttamente a quella che è la base di dati del digital twe, ma viene trattato e quindi viene già contestualizzato in relazione a quella che è una situazione ben precisa, così che Quando il l'informazione viene stoccata, ci sono già delle Dei Delle procedure che sono fondamentalmente l'applicazione della conoscenza che può andare a gestire l'informazione.

  

E avere e generare quella che è poi la la parte più importante che è il feedback, quindi la saggezza e questa saggezza non è nient'altro che ulteriore conoscenza che viene stoccata in quella che è.

  

Una struttura di stoccaggio della conoscenza.

  

Quello che ti ho detto è quello che io io e la letteratura scientifica vede come Digital.

  

Tutta la parte di cognizione, come tu hai potuto leggere nella Nella nella tesi di dottorato, si appoggia a strumenti semantici e strumenti cognitivi.

  

Gli strumenti semantici che sono rappresentati all'interno della della tesi sono sono stati Sono stati diciamo esemplificati attraverso un'ontologia e non so se hai dato un'occhiata fondamentalmente un'ontologia sono tanti concetti legati tra di loro con delle regole, però fatta molto molto veloce.

  

Dall'altra parte la parte cognitiva.

  

A parte tutta la disquisizione scientifica di che cos'è la cognizione e che cos'è un sistema cognitivo, noi l'abbiamo attualizzata attraverso un'architettura cognitiva e questa cosa fondamentalmente a che cosa ci è servita?

  

Ci è servita per stoccare una delle funzioni principali di un sistema cognitivo, ovvero la memoria. Utilizzare quelle che sono la parte semantica e la parte di Stoccaggio informazioni e stoccaggio dati per poi essere utilizzato utilizzando o l'inferenza o semplicemente delle regole che sono altresì stoccate all'interno dell'architettura cognitiva.

  

Ora da una parte tu c'hai il sistema del Digital Twin dall'altra parte tu hai un'architettura cognitiva queste due entità in maniera operazionale possono essere offuse insieme o semplicemente staccate e ci sono dei vari contatti dei protocolli di comunicazione che permettono al sistema di di funzionare in maniera cognitiva.

  

Quello che secondo me step by step potrebbe essere fatto nella tesi è Come diceva giustamente Andrea, immaginare un un esempio questo esempio deve essere strutturato secondo Una progettazione di Digital Twin senza la parte cognitiva, strumenti capaci di fare delle interazioni con il mondo reale E vedere che cosa abbiamo come risposta senza prendere in conto la parte semantica nella parte cognitiva.

  

Questo perché perché utilizzando per esempio degli LLM abbiamo che la semantica è implicita all'interno del modello.

  

Quindi, ok, non la stiamo esplicitando non la stiamo formalizzando, ma ci sta e la usiamo.

  

Nel momento in cui questo questo esercizio, questo esempio va a darci dei risultati, vediamo poi se possiamo integrare all'interno di questa struttura che abbiamo creato, quindi Digital Twin, l'LM o quello che sia dati e risultato, se possiamo inserirci delle strutture formali.

  

Quindi, knowlege graph, ontologie e vedere come l'utilizzo di queste strutture vanno a modificare il risultato.

  

Cercheremo anche di fare dei benchmark per verificare che il risultato con l'aggiunta della formale della conoscenza formale esplicita sia più o meno interessante una volta che abbiamo anche fatto questo, passiamo alla parte cognitiva.

  

Non voglio che tu studi e crei una struttura cognitiva o un'architettura cognitiva, prenderemo delle architetture cognitive in Python già esistenti, le inseriamo all'interno di quelle che è il sistema del Digital Twin, quindi poi dobbiamo decidere se inserirle dentro come moduli inseriti proprio all'interno della struttura oppure fuori con una una comunicazione se tu hai letto anche la parte di user use case della della della tesi hai visto che la nostra la nostra idea è stata quella di mettere la l'architettura cognitiva al di fuori del sistema digital Twed e comunicavano attraverso l'ontologie o attraverso le basilari, quindi non era accoppiata in maniera rigida e vedere ancora una volta come benchmark che cosa hai come risultato in realtà relazione alle altre due punto hai finito la tesi.

  

Hai finito la tesi perché in maniera incrementale hai dato luogo a quelle che sono le Le differenti istanziazioni di una struttura di relazione con il mondo reale e il mondo digitale.

  

Hai fatto la parte semantica e la parte di formalizzazione semantica, quindi esplicitazione semantica e poi ci hai messo dentro anche la parte di cognizione.

  

Qual è l'apporto scientifico l'apporto scientifico è come nell'ultima parte la terza parte la cognizione impatta nella struttura della comprensione della realtà rispetto a quelli che sono i modelli digitali. Questa cosa ha un impatto scientifico interessante tiremo fuori anche una una un articolo scientifico da questo e tutta la parte implementativa sarà il backbond Lo scheletro dai grazie lo scheletro e lo scheletro di quello che è poi la parte scientifica vera e propria.

  

Questo è quello che mi viene di dirti di come io vedo la tesi che tu hai iniziato.

  

Sì, sì, perfetto.

  

Anche perché appunto non è che ho altre esperienze di questo tipo, perché in triennale.

  

Non fondamentalmente non avevamo da fare tesi. Quindi per me, appunto già l'approccio è quello di tipo un po'' buttarsi e fare le cose. Invece questa parte scientifica qua diciamo questo rigore mi manca un pochino .

  

Quindi anche questo è importante quello che hai appena detto.

  

Assolutamente, anche perché è fondamentale avere rigore scientifico se vuoi la tesi di laurea in primis e Lavorare in ricerca e sviluppo successivamente.

  

Ok, mi ricollego a questo non abbiamo parlato dello use case che però.

  

Sarà, cioè c'è appunto la parte di studio, la definizione del dell'infrastruttura concettuale e poi vediamo come applicarla.

  

Come applicarla il caso questo c'è Francesco Perché lo andremo a diciamo anche a livello strategico è anche poi importante andare a declinare un caso d'uso che ha un impatto.

  

E quindi che può essere vendibile noi diciamo abbiamo competenze sul 5G e l'oggetto poi lascia parola a Francesco potrebbe sia essere un oggetto realistico 5G, ma il tipo di Azioni che farà il con il digital sono legate anche ad aspetti potrebbero essere legati aspetti di sicurezza, cioè noi potremmo sia simulare anomalie di tanti tipi oppure il corretto funzionamento sarebbe anche interessante inserire quel quel tipo di Di contesto, quindi di cyber security, perché abbiamo anche un'area di cyber security, quindi.

  

Sempre più realistico il caso d'uso e le problematiche e su quello poi vedremo come interviene il Digital Twin e che tipo di cognitive di ragioni in ti può andare a fare questo lo dico come fine del diciamo della chiaramente come dicevo prima, probabilmente come diceva anche Mario prima di arrivare alla parte cognitiva con Digital Twin e sarà un Digital Twin dobbiamo ragionare, ma un esempio più piccolo, perché chiaramente se no ti sfugge subito di mano a me basterebbe un frigorifero, apri chiudi e qual è il termostato c'è qualcosa che è andato male dentro che interviene cioè perché per sviluppare, ma anche fare esperienza, intanto i benchmark li puoi fare sia sul caso semplice sia sul caso complesso, però intanto hai benchmark.

  

Detto questo, Francesco che ieri c'era stato un grande scambio di mail di questa parola Allora sì, no giusto per collegarmi quello che ho detto, cioè diciamo all'inizio il caso Nun serve anche un po' per chiudere, diciamo tutto il l'obiettivo della tesi, perché pure quando si scrive un articolo l'importante è anche un po' il placement, quindi capire diciamo dove tu vai ad applicare e poi il passaggio dalla trip alla ovviamente all'inizio c'è diciamo il focus come diceva Andrea sarà le reti 5G in particolar modo qualcosa legato alla sicurezza, diciamo questa è un po' l'area diciamo coinvolta l'area della coinvolta quindi diciamo l'idea è sempre andare a capire.

  

Come il sistema reagisce nel momento in cui si ha una situazione di rischio in una situazione che può essere sia di anomalie di comportamento a livello di performance, ma anche a livello di comportamento, diciamo proprio a livello sequenziale nel momento in cui vediamo che ci sono dei pattern di comunicazione che non non sono più quelli standard.

  

Oppure diciamo una volta che hai fatto analisi, vedi che ci sono una deviazione da un comportamento aspettato, allora lì.

  

Diciamo alzo un flat, è tipo una sorta di intrusion system. All'inizio, cioè diciamo adesso concentrati sulla parte diciamo teorica strutturale. Sulla parte questa qua, diciamo del dell'emulatore, diciamo quindi la parte fisica all'inizio è inutile che. Impazziamo su una cosa super complessa, quindi come dicevo l'altra volta sarà Black box molto semplice che avrà diciamo input output che avrà delle API e in base a quello diciamo ti restituirà poi diciamo gli sarà semplicemente come dice un server con un black box con un server. Questo diciamo proprio il punto base, quindi come diceva Andrea, una cosa aumenta che ne so tipo aumenta il traffico il traffico.

  

Comportamenti semplici blocca l'usoer givement, attiva quell'altromen diciamo comportamenti molto semplici per farla un po' più realistica come dicevo l'altra volta si può tirar su un emulatore un po' più strutturato, quindi qualcosa non diciamo con un pa trasher che fa emula un g e anche la parte degli user dietro, quindi che ne so, tipo una sede in g quindi diciamo un parco di tutti i siti e un parco di g2B diciamo quella sarebbe il desiderato non è che tutti sanno cos'è un giro faccio le cose più semplici proprio quelle praticamente sarebbe la l'antenna della la struttura antenna del 5G e anche il telefono.

  

L' E quindi diciamo quello lì c'è tutto uno scenario di situazioni, quindi sia questi user gam che si comportano male.

  

Volendo anche questi gB che si comportano male che sono più di uno e poi situazioni in questi g B puoi decidere magari di.

  

Fare ebover che significa spostare un telefono da una certa all'altra.

  

Quello sarebbe proprio il desiderato al più grande ho detto all'inizio cominciamo con uno scatolotto semplice con un'antenna, un userment, vediamo se il comportamento inseriamo magari qualche anomalia. E vediamo ciò che sistema come reagisce questa cosa e tu come tramite il tuo nodo centrale, come vuoi influenza questo sistema, spegnici questo è il Poi diciamo te lo possiamo complicare a piacere occuperò un po' di questa cosa non se ci sono dubbi.

  

A parte linguaggio che devi semplificarlo per tutti, ma quello passa un telefono in un'antenna Allora vabbè, ti direi Francesco non adesso è tanto è inutile comunque servirà una.

  

Una guida in tre magnifico mondo del 5G o qualcosa anche per contestualizzare, ma da qui a un mesetto e via questo non lo voglio sovraccaricare questo scatolotto comincia una forma un po' più articolata poi aspetta un attimo.

  

Poi anche iniziare Francesca ha ragionare sullo scatolotto, quello a tre funzioni.

  

Sì, sì.

  

Balmente prima stavo adesso parlando al volo con Mario a me basterebbe un web server. Poi dietro ci può essere anche WordPress, cioè però capire Sì, no nel senso Wordpress ok fai una modifica adesso è fuori dal contesto, però gli dici pubblica hai pubblicato cose studi, però per capire il concetto del digital però la direi ancora continua a fare, diciamo Nicolò come percorso seguire quei corsi che ti ho passato, perché allora noi.

  

Dovremo poi andiamo di pari passo adesso Mario ci manderà anche altro materiale prima di iniziare a concettualizzare, magari meglio il Digital Twin e vedere come andare a implementare, cioè anche la parte sul digital Twin.

  

Studierei ancora, perché quei corsi sono diciamo l'ultimo Berk era di fine 2025 in più c'è tante cose io ti ti chiederò anche di guardare Open Clow come ti dicevo.

  

Perché a un certo punto dovremmo fare anche delle scelte io per esempio, mi ero messo a giocare a Open clow, visto che è un tipo di gestione della memoria che sono file in markdown che potrebbe essere interessante. Però Vai Mario. Vogliamo sapere una cosa, Nicolò ti va se quando finisci tutti i corsi ci fai una panoramica di quello che hai che hai capito o che hai preso non in maniera pedissecua o estremamente istanzializzata, però comunque sia qualche cosa che ci permetta di comprendere i vari domini su cui ti sei interessato e il fare il fatto che poi lo restituisci a noi ti permette anche a te di formalizzarlo, concettualizzarlo E poi avere la possibilità di rispondere a qualche domanda che ci fa come che ci arriva a noi in relazione a quelle che sono le tue le tue slide.

  

Guarda, volevo proporre esattamente la stessa cosa, anche perché appunto nella premia facevo frutto questa occasione anch'io per diciamo migliorare la mia formazione, volevo solo magari proporre non proprio alla fine di tutti i corsi, ma magari con una certa frequenza o alla conclusione di una.

  

Una porzione di studio, magari se ci potevi un po' raccontare come quali erano appunto i concerti appresi in quella corso in quella te che avevi letto, insomma Posso parlare sì ok allora cosa è successo dopo l'ultimo messaggio che avevo inviato?

  

Poi appunto, visto che il numero di tesi continuava ad aumentare, no quindi ho detto okay qua il numero di tesi mi sa che continuerà e non finirà.

  

E allora ho detto un attimo, mi sono insegnato un attimo a guardare in giro. E vabbè, il fatto è che il problema è che sono molto lunghi, quindi comunque sì, sottolinea leggi, però comunque perdi almeno.

  

Io non essendo abituato a leggere questo questi argomenti così tecnici scientifici, magari mi perdo magari dei collegamenti, quindi.

  

E allora ho iniziato a dire vabbè, come supporto comunque già da già dato che lo so facendo con proprio con lo studio al poli mi trovo bene.

  

Ho provato a integrare un po' di AI, no nel senso che comunque mi sono come strumento di supporto.

  

Poi, in base riguardo quello che stai dicendo tu, Andrea, sul fatto degli MD mi è arrivata.

  

Come dire su perché comunque appunto, io esploro varie cose mi è arrivato non so se anche voi avete visto sulla parte di Obsidian.

  

Che questo praticamente come se fosse Noon alla fine è un semplicemente un gestore di file che lavora solo con file MD. E ti permette anche di avere una visione a grafo dei vari collegamenti, perché questi file MD li puoi differenziare, quindi da un file puoi andare a un altro. E il contesto l'hai visto questo esempio?

  

E praticamente c'è Carpati che è il mio il mio grande eroe sta finendo la sua intervista di una settimana fa sì che ha Come dire, proposto questa LLM Wiki non so se ne avete sentito parlare, ma praticamente il il suo concetto è quello di dire Io creo due cartelle, una robaw e una chiamata Wiki nella cartella Row ci metto il mio materiale e le mie ricerche, quindi tutto quello che concerne il lavoro standard di un umano fino al giorno d'oggi.

  

Nella cartella Wiki invece cosa faccio?

  

Do delle istruzioni precise e poi l'AI automatizza certi processi. Tipo io, per esempio, adesso nella parte di esplorazione delle tesi. Magari appunto, mi facevo creare prima un riassunto per avere una visione globale.

  

Poi gli chiedevo di correlarmela, magari a il nostro percorso di tesi, se ci sono aspetti interessanti o meno.

  

E quindi diciamo che poi appunto, solo che questa cosa la dovevo fare a mano per ogni file invece grazie a questo strumento qua sono riuscito bene a Automatizzare il tutto con delle skills, perché alla fine anche le skill sono file md o è in parallelo hai già vinto il primo seminario che ci farai fra 10 giorni infatti io stavo proprio per questo perché non ci fai una demo di questa cosa che ci sta, sì, sì mostro lo Come condivido solo lo schermo un attimo impostazioni di sistema io sono un un ossessionato dei modelli, quindi mi piacerebbe anche vedere sia il processo che tu utilizzi nei vari passaggi sia il modello proprio A livello semantico di che cosa cosa significa quello che tu fai.

  

Allora, solo l'unica cosa mi sta chiedendo di dargli degli accessi mi dice di uscire e rientrare.

  

Se riesco a uscire, cioè se per caso mi butta fuori e rientro dall'Inter. Ok. Filosofico eccoci, un intero schermo.

  

Mi sono distratto un attimo, cioè ovviamente sto finendo una cosa di due di una settimana fa, ma già non l'ho finito Obsidian, che però è a pagamento.

  

No, no, è open source infatti è quella la cosa bella.

  

Ok ok. Sta su sulla parte se tu vai su Odiki lo trovi quello che vi dicevo, appunto qua nella cartella Raw ho fatto i paper dove ci sono Tutti i vari paper con discusso qua è quello che mi sembra sia della ragazza esatto. Ci sono i vari paper poi come vi dicevo i valori per la cioè mi sono fatto fare il percorso che vi dicevo prima.

  

Però quindi c'è degli agenti che operano in automatico.

  

E allora anche qua il discorso agenti Come dire, perché ho visto un altro video che c'era questo signore che. Nel nel corso del tempo ha provato vari agent coder adesso non mi viene il termine specifico, però tipo open quello di cloud code tipo siamo siamo lì come adesso i nomi mi mi sfuggono perché sto facendo tutto un po' di fretta, quindi un attimo. Però il problema che lui mostra è che molti di questi fanno le cose come vogliono loro sotto il naso, cioè non è che ti dicono.

  

Bene, cioè non hai il controllo totale di quello che sta facendo la gente. E quindi molto spesso, cioè è finito per svilupparsene uno suo adesso come si chiamava P Vabbè, guarda, tanto hai già vinto un seminario, quindi non ti preoccupare ce la ripresenti Vabbè poi raccolgo il materiale comunque, io adesso il mio flusso di lavoro standard è dato che abbiamo cloud code con l'università. Quello che faccio è il fatto uso qua Obsidian come visualizzazione per me, perché comunque i file MD qua vengono visualizzati in maniera carina, diciamo leggibile.

  

Invece qua su visual Studio code è un po' È un po'' tipo sempre non lo so, non mi piace cioè viene questa visualizzazione, ma non mi non mi ispira granché.

  

E quindi una volta che sono all'interno di Studio code posso semplicemente usare Cloud code per per per farlo interagire, perché poi alla fine è un agente, quindi tramite chat faccio interagire.

  

Il punto di ingresso è questo cloud MD in cui gli ho dato tutte le specifiche.

  

Su come è composta la wiki su qual è qual è il suo obiettivo.

  

La Wiki di Obsidian la cioè allora perché il concetto generico che ha presentato. Che è proprio Carpati che ha proposto qua è il fatto di dire che in maniera generica, quando qualcuno si approccia a un nuovo argomento, no quindi c'è da fare raccolta e poi stilare del materiale.

  

Allora lui ha mantenuto la cosa generica, quindi proprio per questo anche i nomi sono Row e Wiki perché Row è qualunque materiale, quindi quello che tendenzialmente da fare è che tu ti crei la tua cartella di un argomento in questo caso l'ho chiamata tesi. Tesi volte e poi all'interno di questa vai a contestualizzare le cose, quindi ho trovato.

  

Questo ragazzo che perché Carpati mi sembra non abbia poi pubblicato una sua guida, cioè aveva solo fatto questa idea. Ho trovato questo ragazzo che aveva un po po' cercato di formalizzare il concetto con un primo file MD.

  

E appunto come file d'ingresso nella Wiki troviamo il glossario per tutta la terminologia delle degli acronimi.

  

Poi c'è questo index che serve un po'' come indice del del del materiale raccolto.

  

Quindi specifica anche poi all'AI dove andare a spostarsi perché poi è quella la la roba interessante secondo me. Il fatto che tu hai poi tutta questa conoscenza che comunque è strutturata con questi file MD che sono referenziati.

  

Quindi, volendo c'è una gerarchia. E quindi poi quando si va a lavorare anche con l'AI no sempre il fatto del del contesto. Aiuta perché comunque lui partendo dal dall'alto riesce poi a muoversi solo dove gli serve. Va a scegliere il ramo che è più pertinente rispetto all'azione da svolgere, giusto è questo quello che fa tendenzialmente sì, si legge proprio i file completi tipo io qua nel nel cloud medi do quando creo una nuova sessione , quindi partendo da zero come dire, me lo porto subito al passo no quindi gli dico tutto quello che di cui ha bisogno. E li indico anche per esempio il fatto che c'è la skill, quella per ingestire le tesi rispetto a.

  

Al worklow che facevo io a mano. Però sì, la la questione dei MD che tu fai che ne ho visti vari di MD sono tutti automatici non sai sì sì nella parte della wiki sono tutti automatici nella parte di Raw sono io che a mano me li sono messi come gestione mia. La sua specializzazione poi il resto lo fa la macchina però su questo ho due domande la prima ho visto che hai messo anche quello di Berkeley immagino che siano le slide a questo punto.

  

Sì, lì in realtà o i video perché i video iniziano a diventare interessante.

  

No avevo sì, perché in realtà sempre con l'università abbiamo anche Gemini.

  

E quindi mi sono fatto gli ho fatto prendere il video anche direttamente Come allora diciamo che perché cosa è successo all'inizio stavo facendo le cose a mano in realtà infatti qua nei vari varie cartelle row ci sono i vari file già fatti.

  

Ma perché appunto, non non avevo ancora costruito tutto questo poi mentre stavo facendo questo E mentre guardavo gli altri video, ho detto aspetta, ma io queste cose le posso collegare.

  

E allora ho fatto poi ho fatto partire tutta questa macchina.

  

Però ecco, diciamo che la roba nasce, cioè dal punto di vista più dei programmatori adesso tornando più.

  

Su come è nato il tutto e nasce un po'' come alternativa al rag.

  

Perché appunto, nel rag tu hai bisogno di un sistema a parte che ti prende il materiale con.

  

Appunto la ricerca vettoriale che poi c'è anche quella ibrida con quella un po'' più standard ecco.

  

Però comunque, hai bisogno di creare tutta un'infrastruttura che invece qua non non c'è perché appunto l'AI lavora bene coi falli MD. Ed è anche poi leggibile per per l'umano.

  

Nel senso, non c'è perché qualcuno l'ha già fatto prima.

  

Perché se tu hai il il chatbot o comunque la struttura che ti permette di fare questo tipo di analisi è perché qualcuno ha fatto un rang su una quantità enorme di di documenti li ha fatti mangiare dal dall'LLM e poi lui ti permette di utilizzare quello.

  

Sì, sì, cioè ovviamente ci si basa sempre sugli LLM che col tempo si evolvono, cioè li migliorano ecco quella è un po'' la logica.

  

L'unica limitazione che ho visto che dicevano online che Questo lo puoi sostituire a rag solo fino a un certo numero di documenti, perché poi appunto si basa sul contesto che tu dai all'AI quindi se quindi sì, sì, diciamo che qua è proprio come lavorare nel contesto delle AI, quindi Andare secondo me, cioè è da vedere come la la classica interazione che abbiamo adesso, quindi via chat. Su ma espansa, quindi col fatto di per noi programmatori diciamo è molto meglio, cioè per noi c'è programmi e c'è la visione anche del del testo ecco non è. È chiaro che questo è come se fosse uno strumento in cui tu hai una base bella solida, un pavimento.

  

E poi con questo hai la possibilità di sul pavimento di costruirci qualche cosa in relazione a quelle che sono le le specifiche più stimolanti e poi magari costruisci passatemi il termine piccole strutture e poi.

  

Sopra queste strutture ci costruisci dei ponti e quindi hai la possibilità a struttura piramidale di basarti sempre su la densità di conoscenza che tu hai succhiato via e distillato da un insieme sempre più raffinato di di documenti. Perché no?

  

Due domande. Allora la prima tu hai anche il prompt a cui puoi fare domande, immagino. Sulla base della conoscenza, non è sulla parte diciamo tutta di elaborazione del del Rw giusto.

  

Sì, nel senso cioè intendi come inesto i file la parte diciamo dei dati grezzi hai la parte dei dati elaborati dall'LM sulla base dell'MD E su quella conoscenza, tu hai anche un'interfaccia con cui puoi comunicare.

  

Sì, sì, volendo sì, perché alla fine essendo che è sempre via chat, no la comunicazione. Lui perché il cloud cloud MD perché appunto si ispira al fatto che che utilizzi i servizi cloloud, cioè di di cloud Però il concetto è che lì tu specifici, cioè come non so quante volte magari vi capita appunto di ogni volta di scrivere magari prompt simili solo per riavere lo stesso comportamento, no quindi diciamo quello serve come base di inizio.

  

Poi da lì già con quello, se vuoi interrogare la base dati sì, perché dato che sa la struttura. Poi il primo passo che fai andare nell'index e poi dall'index si muove ulteriormente, quindi sì, poi la base è anche interrogabile.

  

Infatti, cioè il discorso è che tutta la cartella wiki è gestita interamente dall'AI.

  

Quindi la tua tesi Sì, praticamente crea la base poi volendo se si può fare quello che si vuole ecco Allora ti direi adesso poi ci sentiamoamo la mia chat magari poi fissiamo un giorno in cui vedi la parte, diciamo d'architettura dietro ce la spieghi più però suggerimento, allora questo è un ottimo strumento per velocizzare però i documenti Sì, no lo so lo so lo so lo so infatti infatti era il mio disclaimer era ho fatto questo giusto per avere una mia base, però comunque devo verificare tutte le fonti perché Sì, no, no, ma non è solo quello intanto è interessante perché io non la conoscevo quindi si potrebbe utilizzare adesso ci ragioniamo come utilizzarla anche per altre applicazioni o anche all'interno della tesi, a parte questa tua utilizzo, però lo sforzo è come quando uno che ne parli con un inglese con accento indiano, parli un inglese con accento cinese ecco quella. Forma menti che ti te la devi piuttosto che farti solo aiutare dall'interfaccia che ti spiega la tesi e l'articolo un po' ci devi sbattere la testa per capire così ti metti anche nei panni di chi ha scritto quell'articolo se la tesi dottorato no no ma è per essere diciamo autonomo perché Noi più o meno, chi più chi meno ci abbiamo sbattuto la testa ecco la fasi sbattere la testa ti serve comunque, quindi gli articoli più importanti per cui la tesi dottorato guidato dal diciamo dalla sintesi e della spiegazione, certi capitoli leggili.

  

No, no, ma la tesi l'avevo cioè il punto è che comunque cioè sono d'accordo con quello che dici, perché anche al poli.

  

Ho visto dei miei compagni che erano bravissimi, poi è arrivata l'AI e si sono tipo lobottomazzati il cervello, quindi la usano solo tipo macchinetta dei delle sala giochi Che premono e si usano il risultato. Tornando alla tesi, sì sì, cioè nel senso anche lì sono partito leggendela, soprattutto Le prime condivise fino fino all'ultimo messaggio che avevo scritto quelle le ho le ho lette, ma è stato anche utile proprio per entrare nel nel dominio in cui.

  

Dobbiamo scrivere la tesi, ecco.

  

Poi da lì adesso invece un po' alla volta, anche anche perché comunque appunto devo c'è anche il poli da portare avanti. Quindi adesso un po' alla volta cerco di leggermi le le altre tesi e controllare che che appunto non siano state scritte cavolate, ecco.

  

Sì, no, no, ma a prescindere quello vai nell'allucinazione, quello ci potrebbe stare di quello non non ti devi mai fidare, no, ma era giusto.

  

Come tuo gradino iniziale sport E ok, guarda detto questo a parte guarda molto interessante, anzi continua visto che hai la passione se interessato continua a proporci novità perché siamo tutti curiosi poi vediamo.

  

Cioè, in teoria, appunto, io lo vedevo lato open clow perché c'era quella memoria che era in MD.

  

Nulla vieta perché esatto anche legato a questo argomento, perché alla fine cioè a me sembra di capire che.

  

Tutti questi agenti sono semplicemente poi, cioè o comunque queste architetture framew che creano.

  

Sono semplicemente LLM vppati in una architettura agentica, quindi per fare azioni e Robe.

  

Ma poi tutto il resto si basa su file, perché anche gli MS MCS, quelli che per fare i tool o le skill, cioè alla fine, c'è proprio le skill sono solo un file MD che che dice l'AI in maniera sequenziale quali sono le operazioni da fare fare Allora sì, nel senso prima vabbè adesso che ce l'abbiamo il locale, sì, prima era magia.

  

Sì, sì, beh no, sì, sì, prima certo.

  

Adesso sì, alla fine comunque sono file, La sfida è nella memoria alla fine le skill sono brevi da memoria quello io sarà una cosa da capire.

  

Cioè, quanta memoria quanto contesto, perché poi dipende anche dalla tua configurazione locale, chiaramente cosa cosa andare a registrare e come immaginiamo nel coni di Digital Twin chiaramente dovrà basarsi sia su una parte di regole poi vediamo l' tipo una sorta di memoria statica, quella delle regole.

  

Sì, quella è statica, però poi anche una memoria degli eventi.

  

Cioè tu chiaramente fai prendi le decisioni in base a quello che è successo.

  

Che poi potrebbe esserci nuove nuovi scenari fra eventi fra loro correlati in particolare nel caso della cy per sicurezza di anomalie che singolarmente sono anomalie prese insieme e quindi però avendo un pattern storico di che ne so un giorno capisci che è un attacco un attacco che è fatto di varie punti non lo so però ecco quello il problema della memoria ci sta quello di Open Clow che mi era piaciuto era che la vedevo.

  

La vedevo poi alla fine un MD adesso potrebbe essere questo approccio di Obsidian o qualche tanto da qui a due mesi ne uscirà un altro ancora.

  

Sì, no vabbè, poi è un campo che che si muove una velocità ma con l'obiettivo che hai della tesi, cioè tu continua a portare queste questi spunti.

  

Allora, tornando a noi, perché io fra 10 minuti ho un'altra riunione rimaniamo che tu continua comunque a seguire i corsi questi corsi sei spunti.

  

Tipo di questo tipo ce li mandi immaginiamo fra una decina di giorni Obsidian o quello o chi sarà diventato in 10 giorni ce lo racconti un po' meglio.

  

Poi vediamo il formato Sì, adesso magari su strutturo un attimo esatto cioè faccio slide tipo presentazione o vi va bene un documento che vi leggete secondo me le slide aiutano perché poi è una cosa che rimane poi vediamo se se poi diventa un documento lo vediamo dopo poi con le slide sono più anche per la nostra attenzione che ormai abbiamo una certa età dobbiamo avere pochi concetti semplici però se devono essere Di suggestione sì sia quello che ci fai adesso e quello che ci si potrebbe fare e intanto poi Mario ci manda altro materiale di cui la presentazione della quella te la vedi tutta Cioè ci tocca a tutti poi noi chiaramente adesso ci fai mettere ci dai questo strumento e lo usiamo noi perché così facciamo meno fatica noi tu dovrei faticare.

  

Sì, sì, no, ma quello è qua ho trovato si chiamava PDv la chiamata.

  

Che che alla fine è appunto un open cloud, diciamo open clow, però open source, quindi si può volendo c'è il Gitub ci si può lavorare.

  

Io per esempio, di open clow, visto che non mi fido, avevo preso la parte di quello di invidia che era Nemoclo era quello ho usato quello perché evitava che prendesse il nel dubbio e ti creava un docker ad hoc, però questi si vedono questo ci vedranno più avanti l'importante è sapere che esistono e che iniziare a capire su cosa si basano appunto la memoria fatta in MD cioè tutto quello che è architettura del del sistema d'agenti, perché poi finora e poi chiudiamo fra poco non abbiamo parlato del Cioè qui abbiamo l'infrastruttura, ma poi se usi cloud discorso, usi Deepsi che è un altro.

  

Sì, no, certo il motore che metti sotto poi cambiano le belle prestazioni.

  

Sì, cambiano e anche di molto il paradigma che usi di di reasoning ecco quelle saranno altre cose da buttare dentro che però fa diventa diventerà nel momento in cui abbiamo il caso semplice. Saranno variabili da modificare di cui puoi fare delle misure, perché a me era capitato che appunto QN funzionasse meglio di altri e l'ho verificato, cioè prima ne ho messi tanti insieme ho visto che Qen per quel problema risolveva meglio.

  

Creato architettura ha creato il modello base Che sia questo o un altro, poi inizia a mettere le varie versioni e vedi. Quale funziona meglio e anche cercare di capire anche il paradigma è perché io per esempio di questo boh dietro che cosa fa React non non lo so.

  

Non so come li gestisce come i singoli oggetti dal dalla cartella, diciamo dei dati a RAw agiscono in modo autonomo oltre ad avere quella MD ecco quello sarebbe interessante poi da capire Una domanda che Volevo sapere i file MD che tu hai strutturato.

  

Io so che hanno sono dei markup molto molto leggeri.

  

Hai definito tu il modello di i meta tag che possono darti poi informazioni supplementari o l'hai utilizzati semplicemente come file di testo che poi sono interpretabili attraverso quelli che sono i gli agenti o l'LLM che fa da interpretazione di quello che è il file.

  

Nel senso li hai caricati un po' di più attraverso quelle che sono delle strutture di conoscenza che tu decidi di di creare oppure le hai utilizzati come un diario ho letto questo la l'informazione si trova su questo file ho letto questo l'informazione sotto questo file eccetera, eccetera. Ma dici nella parte Rw o nella parte parte che è quella che hai creato tu nella parte Rho in realtà no sono molto più semplici perché appunto Come dire contenuto nel nelle mie abilità e quindi ho fatto semplicemente appunto dei riassunti però anche lì cioè mi sono fatto comunque aiutare, cioè via via via via via, cioè Sono più secondo me, quello più interessante è il valore per la questi file qua chiamati valore per la mia tesi, perché.

  

Prendono la la tesi in oggetto, la nostra con tutto quello che ci siamo detti nelle nelle varie call o comunque nella proposta.

  

E cerca di trovare punti in cui . Portare acqua al nostro mulino, ecco lì per esempio c'è una struttura no per esempio aree da approfondire del paper due immagino che ci siano dei dei capitoli uno due questa struttura.

  

Che implicitamente crea una gerarchia Una gerarchia semantica all'interno dei messaggi che ci sono scritti dentro li ha fatti li hai fatti tu l'ha fatti lei non sono definiti da nessuna parte, quindi sono impliciti giusto?

  

Sì, cioè sì, non non credo di capire bene quel punto la tabella che hai creato l'ha creata lui, le intestazioni le ha create lui, giusto?

  

Sì, sì, sì, sì.

  

Perfetto, percezione, ragionamento, memoria, eccetera, eccetera l'ha prese direttamente riassunto lui Un riassunto lui da quelle che sono le funzioni cognitive, diciamo di base.

  

Tutta la struttura l'ha fatta lui, quindi anche quelle che per noi sono delle una formattazione che ci permette a noi di comprendere meglio come è strutturata la conoscenza è stata espressa direttamente dal riassunto dell'LLM, giusto?

  

Sì, sì, sì alla fine sì sì.

  

Ok. Va bene, niente questo quindi fondamentalmente La semantica implicita è utilizzata in maniera implicita ugualmente.

  

Era per capire se avevi inserito tu delle strutture e se magari queste strutture erano state. Non so se tu hai mai lavorato con i file XLM li ho visti ok sopra i file XLM ci stavano gli XLS che erano fondamentalmente dei delle strutture che spiegavano all'interprete XLM Che cosa era un insieme che cos'era un insieme di tag, eccetera, eccetera.

  

Questa struttura, tu qui semplicemente non l'hai fatta perché è implicita all'interno del dell'oggetto che stai descrivendo, semplicemente questo.

  

Sì, Sì, a questo formalismo, ammetto che mi manca un pochino, ma perché appunto. Preoccupare.

  

Sì, sì, sì no è che appunto il fatto è che noi lì al Poli, avendolo opportunità di provare questi sistemi, cioè io vista questa opportunità, mi sto buttando proprio a capofitto E quindi sto per cioè magari formalismi Robe le sto un attimo mettendo da parte è che tu tu sai che dietro questa facilità di utilizzo e questo struttura zzazione obbligatoria perché se no non arriveresti ad avere questi risultati semplicemente questo.

  

Ok grazie.

  

Chi fa la formalizzazione , quello è un altro problema, quella è magia e la scopriremo.

  

Allora direi che visto che c'è un minuto con pausa toilette, direi che ottimo Nicolò e ci sentiamo in chat e poi fissiamo un attimo con l'agenda per il prossimo incontro va bene.

  

Sì, va benissimo quindi ok giusto perso la pagina non mi vedo più vabbè, spero voi mi vediate. Continua sui corsi che stai finendo Mario manderà altro materiale e poi faremo diciamo presentazione magari Struttu magari un attimo meglio questo discorso così sì, no cioè è uno strumento lo devi un attimo testare una volta che hai visto che da dei risultati, ecco fai un passo cerca di capire Come da questi risultati, come funziona e ce lo racconti poi potrebbe essere questo uno strumento che che continuiamo ad utilizzare, cioè tu lo stai utilizzando, però astraendo un po' nel momento in cui ce lo viene a raccontare, sei costretto adstrarre.

  

A quel punto vediamo anche se può essere di utilizzo sicuramente il discorso della memoria in MD e dei delle skill in qualche modo verrà è uno è fondamentale Sì, sì, adesso per questo mese è fondamentale il prossimo mese potrebbe non esserlo, però a quel punto se sei riuscito ad astrae a quel punto quando ti chiederò guarda open clow E sarai in grado di sovrapporre due architetture diverse e capire.

  

Però e contro, cioè a parte cioè perché hanno sviluppato questa più leggera più veloce veloce e così via e quindi poi ad un certo punto avremo nel momento in cui si passa la fase implementativa, avrai Quella conoscenza maturata dal campo che ti permette di prendere delle scelte di fare delle scelte o proporne.

  

Ok, dai va benissimo Allora, un saluto, grazie a tutti e ci aggiorniamo poi in chat.

  

Adesso poi metto anche Mario nel numero un po'.

  

Perfetto, ciao ciao ciao a tutti.

  

Ciao ragazzi 

  

  

La trascrizione è stata [utile](applenotes://transcriptionFeedback?isPositive=1&attachmentID=8041CB13-DDF8-4C82-BFAB-F523722D9ACD) o [inutile](applenotes://transcriptionFeedback?isPositive=0&attachmentID=8041CB13-DDF8-4C82-BFAB-F523722D9ACD)?