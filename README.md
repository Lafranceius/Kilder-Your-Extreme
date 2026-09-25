# Kilder til Your Extreme

Datagrunnlag og geografisk studie bak [Second Signal](https://kongsberg.bighiro6.com).

Kildene ble undersøkt 24. september 2026. Data og resultater ble publisert 25. september 2026.

Her finner du dataene som brukes på nettstedet, kildeuttrekkene og beregningene bak studien.

## Finn frem

- [Hele den geografiske studien](kartlegging-40km.md) (også gjengitt nedenfor).
- [Kilderegister og vurdering av stasjonsgrunnlaget](bensinstasjoner-primarkilder.md).
- [Oversiktskart](dekningskart-40km.png) · [SVG](dekningskart-40km.svg).
- [Foreslåtte stasjoner som CSV](data/foreslatte-stasjoner.csv) · [GeoJSON](foreslatte-punkter.geojson).

## Datasett

| Filer | Innhold |
|---|---|
| [`data/planner.json`](data/planner.json) | Befolkning, kandidatstasjoner og sammendrag som den interaktive planleggeren laster. |
| [`data/nordic-map.json`](data/nordic-map.json) | Kartgrenser brukt på nettstedet, bearbeidet fra Natural Earth. |
| [`data/ssb-population-1km-2025.json`](data/ssb-population-1km-2025.json) | SSBs publiserte befolkede kilometerruter for 2025. |
| [`data/ssb-raw/`](data/ssb-raw/) | Lagrede XML-sider fra SSBs geodatatjeneste. |
| [`data/all-stations.json`](data/all-stations.json) | 1 098 kandidatpunkter etter filtrering og sammenslåing. |
| [`data/circlek-stations.json`](data/circlek-stations.json), [`data/yx-stations.json`](data/yx-stations.json), [`data/bunkeroil-stations.json`](data/bunkeroil-stations.json), [`data/unox-raw.json`](data/unox-raw.json) | Uttrekk fra operatørenes publiserte stasjonsdata. |
| [`data/verified-extra-stations.json`](data/verified-extra-stations.json) | Ekstra kandidater kontrollert mot primærkilder. |
| [`data/selected-stations.json`](data/selected-stations.json), [`data/foreslatte-stasjoner.csv`](data/foreslatte-stasjoner.csv) | Det beregnede forslaget på 147 stasjoner. |
| [`data/summary.json`](data/summary.json) | Nøkkeltall fra den geografiske studien. |
| [`data/unresolved-cells.json`](data/unresolved-cells.json), [`data/gap-groups-preliminary.json`](data/gap-groups-preliminary.json) | Uavklarte ruter og foreløpig geografisk gruppering. |
| [`data/analysis.npz`](data/analysis.npz) | Lagrede NumPy-arrayer fra analysen. |
| [`data/natural-earth-50m.json`](data/natural-earth-50m.json) | Kartgrunnlag fra Natural Earth før regional bearbeiding. |

## Kilder

Befolkningsdata kommer fra [Statistisk sentralbyrå](https://www.ssb.no/natur-og-miljo/areal/artikler/kart-og-geodata-fra-ssb), stasjonsdata fra operatørenes egne publiseringer, og kartgrenser fra [Natural Earth](https://www.naturalearthdata.com/). Detaljerte kildelenker og avgrensninger finnes i [kilderegisteret](bensinstasjoner-primarkilder.md) og datafilenes kildefelt. Materialet har flere opphav; dette repositoriet gir ingen ny, felles lisens til tredjepartsdata.

## Hvor godt samsvarer nettstedet med studien?

Nettstedet bruker de samme befolkningsdataene og kandidatstasjonene som studien. Ved **40 km radius og 147 punkter** beregner den interaktive modellen **99,872 %** befolkningsdekning, mot studiens **99,877 %**. Forskjellen er 281 personer i rutenettet, eller omtrent 0,005 prosentpoeng. Ved denne innstillingen gir nettstedet dermed et svært likt bilde av den geografiske dekningen.

Begge beregningene trekker fra 710 meter fra radiusen for å ta høyde for at folk kan bo hvor som helst i en kilometerrute. Ved 40 km radius må rutesenteret derfor ligge innenfor 39,29 km fra stasjonen.

Metodene skiller seg på to punkter:

- **Avstander:** Nettstedet regner jorden som en kule. Studien bruker WGS84, som tar hensyn til at jorden er litt flattrykt. Dette kan påvirke hvilke ruter som regnes med nær dekningsgrensen.
- **Valg av stasjoner:** Nettstedet legger til den stasjonen som når flest nye personer for hvert trinn. Studien gjør også en etterkontroll og fjerner stasjoner som er blitt overflødige. Derfor kan stasjonsutvalget og antallet punkter bli forskjellig.

Sammenligningen gjelder den publiserte modellen ved 40 km. Når radiusen eller antallet punkter endres, viser nettstedet en ny beregning for den valgte innstillingen.

---

## Kartlegging av 40 km dekning fra drivstoffpunkter i Norge

Et utvalg på **147 drivstoffpunkter** dekker geografisk **99,877 % av befolkningen i SSBs publiserte kilometerruter** med en antatt radius på 40 km og en rutemargin på 710 meter. Beregningen omfatter Fastlands-Norge med øyer.

| Resultat | Antall |
|---|---:|
| Kandidatpunkter etter sammenslåing av plasseringer innen 150 meter | 1 098 |
| Befolkede kilometerruter i SSBs 2025-lag | 55 268 |
| Personer i datasettet | 5 585 868 |
| Personer innen 40 km fra en kandidat, målt til rutesenter | 5 579 223 |
| Ruter uten treff innen 40 km, målt til rutesenter | 267 |
| Personer dekket med 710 meter rutemargin | 5 579 014 |
| Ruter som ikke dekkes med rutemarginen | 292 |
| Personer i disse rutene | 6 854 |

Kandidatpunktene fordeler seg slik etter sammenslåing:

| Kjede | Punkter |
|---|---:|
| Circle K | 443 |
| Uno-X | 309 |
| YX | 270 |
| Bunker Oil | 74 |
| Joker | 1 |
| St1 | 1 |
| **Totalt** | **1 098** |

Tallene er beregnet fra [SSBs befolkningsrutenett for 2025](https://data.norge.no/nb/datasets/1f11afd2-16c7-3f7e-abca-6feb02ca024d/befolkning-pa-rutenett-1000-m-2025) og de kartlagte stasjonene. Dekningsandelen gjelder befolkningen i dette datasettet.

### Forutsetninger og begrensninger

Radiusen på 40 km er en antakelse om geografisk rekkevidde. Radioutbredelse, ballongdrift, strøm, kapasitet, forbindelser mellom stasjoner og tilgang til plasseringene er ikke undersøkt. Utvalget på 147 punkter er én beregnet løsning; det er ikke dokumentert at dette er det laveste mulige antallet, eller at dekningen opprettholdes ved bortfall av en ballong. Svalbard inngår ikke.

## Hvordan punktene er valgt

Studien beregner luftlinjeavstander langs jordoverflaten med WGS84. En rute regnes som dekket når rutesenteret ligger høyst 39,29 km fra en kandidat. Rutemarginen tar høyde for avstanden til rutens hjørner; usikkerhet i stasjonskoordinater og ballongdrift inngår ikke.

Stasjonene velges én om gangen etter hvor mange nye personer de dekker. Når alle rutene som kan nås av kandidatene er dekket, gjennomgås utvalget baklengs. En stasjon fjernes dersom de øvrige stasjonene dekker alle rutene dens.

SSB-dataene ble hentet i grupper på 1 000 ruter og kontrollert for antall og unike rute-ID-er. Kildeuttrekk og resultater ligger i dette repositoriet; programmene for innhenting og analyse ligger i nettstedsprosjektet.

## Stasjonsgrunnlag og begrensninger

Stasjonsgrunnlaget kommer fra [Circle K](https://www.circlek.no/station-search), [YX](https://www.yx.no/stasjon), [Uno-X](https://unox.no/finn-uno-x/), [Bunker Oil](https://bunkeroil.no/en/map-petrol-stations), samt [Joker Træna](https://joker.no/finn-butikk/joker-trana) og [St1 Skjervøy](https://st1.no/stasjon/skjervy). Ladestasjoner og bilvask uten registrert drivstoff er filtrert ut. Bunker Oil inkluderer marine utsalg, og Træna-punktet er en butikk med drivstoff. Resultatet gjelder derfor **drivstoffpunkter**, ikke utelukkende bemannede bensinstasjoner med biladkomst.

YX: 275 oppføringer fra API-et brukt av operatørens eget kart, alle samsvarende med nettstedets sitemap; 274 med drivstoff. Uno-X: primærkategori bensinstasjon eller truckstopp i operatørens PinMeTo-publisering; dette er kategoribasert dokumentasjon, ikke individuell produktkontroll. Circle K: 445 av 460 publiserte punkter har flytende drivstoff. Bunker Oil: 76 kartpunkter; operatøren omtaler flere, så kartet er ikke komplett. Kildene er bevart i `data/`.

Registeret mangler fullstendige nett for Esso og St1 samt flere uavhengige utsalg. Oransje kryss i [oversiktskartet](dekningskart-40km.png) viser derfor ruter som trenger videre kontroll. Flere kan bli dekket når manglende stasjoner legges til.

## Områder for videre kontroll

- **Røst/Værøy:** rutenettet på Røst ligger ca. 62–65 km fra Reine i dette uttrekket. Værøy har dokumentert drivstoffinfrastruktur, men eksakt kandidatkoordinat er ikke lagt inn. Det må testes mot Røst før man krever eget Røst-punkt. [Værøy kommunes brosjyre](https://varoy.kommune.no/_f/p1/i991aeac6-4edd-44fb-9461-39bf689098a7/touristbrochure-2024-english.pdf).
- **Sørøya/Hasvik–Breivikbotn:** flere bebodde ruter har over 40 km til kartlagte stasjoner utenfor øya. Lokale og andre kjeders utsalg må innhentes før dette kalles et reelt hull.
- **Honningsvåg/Magerøya:** egne lokale kandidatpunkter må verifiseres og stedfestes; Havøysund/Kjøllefjord dekker ikke automatisk alle ruter her.
- **Steigen og enkelte fjordområder i Nordland:** manglende kjeder kan forklare udekkede ruter; lokal kontroll kreves.
- **Øvre Pasvik og indre Finnmark:** de ytterste befolkede rutene må avstandstestes mot lokale utsalg, ikke bare Hesseng, Alta og Kautokeino.

Den fullstendige listen over uavklarte ruter, med nærmeste kjente kandidat og avstand, ligger i [data/unresolved-cells.json](data/unresolved-cells.json).
