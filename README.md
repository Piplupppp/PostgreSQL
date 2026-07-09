# Video Rental Management System - Database

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-000000?style=for-the-badge&logo=sql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Fase_1_Completata-success?style=for-the-badge)

>  **Progetto realizzato all'interno del corso Academy Fullstack powered by Accenture.**

Questo progetto rappresenta il cuore (livello Dati) di un sistema gestionale automatizzato per una società di videonoleggio. Attualmente il progetto si concentra sulla progettazione e implementazione di un **Database Relazionale in PostgreSQL**, ma è stato concepito con un'architettura scalabile per essere esteso in futuro con logiche di Back-end e interfacce Front-end.

## Indice
- [Descrizione e Regole di Business](#-descrizione-e-regole-di-business)
- [Struttura del Database (ER)](#-struttura-del-database-er)
- [Funzionalità Implementate (Query)](#-funzionalità-implementate-query)
- [Contenuto della Repository](#-contenuto-della-repository)
- [Installazione e Setup](#-installazione-e-setup)
- [Sviluppi Futuri (Roadmap Fullstack)](#-sviluppi-futuri-roadmap-fullstack)

---

## Descrizione e Regole di Business

Il sistema gestisce l'operatività di **8 punti vendita** e l'interazione con **6 fornitori**. Il database è stato progettato per rispettare rigorosamente le seguenti logiche aziendali:

* **Gestione Magazzino e Fornitori:** Le copie fisiche dei video restano in negozio per un massimo di **90 giorni**, dopodiché il sistema segnala che devono essere restituite al fornitore.
* **Tariffazione Dinamica:** I noleggi sono calcolati a giorni interi con tariffe decrescenti all'aumentare della durata del noleggio (es. da 3,00€/gg per noleggi brevi a 1,00€/gg per noleggi oltre i 40 giorni).
* **Sconti e Fidelizzazione:** Il sistema prevede l'applicazione di sconti percentuali codificati (es. 20% di sconto ogni 5 noleggi) per i clienti abituali.
* **Incentivi per lo Staff:** I dipendenti (organizzati in responsabili e addetti) ricevono bonus calcolati automaticamente in base alle soglie di vendita mensili (da 20 a 100+ noleggi).
* **Privacy e Tracciabilità:** Ogni cliente è registrato con i propri contatti e il riferimento al documento cartaceo della liberatoria privacy.

## Struttura del Database (ER)

Il database utilizza i tipi di dato nativi di PostgreSQL (inclusi gli `ENUM` per gli stati) per garantire la massima integrità dei dati. Le tabelle principali sono:

* **Anagrafiche:** `cliente`, `staff`, `store`, `fornitore`, `attore`, `video`.
* **Relazioni Intermedie:** `video_attore` (relazione molti-a-molti tra film e cast).
* **Inventario:** `copia_video` (identifica univocamente ogni singola cassetta/DVD per tracciarne il carico e il ritiro).
* **Transazioni:** `noleggio` (cuore del sistema, traccia lo storico, lo stato e gli importi pagati), `tariffa`, `sconto`, `incentivo`.

## Funzionalità Implementate (Query)

Nello script SQL sono incluse logiche avanzate e query di reportistica (DML e DQL) che permettono di:

1. **Gestione Catalogo:** Ricerca di film per titolo o genere, calcolando dinamicamente le copie **effettivamente disponibili** in negozio in tempo reale (escludendo copie affittate o rese al fornitore).
2. **Storico Noleggi:** Tracciamento dei movimenti di ogni singolo cliente.
3. **Scadenziario Fornitori:** Calcolo automatico della data di scadenza dei 90 giorni per la restituzione della merce.
4. **Report Finanziario:** Calcolo dell'incasso totale giornaliero suddiviso per punto vendita e per singolo addetto.
5. **Calcolo Incentivi:** Estrazione dei volumi mensili generati da ogni dipendente per l'assegnazione dei bonus.
6. **Gestione Prenotazioni (Extra):** Tracciamento dei titoli non ancora disponibili ma prenotati dai clienti per un ritiro futuro.
7. **Addebiti per Danni (Extra):** Calcolo automatico di una penale (es. 3x la tariffa giornaliera) per i clienti che restituiscono i video danneggiati.

## Contenuto della Repository

All'interno di questa repository troverai tutti i file di progettazione e implementazione:

- `esercizio1.sql`: Lo script SQL completo. Contiene le istruzioni DDL (creazione schema e tabelle), l'aggiunta dei vincoli `FOREIGN KEY`, le istruzioni DML (inserimento dati di mock realistici e corretti temporalmente) e le query di reportistica.
- `schemaAzienda.pgerd`: L'esportazione dello schema ER direttamente da pgAdmin.
- `azienda_noleggi.drawio.pdf`: Il diagramma Entità-Relazione concettuale/logico del database.
- `image_908540.jpg`: Screenshot di test che dimostra il corretto funzionamento delle query nel DBMS.
- `Esercizio 1.pptx` / `info_azienda_noleggi.docx`: Traccia originale dell'Academy con i requisiti, i listini tariffari, gli sconti e le logiche di business applicate.

## Installazione e Setup

Per testare il progetto in ambiente locale:

1. Clona questa repository sul tuo computer.
2. Assicurati di avere in esecuzione un server **PostgreSQL**.
3. Apri un client per la gestione del database (es. *pgAdmin 4* o *DBeaver*).
4. Apri il file `esercizio1.sql` ed eseguilo.
   *(Nota: lo script include i comandi `CREATE DATABASE azienda;` e popola automaticamente uno schema dedicato chiamato `noleggi`).*

## Sviluppi Futuri (Roadmap Fullstack)

Questo progetto è nato come base per lo sviluppo di un'applicazione web completa. Nelle prossime fasi dell'Academy (o come progetto personale), il sistema verrà esteso nel seguente modo:

### Fase 2: Back-end (API RESTful)
- Sviluppo di un server back-end (utilizzando tecnologie come **Java Spring Boot**, **Node.js/Express** o simili).
- Mappatura del database tramite ORM (es. Hibernate o Prisma).
- Creazione di endpoint API per separare le logiche di business dal database (es. endpoint per calcolare automaticamente il prezzo in base alle date selezionate, o per inserire un nuovo noleggio).
- Implementazione della sicurezza, autenticazione e autorizzazione (JWT) per distinguere i ruoli tra "cliente", "dipendente" e "responsabile".

### Fase 3: Front-end (Web App)
- Sviluppo di una Single Page Application (SPA) utilizzando framework come **Angular** o **React**.
- **Dashboard Amministrativa:** Interfaccia dedicata allo Staff per registrare nuovi noleggi, gestire i rientri, visualizzare alert sulle scadenze dei fornitori e monitorare gli incassi e i propri incentivi.
- **Portale Cliente:** Interfaccia rivolta all'utente finale per registrarsi, sfogliare il catalogo, verificare la disponibilità nei vari store, prenotare titoli futuri e consultare il proprio storico.

---
*Progetto sviluppato da Giulia Trentarossi durante il corso Fullstack Academy powered by Accenture.*
