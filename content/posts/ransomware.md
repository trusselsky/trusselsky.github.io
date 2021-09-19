---
title: "Hvordan redusere risikoen for å bli utsatt for Ransomware angrep"
date: 2021-09-18T23:38:06+02:00
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

De siste månedene har det vært en voldsom økning knyttet til ransomware angrep, derfor ønsket vi å komme med en den generelle råd i forhold til hvordan man kan redusere risikoen for å bli utsatt for ransomware angrep. NB: Dette er en liste med tiltak som vil bli kontinuerlig oppdatert (19/09/2021)

Det er viktig å påpeke at ransomware angrep har i det siste også vært mye tidligere ute med å ta i bruk nye sårbarheter. Dette betyr at viktigheten med å få på plass sikkerhetsoppdateringer er essensielt. 

## Angrepsvinklene
De siste årene har ransomware aktørene endret taktikk i forhold til hvordan ransomware angrep blir gjennomført. Ransomware angrep forekommer ofte i to ulike varianter.

### DDoS Ransomware angrep
som omhandler at en organisasjon blir utsatt for distribuert angrep mot eksterne tjenester eller mot datasenteret med ofte veldig store mengder data som gjør det vanskelig å håndtere. Senest i sommer kom det frem at en organisasjon ble utsatt for en DDoS angrep som ble målt opp til 17 millioner forespørsler per sekund. Når disse angrepene forekommer vil ofte de som fasiliterer angrepet sende epost til IT-kontaktene i organisasjonen å deretter be om løsepenger eller så vil angrepet øke i omfang og lengde. 

### Kryptering ransomware angrep
som omhandler at en organisasjon blir utsatt for angrep hvor hackerene ofte vil gjøre data utilgjengelig ved å kryptere informasjon/data de har tilgang til. Dette er den vanligste angrepsformen, men vi ser nå i det siste så har også hackerene endret taktikk til at det også gjør flere ting for å øke sannsynligheten for at løsepenger blir betalt.

* Henter ut data og lagrer på sine egne servere og deretter kjører omvendt auksjon - ergo organisasjonen må by på sine egne filer og data eller så blir informasjon publisert ut mot internett 
* Truer med å kontakte media, samarbeidspartnere eller sluttkunder av organisasjonen. Om de har sensitive opplysninger om enkeltpersoner eller andre foretak som de har tilgang til vil de også bruke dette for å eventuelt true disse individene også. 

Denne angrepsformen er ofte gjennomført eller starter via

* ***Phising angrep mot sluttbrukere***
* ***Feilkonfigurert infrastruktur (som f.eks tjenester som er eksponert ut mot Internet uten noen sikkerhetsmekanismer)***
* ***Sårbarheter***
* ***Gjenbruk av identitet***

Når en eventuelt hacker har fått tilgang til en kompromitert klient eller via en sårbar tjenester så vil de benytte ulike mekanismer for å komme lengre innover i infrastrukturen. Veldig ofte hvor hackere har greid å gjennomføre angrep hvor de tilslutt har greid å gjøre all infrastruktur utilgjengelig er det ofte enkle ting som har vært den utløsende faktoren. Ofte ser vi at det er tjenester som er sårbare hvor leverandøren har hatt sikkerhetsoppdatering tilgjengelig lenge eller bare dårlig sikkerhetshygine, eller en kombinasjon av begge deler. 

## Tiltak 
Her vil vi gå overordent igjennom en del tiltak som man bør ha gjennomført for å redusere risikoen tilknyttet ransomware. Et viktig element som er viktig å forstå er at ransomware utnytter i prinsippet alltid de svakeste leddene i en IT infrastruktur så derfor er det viktig å ha kontinuerlig forbedringer og jobbe systematisk med sikkerhet.

