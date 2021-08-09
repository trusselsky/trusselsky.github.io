---
title: "ProxyShell - Nye sårbarheter mot Exchange"
date: 2021-08-09T16:44:01+02:00
draft: false
tags: [""]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: true
draft: false
hidemeta: false
comments: false
description: "ProxyShell, nye sårbarheter mot Microsoft Exchange. Over 100+ Løsninger i Norge fortsatt sårbare"
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/trusselsky/trusselsky.github.io/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
Under årets BlackHat Conference, ble det presentert detaljer rundt nye sårbarheter som ble kjent i Microsoft Exchange som nå har blitt dubbet til "ProxyShell" som er en kombinasjon av 3 sårbarheter.
* **CVE-2021-34473** - Pre-auth Path Confusion leads to ACL Bypass (Fikset i April av KB5001779)
* **CVE-2021-34523** - Elevation of Privilege on Exchange PowerShell Backend (Fikset i April av KB5001779)
* **CVE-2021-31207** - Post-auth Arbitrary-File-Write leads to RCE (Fikset i Oppdatering i Mai av KB5003435)

Sårbarhetene kan gjøre at uvedkommende kan få tilgang til Exchange løsningen å laste ned epost databaser som da inneholder alt av f.eks epost kontoer (epost, kalender,kontakter osv) siden tilgangen som uvedkommende får ved å utnytte sårbarhetene er lokal system.

Viktig at man dobbeltsjekker hvilken versjon man er på --> https://exchangeserverversions.blogspot.com/2016/01/exchange-server-2016.html (Her er en liste for Exchange 2016)

MERK: Dette er ikke samme sårbarhet som ble utnyttet i angrepet mot Stortinget som også benyttet en sårbarhet mot Exchange, som heter ProxyLogin. 

Disse sårbarhetene ble presentert av sikkerhetsforsker Orange Tsai (https://twitter.com/orange_8361)

Du kan se presentasjonen her --> https://i.blackhat.com/USA21/Wednesday-Handouts/us-21-ProxyLogon-Is-Just-The-Tip-Of-The-Iceberg-A-New-Attack-Surface-On-Microsoft-Exchange-Server.pdf?fbclid=IwAR2V0-4k2yb8dmPP5Mksd8iHYTOfE6sBwygMt4wjq3M9be8Tw6TlH0andhA

Her kan man også se et video eksempel hvor noen har laget script som utnytter alle sårbarhetene for å kunne ekspotere epost fra Exchange serveren. 

{{< youtube LbIYPFrltdA >}}  

<br/> Samtidig kan man også se at bare i Norge er det i overkant av 100+ som har offentlige Exchange servere som fortsatt er sårbare. 

![ProxyLogin](/proxyshell.jpg)

Samtidig er det flere nå som merker økt Exchange trafikk, i tillegg er det noen angripere nå som allerede har begynt å utnytte sårbarhetene. 

{{< tweet 1423764613829701632 >}}

## Indikatorer ##

Flere som scanner nå etter sårbare Exchange servere prøver å utnytte sårbarheten via Autodiscovery bibloteket på CAS serverene. 
Et eksempel som har blitt flagget er trafikk mot 

```
https://exchange-server/autodiscover/autodiscover.json?@abc
.com/owa/?&Email=autodiscover/autodiscover.json%3F@abc.com 
```

Om din Exchange løsning fortsatt er sårbar vil den respondere med en HTTP 302 kode tilbake. 