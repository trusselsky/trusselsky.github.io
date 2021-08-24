---
title: "DDoS angrep og trender fremover"
date: 2021-08-24T08:16:36+02:00
draft: false
tags: [""]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: false
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

Tidligere i sommer stoppet Cloudflare det som er beskrevet som det største DDoS angrepet noensinne, med lit over 17.2 millioner forespørsler-per-sekund over HTTP trafikk (som ofte gjøres for å kamuflere angrepet som mer legitim trafikk). Til sammenligning så håndterer Cloudflare som i dag leverer cirka 13% av all HTTP trafikk på verdensbasis, ca 25 millioner forespørsler-per-sekund. Motivet bak å kjøre DDoS angrep er for å kunne gjøre tjenester utilgjengelig eller for å ta ned infrastruktur med å overbelaste systemene. 

![ddos](/ddos.jpg)

Ofte kjøres slike angrep fra kontrollerte Botnet. Som er maskiner som er infisert med malware som igjen blir styrt av en Botnet Operatør for å kunne utføre DDoS angrep. 

Samtidig kan vi også se at det skjer flere DDoS mot Norge organisasjoner, som man kan se mer info av her --> (https://radar.cloudflare.com/no) som ofte gjøres av ulike årsaker. 

1: For å gjennomføre et ransomware angrep (Enten betaler du X antall kroner eller så vil din tjeneste være utilgjengelig) Dette har vi sett også kan gjøres samtidig som hackere gjør angrep via andre vektorer også. Dette er blant annet noe som ble gjort mot Vinmonopolet i fjor høst --> https://www.digi.no/artikler/hackerne-tok-ned-vinmonopolet-no-i-dag-har-de-varslet-et-mye-verre-angrep/504268

2: For å gjøre en tjeneste utilgjengelig, enten politisk mål eller andre årsaker. 

Samtidig vil vi se en trend fremover med flere DDoS angrep. Litt av bakgrunn for dette er fordi at flere applikasjoner og tjenester nå bytter gradvis over til å bruke UDP basert transport i stedet for tradisjonelle TCP. Dette da for å kunne redusere latency å andre hopp frem og tilbake på kommunikasjon samt gi en bedre brukeropplevelse på noen tjenester. På toppen av UDP er det flere nå som benytter DTLS som protokoll. DTLS er en protokoll som er hybrid som gir same pålitelighet som TCP men levert via UDP. Spesielt er det tjenester som Citrix HDX, Microsoft RDP samt Zscaler og noen VPN leverandører som DTLS som kommunikasjonsprotoll.

![DTLS](/dtls.jpg)

En grunn til at dette vil gi flere DDoS angrep er pga hvordan de ulike leverandørene har implementert DTLS protokollen. Som en del av standarden er det en attributt som er angitt i standarden som en opsjon (å er derfor ikke nødvendig). Denne atributten gjør at om noen initierer et angrep mot en tjeneste via DTLS, vil tjeneren svare med en Cookie under (HelloVerifyRequest) for å forsikre seg om at kommunikasjonen kommer fra en legitim klient, den kommunikasjon blir etablert. For tjenester som ikke har implementert denne attributten på tjenester som bruker DTLS vil angripere i visse sammenhenger kunne utnytte dette for et omvendt DDoS angrep. 

De siste årene har det vært en svakhet som har kommet frem både fra Microsoft RDP (via RD Gateway) og Citrix NetScaler ADC (for Citrix sesjoner) du kan også lese en eldre artikkel her fra Palo Alto om problematikken som var tidligere på Microsoft --> https://unit42.paloaltonetworks.com/dtls-vulnerabilities-cve-2014-6321/

 Den andre utfordringen er at mer og mer av vanlig web trafikk beveger seg over til å bruke HTTP/3 som nå begynner å bli ferdig som en standard. Statistikk som man kan se her, så er cirka 10% av all trafikk som går mot Norske sider via Cloudflare basert på HTTP/3 --> https://radar.cloudflare.com/no du kan også lese mer om HTTP/3 her --> https://trusselsky.no/posts/http3ogfremtiden/
 Utfordringen ligger i trafikk inspeksjon. Mange av dagens brannmur/sikkerhetstjenester er avhengig av å kunne inspisere trafikken for å kunne avdekke angrep eller skadelig innhold. Med HTTP/3 så er det ikke mulig å få direkte inspeksjon av innholdet å derfor vil det vær enklere for angripere å kunne kamuflere innholdet når de gjennomfører et angrep. Samtidig så legger HTTP/3 mer trykk på serveren i form av ressurser for å håndtere kommunikasjonen, som gjør også at et DDoS angrep via HTTP/3 vil ikke kreve like mye trafikk for å kunne ta ned en tjeneste. 

Heldigvis har vi ennå ikke sett store angrep som har blitt gjort via HTTP/3, men basert på trenden vil nok dette også øke fremover --> https://blog.cloudflare.com/ddos-attack-trends-for-2021-q2/ som man må være varsom til nettverksaktivitet mot eksterne tjenester. Spesielt om man som virksomhet leverer f.eks nettbutikker kan man være veldig utsatt for slike angrep. 





