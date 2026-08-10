# Logbook — registro immersioni in markdown

Un logbook per subacquei basato su file markdown + [Obsidian](https://obsidian.md),
pensato per essere compilato in barca dal cellulare e consolidato a casa.
Ogni dive è una nota, con frontmatter strutturato (profondità, gas, pesata,
condizioni...) e un file `.base` che genera tabelle e statistiche aggregate
in automatico, senza bisogno di fogli di calcolo esterni.

Questa cartella è uno strumento autonomo, pensato per essere condiviso (es.
su GitHub) senza portarsi dietro nessun altro contenuto personale.

## Requisiti

- [Obsidian](https://obsidian.md) (gratuito)
- Plugin core **Bases** abilitato: `Impostazioni → Core plugins → Bases`
  (incluso in Obsidian dalla v1.9+; se non lo vedi, aggiorna Obsidian)

## Setup

1. Scarica/clona questa cartella (`Logbook/`) da qualche parte sul tuo disco.
2. In Obsidian: `Apri cartella come vault` → seleziona `Logbook/`.
   In alternativa, se hai già un vault tuo, copia l'intera cartella
   `Logbook/` dentro il vault esistente.
3. Apri `Logbook.md`: dovresti vedere la tabella live generata da
   `Logbook.base` con la dive di esempio già dentro.
4. Cancella o modifica la dive di esempio in `Dives/` quando sei pronto a
   registrare le tue.

## Layout

```
Logbook/
├── Logbook.md               # MOC: indice + vista embed del .base
├── Logbook.base              # Definisce le viste (tabelle, gallerie, summaries)
├── _templates/
│   ├── Dive_Template_Rec.md  # Dive ricreativa (no sezione Tec)
│   └── Dive_Template_Tec.md  # Dive tecnica (include Piano deco + Soste effettive)
└── Dives/
    ├── YYYY-MM-DD_Sito.md          # 1 dive nella giornata
    ├── YYYY-MM-DD_Sito_1.md        # più dive nella giornata
    └── YYYY-MM-DD_Sito_2.md
```

## Convenzioni di naming

- File: `YYYY-MM-DD_Sito.md`, **underscore al posto degli spazi** negli
  spazi dei nomi.
- Più dive nella stessa giornata: suffisso progressivo `_1`, `_2`, ...
- `dive_number`: progressivo reale di carriera (allinealo al tuo libretto
  cartaceo se ne tieni uno).

## Filosofia di compilazione

Il frontmatter è pensato per essere compilato in **due fasi**:

**In barca dal cellulare** — i dati raw che si raccolgono lì:
- `date`, `site`, `buddy` (solo se buddy ricorrente, altrimenti vuoto),
  `guided` (true se segui una guida), `dive_type`, `entry`
- `time_in`, `time_out`, `max_depth`
- `back_mix`, `back_start`, `back_end`, `tank_volume`, `tank_type`,
  `tank_configuration`
- `visibility`, `current`, `sea`, `weather`, `temp_surface`, `temp_bottom`
- 2-3 righe in `## Note generali`, eventuali `## Animali e note`

**Post-dive a casa** — consolidamento col computer scaricato:
- `avg_depth`, `total_time`
- Pesata (`weight_*`), undersuit, fins, gloves
- Sezione `## Tec` (piano deco + soste effettive, **solo per dive tec** —
  usa il template `Dive_Template_Tec.md`)
- `## Drill`, `## Note attrezzatura`, `## Lezioni apprese`
- `rmv` e altri derivati: calcolali a parte (script/foglio) e riportali nel
  campo, non serve una formula live nel frontmatter

## Aggiungere una nuova dive

1. **Crea il file** in `Dives/` copiando il template adatto:
   - `_templates/Dive_Template_Rec.md` per dive ricreative
   - `_templates/Dive_Template_Tec.md` per dive tec con deco (Piano deco +
     Soste effettive nel body)
2. **Compila il frontmatter** secondo la filosofia sopra. Campi minimi per
   comparire nelle viste: `type: dive_log`, `date`, `dive_number`, `site`,
   `max_depth`, `total_time`.
3. **Wikilink in stringhe**: se `site` punta a una nota (es. una scheda del
   sito), va tra virgolette: `site: "[[Sito|Nome]]"` (virgolette
   obbligatorie, altrimenti YAML rompe). Altrimenti va bene testo semplice:
   `site: Secca Esempio`.
4. **Numerici senza virgolette e senza unità**: `max_depth: 17.7` ✓,
   `max_depth: "17.7"` ✗ (quotato → trattato come stringa, summaries e
   formule non funzionano), `max_depth: 17.7 m` ✗.
5. **Verifica** che la nuova dive compaia nelle viste del `Logbook.base`.

> [!warning] snake_case obbligatorio
> I nomi proprietà nel frontmatter usano `snake_case` (`max_depth`, non
> `Max Depth`). Il `.base` referenzia per quel nome esatto.

> [!warning] Niente struct nested nel frontmatter
> La Properties UI di Obsidian gestisce male oggetti annidati e liste di
> oggetti. Tenere il frontmatter **flat**: scalari (string, number, boolean)
> o liste di stringhe. Per dati strutturati (drill praticati, piano deco,
> gas log) usa sezioni body in markdown, come già fanno i template.

## Le viste del `Logbook.base`

| Vista | Per cosa |
|---|---|
| **Tutte le dive** | overview cronologica, buddy/guided, max depth, count, BT cumulato |
| **Per sito** | groupBy sito, statistiche per spot |
| **Condizioni** | meteo, mare, visibilità, temperature |
| **Configurazione e pesata** | muta/sottomuta/zavorra per analizzare la pesata |
| **Gas e consumi** | back mix + aria usata (`back_start - back_end`) |
| **Riassunto per tipo** | groupBy `dive_type`: count, BT totale (Sum), run time medio (Avg), avg depth medio, max depth massima |
| **Galleria** | cards view con nome file + sito + max depth |

In Obsidian: click sul nome della vista sopra la tabella per cambiare. Sort
cliccando sull'header colonna.

## Filtri ad hoc

Filtro globale: `type == "dive_log"`. Per filtri rapidi (es. profondità >
20m) usa la UI di Obsidian sopra la tabella, oppure aggiungi una vista nel
`.base`:

```yaml
- type: table
  name: "Profonde (>20m)"
  filters:
    and:
      - 'max_depth > 20'
  order:
    - dive_number
    - date
    - site
    - max_depth
```

## Aggiungere un campo nuovo

1. Aggiungilo al frontmatter delle dive **e** a entrambi i template
   (`Dive_Template_Rec.md` + `Dive_Template_Tec.md`).
2. Aggiungilo in `properties:` del `Logbook.base` con un `displayName`.
3. Aggiungilo al `order:` delle viste dove vuoi vederlo.
4. (Opzionale) `summaries:` (Sum / Average / Max / Filled).

## Formule personalizzate

In `Logbook.base` sezione `formulas:`. Esempi attivi:

```yaml
formulas:
  max_depth_label: 'if(max_depth, max_depth + " m", "")'
  air_used:        'if(back_start && back_end, back_start - back_end, "")'
  runtime_avg:     total_time   # alias per usare Sum + Average sullo stesso campo in una vista
```

Proteggi sempre con `if()` per gestire valori nulli. Le formule referenziano
i campi del frontmatter per nome esatto. Nelle viste si usano come
`formula.air_used`. **Trucco**: per applicare due aggregate diversi (es. Sum
e Average) sullo stesso campo nella stessa vista, crea una formula alias
(es. `runtime_avg: total_time`) e usala come secondo summary — `summaries`
non accetta due chiavi uguali.

## Troubleshooting

- **La dive non compare**: controlla `type: dive_log` nel frontmatter
  (case-sensitive) e che il file sia in `Dives/`.
- **Errore YAML**: wikilink fra virgolette doppie (`site: "[[...|...]]"`).
  Senza virgolette YAML rompe.
- **Summaries vuote**: la colonna deve essere numerica.
  `total_time: 60` ✓, `total_time: "60 min"` ✗.
- **GroupBy con duplicati apparenti**: stringhe diverse (case, spazi)
  creano gruppi separati. Standardizzare i nomi sito.
- **Obsidian Properties UI lenta / bug**: vedi warning sopra — niente
  struct nested.

## Note

Questo strumento non calcola piani di decompressione, non sostituisce un
computer subacqueo e non fa alcun controllo di sicurezza sui dati inseriti:
è solo un registro strutturato. Usalo come diario, non come strumento di
pianificazione immersioni.

## Licenza

[CC0 1.0 Universal](LICENSE) — pubblico dominio, nessuna attribuzione
richiesta. Usa, modifica e ridistribuisci liberamente.
