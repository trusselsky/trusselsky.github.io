---
title: "Hvordan komme til en passordløs hverdag?"
date: 2021-09-21T23:28:51+02:00
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
Microsoft lanserte nylig at man kunne begynne å logge inn mot Microsoft-kontoen uten passord men heller benytte seg av Microsoft authenticator appen (eller andre mekanismer som f.eks fysiske adgangsnøkler) for innlogging.

Funksjonen er ikke ny, men har primært vært tilgjenglig for bedriftsmarkedet frem til nå. Alikevel er det ikke mange som har benyttet seg av funksjonaliteten, derfor ønsket vi å belyse litt hvordan tjenesten fungerer. Litt om hva som behøves, hva som er supportert og hvorfor det er sikrere en vanlig brukernavn og passord. Samt litt om økosystemet rundt å hvem som supporterer denne autentiseringsmekanismen. 

![FIDO2](/passordløs1.png)

## FIDO2 
FIDO (Fast IDentity Online) alliasen er en rekke organisasjoner som samarbeider ved å utvikle en sikrere og enklere måter å autentisere på. Denne gruppen kom med FIDO2 standarden som var et utvidelse av det eksisterende rammeverket som de hadde laget men skulle tilby sikker autentisering basert på passordløs autentisering både for mobile og vanlige arbeidsstasjoner. 

FIDO2 Består av to standard hoved komponenter 
* Et Web API (WebAuthn)
* Client Authentication Protocol (CTAP)
CTAP definerer protokollen for en ekstern sikkerhetsnøkkel og snakker med en klientenhet. Begge disse er tett ingrert å leverer med det en passordløs pålogging mekanisme. 

![FIDO2](/fido1.png)

For å kunne benytte seg av FIDO2 standarden er man avhengig av å ha støtte for WebAuth og CTAP protokollen på underliggende systemer som f.eks identitetstjenesten, nettleseren og ikke minst operativsystemet for å kunne håndtere autentiseringsmekanismen. Så hvem støtter FIDO2 standarden?

De fleste moderne nettlesere støtter FIDO2 standarden mot Azure Active Directory med ulike CTAP støtte som USB, NFC eller Bluetooth (BLE)

![browserfido](/browserfido.png)

I tillegg må man ha FIDO2 godkjente sikkerhetsnøkler fra en supportert leverandør. Som disse leverandørene her som tilbyr en rekke sikkerhetsnøkler som kommer med ulike funksjonalitet som f.eks Yubiko som leverer USB/NFC nøkler med touch-basert autentisering. Men de fleste leverandørene har ulike alternativer basert på ulik USB(A/C) format 

* Feitian
* Kensington
* Thales
* Thetis
* Token2 Switzerland
* TrustKey Solutions
* Yubico

## Hva støtter FIDO2? 

Men hvilken identitetstjenester støtter FIDO2? (Ikke en helt fullstendig liste)

