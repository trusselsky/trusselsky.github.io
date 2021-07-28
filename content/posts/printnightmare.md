---
title: "PrintNightmare - CVE-2021-34527"
date: 2021-07-27T16:33:39+02:00
draft: false
tags: ["Microsoft", "Windows","CVE-2021-34527", "Print Spooler"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Svakheter funnet i Print Spooler tjenesten i Windows"
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "printnightmare.jpg" # image path/url
    thumbnail: "printnightmare.jpg"
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: true # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/trusselsky/trusselsky.github.io/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

### Hva er det? ###
Den 30 Juli, ble det avdekket en sårbarhet i Print Spooler tjenesten i Windows. Som er en innebygget tjeneste i Windows som håndterer utskrift samt er også ansvarlig for driver innstallasjon knyttet til oppkobling av skrivere på Windows operativsystem. 

Det har kommet en del informasjon knyttet til denne sårbarheten samtidig som den er veldig omfattende og dekkes av flere CVE'er. 

1: CVE-2021-1675 (https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-1675) som ikke er sårbarheten dubbet PrintNightmare. Microsoft kom med egen patch for denne med månedlig oppdateringer i Juli.  
2: CVE-2021-34527 (https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-34527) har også kommet med egne patcher for de ulike operativsystemene.  
3: CVE-2021-34481 (https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-34481) ny sårbarhet for lokal eskalering av tilganger. (Egen artikkel, kom 16 Juli)

### Hvilken versjoner gjelder det? ###
Denne sårbarheten gjelder alle Windows Operativsystem (både klient og Server) fra Windows 7/2008 til Windows 10/2019. 

### Hvilken konsekvenser har det? ###
Denne sårbarheten kan gjøre det mulig å kompromitere maskiner i gitte scenarioer hvor man har Print Spooler tjenesten kjørende. Dette kan da være nettverksbaserte maskiner som domene kontrollere eller andre typer maskiner. Print Spooler tjenesten kjører som standard. Svakheten er definert slik at man kan lage en egendefinert DLL fil (som gjenspeiler en Print Driver) som man kan få print tjenesten i Windows til å importere under SYSTEM kontekst om Remote Printing tjenestne er aktivert. Denne egendefinerte DLL filen kan f.eks inneholde skjulte kommandoer for å tildele f.eks lokal administrator tilgang.  Basert på informasjon vi har tilgjengelig er det ingen aktive angrep som benytter seg av denne angrepsvektoren ennå. Det krever tilgang til f.eks en maskin innenfor domenet for å kunne utnytte seg av sårbarheten som en da autentisert bruker.

### Løsninger/Workarounds ###
Microsoft har kommet med sikkerhetsoppdateringer som løser sårbarheten. Men pga flere sårbarheter som nå blir avdekket i Print Spooler tjenesten, samt generell råd er at man deaktiverer Print Spooler tjenesten på maskiner som ikke har behov for den, som f.eks Domene kontrollere.  Merk at sikkerhetsoppdateringene fra Microsoft krever omstart av maskinene som blir oppdatert. 
 * **PowerShell eksempel**
```
Stop-Service -Name Spooler -Force
Set-Service -Name Spooler -StartupType Disabled
```
Merk at ved å deaktivere Print Spooler tjenesten vil stoppe muligheten for å kjøre print jobber, dette omfatter også f.eks konvertering til PDF. For maskiner hvor man har behov for print som f.eks Citrix servere eller lokale arbeidsstasjoner er det anbefalt at man deaktiverer inbound remote print for å kunne  

### Mer informasjon ###
* Eksempler på exploit https://github.com/nemo-wq/PrintNightmare-CVE-2021-34527
* Her er også et eksempel på hvordan man kan koble opp til en ekstern fiktiv print tjeneste som deretter gir System tilganger på maskinen. Merk at skaperen bak Mimikatz skriver også hvordan man kan begrense dette til kun godkjente systemer også via Group Policy. 
{{< tweet 1416429860566847490 >}}





