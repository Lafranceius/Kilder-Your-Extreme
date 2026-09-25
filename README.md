#Kilder til Your Extreme

Datagrunnlag og geografisk studie bak [Second Signal] sin nettside: 
https://kongsberg.bighiro6.com

Øyeblikksbilde publisert 25. september 2026; kildene ble undersøkt 24. september 2026.

Dette repositoriet inneholder forskningsnotater, kildeuttrekk og data brukt i nettstedet og beregningene bak det. Nettsidens programkode og drift er ikke inkludert.

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

## Kilder og tolkning

Befolkningsdata kommer fra [Statistisk sentralbyrå](https://www.ssb.no/natur-og-miljo/areal/artikler/kart-og-geodata-fra-ssb), stasjonsdata fra operatørenes egne publiseringer, og kartgrenser fra [Natural Earth](https://www.naturalearthdata.com/). Detaljerte kildelenker og avgrensninger finnes i [kilderegisteret](bensinstasjoner-primarkilder.md) og datafilenes kildefelt. Materialet har flere opphav; dette repositoriet gir ingen ny, felles lisens til tredjepartsdata.

Nettstedets interaktive beregning bruker avstander på en kuleflate og en rutemargin på 710 meter. Studien nedenfor bruker WGS84-geodesi og etterfølgende fjerning av overflødige stasjoner. Derfor kan den interaktive planleggeren gi andre resultater enn studiens referansetall.

Dette er en geografisk mulighetsstudie. Den dokumenterer ikke radiodekning, operativ beredskap eller et bevist minimum av stasjoner. Svalbard inngår ikke.

---

# Kartlegging av 40 km dekning fra drivstoffpunkter i Norge

**Drivstoffpunkter kan geografisk dekke svært mye av bosetningen, men det er ikke dokumentert at alle bebodde områder i Norge har en bensinstasjon innen 40 km.** Beregningen nedenfor er en landsdekkende screening av Fastlands-Norge med øyer. Den er ikke en ferdig beredskapsplan eller et fullstendig stasjonsregister.

- 1098 ulike kandidatpunkter etter sammenfallende posisjoner innen 150 meter er slått sammen. Kjedetall etter sammenslåing: {'Circle K': 443, 'Bunker Oil': 74, 'Joker': 1, 'St1': 1, 'YX': 270, 'Uno-X': 309}.
- Alle 55268 publiserte befolkede 1 × 1 km-ruter i SSBs 2025-lag er hentet, med 5,585,868 personer i datasettet.
- Målt til rutesenter: 5,579,223 personer ligger i ruter med kjent stasjon innen 40 km; 267 ruter har ikke slikt treff.
- Med 710 meter margin for plasseringen inne i kilometerruten: 5,579,014 personer, eller **99.877 % av datasettets befolkning**, i ruter med dekningsmargin. 292 ruter med 6,854 personer er uavklart eller ved grensen.
- Et beregnet utvalg på **147 drivstoffpunkter** dekker alle rutene som kan dekkes med denne marginen av kandidatene. Dette er ett forslag, ikke et bevist minsteantall, og ikke et bevis på at akkurat disse punktene må benyttes.

Tallene er egne beregninger. [SSBs datasettbeskrivelse](https://data.norge.no/nb/datasets/1f11afd2-16c7-3f7e-abca-6feb02ca024d/befolkning-pa-rutenett-1000-m-2025) og [SSBs geodataportal](https://www.ssb.no/natur-og-miljo/areal/artikler/kart-og-geodata-fra-ssb) beskriver datagrunnlaget. Prosentsatsen gjelder befolkningen i de publiserte rutene; den er ikke en målt andel av alle personer som oppholder seg i Norge i dag.

## Filer

- `dekningskart-40km.png` og `.svg`: nasjonalt oversiktskart. Oransje kryss er uavklarte ruter, ikke bekreftet fravær av bensinstasjon.
- `data/foreslatte-stasjoner.csv`: hele forslaget med navn, koordinater, adresse og kilde.
- `foreslatte-punkter.geojson`: samme punkter til GIS.
- `data/all-stations.json`: alle kandidatene og om de er valgt.
- `data/unresolved-cells.json`: alle ruter som trenger videre kontroll, med nærmeste kjente kandidat og avstand.
- `bensinstasjoner-primarkilder.md`: verifiserte lokale stasjoner, kildeoversikt og Svalbard-avgrensing.

## Hvordan punktene er valgt

Avstander beregnes geodetisk på WGS84, ikke som kjørelengde. For hver rute undersøkes nærmeste kandidater. En stasjon dekker en hel kilometerrute konservativt dersom avstanden til rutesenter er høyst 39,29 km: resterende 710 meter tar høyde for avstanden til hjørnene. Marginen er for rutegeometrien, ikke for feil i operatørens koordinater eller ballongdrift.

Utvalgsalgoritmen velger gjentatte ganger stasjonen som dekker flest hittil udekkede personer, fortsetter til alle dekkbare ruter er dekket, og fjerner overflødige stasjoner i revers rekkefølge. Det finnes normalt flere alternative løsninger. Dette beregnede utvalget skal ikke tolkes som et globalt optimum.

Datainnhenting: SSB-laget ble hentet i sider på 1000 med kontroll av antall og unike rute-ID-er. Beregningene ble utført fra de lagrede kildene. Dette repositoriet inneholder datagrunnlaget og resultatene; innhentings- og analyseprogrammene ligger i nettstedsprosjektet.

## Stasjonsgrunnlag og begrensninger

Bruker kjedenes egne data: [Circle K](https://www.circlek.no/station-search), [YX](https://www.yx.no/stasjon), [Uno-X](https://unox.no/finn-uno-x/), [Bunker Oil](https://bunkeroil.no/en/map-petrol-stations), samt [Joker Træna](https://joker.no/finn-butikk/joker-trana) og [St1 Skjervøy](https://st1.no/stasjon/skjervy). Ladestasjoner og bilvask uten registrert drivstoff er filtrert ut. Bunker Oil inkluderer marine utsalg, og Træna-punktet er en butikk med drivstoff. Resultatet gjelder derfor **drivstoffpunkter**, ikke utelukkende bemannede bensinstasjoner med biladkomst.

YX: 275 oppføringer fra API-et brukt av operatørens eget kart, alle samsvarende med nettstedets sitemap; 274 med drivstoff. Uno-X: primærkategori bensinstasjon eller truckstopp i operatørens PinMeTo-publisering; dette er kategoribasert dokumentasjon, ikke individuell produktkontroll. Circle K: 445 av 460 publiserte punkter har flytende drivstoff. Bunker Oil: 76 kartpunkter; operatøren omtaler flere, så kartet er ikke komplett. Kildene er bevart i `data/`.

Fullstendige Esso- og St1-nett samt alle uavhengige utsalg inngår ikke. Derfor vil flere av de oransje områdene kunne dekkes når nye stasjoner legges til. Det er ikke faglig grunnlag for å kalle disse områdene «uten bensinstasjon innen 40 km».

## Områder som må avklares før man hevder full dekning

- **Røst/Værøy:** rutenettet på Røst ligger ca. 62–65 km fra Reine i dette uttrekket. Værøy har dokumentert drivstoffinfrastruktur, men eksakt kandidatkoordinat er ikke lagt inn. Det må testes mot Røst før man krever eget Røst-punkt. [Værøy kommunes brosjyre](https://varoy.kommune.no/_f/p1/i991aeac6-4edd-44fb-9461-39bf689098a7/touristbrochure-2024-english.pdf).
- **Sørøya/Hasvik–Breivikbotn:** flere bebodde ruter har over 40 km til kartlagte stasjoner utenfor øya. Lokale og andre kjeders utsalg må innhentes før dette kalles et reelt hull.
- **Honningsvåg/Magerøya:** egne lokale kandidatpunkter må verifiseres og stedfestes; Havøysund/Kjøllefjord dekker ikke automatisk alle ruter her.
- **Steigen og enkelte fjordområder i Nordland:** manglende kjeder kan forklare udekkede ruter; lokal kontroll kreves.
- **Øvre Pasvik og indre Finnmark:** de ytterste befolkede rutene må avstandstestes mot lokale utsalg, ikke bare Hesseng, Alta og Kautokeino.

Dette er områder for videre kontroll, ikke en liste over dokumentert fravær av drivstoffinfrastruktur. Alle resterende ruter ligger i `data/unresolved-cells.json`.
