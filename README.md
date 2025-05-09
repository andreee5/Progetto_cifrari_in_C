# Programma Cifrari Classici (in C)

[![Download v1.0](https://img.shields.io/github/v/release/andreee5/Progetto_cifrario_a_trasposizione?label=Download%20v1.0)](https://github.com/andreee5/Progetto_cifrario_a_trasposizione/releases/latest)

Questo progetto è un'applicazione in linguaggio C che permette di cifrare e decifrare messaggi tramite tre metodi di crittografia classica, selezionabili da un semplice menù all'avvio del programma.

---

## ✍️ Autori

- Andrea Sartoni
- Filippo Lazzari

---

## 🔐 Descrizione del programma

All'avvio, l'utente può scegliere quale dei tre cifrari utilizzare:

1. **Cifrario a trasposizione colonnare**  
   - Riordina i caratteri del messaggio basandosi su una parola chiave.  
   - Tipico esempio di cifratura per anagramma.

2. **Cifrario carbonaro**  
   - Ispirato ai sistemi di cifratura usati dai carbonari, con sostituzione simbolica o lessicale.  
   - Ha valore storico oltre che didattico.

3. **Cifrario ROT13**  
   - Ogni lettera viene sostituita con quella a 13 posizioni dopo nell'alfabeto.  
   - È un metodo semplice ma efficace per oscurare messaggi.

---

## 🖥️ Come si usa

### 1. Compilazione

Apri il terminale nella cartella del progetto e digita:

```bash
gcc -o cifrari Progetto_cifrario_a_trasposizione_colonnare-cifrario_carbonaro-cifrario_ROT13.c
