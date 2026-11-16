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

I dati **non sono inclusi** nel repository per le dimensioni (il solo `repubblica.csv` supera i 240 MB). Sono reperibili alle fonti seguenti.

- **CHANGE-IT** (articoli de la Repubblica): <https://sites.google.com/view/change-it>. Raccolta di articoli estratta nell'ambito del task CHANGE-IT di EVALITA 2020 (De Mattei, Cafagna, Dell'Orletta, Nissim, Gatt, 2020), distribuita con licenza CC BY-NC-SA 4.0. Il notebook usa un file CSV con tre colonne: `headline` (titolo), `full_text` (testo completo) e `url`. Dall'URL vengono ricavati anno e tipologia di ogni articolo.
- **ISTAT** (stranieri residenti per comune e Stato di cittadinanza): <https://demo.istat.it/app/?i=RCS>. Un file CSV per anno, con separatore `;`.

**Anni analizzati:** 2013–2019, il periodo in cui si concentrano gli articoli del corpus (con un picco nel 2016). L'indice di tono esclude il 2019, per il numero ridotto di articoli. Il notebook importa i file ISTAT di tutti gli anni dal 2002 al 2025 e poi filtra il periodo 2013–2019.

Per riprodurre il notebook, posiziona i file accanto al notebook con questa struttura:

```
dati_progetto/
└── data/
    ├── CHANGE-it/repubblica.csv
    └── istat/Dati_RCS/Dati_cittadinanza_<anno>.csv   (un file per anno, 2002–2025)
```

## Come eseguire

```bash
pip install -r requirements.txt
jupyter notebook Progetto_Programmazione.ipynb
```
