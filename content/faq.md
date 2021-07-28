---
title: "Hva er Trusselsky?"
date: 2020-09-15T11:30:03+00:00
weight: 1
# aliases: ["/first"]
author: "Marius Sandbu"
# author: ["Me", "You"] # multiple authors
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Ofte stilte spørsmål rundt Trusselsky."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: true
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
cover:
    image: "https://i.imgur.com/2zPJqZ4.png" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
### Hva er Trusselsky? ###
Hensikten bak Trusselsky er å ha en lettvekt tjeneste for informasjonsdeling knyttet til digitale sikkerhetstrusler, men uten at man må
* Betale $$$ for eksterne tjenester for varslinger
* Abonere på X antall ulike leverandører knyttet til varslinger

Men samtidig kunne få
* Tilgang til informasjon knyttet til nye sårbarheter og andre sikkerhetsrisikoer.
* Få mer målrettet informasjon i forhold til trusler, tiltak man kan gjøre.
* Nyheter relatert til IT-sikkerhet

### Hvorfor navnet Trusselsky? ###
ThreatCloud som var det tiltenkte orginale navnet er trademarket Checkpoint så derfor ble det på Norsk istedet... 

### Hva er ikke Trusselsky? ###
Trusselsky er kun ment til informasjonsdelding, dette erstatter ikke behovet for andre tjenester som. 
* Sikkerhetsmonitorering
* Sikkerhetsoppdateringer
* Ressurser som gjennomfører punkt 1 og punkt 2

Men er kun ment som et supplement til de som ønsker litt mer informasjon rundt hva som skjer på IT-sikkerhet. 

### Hvordan samler du/dere inn informasjon? ###
Vi benytter en del ulike informasjonskanaler som blir kvernet igjennom trakten å deretter videreformidlet blant annet. 
* Informasjon fra ulike leverandører (Cisco, Microsoft, CheckPoint, Fireeye, F-secure, Palo Alto, VMware)
* Ulike Sosiale Medier
* E-post fra andre sikkerhetsinstanser
* RSS fra andre blogger og nettsider

Høres ut som mye informasjon som må prosesseres å det er det, men dere vil bli overrasket over hvor mye fritid undertegnende har. 

### Hvorfor laget du Trusselsky? ###
Etter å ha jobbet i IT en del år ser jeg at i mange sammenhenger er utfordringer knyttet til informasjonsflyt som gjør at organisasjoner blir utsatt for angrep.
F.eks at de ikke får informasjon om at det er en sårbarhet knyttet til et spesifikt produkt eller tjeneste som en organisasjon benytter. Samtidig så er det for mange altfor mye informasjon å fordøye så derfor ønsket jeg å lage dette som en lettvekt måte å få ut nødvendig informasjon. 

### Hvordan fungerer tjenesten? ###
Det er egentlig veldig VELDIG...enkelt, vi samler inn informasjon som vi deretter skriver om med litt mer utfyllende data (på Norsk) som deretter da blir tilgjengelig direkte via ulike informasjonskanaler. Så tanken bak det er å ha en felles informasjonskanal som dekker ulike leverandører i stedet for at man må følge med på mange ulike kanaler, eller at man bare ønsker å få litt mer informasjon.

* RSS Feed fra nettsiden (Kan også filtrere basert på tjeneste/produkter/informasjon) hvor man kan benytte ulike RSS tjenester som f.eks Feedly til å få info. Dette kan gjøres enten basert på produkt/kategori/teknologi osv. Et eksempel her er å kategorisere på produkt. ![RSS](https://i.imgur.com/ePezLVh.png)
* Abonnere på epost varsling (Påmelding kan justeres basert på produkt/tjeneste) styres via Mailchimp
* Ulike sosiale medier (Twitter) --> https://twitter.com/trusselsky
* Fremover vil det også komme push notification for varslinger (Se mer info om planer under --> https://github.com/trusselsky/trusselsky.github.io/issues)

### Hvordan samler dere inn informasjon om trusslene? ###
Vi benytter ulike former for innsamling, mye kommer fra sosiale medier, oppdateringer fra ulike leverandører og ulike sikkerhets fora.  

### Hvor lagrer dere data? ###
Det som eventuelt er lagret av informasjon er via epost utsendinger som foregår automatisk når det kommer nye sårbarheter relatert til spesfikke produkter, alt av informasjon er publisert direkte via GitHub (Helt Sant! se her --> ) https://github.com/trusselsky/trusselsky.github.io

### Hvilken informasjon er det dere formidler? ###
Vi bruker ulike felt avhengig av informasjon som skal ut, de fleste artikler vi lager pleier å innholde en eller flere av følgende felter. 
* Leverandør + Produkt
* CVE (Om finnes)
* CVE Link til leverandør (om finnes)
* Dato
* Hva er det for noe, hvordan?
* IOC (Indikatorer som f.eks IP addresser, prosesser) brukes ofte som informasjon knyttet til angrep. 
* Tiltak som kan gjøres

### Hva er nettsiden laget av? ###
Github pages + Hugo, bygging skjer via GitHub actions. Ikke så mye mer spennende en det..

### Hvordan kan jeg bidra? ###
Om det er mer informasjon knyttet til enkelt innlegg eller artikler så stikk gjerne over til Github å kom med tilbakemeldinger eller marker det som "Issues" 
Alternativt om du har andre ideer, send meg gjerne en epost på marius@trusselsky.no, jeg biter ikke.. 
