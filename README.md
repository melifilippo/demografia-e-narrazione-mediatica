# Demografia e narrazione mediatica degli stranieri in Italia (2013–2019)

Progetto per il corso di **Introduzione alla Programmazione – Modulo 2** (a.a. 2025/26), laurea magistrale in Dati, metodi e modelli per le scienze linguistiche, Università di Bologna.

**Autori:** Filippo Meli, Simone Naponiello, Marco Ruggiero

## La domanda di ricerca

I media funzionano come uno "specchio" della realtà demografica, oppure seguono criteri editoriali propri, indipendenti da quante persone compongono una comunità?

Per rispondere, il progetto confronta due fonti nel periodo 2013–2019:

- gli archivi **ISTAT** sulla popolazione residente in Italia per cittadinanza;
- il corpus di articoli de **la Repubblica** contenuto nel dataset **CHANGE-IT**.

L'analisi riguarda sei nazionalità: le cinque comunità straniere più numerose in Italia nel periodo (Romania, Albania, Marocco, Cina, Ucraina) e la Germania, inserita intenzionalmente come gruppo di controllo occidentale.

Il lavoro è svolto interamente con `pandas`, `numpy`, `matplotlib` e `seaborn`, senza librerie di elaborazione del linguaggio naturale: per questo l'analisi del testo si basa su espressioni regolari e su un'euristica costruita a mano.

## Preparazione dei dati

**Articoli de la Repubblica**

- Titoli e testi vengono puliti: minuscolo, apostrofi e trattini sostituiti da spazi, rimozione di punteggiatura e caratteri speciali.
- Dall'URL di ogni articolo si ricavano l'anno di pubblicazione e la tipologia (cronaca, politica, cultura e così via). I 1.354 articoli privi di URL vengono esclusi, perché non si possono datare né classificare.
- Gli articoli si concentrano tra il 2013 e il 2019, con un picco nel 2016: da qui la scelta del periodo.
- La tipologia "esteri" viene esclusa, per evitare che la politica internazionale influenzi il conteggio.

**Dati ISTAT**

- Ogni file riporta gli stessi residenti a più livelli territoriali (comuni, province, regioni, ripartizioni, Italia). Dopo aver verificato che i totali coincidono, si usano solo i comuni, per non contare più volte le stesse persone.
- Le nazionalità vengono scelte dalla classifica dei residenti stranieri nel periodo 2013–2019.

## Parte 1: quanto spazio mediatico?

**Indice di sovrarappresentazione**

Gli articoli che citano una nazionalità vengono individuati con espressioni regolari sulle forme dell'aggettivo (per esempio `rumeno/romeno`, `albanese`, `tedesco`). Per ogni nazionalità e anno si calcolano:

- il **peso mediatico**: quota di articoli che la menzionano sul totale degli articoli dell'anno;
- l'**incidenza demografica**: quota dei residenti di quella cittadinanza sul totale dei residenti in Italia;
- l'**indice**: peso mediatico diviso incidenza demografica.

Un valore vicino a 1 indica una rappresentazione proporzionata, sotto 1 una sottorappresentazione, sopra 1 una sovrarappresentazione.

**Euristica: persone o Stati?**

L'indice grezzo è gonfiato dagli usi non riferiti a persone: "governo cinese", "economia tedesca", "squadra tedesca". Per correggerlo, ogni occorrenza viene classificata guardando le cinque parole precedenti e le cinque successive:

- **persona**, se nel contesto compaiono parole come "cittadino", "residente", "famiglia", "lavoratore", "studente";
- **non persona**, se compaiono parole come "governo", "mercato", "azienda", "squadra", oppure termini specifici per Paese (Merkel, Putin, i colossi tecnologici cinesi);
- **ambiguo**, in tutti gli altri casi.

L'indice viene poi ricalcolato sui soli articoli classificati come "persona": 299 per la Germania, 154 per la Cina, 101 per il Marocco, 99 per la Romania, 75 per l'Albania, 72 per l'Ucraina.

**Cosa emerge**

- Nessuna nazionalità ha un indice stabile intorno a 1.
- Per la Cina l'indice filtrato scende in molti anni da valori molto superiori a 1 a valori vicini o inferiori a 1. Per la Germania cala nettamente ma resta sopra 1 in tutti gli anni.
- Romania e Albania risultano quasi sempre sottorappresentate, pur essendo comunità numerose.
- **Ucraina 2014**: l'indice grezzo è 4,9, quello filtrato 0,5. La crisi di quell'anno aumenta gli articoli sull'Ucraina come Stato, non quelli sulle persone ucraine. Cambia però il contesto in cui se ne parla, che si sposta verso la solidarietà.

**Correlazione di Pearson**

La correlazione tra incidenza demografica e peso mediatico filtrato, anno per anno, misura se la visibilità segue la demografia.