* Google Identity
* Azure Active Directory (omfatter og Office 365)
* Okta
* Github
* Buypass ID & Authentication tjenesten (https://buypassdev.atlassian.net/wiki/spaces/BFIS/overview)
* PingIdentity
* Sosial medier som (Facebook/Twitter)
* Passordtjenester som (1Password, LastPass f.eks)

Det finnes også en fullstendig liste som spesielt Yubikey støtter her --> https://www.yubico.com/no/works-with-yubikey/catalog/?sort=popular 

Selv om ikke alle applikasjoner har innebygget støtte for WebAuth så vil det fungere om applikasjoner og tjenester man benytter seg av er integert mot en av disse identitetstjenestene over som (f.eks AzureAD), betyr det at man kan benytte seg av f.eks passordløs autentisering mot disse tjenestene. 

![webauth](/webauthflow.png)

Fra en sluttbruker perspektiv som skal autentisere mot en angitt tjeneste, vil arbeidsflyten være slik.(NB WebAuth er et javascript biblotek som kjører i nettleseren)
* 0: Bruker går mot angitt applikasjon som krever autentisering, går tilbake til iDP.
* 1: Relay party (som er en komponent hos iDPen) sender 
* 2: Nettleseren sender en authenticatorMakeCredential() som inneholder til authenticator (via CTAP) tjenesten å be brukeren legge inn enten pinkode eller touch
* 3: Brukeren verifiserer autentiseringen tilbake til CTAP.
* 4: CTAP returnerer data tilbake til nettleseren med en ny credential ID og annen informasjon
* 5: Nettleseren sender data tilbake til server (Relay party hos iDPen)
* 6: Server godkjenner forespørselen å sender tilbake et access token fra iDPen som gir SSO. 

## Hvordan sette opp en passordløs løsning med Yubikey?

Oppskriften her er å sette opp dette mot Azure Active Directory. Hvor det første steget er å aktivere FIDO2 som en påloggingsmekanisme i Azure AD. Dette gjøres under Azure AD Properties --> Security --> Authentication Methods. Deretter må FODI2 aktiveres. 

![azuread1](/azuread1.png)

* Når dette er gjort, men per bruker aktivere nøkkelen for sin bruker. Dette kan gjøres via myapps.microsoft.com å under Security og Sign-ins velge Security information og velge "Add Method". Under der vil man ha valg om å legge til Security Key. 

![azuread1](/azuread2.png)

* å deretter velge hva slags type nøkkel man har. I eksempelt her har jeg en Yubikey v4 som kun er støtte via USB. 

![azuread1](/azuread3.png)

* Når man velger nøkkeltype, vil iDP tjenesten trigger autentiseringsflyten via WebAuthn som vil kjøre registrering av nøkkelen. Så vil man se en typisk bilde som dette for å registrere nøkkelen sin.

![azuread1](/azuread4.png)

* Når dette er gjort, vil man også avhengig av type nøkkel fullføre en autentiseringsprosess enten ved å legge inn pinkode eller touch basert autentisering

![azuread1](/azuread5.png)

* Når dette er gjort vil man via Azure AD login som dekker O365 og andre tjenester ha "Sign in with a Security Key" som opsjon. Pinkode i tilfelle ved logging vil være andre faktoren som oppfyller kravene til MFA. 

![azuread1](/azuread6.png)

* Det skal også sies at samme autenseringsmekanisme er også tilgjengelig direkte mot Windows. Som krever at Windows Hello For Business er aktivert. 
I prinsippet så har Microsoft integert CTAP komponenten inn i sitt operativsystem for å få til dette. Om klienten også er en del av Azure AD vil man også kunne få SSO fra Windows login ut til alle tjenester som er integrert mot iDP tjenesten. 

![azuread1](/windows10.png)

## Hensyn man må ta om man setter dette opp for Windows infrastruktur

Så langt har vi beskrevet oppsettet inn mot en skybasert identitestjeneste, kan dette også virke mot mer tradisjonelle tjenester som Active Directory?
Det er også supportert men krever noe modifikasjoner mot Active Directory som beskrives her --> https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-authentication-passwordless-security-key-on-premises (men merk det krever fortsatt at man har identitet synkronisert ut mot Azure Active Directory)

Men det er viktig å påpeke at denne tjenester er ikke supportert mot alle protokoller som f.eks RDP eller "Run-as" eller pålogging mot servere via WMI/PowerShell. 

## Er vi tryggere nå?
Er man tryggere når en bruker ikke lengre vet sitt eget passord? Om en bruker ikke lengre har tilgang til sitt eget passord betyr det også at man ikke kan oppgi denne type informasjon som også gjør at man blir mindre sårbar for brukerinformasjon som er på avveie. Alikevel vil ikke f.eks implementering av slike løsniger forhindre at brukernavn og passord kan komme på avveie alikevel. Selv om brukeren bruker en FIDO2 basert nøkkel for passordløs autensering så sitter fortsatt passordet lagret hos identitetstjenesten. Eneste måten man da kan forhindre det på er om idenditetsleverandøren tar bort passordet helt fra løsningen, slik som Microsoft har gjort som mulighet for Microsoft online kontoer. 

Samtidig har man også mulighet til å definere sikkerhetsregler som krever f.eks at om man skal kunne logge inn så må man ha nøkkelen for å gjennomføre MFA autentiseringen. 

Om den også skal ha ønsket effektv ved å eliminere passord, må man også se på resten av økosystemet. Hva slags tjenester er det som brukeren har behov/tilgang til som krever passord? mobilen? print systemet? adgangskontroll? Det er selvsagt viktig å vurdere hvordan og hvilken type løsning som passer til det økosystemet man har for å kunne få til en sømløs opplevelse for brukerene. 





