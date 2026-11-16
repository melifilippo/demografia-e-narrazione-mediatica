# Demografia e narrazione mediatica degli stranieri in Italia (2013–2019)

Progetto per il corso di **Introduzione alla Programmazione – Modulo 2** (a.a. 2025/26), Università di Bologna.

**Autori:** Filippo Meli, Simone Naponiello, Marco Ruggiero

## Obiettivo

Analizzare il rapporto tra la presenza demografica degli stranieri in Italia e la loro rappresentazione nei media nel periodo 2013–2019, combinando due fonti:

- gli archivi **ISTAT** sulla popolazione residente per cittadinanza;
- il corpus di articoli de **la Repubblica** (dataset **CHANGE-IT**).

L'analisi riguarda sei nazionalità: le cinque comunità straniere più numerose in Italia (Romania, Albania, Marocco, Cina, Ucraina) e la Germania, inserita come gruppo di controllo occidentale.

## Struttura dell'analisi

1. **Quanto spazio mediatico?** Indice di sovrarappresentazione, euristica per filtrare i contesti non riferiti a persone e correlazione di Pearson tra incidenza demografica e visibilità mediatica.
2. **Come vengono raccontati?** Analisi delle tipologie di articoli in cui compare ciascuna nazionalità (heatmap e confronto tra nazionalità).

Il progetto è un'analisi esplorativa: i media funzionano da "specchio" della realtà demografica o seguono criteri editoriali propri?

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
