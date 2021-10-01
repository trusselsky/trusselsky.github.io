---
title: "Sikkerhetsmåneden Oktober"
date: 2021-10-01T10:12:31+02:00
draft: false
tags: [""]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
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

Her kommer vi løpende med korte tips og tricks man kan gjøre for å øke sin sikkerhetshygiene. Målet er å komme med nye tips hver dag i hele Oktober! 

## 1 Oktober
En ting vi har sett mye av de siste årene har vært sårbarheter tilknyttet nettleseren. Dette er litt fordi at nettleseren er kontinuerlig under utvikling, nye web standarder som skal supporteres, nye funksjonalitet med add-ons og ikke minst skal bli tettere integrert med det underliggende operativsystemet for å kunne understøtte nye tjenester som WebRTC, WebGL, QUIC/HTTP3. 

Nettleseren er også mye av hovedverktøyet til alle ansatte å må derfor viktig angrepsflate som må beskyttes. Så langt i år har Google Chrome hatt 13 (0-dags) sårbarheter med noen av disse har også blitt utnyttet for å gjennomføre angrep. Vi har også sett eksempler på hvor extensions som har hatt over 20 millioner brukere som har blitt brukt for innsamling av informasjon eller videresende brukere til phising nettsider. Så det er veldig viktig å ha kontroll på nettleseren i forhold til å ha oppdateringer automatisk samt kontroll på addons samt noen andre justeringer. 

For Administrerte klienter kan dette styres via Group Policy som kan lastes ned her --> https://enterprise.google.com/chrome/chrome-browser/#download samt det finnes en egen Group Policy for styring av oppdateringer (https://dl.google.com/update2/enterprise/googleupdateadmx.zip) 

Her er det en rekke innstillinger man bør definere

* Google Chrome --> Extensions --> Blocks external extensions from being installed
* Google Chrome --> Extensions --> Configure extension installation blocklist (med verdi *) dette forhindrer at extensions blir innstallert med mindre de ligger i allow listen.
* Google Chrome --> Set the time peroid for update notifications --> Når brukere får beskjed om at Chrome må restarte pga oppdateringer vil verdien man definere her gjør at Chrome blir automatisk restartet. 
* Google Chrome --> Notify a user that a browser relaunch or device restart is recommended or required --> Show a recurring prompt to the user indicating that a restart is required. 
* Google --> Google Update --> Applications. Always Allow Updates (recommended)
* Google --> Google Update --> Application --> Google Chrome. Always Allow Updates (recommended)

## 2 Oktober

Har du noen tips til andre innstilliger man bør ha med? gi oss beskjed! marius@trusselsky.no




