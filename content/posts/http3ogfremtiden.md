---
title: "HTTP/3 og fremtidens websikkerhet"
date: 2021-08-05T21:56:46+02:00
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

Arbeidsgruppen i IETF begynner å komme i mål med HTTP/3 standarden som vil påvirke både ytelsen og sikkerheten på all nett-trafikk, så hva er de viktigste endringene å hvordan påvirker det også sikkerheten? 

## Historien så langt ##

Det skjer for tiden veldig mye utvikling på teknologifronten når det gjelder web og hvordan vi kommuniserer med netttjenester. 
Når man åpner en nettleser mot f.eks vg.no vil enhenten du sitter på benytte en rekke nettverksprotokoller for å kommunisere med VG sin infrastruktur. 

Protokollen som benyttes i bunn på nettleser trafikk er HTTP. HTTP har eksistert lenge og majoriteten av nettlesern trafikken i dag benytter HTTP 1.1 protokollen (som har eksistert siden 90-tallet).
Problemet med den protokollen var (og er) all trafikk blir sendt i klartekst, derfor måtte man lage en ny versjon av denne protokollen som her HTTPS som krypterer innholdet mellom tjenester og enhet. Her benyttet man til og begynne med SSL og deretter TLS protokollen som krypteringsprotokoll for å kryptere innholdet mellom klient og tjener. 

HTTP benytter TCP som kommunikasjonsprotokoll for overføring av data, som også gjør den sårbar for pakketap eller høy latency. Kombinert med TLS kommunikasjonen fører til høyere tid mellom klient og tjenester for å få etablert kommunikasjon. 

HTTP 1.1 som protokoll har også en del svakheter blant annet at den ikke støtter multiplexing på en god måte som gjør at HTTP trafikk som kommer fra ulike tjenere må vente i tur. Samtidig med f.eks HTTP/2 kom de også med multiplexing som gjør at man ikke får dette problemet. Samtidig introduserte de også blant annet HPACK (Header Compression) som gjør at man reduserer båndbredden. 

Når HTTP/2 standarden kom valgte også flere leverandører og kreve at all kommunikasjon som skulle støtte HTTP/2 måtte bruke TLS som standard. Som gjorde blant annet f.eks ulike nettlesere som Firefox, Chrome og Edge krever HTTPS når man skal bruke HTTP/2 som protokol. 

**NB:** Med TLS 1.3 prøver man å redusere tiden det tar å etablere kommunikasjon mellom klient og tjener ved å benytte. Her ser man en sammenligning mellom TLS 1.2 over HTTP mot TLS 1.3

![TLS13](/tls12vs13.jpg)

Samtidig som utviklingen har pågått med å prøve å sikre kommunikasjonen (som også i utgangspunktet har ført til tregere kommunikasjon og flere forsinkende ledd) har web utviklingen rast videre, hvor vi nå har mye mer multimedia innhold (bilder,videoer) mye mer 3.parts biblotek og eksterne tjenester. Før var nettleser trafikken mer statisk innhold, hvor det nå har blitt til mye dynamisk innhold og store rammeverk (CMS) med mer multimedia og streaming mekanismer som gjør at man må ha en transport mekanisme som kan overføre data mer effektivt. 

## Sikkerhet og inspeksjon ## 

Med introduksjon av SSL/TLS krypteringsprotokollene betydde dette at kommunikasjon ble kryptert. (dog dette betyr ikke at innholdet nødvendigvis er trygt)

{{< tweet 187572289724887041 >}}

Med mer ondsinnet trafikk som gikk over nett betydde dette at flere måtte begynne å bruke tjenester for å kunne analysere innholdet (som i dag tilbys av de fleste brannmur/proxy leverandører). Dette  kunne da analysere innholdet etter f.eks ondsinnet trafikk eller beskytte brukere fra ukjente adresser eller annet innhold. Flere leverandører bruker også lignende mekanismer for å kunne kategorisere innhold samt definere hvilken applikasjon/tjeneste som en bruker kobler seg opp i mot. Dette betyr i prinsippet at proxy/brannmur tjenesten dekrypterer innholdet for å kunne "se" hva som skjer i trafikk strømmen før trafikken blir kryptert igjen og sendt videre, som en type MiTM (Man-in-the-middle) tjeneste. 

Denne mekanismen ble også brukt for lastbalanseringstjenester der man kunne balansere trafikk basert på spesifikt innhold. 

## Hvorfor HTTP/3 ? ##

Allerede nå er det mange nettsider/leverandører som har beveget seg videre til HTTP/3, som man ser her så er cirka **13% av all kommunikasjon går via HTTP/3 protokollen** Som store leverandører som Google, AWS og Cloudflare, mens resten er fordelt på HTTP 1.1 og HTTP/2 (Statistikk fra Cloudflare Radar siste 30 dagene) som også er supportert av de fleste moderne nettlesere. 

![HTTP/3 Bruk](/http3.jpg)

Men man ser også at HTTP/3 har vesentlig forbedret tiden det tar både å etablere kommunikasjon samt også hvordan håndtere pakketap. 

![HTTP3](/http2-http3.png)

Så er forandret i HTTP/3 ? 

* I stedet for TCP benytter HTTP/3 seg av QUIC (Quick UDP Internet Connections) som overføringsprotokoll som er bygget på UDP. Men samtidig tilbyr flere av TCP egenskapene som pålitlighet og overbelastingskontroll algoritmer som f.eks CUBIC eller New Reno. (Dette krever dog at UDP/443 er åpnet i brannmuren)
* Benytter seg QPACK for komprimering av HTTP headere (Sammenlignet med HPACK som ble brukt i HTTP/2)
* Krever TLS kryptering for kommunikasjon (Var ikke et krav i HTTP/2, selv om flere leverandører krevde det) 

Samtidig er også kryptering som før har blitt håndtert av TLS nå gjort direkte i kommunikasjonsprotokollen som gjør at trafikk inspeksjon som før ble gjort av brannmurer/proxy tjenester ikke lenger er mulig. 

## Hvordan sikre trafikk fremover ? ## 

Med mer og mer av internett trafikken beveger seg mot bruk av HTTP/3 samtidig som standarden blir ferdigstilt, betyr dette også at flere organisasjoner må ta stilling til hvordan det skal håndtere HTTP/3 trafikken. Flere leverandører nå begynner å komme med støtte for HTTP/3

* Blant annet så kommer nå Microsoft med en ny versjon av SMB som også støtter QUIC (https://techcommunity.microsoft.com/t5/itops-talk-blog/smb-over-quic-files-without-the-vpn/ba-p/1183449)
* Google Cloud støtter QUIC (https://cloud.google.com/blog/products/networking/cloud-cdn-and-load-balancing-support-http3)
* Citrix ADC Quic (https://docs.citrix.com/en-us/citrix-adc/current-release/system/quic.html)

Akkurat nå er det få til ingen brannmur/proxy leverandører som supporterer inspeksjon av QUIC og HTTP/3 og den generelle anbefalingen er å deaktivere de protokollene i brannmuren, men dette gjør at klientene som sitter på innsiden vil falle tilbake til HTTP 1.1 med TLS. Samtidig beveger flere seg på utsiden av den tradisjonelle brannmuren ved å jobbe fra hjemme eller andre lokasjoner, som gjør at den tradisjonelle brannmuren mister litt av den orginale hensikten ved å beskytte trafikken mellom innsiden og utsiden. 

Derfor vil det være viktig fremover å se på løsninger som gir mer innsikt direkte fra endepunktet perspektivet for å kunne ivareta sikkerhet på samme måte, men samtidig ivareta forbedringene som HTTP/3 kommer med. 

