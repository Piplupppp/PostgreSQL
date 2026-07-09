# 🎬 Video Rental Management System - Database

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-000000?style=for-the-badge&logo=sql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Fase_1_Completata-success?style=for-the-badge)

> 🎓 **Progetto realizzato da: Giulia Trentarossi** > Corso: *Academy Fullstack powered by Accenture.*

Questo progetto rappresenta il cuore (livello Dati) di un sistema gestionale automatizzato per una società di videonoleggio. Attualmente il progetto si concentra sulla progettazione e implementazione di un **Database Relazionale in PostgreSQL**, coprendo l'intero ciclo di vita operativo e analitico richiesto.

## 📋 Indice
- [Descrizione e Regole di Business](#-descrizione-e-regole-di-business)
- [Struttura del Database (ER)](#-struttura-del-database-er)
- [Funzionalità Operative e Query](#-funzionalità-operative-e-query)
- [Contenuto della Repository](#-contenuto-della-repository)
- [Installazione e Setup](#-installazione-e-setup)
- [Sviluppi Futuri (Roadmap Fullstack)](#-sviluppi-futuri-roadmap-fullstack)

---

## 📝 Descrizione e Regole di Business

Il sistema gestisce l'operatività di **8 punti vendita** e l'interazione con **6 fornitori**. Il database è stato progettato per rispettare rigorosamente le seguenti logiche aziendali:

* **Ciclo di Vita Prodotto:** Gestione carico/scarico video a magazzino. Le copie fisiche vengono restituite al fornitore dopo 90 giorni di affitto.
* **Operatività di Noleggio:** Gestione completa con stampa ricevute di attivazione e termine noleggio.
* **Tariffazione Dinamica:** Tariffe decrescenti basate sulla durata.
* **Incentivi Staff:** Calcolo bonus mensili basati sui volumi di vendita (20, 40, 60, 80, 100 soglie).
* **Gestione Danni:** Calcolo automatico penali (3x tariffa giornaliera) per video restituiti danneggiati.

## 🗄️ Struttura del Database (ER)

Il database utilizza tipi nativi PostgreSQL (`ENUM`) per garantire integrità. Le tabelle principali includono:
* **Anagrafiche:** `cliente`, `staff`, `store`, `fornitore`, `attore`, `video`.
* **Inventario e Transazioni:** `copia_video`, `noleggio`, `tariffa`, `sconto`, `incentivo`.

## ⚙️ Funzionalità Operative e Query

Il sistema è pronto per supportare le operazioni di business tramite query SQL specifiche:
1. **Logistica:** Carico/Scarico automatico delle copie basato sulla data di fornitura (90gg) e disponibilità.
2. **Operations:** Stampa ricevute (Attivazione/Termine noleggio), gestione prenotazioni e addebito penali per danni.
3. **Analisi & Business Intelligence:**
   - Ricerca catalogo per titolo (con `ILIKE`) o genere.
   - Calcolo disponibilità in tempo reale (gestione dinamica tra attivo e prenotato).
   - Analisi incassi giornalieri per punto vendita/addetto.
   - Monitoraggio performance staff per incentivi mensili.

## 📂 Contenuto della Repository

- `esercizio1.sql`: Codice SQL completo (DDL, DML, Query).
- `schemaAzienda.pgerd`: Schema relazionale (pgAdmin).
- `azienda_noleggi.drawio.pdf`: Diagramma ER.
- Documentazione: `Esercizio 1.pptx` e `info_azienda_noleggi.docx`.

## 🚀 Installazione e Setup

1. Clona la repository.
2. Esegui lo script `esercizio1.sql` su un'istanza **PostgreSQL** tramite un client SQL (pgAdmin/DBeaver).

## 🔮 Sviluppi Futuri (Roadmap Fullstack)

Questo database è la base per un'applicazione Fullstack completa:

### Fase 2: Back-end (API RESTful)
- Implementazione server (es. Java/Spring Boot o Node.js/Express).
- Esposizione di endpoint API per gestire in sicurezza noleggi, prenotazioni e report.

### Fase 3: Front-end (Web App)
- SPA in **React** o **Angular**.
- **Dashboard Staff:** Interfaccia per operazioni rapide di carico/scarico e gestione scontrini.
- **Portale Cliente:** Area riservata per consultazione catalogo, storico noleggi e prenotazioni.

---
*Progetto sviluppato da Giulia Trentarossi durante il corso Fullstack Academy powered by Accenture.*
