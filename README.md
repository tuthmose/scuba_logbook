# Logbook — registro immersioni in markdown

Ogni immersione è un file di testo: in testa il frontmatter YAML con i dati
strutturati (profondità, gas, pesata, condizioni), sotto lo spazio per
raccontarla. Un file `.base` legge tutti i file della cartella e ne tira
fuori tabelle ordinabili e statistiche aggregate, senza fogli di calcolo
appesi da qualche parte. Ricorda: __Excel e' il male__.

## Perché markdown

Perché è testo, e lo puoi modificare come vuoi e ne mantieni il controllo.
E lo puoi dare in pasto ad un assistente AI, che sono il male pure loro ma tant'è.
Ad esempio puoi creare uno script che pesca i numeri dall'export di Subsurface. Nessun formato
proprietario, nessun database che fra cinque anni non si apre più, nessuna
app da cui esportare pregando che l'export sia decente.

Perché? Perché immersioni diverse -> equipaggiamento diverso e vatti a ricordare 
la pesata.
Il vantaggio pratico si vede sui valori derivati. RMV, pesata, consumi non
sono numeri congelati dentro un'applicazione: sono campi che riscrivi. Se ti
accorgi che il volume bombola impostato sul computer era sbagliato, o che la
pesata di quel giorno andava letta diversamente, correggi il campo e tutte
le viste si riallineano da sole. Lo stesso vale per i confronti a posteriori
— quanto consumo davvero con la 15 L rispetto alla 12, come cambia la
zavorra fra umida e stagna — che sono la ragione per cui uno tiene un
logbook invece di fidarsi della memoria.

## Serve Obsidian?

No, ma aiuta parecchio.

I file sono markdown normale: si aprono e si modificano con qualsiasi
editor, incluso quello del telefono, e si versionano con git.