### Identitet
* Definere en strengere passord policy som angir at passord bør være melom 15 - 20 bokstaver som ikke bør inneholde ord som kommer fra typisk ordbok som gjør at det man være enkelt å kjøre brute-force angrep. Samtidig bør også varigheten på settes til at den ikke utløper eller så lenge som mulig. Det er derimot viktigere å ha MFA mekanismer på toppen. Tjenester som Azure AD Password Protection kan brukes for unngå at noen bruker standard ord som en del av passordene sine.
* Definere MFA for all tilgang. Tjeneste som Windows Hello for Business, eller tjenester som støtter SAML/OAuth bør brukes for tjenester for å kunne gi MFA kombinert med SSO for tilgang til tjenester. SAML/Oauth bør også brukes for å etablere integrasjoner mot andre SaaS tjenester slik at man så få brukerkontoer som mulig fra en brukerkontekst. 
* Bruk tjenester som Azure AD Identity Protection, Haveibeenpwnd.com eller f-secure identity protection for å overvåkning på sluttbrukerens identitet. Disse tjenestene kan gi indikasjon på om bruker informasjon er på avveie eller brukerkontoer har blitt kompromitert via en hacket 3.parts tjeneste. 
* Om man har Azure AD Connect sett på password hash sync (om det ikke er aktivert) dette vil også gjøre at Microsoft kan sammenligne hash med informasjon som sikkerhetsforskerene der finner på kompromiterte 3.parts sider å kan informere om bruker informasjon er på avveie. 
### Sårbarheter
* Sårbarheter er noe som blir funnet kontinuerlig, enten det er da sårbarheter i kjente produkter som Windows eller om det er sårbarheter tilknyttet egenutviklet tjenester. Ofte handler det om å ha automatisert oppdateringsmekanismer på plass som en sentralisert. Ofte er dette f.eks WSUS for Windows infrastruktur eller Windows Update for Business for klient via Intune eller Red Hat Satellite for Linux infrastruktur. Men utfordringen er 3.parts tjenester som ikke blir dekket av de sentralisrte patchesystemene. Da må man enten benytte 3.parts tjenester som Qualys eller Rapid7 produkter for å få kontinuerlig informasjon om sårbarheter. Eller at man må kontinuerlig overvåke applikasjonslandskapet å følge med på sikkerhetspatcher som kommer fra leverandørene. Man kan også se her for en kompilert liste over standard sårbarheter ransomware aktører har utnyttet de siste årene --> https://www.bleepingcomputer.com/news/security/researchers-compile-list-of-vulnerabilities-abused-by-ransomware-gangs/ 
### Nettverk
* Forsikre dere om at ingen unødvendige tjenester er eksponert ut. Mange ransomware angrep starter som oftest av maskiner som blir kompromiterte som er feil konfigurert som f.eks en Windows Server med RDP som er aktiv. 
* For tjenester som er eksponert pass på at kun godkjente tjenester er tilgjengelige, slik at tjenester som f.eks SMB (filtrafikk) er tilgjengelig ut mot Internett. 
* Om tjenester som RDP skal være tilgjengelig eksternt må det være MFA tjenester på plass. 
* Om man driver med ecommerence eller nettshop løsning, se på desentralisert brannmur tjenester for å forhindre at DDoS trafikk blir rutet mot eget datasenter eller mot hosting leverandør. 
### Klienter
* Definere en standard Group Policy for hvilken standard applikasjoner som skal brukes for åpning av filer som HTA, JS eller lignende. Norsk Helsenett har definert en standard liste som er grei å følge --> https://www.nhn.no/Personvern-og-informasjonssikkerhet/helsecert/anbefalte-sikkerhetstiltak/blokkering-av-script-og-programfiler
* Macroer tilknyttet Microsoft Office bør deaktiveres eller begrenset kun til å kjøre fra godkjente lokasjoner. Finnes også en rekke tiltak her som bør følges --> https://adsecurity.org/?p=3299
* Benytt tjenester som Identity Guard (Benyttes for å forhindre lesetilgang til LSASS som typisk brukes for å hente ut lokal brukerdatabase) Application Guard (Gjør at tjenester som Microsoft Edge, Office kan kjøres i en egen container som er isolert fra resten av operativsystemet)
* Fjern at brukeren kjører som lokal administrator, ha eleveringsmulighet med f.eks bruk av https://github.com/pseymour/MakeMeAdmin/wiki
* Forsikre seg om at tjenester som antivirus og (eventuelt EDR) tjenester er innstallert og oppdatert på alle klienter. (Her er en god oversikt på gode antivirus leverandører --> https://www.av-comparatives.org/tests/real-world-protection-test-july-august-2021-factsheet/)
* Om man bruker Microsoft Edge eller Google Chrome ha Password Monitoring aktivert i nettleseren.
* Ha regelsett på plass for nettleseren via Group Policy for å forhindre at det ikke er tillatt å surfe på nettsider med et self-signed sertifikat. Samt verifisere at Safe Browsing og Smartscreen filter er aktivert.
* Tilby login via bruk av tjenester som Windows Hello for Business eller tjenester som støtter WebAuth ved login som gjør at man kan logge inn med bruk av f.eks hardware nøkler som Yubikey. 
* Ha utvidelser eller extensions som blokkerer pop-ups. 
* Flytt klienten ut av Active Directory og ut til Azure Active Directory. All ransomware kode som er laget i dag som tar utgangspunkt i en kompromitert klient er laget for å deretter bevege seg videre innover i infrastrukturen via Active Directory. Ved å flytte klienten ut til Azure AD tar man i prinsippet bort denne muligheten. Det samme prinsippet gjelder for Chromebooks/tynnklienten hvor det er liten til null sjans for å kompromitere endepunktet. 
* Bruk Attack Surface Reduction rules til å aktivere regelsett mot at Microsoft Office skal få lov til å starte "child processes" som var utnyttet i forbindelse med siste MSHTML sårbarhet. 
* Deaktiver autorun
* Eventuell tilgang til sentrale tjenester bør følge et zero-trust prinsipp. Hvor ihvertfall bruker og enhets kontekst bør evalueres før tilgang gis. Som f.eks via Conditional Access. 
### Epost
* Forhindre mottak av filer med spesifkke filtyper. (https://docs.microsoft.com/en-us/exchange/troubleshoot/email-delivery/how-to-block-message-from-being-sent-or-received)
### Windows Infrastruktur
* Slå av bruk av eldre versjoner av SMB fil protokollen. Mange har oppgraderte Windows fil servere som i mange sammenhenger fortsatt har eldre versjoner av SMB som har en del sårbarheter. Disse bør skrus av/deaktivere å man bør passe på at kun SMB 3 er mulig å bruke. 
* Aktiver SMB Signing - Dette gjøres via Group Policy
* Avinnstaller eldre versjoner av PowerShell. PowerShell kan ha flere versjoner innstallert samtidig. Mange Ransomware script prøver å kjøre via PoewrShell v1 pga mangel av logging og sikkerhetsmekanismer. Verifiser at siste versjon er tilgjengelig på Windows Servere. Det bør ihvertfall være fra versjon 5 og oppover innstallert. 
* Forsikre også at PowerShell har script block aktivert, samt transaksjons logging slik at man kan logge all bruk av PowerShell. 
* Innstallere Windows LAPS (Local Administrator Password Solution) dette for å automatisk rotere lokal administrator passord på maskinene. 
* Definer Group Policy for å skru på "Deny log on trough Remote Desktop Services" Mange ransomware aktører benytter RDP for å logge på andre servere i infrastrukturen, ved å angi denne group policyen kan man begrense hvilken kontoer som får lov til å logge på miljøet. 
* Slå av Widows tjenester som ikke skal brukes på aktuelle servere. Som f.eks domene kontrollere har ikke behov for Print Spooler tjenesten å bør skrus av der. 
* Om man benytter noen provisjoneringstjeneste for enten Citrix eller templates for VMware, er det viktig å ha en rutine på plass for å huske å oppdatere image jevnlig med de siste sikkerhetsoppdateringene. 
* Unngå helst bruk av tradisjonell RDP som managmenet løsning, men om det kreves bruk ihvertfall Remote Credential Guard for å unngå eventuelle pash-the-hash angrep. Eller bruk av Protected Privileged Accounts som krever domene nivå satt til 2012 R2 men forhindrer at man kan logge inn med NTLM eller delegert tilgang.  
* Sett antall cached credentials til null (med mindre det er et Citrix miljø) 
### Skytjenester
* For SharePoint/Onedrive definer policier hvor man angir godkjente filtyper som kan synkroniseres via OneDrive. (Set-SPOTenantSyncClientRestriction -ExcludedFileExtensions « exe;js;hts") 
* Ha Conditional Access regelsett på plass som deaktiverer legacy protokoller i Azure AD. 
### Generelle tiltak
* Backup tjenesten bør være frakoblet fra virtuell infrastruktur samt Active Directory. I mange sammenhenger har vi sett at backup data har blitt kryptert sammen med resten av infrastrukturen. Man bør redusere risikoen for at backupen blir infisert derfør bør backup løsningen kjøre isolert med egne brukeridentitet. 
* Følge 3-2-1 reglene i forhold til backup. At man har 3 kopier av data (produksjonsdata samt 2 backup kopier) på 2 ulike medier samt med en kopi offiste. 
* Verifiser backup dataene ofte, har rutiner på plass. Samt at flere backup levernadører kan nå tilby automatisert sjekk av data som bør settes opp som en automatisert jobb.
* Bruk immutable backup data om mulig. Dette forhindrer at ransomware aktører kan overskrive backup data (ved å f.eks kryptere innholdet) men krever at man har en backup leverandør som supporterer dette.
* Eksterne web-tjenester hvor man er usikker på angrepsflaten bør plasseres bak en WAF (Web Application Firewall) tjeneste. 
### Data og informasjon
* Se på mulighet for kryptering av sensitiv data. F.eks filer som databaser eller filer som inneholder sensitiv informasjon bør krypteres med type DLP tjenester for å unngå at informasjon kommer på avveie. Flere tjenester er tilgjenglig til f.eks SQL Server som kan kryptere informasjon slik data ikke kan leses direkte selv om uvedkommende har fått tak i data filene til databasen. Det finnes også tjenester som kan automatisk klassifisere og kryptere data basert på innhold som f.eks Microsoft AIP. 
### Overvåkning
* Ha en sentralisert loggingstjeneste for overvåkning av bruker aktivitet. Viktige elementer og eventIDer som man bør følge med på er (Event ID 4625 (Failet pålogging), 4740 (konto last ute) eller 1102 (Event Cleared) her er også en kompilert liste over eventer man bør ha aktivert --> https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/audit-policy-recommendations. For sentralisert overvåkning kan man benytte Windows Event Forwarding, SCOM Audit Collector, Splunk, ELK eller skytjenester som Azure Sentinel. 
* Prosess overvåkning - Mange ransomware aktører bruker også tjenester som Anydesk, Teamviewer, Bloodhound, PSEXEC og annet for å kartlegge eller ha en enkel måte å gi tilgang til infrastrukturen på. Se på muligheten for å få sentralisert overvåkning på disse angitte prosessene som kan enten gjøres via EDR verktøy eller bruk av Sysmon fra Sysinternals pakken å deretter definere overvåknignsregler. 
* Ha DNS Overvåkning - Man kan også forhindre og blokkere phising angrep, eller at tjenester prøver å oppnå kommunikasjon tilbake til noen Command og Control tjenester ved å forhindre dette på DNS nivå. Det finnes DNS tjenester som kan brukes som f.eks Cloudflare for Teams, Cisco Umbrella som forhindrer DNS oppslag mot mistenkelig DNS domener. Samtidig bør man også ha DNS overvåkning på plass for å kunne se etter mistenkelig domener som det har blitt gjort oppslag mot. 
* Flere ransomware aktører benytter nå også nyere protokoller for innhenting av script og annen payload via tjenester som f.eks HTTP/3 som i dag effektivt ikke kan inspiseres via brannmur eller proxy tjenester. Man bør også ha en EDR/XDR tjenester på sluttbrukerens maskiner for å kunne se på nettverksflyten. 
* Logg trafikk også tilknyttet TerminalServices-RemoteConnectionManager samt Security og SMB loggene jevnlig for å se etter unormal aktivitet. 


