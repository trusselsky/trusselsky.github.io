---
title: "Serious Sam - CVE-2021-36934"
date: 2021-07-26T09:57:04+02:00
draft: false
tags: ["Microsoft", "Windows", "CVE-2021-36934", "HiveNightmare", "Serious Sam"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "En svakhet på tilgangskontroll på nyere versjoner av Windows 10 til Kritiske System Filer"
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "serioussam.jpg" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/trusselsky/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

### Hva er det? ###
Den 19 Juli, ble det avdekket en sårbarhet i SAM (Security Account Manager) databasen i Windows 10 på nyere versjoner. Denne sårbarheten gjorde at brukerdatabasen kunne bli lest av ikke-administrator kontoer i Windows 10 under en gitt kontekst. Dette var kun mulig å gjøre om det fantes VSS (Volume Shadow Service) som oftest brukes for å lage lokale snapshots i Windows (som f.eks Previous Versions). Om man har f.eks backup tjenester som brukes mot Windows 10 klient maskiner vil den ofte bruke VSS for å lage snapshots. Samt f.eks System Restore funksjonen i Windows bruker VSS for å lage snapshosts. 

Sårbarheten ble avdekket av Jonas Lyk (https://twitter.com/jonasLyk/status/1417205166172950531)

### Hvilken versjoner gjelder det? ###
Dette gjelder Windows 10 (fra 1809 oppover) samt Windows Server 2019. Sårbarheten er kun mulig å utnytte om man har tilgang til å kjøre kode på det aktuelle systemet. 
### Hvilken konsekvenser har det? ###
Om en klient maskin blir kompromitert samt har shadow copies lokalt på maskinen, kan en angriper bruke dette for å elevere seg selv til å bli lokal administrator. Eller hente ut informasjon om andre brukerkontoer som ligger igjen lokalt, som f.eks domene kontoer. 
### Løsninger/Workarounds ###
Microsoft har ikke kommet med patch ennå, men det finnes en workaround for å kunne løse opp i sårbarheten. Samtidig er det viktig å påpeke at sårbarheten ikke blir aktivt utnyttet ennå, men at Microsoft vil komme med en oppdatering fortløpende. 
* Begrens tilgang til SAM databasen, kjør CMD/PowerShell som Administrator icacls %windir%\system32\config\*.* /inheritance:e
* Slett tidligere Shadow Copies som ble laget før punkt 1 ble gjort. Her er mer informasjon knyttet til hvordan finne og slette Shadow Copies --> https://support.microsoft.com/en-gb/topic/kb5005357-delete-volume-shadow-copies-1ceaa637-aaa3-4b58-a48b-baf72a2fa9e7

### Mer informasjon ###
* Microsoft CVE-2021-36934 (https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-36934)
* Python PoC (https://github.com/GossiTheDog/HiveNightmare)

### Video av Exploit ###
{{< youtube 5zdIq6t3DOw >}}
