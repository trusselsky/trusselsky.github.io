---
title: "Windows 11 og Measured Boot m/TPM"
date: 2021-07-29T10:15:54+02:00
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
    image: "windows11tpm.jpg" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/trusselsky/trusselsky.github.io/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
Som en del av Windows 11, har Microsoft introdusert en del rekke endringer i forhold til sikkerhet og hardware krav som følger de sikkerhetsfunksjonene.
En av de største endringene er at Microsft nå vil kreve at maskiner som skal kjøre Windows 11 på fysiske maskiner, støtter en funksjon i Windows som heter Measured Boot. 

![Secure Boot](https://i0.wp.com/docs.microsoft.com/en-us/windows/security/information-protection/images/dn168167.boot_process(en-us,msdn.10).png?zoom=1.25&w=750&ssl=1)

## Measured Boot ##

Measured Boot er delt opp i 2 deler, ene som er Secure Boot prosessen som ble laget for at operativsystemet kun starter opp med programvare som leverandøren kan stole på. Når maskinen starter Secure boot vil den første finne OS Bootloader partisjonen, verifisere at firmwaren er digital signert samt at den ikke er modifisert. Om innholdet er inntakt vil den deretter starte operativsystemet.    Andre delen som kalles Trusted Boot sjekker integriteten av alle Windows baserte komponenter (samt ELAM "Early Launch Anti-Malware" sjekker at alle drivere er digital signerte før de blir lastet inn i bruker kontekst).

NB: Secure Boot er en funksjon som ligger i UEFI å ikke noe Microsoft har utviklet. 

For å kunne bruke Measured Boot (m/Secure boot) i Windows krever to ting, det ene er UEFI firmware samt TPM på maskinen. 

## Hva slags angrep stopper denne tjenesten? ##

Selve sikkerhetsmekanismen er beregnet på å stoppe Bootkits og RootKits. Bootkits er skadelig kode som starter før selve operativsystemet laster inn som gjør at om man skulle bli infisert av en Bootkit, kan koden ligge i maskinen og overleve reinnstallasjon av operativsystem blant annet. Trickbot er en malware aktør som benytter seg av Bootkit som de har kalt TrickBoot (Man kan lese mer om det her --> https://eclypsium.com/2020/12/03/trickbot-now-offers-trickboot-persist-brick-profit/)

Samt med ELAM og verifisering av Windows komponenter kan man også unngå Rootkits ved at anti-virus tjenesten kan starte før en eventuelt Rootkit som ofte starter som en prosess eller scheduled task kan starte. 

Selvsagt viktig å påpeke at disse sikkerhetsfunksjonene vil ikke ha noe direkte effekt mot f.eks ransomware angrep, hvor angripere ofte angriper kjørende maskiner ved å utnytte andre sårbarheter. Men dette er rettet mot f.eks mot fysisk angrep hvor noen prøver å modifisere boot prosessen. 

## Hvorfor er disse TPM kravene her? ##

Så trenger jeg virkelig TPM? å i tilfelle hvilken versjon trenger jeg? Microsoft har endret litt på kravene sine, så for å få lov til å innstallere Windows 11 må man ha støtte for ihvertfall TPM 1.2 eller høyere. 

TPM 1.2 standaren ble ferdig i 2011 så mange av dagens maskiner har 

![Windows 11 krav](https://pbs.twimg.com/media/E4rU5YiWYAMDqlA?format=png&name=900x900) 

Man kan også slå av denne sjekken under installasjon ved å legge til en enkel registry nøkkel på maskinen. 
Ved innstallasjon trykk Shift+F10, åpne registry og legg til nøkkel
```
HKEY_LOCAL_MACHINE\SYSTEM\Setup “BypassTPMCheck”=dword:00000001   
“BypassSecureBootCheck”=dword:00000001
```
Microsoft anbefaler at man helst har TPM 2.0 chip på maskinene pga det er en stor løft fra TPM 1.2 til TPM 2.0 --> (https://docs.microsoft.com/en-us/windows/security/information-protection/tpm/tpm-recommendations#tpm-12-vs-20-comparison)

## Andre funksjoner som vil kreve dette ##

Microsoft ønsker også å kunne benytte denne funskjonen som en autentiseringsfaktor også. Mange av tilgangsmekanismene som i dag finnes i Azure AD er basert på enten bruker m/tofator autentisering. Men i bunnen av Windows 11 har Microsoft også utviklet en ny funksjon for utveksling av helse status på maskinen. 

![Microsoft Azure Attestation](https://pbs.twimg.com/media/E49JZwLWUAAJWlT?format=jpg&name=large) 

Som betyr f.eks at Windows 11 maskiner kan sende helse signal til Azure AD ved å gi beskjed om status i forhold til Secure Boot før f.eks en enhet får tilgang til data og tjenester, men dette er noe som kommer på sikt. 

## Mer informasjon ##

NSA har også laget en god oppsummering på UEFI og Secure Boot prosessen --> https://media.defense.gov/2020/Sep/15/2002497594/-1/-1/0/CTR-UEFI-SECURE-BOOT-CUSTOMIZATION-20200915.PDF/CTR-UEFI-SECURE-BOOT-CUSTOMIZATION-20200915.PDF