| Nazionalità | Correlazione |
|---|---|
| Marocco | 0,695 |
| Albania | 0,337 |
| Cina | -0,146 |
| Romania | -0,404 |
| Germania | -0,679 |
| Ucraina | -0,772 |

Solo Marocco e Albania mostrano una correlazione positiva. Per le altre la visibilità è scollegata dall'andamento demografico, o va in direzione opposta.

## Parte 2: come vengono raccontati?

**Tipologie di articoli**

Per gli articoli classificati come "persona" si calcola la distribuzione su nove tipologie: cronaca, politica, solidarietà, cultura, tecnologia, scienze, ambiente, salute, scuola.

| Nazionalità | Contesto prevalente |
|---|---|
| Albania | cronaca (63,6%) |
| Romania | cronaca (61,1%) |
| Marocco | cronaca (60,0%) |
| Ucraina | solidarietà (31,1%), poi cronaca (29,5%) |
| Germania | cronaca (22,9%), cultura (16,5%), scienze (12,0%), salute (11,2%) |
| Cina | tecnologia (22,1%), cronaca (17,9%) |

**Indice di tono**

A ogni tipologia è assegnato un peso, da +1,0 (scienze) a -1,0 (cronaca), con la politica a 0. L'indice di tono è la media dei pesi degli articoli di una nazionalità in un anno. Il 2019 è escluso, perché i pochi articoli disponibili renderebbero il valore instabile.

- **Albania, Marocco, Romania**: valori negativi in tutti gli anni.
- **Germania e Cina**: valori spesso vicini o superiori a zero.
- **Ucraina**: andamento irregolare, da -0,67 nel 2013 a +0,22 nel 2014.

I pesi sono una scelta degli autori e servono per il confronto tra nazionalità, non come misura assoluta.

## Conclusioni

1. **La visibilità mediatica non dipende dalla consistenza numerica delle comunità.** L'andamento dei residenti non basta a spiegare l'attenzione del quotidiano.
2. **Le nazionalità sono associate a contesti narrativi ricorrenti.** Albania, Marocco e Romania compaiono soprattutto nella cronaca; l'Ucraina nella solidarietà; Germania e Cina in cultura, scienze e tecnologia.

Nel periodo analizzato il quotidiano non si comporta come uno specchio della demografia: la copertura segue criteri di notiziabilità e scelte editoriali.

## Limiti

- L'euristica lascia la maggior parte delle occorrenze nella categoria "ambiguo": l'analisi filtrata si basa su poche decine o centinaia di articoli per nazionalità.
- Un articolo classificato come "persona" non riguarda necessariamente residenti in Italia: può trattarsi di turisti, atleti o politici.
- Il corpus proviene da un solo quotidiano.
- La correlazione di Pearson è calcolata su sette punti annuali per nazionalità.

## Contenuto del repository

- `Progetto_Programmazione.ipynb`: notebook finale con codice, grafici e commenti.
- `dati_progetto/data/istat/Dati_RCS/`: dati ISTAT sui residenti per cittadinanza, un file CSV per anno (2002–2025).
- `requirements.txt`: librerie necessarie.

## Dati

- **ISTAT** (stranieri residenti per comune e Stato di cittadinanza): i file sono **inclusi** nel repository, in `dati_progetto/data/istat/Dati_RCS/`. Un file CSV per anno, con separatore `;`. Fonte: <https://demo.istat.it/app/?i=RCS>.
- **CHANGE-IT** (articoli de la Repubblica): il file `repubblica.csv` **non è nella cartella del repository** per le dimensioni (supera i 240 MB, oltre il limite di GitHub per i singoli file), ma è scaricabile dalla Release `v1.0`: <https://github.com/melifilippo/Analisi_testi_repubblica_e_demografia/releases/download/v1.0/repubblica.csv>. Il file contiene tre colonne: `headline` (titolo), `full_text` (testo completo) e `url`. Dall'URL vengono ricavati anno e tipologia di ogni articolo.
  - Fonte: dataset CHANGE-IT, task di EVALITA 2020 (De Mattei, Cafagna, Dell'Orletta, Nissim, Gatt, 2020), <https://sites.google.com/view/change-it>.
  - Licenza: CC BY-NC-SA 4.0. Il file è ridistribuito qui alle stesse condizioni, per soli fini didattici e non commerciali.

**Anni analizzati:** 2013–2019, il periodo in cui si concentrano gli articoli del corpus (con un picco nel 2016). L'indice di tono esclude il 2019, per il numero ridotto di articoli. Il notebook importa i file ISTAT di tutti gli anni dal 2002 al 2025 e poi filtra il periodo 2013–2019.

Per riprodurre il notebook, scarica `repubblica.csv` dalla Release e mettilo in questo percorso:

```
dati_progetto/
└── data/
    ├── CHANGE-it/repubblica.csv        (da scaricare dalla Release)
    └── istat/Dati_RCS/                 (già nel repository)
```

## Come eseguire

```bash
pip install -r requirements.txt
jupyter notebook Progetto_Programmazione.ipynb
```
