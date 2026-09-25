# Bensinstasjoner som kandidater for 40 km kommunikasjonsdekning

Undersøkt 24. september 2026. Dette er et kildenotat og et sett verifiserte kandidater, ikke dokumentasjon på fullstendig nasjonal dekning. Forutsetningen i casen er 40 km **luftlinjeradius** fra ballongens dekningssenter. Teknologiens egnethet er ikke vurdert.

## Hovedfunn

Bensinstasjoner finnes også i flere av stedene som lett kan bli antatt å være hull i et nasjonalt nett: Berlevåg, Kjøllefjord, Havøysund, Mehamn, Skjervøy og Værøy. Træna har en dagligvarebutikk som selv opplyser at den selger bensin og diesel. Kildene og posisjonene nedenfor gjør det mulig å prøve disse som kandidater i en GIS-analyse. De beviser ikke at alle bebodde områder ligger innenfor 40 km.

Det er særlig viktig å skille mellom **en vanlig bensinstasjon, et automatutsalg, butikk med drivstoff og et marint tankanlegg**. Et nettsted kan markedsføre alle disse som sitt stasjonsnett. Dette notatet beholder skillet slik at casen kan velge om alle typene er aktuelle.

## Nasjonale og regionale datapunkter hentet fra operatørene

| Datakilde | Faktisk uttrekk | Bruk og begrensning |
|---|---:|---|
| [Circle K stasjonssøk](https://www.circlek.no/station-search) | 460 stedspunkter, hvorav 445 har flytende drivstoff oppført | 6 er bilvask uten drivstoff og 9 er bare elbillading. Bruk `has_liquid_fuel == true` i analysen. Alle 460 var merket `Active`. Dette er Circle Ks eget nett, ikke alle norske stasjoner. |
| [Circle K stasjonsliste](https://www.circlek.no/stations) | Publisert lenkeliste | Kan kontrollere konkrete stasjonsnavn og finne stasjonssidene. Stasjonssidene oppgir adresse og kartlenke med koordinater. |
| [Bunker Oil stasjonskart](https://bunkeroil.no/en/map-petrol-stations) | 76 punkter fra operatørens innebygde kart | Inneholder også marine utsalg. Navn/produktbeskrivelse er bevart. Operatørens [beskrivelsesside](https://bunkeroil.no/om-bensinstasjoner) oppgir over 80 automatiserte stasjoner og nevner Mehamn, mens Mehamn ikke forekommer i dette kartuttrekket. Uttrekket må derfor ikke behandles som en sertifisert fullstendig liste. |
| [St1 stasjonssøk](https://st1.no/finn-stasjon) | Ingen nasjonal St1-fil produsert i dette delarbeidet | Offentlig operatørliste. St1 Skjervøy er hentet separat og verifisert. |

Uttrekkstallene er beregnet fra den publiserte kildens HTML/KML på undersøkelsesdatoen; de er ikke offisielle nasjonale statistikkverdier.

Filer produsert:

- `data/circlek-stations.json`: 460 punkter med kjede, navn, latitude/longitude (`lat`, `lon`), adresse, kommune, fylke, drivstoff, aktiv status, kildelenke og hentetdato.
- `data/bunkeroil-stations.json`: 76 punkter med navn, koordinater, produktbeskrivelse, kildelenke og hentetdato.
- `data/verified-extra-stations.json`: Joker Træna og St1 Skjervøy, med koordinater fra deres egen strukturerte nettsidedata.

Circle K-data lå i `application/json`-elementet med `data-drupal-selector="drupal-settings-json"`, under `ck_sim_search.station_results`. Hvert objekt har `/sites/{siteId}/location` med `lat` og `lng`. Feltet `/sites/{siteId}/fuels` ble brukt til å skille flytende drivstoff fra bare lading og bilvask. Dermed var det ikke nødvendig å laste hundrevis av enkeltsider.

Bunker Oils side har en [Google MyMaps-iframe](https://www.google.com/maps/d/embed?mid=1lE7MJKdWIR5W2Jb10eNRFsKM536AdAji&ehbc=2E312F). Det er operatørens eget publiserte kart, selv om Google leverer karttjenesten. Kartets [offentlige KML-eksport](https://www.google.com/maps/d/kml?mid=1lE7MJKdWIR5W2Jb10eNRFsKM536AdAji&forcekml=1) heter «Bunker Oil Bensinstasjoner» og inneholder 76 `Placemark`-objekter. KML-punktene og drivstoffbeskrivelsene ble hentet uten å endre kartet.

## Verifiserte kandidater i nord

Koordinater er operatørens kartposisjoner i WGS84, skrevet som breddegrad, lengdegrad. De er ikke landmålt utskytingsareal.

| Område | Bekreftet anlegg / adresse | Koordinat eller presisjon | Primærkilde og hva den dokumenterer |
|---|---|---|---|
| Berlevåg | Circle K Automat Berlevåg, Storgata 18 | 70.858774, 29.088923 | [Operatørens stasjonsside](https://www.circlek.no/station/circle-k-automat-berlevag): adresse, døgnåpent, bensin og diesel. Kartkoordinaten stemmer med det nasjonale uttrekket. |
| Båtsfjord | Circle K Automat Båtsfjord, Valen 3 | 70.629910, 29.705257 | [Operatørens stasjonsdata](https://www.circlek.no/station/52723), også i [nasjonal stasjonsliste](https://www.circlek.no/stations). |
| Kjøllefjord | Circle K Automat Kjøllefjord, Strandvegen 1 | 70.944720, 27.315178 | [Operatørens stasjonsside](https://www.circlek.no/station/circle-k-automat-kjollefjord): bensin, diesel og døgnåpent. |
| Havøysund | Circle K Automat Havøysund, Strandgata 139 | 70.995020, 24.673016 | [Operatørens stasjonsside](https://www.circlek.no/station/circle-k-automat-havoysund): bensin, diesel, anleggsdiesel og døgnåpent. |
| Mehamn | Bunker Oil / Fermann Service | Bensinstasjon i Mehamn verifisert; eksakt landpumpeposisjon ikke innhentet | [Bunker Oil](https://bunkeroil.no/om-bensinstasjoner) oppgir selv en bensinstasjon i Mehamn. [Gamvik-Nordkyn Havn KF](https://nordkynhavn.no/tjenester/bunkring) dokumenterer i tillegg marint drivstoff fra Fermann Service/Bunker Oil, Værveien 39. Landpumpen og den maritime bunkringen må ikke automatisk behandles som samme punkt. |
| Gamvik | Ingen lokal bensinstasjon verifisert i dette arbeidet | Må testes mot Mehamn/Kjøllefjord-punkter | [Kommunens snøscooterforskrift](https://lovdata.no/dokument/LF/forskrift/2022-02-08-1474/KAPITTEL_1) omtaler bensinstasjon i Værveien i Mehamn. Det dokumenterer ikke en bensinstasjon i selve Gamvik. Manglende lokal stasjon er heller ikke i seg selv et 40 km dekningshull. |
| Russenes | Circle K Automat Russenes, Vestre Porsangerveien 6094 | 70.475550, 25.068956 | [Circle Ks egne stasjonsdata](https://www.circlek.no/station/54697). |
| Karasjok | Circle K Karasjok, Suomageaidnu 1 | 69.471620, 25.510025 | [Circle Ks egne stasjonsdata](https://www.circlek.no/station/54326). |
| Kautokeino | Circle K Kautokeino, Fievroluodda 3 | 69.021255, 23.047840 | [Circle Ks egne stasjonsdata](https://www.circlek.no/station/52747). |
| Skjervøy | St1 Skjervøy, Kveldsolveien 1 | 70.0259722, 20.97721622 | [St1s stasjonsside](https://st1.no/stasjon/skjervy): døgnåpent, ingen butikk, bensin 95, diesel, farget diesel og AdBlue. Koordinat fra sidens JSON-LD. |
| Storslett | Circle K Storslett, Sentrum 34 | 69.771970, 21.027836 | [Circle Ks egne stasjonsdata](https://www.circlek.no/station/54332). |
| Vannøya | Bunker Oil Karlsøybruket | 70.1289805, 19.9794953 | [Bunker Oils eget stasjonskart](https://bunkeroil.no/en/map-petrol-stations). Relevant øypunkt som ikke bør forsvinne ved bruk av bare store veikjeder. |
| Reine | Circle K Reine, Reinevn 84 | 67.934680, 13.088820 | [Circle Ks egne stasjonsdata](https://www.circlek.no/station/53922). Må avstandstestes; det kan ikke uten videre antas å dekke Værøy eller Røst. |

## Øyer som må behandles eksplisitt

### Værøy

Her finnes dokumentert drivstoffinfrastruktur. Kommunens [turistbrosjyre 2024](https://varoy.kommune.no/_f/p1/i991aeac6-4edd-44fb-9461-39bf689098a7/touristbrochure-2024-english.pdf) oppgir Værøy Bunker og drivstoff til både bil og båt. [Kartverkets Den norske los](https://dnl.kartverket.no/api/ogc/v1/collections/dennorskelos/place/items/104ae69a-44cc-4361-b0c0-22b7b2107897?f=html), oppdatert 29. august 2024, bekrefter bensinstasjon på Værøy.

Et [beredskapsdokument fra Værøy kommune](https://innsyn.lofoten.nu/Varoy/innsyn/wfdocument.ashx?dokid=1371651&journalpostid=2021014619&variant=A&versjon=1) skiller mellom Værøy Bunker ved Sørtun/ferjekaia og den private bensinstasjonen sentralt på Sørland. [Brønnøysundregistrene](https://virksomhet.brreg.no/nb/oppslag/underenheter/918534342) viser dessuten Bunker Oil AS Værøy Tankanlegg som underenhet. Registeret bekrefter virksomheten, ikke at et bestemt utsalg er døgnåpent.

Eksakt pumpekoordinat er ikke fastlagt i dette notatet. En foreløpig Værøy-kandidat må derfor merkes som et **område**, ikke en ferdig verifisert utskytingstomt. Avstanden fra Værøy til bebodde deler av Røst skal testes i GIS før man bestemmer om Røst krever et eget punkt.

### Røst

En [offentlig beredskapsanalyse fra 2014](https://www.statsforvalteren.no/siteassets/fm-nordland/bilder-fmno/samfunnssikkerhet-og-beredskap-bilder/samfunnssikkerhet/rapport_langvarig-strombrudd-lofoten_11feb14_endelig.pdf), side 84, dokumenterer John Greger AS som drivstoffleverandør på Røst. Dette er **historisk dokumentasjon**, og er ikke alene nok til å hevde at et bestemt drivstoffutsalg fremdeles er operativt i 2026. [Brønnøysundregistrene](https://virksomhet.brreg.no/nb/oppslag/underenheter/871801622) bekrefter bedriften på Tyvsøyveien 15, men den registrerte næringen er fiskeforedling; det dokumenterer ikke dagens drivstoffsalg.

Røst må inngå i befolkningsdekningen. [SSB Kommunefakta Røst](https://www.ssb.no/kommunefakta/rost) oppgir 0 prosent bosatt i tettsted i 2025. En analyse basert utelukkende på SSB-tettsteder ville dermed utelatt hele kommunens bosetning. Bebodde befolkningsruter er et bedre grunnlag for denne casen.

### Træna

[Joker Træna](https://joker.no/finn-butikk/joker-trana) oppgir bensin og diesel som del av tilbudet. Butikken ligger ved hurtigbåtkai og fergeleie. Butikkens adresse er Janesvågen 6, og dens egne strukturerte kartdata gir 66.50116903026058, 12.101401289033662. Dette er et dokumentert **butikk- og drivstoffpunkt**, selv om det ikke er en vanlig kjedebensinstasjon. Punktet er lagt i `verified-extra-stations.json` med merknad om at koordinaten gjelder butikken.

### Utsira

Ingen oppdatert primærkilde som bekrefter en lokal, ordinær bensinstasjon på Utsira er funnet i dette delarbeidet. [Joker Utsiras egen side](https://joker.no/finn-butikk/joker-utsira) bekrefter butikk og servicetilbud, men oppgir ikke drivstoffsalg. Det er derfor ikke riktig å merke butikken som en bensinstasjon.

Dette er heller ikke dokumentasjon på et dekningshull: 40 km luftlinje må beregnes fra aktuelle stasjoner på Karmøy/Haugalandet til Utsiras bebodde ruter. At en øy mangler egen bensinstasjon eller fast veiforbindelse avgjør ikke luftlinjedekningen.

## Svalbard må avgrenses separat

[Svalbard Auto](https://svalbardauto.no/bensinstasjon/) dokumenterer en bensinstasjon i Sjøområdet i Longyearbyen, døgnåpne drivstoffpumper ved bensinstasjonen og scooterutfarten i Adventdalen, samt sesongpumper for båter i småbåthavna. [Eierselskapet LNS Spitsbergen](https://lnss.no/svalbard-auto-blir-selvstendig-bensinstasjon/) opplyser at Svalbard Auto ble uavhengig bensinstasjon i juni 2025. Eldre Circle K/Statoil-navn må derfor ikke uten kontroll brukes som dagens operatør.

Dette dokumenterer kandidater for Longyearbyen-området. Det dokumenterer ikke dekning av alle bosetninger på Svalbard. Dersom «hele Norge» inkluderer Svalbard, kreves en egen analyse av de bosatte stedene utenfor Longyearbyen. Ingen fullstendig Svalbard-liste er produsert her.

## Hva NVDB-søket avklarte

[NVDB Les API](https://nvdb.atlas.vegvesen.no/docs/produkter/nvdbapil/v4/introduksjon/Oversikt/) er Statens vegvesens åpne API for vegdata og kan gi relevante vei- og objektopplysninger. Jeg fant ikke et dokumentert, komplett offentlig nasjonalt bensinstasjonsdatasett i NVDB i dette arbeidet. Dette er et søkefunn, ikke et bevis på at ingen slik kilde finnes.

Operatørenes egne lister gir dokumenterte, geokodede kandidater uten å måtte anta at NVDB, foretaksregistre eller en tilfeldig stasjonsapp er komplette. En ufullstendig stasjonsliste kan påvise **at et område er dekket av minst én kjent kandidat**, men kan ikke alene bevise **at et område mangler enhver bensinstasjon innen 40 km**. Slike tilsynelatende hull må sjekkes mot andre kjeder, uavhengige utsalg og kommunale kilder.

## Betydning for konklusjonen i casen

Et geografisk mål for analysen er: For hver bebodd rute som inngår i kravet, finnes det minst ett relevant driftspunkt med luftlinjeavstand på høyst 40 km? Hvis kritikalitet skal bety reserve ved bortfall av ett driftspunkt, er spørsmålet i tillegg om hver rute har minst to uavhengige punkter innenfor radiusen. 40 km i seg selv fastsetter ikke et slikt reservekrav.

Det kan ofte finnes flere alternative plasseringer. Verifisering av en stasjon betyr derfor «mulig geografisk kandidat», ikke at akkurat denne stasjonen **må** brukes eller at eiendommen er tilgjengelig for formålet. Antall nødvendige ballonger og den konkrete plasseringen må komme fra dekningsberegningen, ikke fra stasjonslisten alene.
