---
type: dive_log
date: 2025-01-03
dive_number: 3
site: Relitto Esempio
buddy: Nome Buddy
guided: false
dive_type: tec
entry: boat
navigation_lead: true
time_in: 10:05
time_out: 10:50
total_time: 45
max_depth: 40.2
avg_depth: 22.9
temp_surface: 21
temp_bottom: 15
visibility: 15
current: Moderate
sea: Slight
weather: Cloudy
wind: Moderate
weather_notes: Onda corta al rientro, ingresso e uscita dalla poppa
suit: dry
undersuit: 200g
gloves: true
boots: Rock boots
fins: Jet
negative_fins: true
weight_keel: 0
weight_belt: 0
weight_pocket: 4
weight_trim: 0
weight_total: 4
back_mix: aria
back_start: 200
back_end: 130
tank_volume: 12
tank_type: steel
tank_configuration: bibo
rmv: 15.6
rmv_estimated: true
computer: Shearwater Perdix
gf_set: 70/80
gf_end: 74
compass: true
dpv: false
pallone: true
spool_count: 2
wet_notes: []
tags:
  - scuba
  - logbook
---

# Dive

## Note generali

Dive di esempio: **addestramento su skill tecniche** con deco pianificata e un
gas switch. È la variante che usa il template `Dive_Template_Tec` e quindi la
sezione `## Tec`, con piano deco e soste effettive messi uno sotto l'altro —
il punto della sezione è proprio poter confrontare i due.

Configurazione bibo 2×12 L acciaio ad aria, stage ean50 da 7 L per la deco.
Piano: 20 minuti di fondo sul relitto a 40 m, risalita a 21 m, switch su
ean50, deco fino in superficie. Lo switch si esegue con la sequenza **NOTOX**,
riportata per esteso in `## Drill`.

Eseguito: fondo rispettato, switch fatto con un minuto di ritardo perché la
corrente ha allungato il traverso di rientro alla cima. Un minuto in più alla
sosta dei 6 m, per lo stesso motivo.

## Rilevamenti

- Cima di discesa sulla prua, 38 m alla base
- Asse del relitto circa 040°/220°, poppa più profonda della prua
- Traverso prua → cima di risalita circa 25 m con rotta 220°, da fare sul
  fondo e non a mezz'acqua se c'è corrente

## Tec

### Piano deco

| stop (m) | gas | deco acc (min) | run time (min) | stop length (min) | note |
|----------|-----|----------------|----------------|-------------------|------|
| 40 | aria | — | 20 | 20 | fondo |
| 21 | ean50 | 16 | 24 | — | gas switch |
| 12 | ean50 | 14 | 26 | 1 | |
| 9 | ean50 | 12 | 29 | 2 | |
| 6 | ean50 | 9 | 35 | 5 | |
| 3 | ean50 | 0 | 44 | 8 | risalita finale lenta |

### Soste effettive

| stop (m) | gas | deco acc (min) | run time (min) | stop length (min) | note |
|----------|-----|----------------|----------------|-------------------|------|
| 40.2 | aria | — | 20 | 20 | fondo rispettato |
| 21 | ean50 | 17 | 25 | — | switch con 1' di ritardo, corrente sul traverso |
| 12 | ean50 | 15 | 27 | 1 | |
| 9 | ean50 | 12 | 30 | 2 | |
| 6 | ean50 | 9 | 36 | 6 | 1' in più, corrente in aumento |
| 3 | ean50 | 0 | 45 | 8 | |

## Drill

- s_drill — 4/5, condivisione gas sulla long hose a inizio immersione, svolta
  in acqua durante la discesa; passaggio pulito, la frusta si è srotolata
  senza impigliarsi nella torcia
- v_drill — 3/5, manipolazione rubinetteria del bibo con guanti secchi: la
  destra è a posto, la sinistra richiede ancora due tentativi per agganciare
  il volantino
- notox — 4/5, procedura di gas switch a due. Eseguita per intero, solo in
  ritardo sul run time perché la corrente ha allungato il traverso

> [!info] NOTOX — la sequenza del gas switch
> - **N** — *Note your name and the maximum depth on the cylinder labels*:
>   leggi sull'etichetta della bombola il nome del gas e la MOD
> - **O** — *Observe your actual depth and compare to the MOD*: confronta la
>   profondità a cui sei con la MOD appena letta
> - **T** — *Turn on the valve, check the cylinder pressure*: apri il
>   rubinetto dello stage e controlla la pressione
> - **O** — *Orient the second stage by pulling it from the retaining bands*:
>   libera il secondo stadio dagli elastici e orientalo
> - **X** — *eXamine your team mates*: segui la frusta dalla loro bocca fino
>   alla bombola, e verifica che stiano respirando dallo stage giusto
>
> Gli ultimi due passi sono quelli che si saltano quando si va di fretta, ed
> è esattamente il motivo per cui la procedura si fa in due.

## Animali e note

Gronghi in due punti dello scafo, un banco di castagnole sopra la prua.
Nulla di rilevante per la dive, annotato come riferimento per il sito.

## Note attrezzatura

**`rmv_estimated: true` — perché.** Su questa dive l'RMV è **ricostruito, non
misurato**: il computer non ha registrato il profilo campionato e il gas
switch spezza il calcolo in due. Il valore viene dai vincoli:

- gas consumato dal back gas: (200 − 130) bar × 12 L × 2 bombole = 1680 L
- tempo sul back gas: 45 min totali − 21 min sull'ean50 = 24 min
- profondità media della **sola** parte a back gas: circa 35 m → 4.5 ata
- RMV = 1680 / (24 × 4.5) ≈ **15.6 L/min**

Il numero è sensibile alla profondità media assunta per il segmento di
risalita: fra 33 e 37 m di media il risultato oscilla fra 15 e 16.5 L/min. Per
questo il campo `rmv_estimated` è a `true` e la colonna *RMV misurato* del
`.base` lascia la casella vuota, così le medie restano fatte di sole misure.

L'errore da non fare è dividere il consumo per i 45 minuti totali e usare la
profondità media dell'intera immersione: verrebbe circa 8 L/min, cioè un
numero che non descrive niente. Il tempo passato su un altro gas va tolto.

## Lezioni apprese

Il traverso prua → cima va fatto sul fondo, non a mezz'acqua: con corrente si
paga in tempo e il ritardo si propaga su tutta la deco.

Il V-drill sulla rubinetteria sinistra non è ancora automatico con i guanti
secchi. Da ripetere in acqua bassa prima della prossima dive con deco, non
sul fondo a 40 m.
