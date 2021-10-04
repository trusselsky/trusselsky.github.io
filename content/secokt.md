---
title: "Sikkerhetsmåneden Oktober"
date: 2021-10-01T10:12:31+02:00
draft: false
tags: [""]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: true
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

## 1 Oktober - Nettleser kontroll
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

## 4 Oktober - Har du kontroll på DNS?

Hver eneste dag er det tusenvis av nye domener som blir registrerte hos ulike DNS registrarer. Majoriteten av disse nye domenene som blir opprettet er for mistenkelige formål, som enten brukes til phising angrep eller for andre formål. 

Ref: https://unit42.paloaltonetworks.com/newly-registered-domains-malicious-abuse-by-bad-actors/

Mange domener har også kort levetid som ofte henger sammen med en phising kampanje som kjøres for å lure brukere mot f.eks. nettsider som skal imitere nettbanker, sosiale medier eller andre kjente nettsider for å få brukere til å oppgi sensitiv informasjon som brukernavn og passord. 

Det er selvsagt veldig vanskelig å få blokkert alle domener som mulig blir opprettet en gang i fremtiden eller som er av mistenkelig art. 

De fleste brannmurer har mulighet for å blokkere slike såkalte NSD (Newly Seen Domains) slik at de gjør et oppslag først mot den aktuelle WHOIS infoen for å se levetiden på domenet. Dette er derimot litt mer utfordrende når man sitter på hjemme nett eller andre lokasjoner hvor trafikken ikke går igjennom en sentral brannmur tjeneste.
Det finnes derimot gratis tjeneste som kan automatisk blokkere både mot NSD samt domener som er av mistenkelig art. 

Blant annet er det f.eks. Cloudflare og Cisco som begge tilbyr en gratis utgave av DNS tjenestene sine. 
* Cloudflare: https://developers.cloudflare.com/1.1.1.1/1.1.1.1-for-families
* OpenDNS (Cisco): https://support.opendns.com/hc/en-us/articles/227988127-Getting-started-About-using-OpenDNS

Ellers så har også begge leverandører en kommersiell modell som kan brukes for organisasjoner. Fordelen med en slik DNS-tjeneste kontra andre er også at man får en desentralisert DNS tjeneste som vil virke uavhengig hvor brukeren/enheten befinner seg.  Samt at begge leverandørene er også de som leverer de raskeste DNS tjenesten. 

Eksempelvis:

![HTTP/3 Bruk](/dns.png)

Samtidig tilbyr også begge leverandørene DoH (DNS over HTTPS) som gjør at man kan gjøre DNS oppslag kryptert også. Slik at DNS trafikk også er kryptert for nettleseren. Merk at dette krever at nettleser eller det er innebygget funksjonalitet i operativsystemet. Som det blir nå med Windows 11 blant annet, mens de fleste nettleseren har støtte for det allerede. Men merk at sistnevnte kun gir krypert DNS oppslag for nettleser trafikk å ikke for alt annet av tjeneste kommunikasjon. 
 
Har du noen tips til andre innstilliger man bør ha med? gi oss beskjed! marius@trusselsky.no




