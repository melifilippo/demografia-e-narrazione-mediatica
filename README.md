# Demografia e narrazione mediatica degli stranieri in Italia (2013–2019)

Progetto per il corso di **Introduzione alla Programmazione – Modulo 2** (a.a. 2025/26), laurea magistrale in Dati, metodi e modelli per le scienze linguistiche, Università di Bologna.

**Autori:** Filippo Meli, Simone Naponiello, Marco Ruggiero

## Il progetto

I media funzionano come uno "specchio" della realtà demografica, oppure seguono criteri editoriali propri?

Per rispondere, il progetto confronta i dati **ISTAT** sui residenti in Italia per cittadinanza con gli articoli de **la Repubblica** (dataset **CHANGE-IT**) nel periodo 2013–2019. L'analisi riguarda sei nazionalità: le cinque comunità straniere più numerose (Romania, Albania, Marocco, Cina, Ucraina) e la Germania, inserita come gruppo di controllo occidentale.

Il lavoro usa solo `pandas`, `numpy`, `matplotlib` e `seaborn`, senza librerie di elaborazione del linguaggio naturale: l'analisi del testo si basa su espressioni regolari e su un'euristica costruita a mano.

## Metodo

- **Indice di sovrarappresentazione**: quota di articoli che citano una nazionalità, divisa per la quota dei suoi residenti sul totale. Vale 1 se la rappresentazione è proporzionata.
- **Euristica "persona / non persona"**: ogni occorrenza è classificata dalle cinque parole precedenti e successive, per separare gli articoli sulle persone ("cittadino", "famiglia", "lavoratore") da quelli sugli Stati ("governo cinese", "economia tedesca"). L'indice viene ricalcolato sui soli articoli riferiti a persone.
- **Correlazione di Pearson** tra incidenza demografica e visibilità mediatica, anno per anno.
- **Tipologie di articoli e indice di tono**: in quali sezioni del giornale compare ciascuna nazionalità, con un punteggio da +1,0 (scienze) a -1,0 (cronaca).

## Risultati

**Quanto spazio mediatico?** Nessuna nazionalità ha un indice stabile intorno a 1. Romania e Albania sono quasi sempre sottorappresentate; la Germania resta sovrarappresentata anche dopo il filtro. Per l'Ucraina nel 2014 l'indice passa da 4,9 (grezzo) a 0,5 (filtrato): la crisi di quell'anno aumenta gli articoli sullo Stato, non quelli sulle persone.

| Nazionalità | Correlazione di Pearson | Contesto prevalente |
|---|---|---|
| Marocco | 0,695 | cronaca (60,0%) |
| Albania | 0,337 | cronaca (63,6%) |
| Cina | -0,146 | tecnologia (22,1%) |
| Romania | -0,404 | cronaca (61,1%) |
| Germania | -0,679 | cronaca (22,9%), cultura (16,5%) |
| Ucraina | -0,772 | solidarietà (31,1%) |

**Come vengono raccontati?** Albania, Marocco e Romania compaiono soprattutto nella cronaca e hanno un indice di tono negativo in tutti gli anni. Germania e Cina sono associate a cultura, scienze e tecnologia. L'Ucraina è l'unica in cui la solidarietà supera la cronaca.

**In sintesi**: la visibilità mediatica non dipende da quante persone compongono una comunità, e ogni nazionalità è associata a contesti narrativi ricorrenti. Nel periodo analizzato il quotidiano non si comporta come uno specchio della demografia.

**Limiti**: l'euristica lascia molte occorrenze non classificate, quindi l'analisi filtrata si basa su poche decine o centinaia di articoli per nazionalità; il corpus proviene da un solo quotidiano. I dettagli sono nel notebook.

## Contenuto del repository

- `Progetto_Programmazione.ipynb`: notebook finale con codice, grafici e commenti.
- `dati_progetto/data/istat/Dati_RCS/`: dati ISTAT sui residenti per cittadinanza, un file CSV per anno (2002–2025).
- `requirements.txt`: librerie necessarie.

## Dati

- **ISTAT** (stranieri residenti per comune e Stato di cittadinanza): i file sono **inclusi** nel repository, in `dati_progetto/data/istat/Dati_RCS/`. Un file CSV per anno, con separatore `;`. Fonte: <https://demo.istat.it/app/?i=RCS>.
- **CHANGE-IT** (articoli de la Repubblica): il file `repubblica.csv` **non è nella cartella del repository** per le dimensioni (supera i 240 MB, oltre il limite di GitHub per i singoli file), ma è scaricabile dalla Release `v1.0`: <https://github.com/melifilippo/Analisi_testi_repubblica_e_demografia/releases/download/v1.0/repubblica.csv>. Il file contiene tre colonne: `headline` (titolo), `full_text` (testo completo) e `url`. Dall'URL vengono ricavati anno e tipologia di ogni articolo.
  - Fonte: dataset CHANGE-IT, task di EVALITA 2020 (De Mattei, Cafagna, Dell'Orletta, Nissim, Gatt, 2020), <https://sites.google.com/view/change-it>.
  - Licenza: CC BY-NC-SA 4.0. Il file è ridistribuito qui alle stesse condizioni, per soli fini didattici e non commerciali.

**Anni analizzati:** 2013–2019, il periodo in cui si concentrano gli articoli del corpus. Il notebook importa i file ISTAT di tutti gli anni (2002–2025) e poi filtra il periodo.

Per riprodurre il notebook, scarica `repubblica.csv` dalla Release e mettilo in questo percorso:

```
dati_progetto/
└── data/
    ├── CHANGE-it/repubblica.csv        (da scaricare dalla Release)
    └── istat/Dati_RCS/                 (già nel repository)
```

## Come eseguire

1. Scarica il repository (pulsante **Code → Download ZIP**, oppure con Git):

   ```bash
   git clone https://github.com/melifilippo/Analisi_testi_repubblica_e_demografia.git
   cd Analisi_testi_repubblica_e_demografia
   ```

2. Scarica `repubblica.csv` dalla Release `v1.0`. Crea la cartella `dati_progetto/data/CHANGE-it/` (nel repository non esiste, perché Git non conserva le cartelle vuote) e mettici il file.

3. Installa le librerie e apri il notebook dalla cartella del repository:

   ```bash
   pip install -r requirements.txt
   jupyter notebook Progetto_Programmazione.ipynb
   ```

Il notebook cerca i dati a partire dalla cartella da cui viene avviato: va quindi aperto dalla cartella principale del repository. L'esecuzione completa richiede circa un minuto e qualche GB di memoria.

Per vedere solo i risultati non serve eseguire nulla: il notebook si apre direttamente su GitHub, con grafici e tabelle già visibili.
