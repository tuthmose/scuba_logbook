---
type: moc
area: scuba
tags:
  - scuba
  - logbook
---

# Logbook

Registro immersioni in markdown. Una nota per dive in `Dives/`.

## Convenzioni

- **Nome file**: `YYYY-MM-DD_Sito.md` (più suffisso `_n` se più dive lo stesso giorno)
- **dive_number**: progressivo reale di carriera, allineato al libretto cartaceo
- **Profondità**: metri (m), con decimale dove disponibile
- **Heading**: gradi numerici (°)
- **Skills**: autovalutazione 1-5 (vuoto = non praticata)

> [!info] Legenda skills
> 1 = molto faticosa / errata
> 2 = riuscita con difficoltà
> 3 = sufficiente
> 4 = buona
> 5 = automatica

La stessa scala si usa nella sezione `## Drill` del body, nella forma
`- nome_drill — 3/5, commento`.

## Template

Due varianti — copia quella adatta al tipo di dive:

- [[_templates/Dive_Template_Rec]] — ricreativa (no sezione `## Tec`)
- [[_templates/Dive_Template_Tec]] — tecnica con deco (include `## Tec` con Piano deco + Soste effettive)

Il frontmatter è identico tra i due; cambia solo il body.

## Dive registrate

Vista live dal `.base`: ordinabile, filtrabile, con statistiche aggregate.

![[Logbook.base]]

Nella cartella `Dives/` trovi tre immersioni di esempio — **siti, nomi e dati
sono inventati** — che coprono i tre casi tipici. Puoi cancellarle o tenerle
come riferimento.

| File | Cosa mostra |
|---|---|
| `2025-01-01_Secca_Esempio.md` | ricreativa semplice: il caso base, frontmatter e body minimi |
| `2025-01-02_Cala_Esempio.md` | ripasso delle skill ricreative (maschera, recupero erogatore, pedagno): come si usa `## Drill` e perché il consumo di una sessione di addestramento non va confrontato con quello di una dive normale |
| `2025-01-03_Relitto_Esempio.md` | addestramento tecnico con deco e gas switch (S-drill, V-drill, notox): sezione `## Tec` con piano deco contro soste effettive, e un RMV marcato come stima |

## Istruzioni complete

Vedi [[README|README]] per setup, filosofia di compilazione e troubleshooting.
