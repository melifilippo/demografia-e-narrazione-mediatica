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
- `requirements.txt`: librerie necessarie.

## Dati

I dati **non sono inclusi** nel repository per le dimensioni (il solo `repubblica.csv` supera i 240 MB). Provengono dall'archivio `dati progetto.zip` fornito nel materiale del corso su Virtuale (<https://virtuale.unibo.it>). Per riprodurre il notebook, estrai l'archivio e posiziona la cartella `dati_progetto/` accanto al notebook, con questa struttura:

```
dati_progetto/
└── data/
    ├── CHANGE-it/repubblica.csv
    └── istat/
        ├── Dati_RCS/Dati_cittadinanza_<anno>.csv
        └── comuni/elenco_comuni.csv
```

**Fonti**

- **CHANGE-IT** (articoli de la Repubblica): raccolta di articoli estratta nell'ambito del task CHANGE-IT di EVALITA 2020 (De Mattei, Cafagna, Dell'Orletta, Nissim, Gatt, 2020). Pagina del task: <https://sites.google.com/view/change-it>. Licenza del dataset: CC BY-NC-SA 4.0. Il file `repubblica.csv` contiene titolo, testo completo e URL di ciascun articolo.
- **ISTAT**: residenti in Italia per cittadinanza straniera e per luogo di nascita, per comune e ripartizione territoriale, anni 2002–2025. Il file `elenco_comuni.csv` associa a ogni comune i codici e le ripartizioni geografiche.

## Come eseguire

```bash
pip install -r requirements.txt
jupyter notebook Progetto_Programmazione.ipynb
```