Con [Obsidian](https://obsidian.md) (gratuito) ci guadagni le tabelle live,
le statistiche aggregate e i collegamenti fra note — cioè il motivo per cui
il frontmatter è strutturato così. Serve il plugin core **Bases** attivo
(`Impostazioni → Plugin core → Bases`, incluso dalla v1.9 in poi).

## Setup

1. Clona o scarica questa cartella.
2. In Obsidian: `Apri cartella come vault` → seleziona `Logbook/`. Se hai già
   un vault tuo, copiaci dentro l'intera cartella.
3. Apri `Logbook.md`: trovi la tabella generata da `Logbook.base`, con dentro
   l'immersione di esempio.
4. Quando sei pronto, cancella l'esempio e comincia con le tue.

## Layout

```
Logbook/
├── Logbook.md                # Indice + vista embed del .base
├── Logbook.base              # Definisce le viste (tabelle, gallerie, summaries)
├── _templates/
│   ├── Dive_Template_Rec.md  # Ricreativa (senza sezione Tec)
│   └── Dive_Template_Tec.md  # Tecnica (con Piano deco + Soste effettive)
└── Dives/
    ├── YYYY-MM-DD_Sito.md    # una sola immersione in giornata
    ├── YYYY-MM-DD_Sito_1.md  # più immersioni nella stessa giornata
    └── YYYY-MM-DD_Sito_2.md
```

Nomi file `YYYY-MM-DD_Sito.md`, underscore al posto degli spazi, suffisso
progressivo se in giornata ne fai più di una. `dive_number` è il progressivo
di carriera: se tieni un libretto cartaceo, tienili allineati.

## Aggiungere un'immersione

Copia il template adatto dentro `Dives/` — `Dive_Template_Rec.md` per le
ricreative, `Dive_Template_Tec.md` se c'è deco da annotare — e compila.

I campi vuoti non rompono niente: le viste mostrano
quello che c'è. Può anche essere usata come promemoria / programma se fai una
sessione di addestramento, compilandola in parte in anticipo.
Perché l'immersione compaia nelle viste servono almeno `type: dive_log`,
`date`, `dive_number`, `site`, `max_depth`, `total_time`.

## Regole del frontmatter

- **Numeri nudi**: senza unità di misura; ed in ogni caso si usa solo il sistema internazionale.
- **`snake_case`**: `max_depth`, non `Max Depth`. Il `.base` cerca il nome
  esatto.
- **Wikilink fra virgolette**: se `site` punta a una nota,
  `site: "[[Sito|Nome]]"`. Senza virgolette YAML si arrabbia. Testo semplice
  (`site: Secca Esempio`) va benissimo lo stesso.
- **Niente strutture annidate**: solo scalari e liste di stringhe. La
  Properties UI di Obsidian gestisce male oggetti dentro oggetti. Per i dati
  strutturati (piano deco, drill, gas log) ci sono le sezioni nel body, come
  già fanno i template.

## Le viste del `Logbook.base`

| Vista | Per cosa |
|---|---|
| **Tutte le dive** | overview cronologica, profondità, conteggio, bottom time cumulato |
| **Per sito** | raggruppate per spot, con statistiche per posto |
| **Condizioni** | meteo, mare, visibilità, temperature |
| **Configurazione e pesata** | muta, sottomuta e zavorra, per capire come ti stai pesando |
| **Gas e consumi** | mix, pressioni, aria usata (`back_start - back_end`), RMV |
| **Riassunto per tipo** | raggruppate per `dive_type`: conteggio, bottom time totale, medie |
| **Galleria** | vista a schede |

Si cambia vista dal nome sopra la tabella, si ordina dall'intestazione di
colonna.

## Con Subsurface e affini

Subsurface (o l'app del tuo computer) resta il posto giusto per scaricare e
guardare il profilo: campionamento ogni pochi secondi, grafici, ricalcolo
deco. Quello che quegli strumenti fanno male è la parte che conta dopo — la
narrazione, i drill provati, le note sull'attrezzatura, le cose da ricordarsi
la prossima volta.

I due convivono senza attrito. Dal profilo prendi i numeri (`avg_depth`,
`total_time`, temperature) e li riporti qui, a mano o con uno script:
Subsurface esporta XML, CSV e UDDF, tutti formati leggibili senza penare, e
convertirli in frontmatter è esattamente il genere di compito noioso che si
delega volentieri a un assistente AI.

## Personalizzare

**Aggiungere un campo**: mettilo nel frontmatter e in entrambi i template,
poi in `properties:` del `.base` con un `displayName`, poi nel `order:` delle
viste dove lo vuoi vedere. Se ha senso sommarlo o mediarlo, aggiungilo anche
in `summaries:`.

**Filtrare al volo**: il filtro globale è `type == "dive_log"`. Per il resto
usa la UI sopra la tabella, o scrivi una vista nuova:

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

**Formule**: stanno nella sezione `formulas:` del `.base` e si usano nelle
viste come `formula.nome`.

```yaml
formulas:
  max_depth_label: 'if(max_depth, max_depth + " m", "")'
  air_used:        'if(back_start && back_end, back_start - back_end, "")'
  runtime_avg:     total_time   # alias, vedi sotto
```

Proteggile sempre con `if()`, altrimenti un campo vuoto sporca la colonna.
Il trucco dell'alias serve quando vuoi due aggregati diversi (Sum e Average)
sullo stesso campo nella stessa vista: `summaries` non accetta due chiavi
uguali, quindi ne crei una copia con un altro nome.

## Quando qualcosa non torna

- **L'immersione non compare**: manca `type: dive_log` (case-sensitive) o il
  file non è in `Dives/`.
- **Errore YAML**: quasi sempre un wikilink senza virgolette.
- **Colonna senza totali**: c'è dentro una stringa. `total_time: 60` ✓,
  `total_time: "60 min"` ✗.
- **Lo stesso sito appare due volte nei raggruppamenti**: due scritture
  diverse (maiuscole, spazi). Standardizza i nomi.

## Nota

Questo è un registro, __non uno strumento di pianificazione__. Non calcola deco,
non sostituisce il computer subacqueo e non controlla in alcun modo la
sensatezza di quello che ci scrivi dentro.

## Licenza

[CC0 1.0 Universal](LICENSE) — pubblico dominio, nessuna attribuzione
richiesta. Usa, modifica e ridistribuisci liberamente.
