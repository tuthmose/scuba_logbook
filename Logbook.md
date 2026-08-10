---
type: scuba_logbook
area: scuba
tags:
  - scuba
  - logbook
---

# Logbook

Registro immersioni in markdown. Una nota per dive in [[Dives/]].

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

## Template

Due varianti — copia quella adatta al tipo di dive:

- [[_templates/Dive_Template_Rec]] — ricreativa (no sezione `## Tec`)
- [[_templates/Dive_Template_Tec]] — tecnica con deco (include `## Tec` con Piano deco + Soste effettive)

Il frontmatter è identico tra i due; cambia solo il body.

## Dive registrate

Vista live dal `.base`: ordinabile, filtrabile, con statistiche aggregate.

![[Logbook.base]]

Nella cartella [[Dives/]] trovi una dive di esempio (`2025-01-01_Secca_Esempio.md`,
sito e dati inventati) che mostra come compilare frontmatter e body — puoi
cancellarla o tenerla come riferimento.

## Istruzioni complete

Vedi [[README|README]] per setup, filosofia di compilazione e troubleshooting.
