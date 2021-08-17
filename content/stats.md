---
title: "Stats"
date: 2021-08-07T01:50:33+02:00
draft: true
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
Denne viser ulikk statistikk fra honeypot miljøet vårt. Hvor vi blant annet måler eller kjente IP addresser som blir brukt for ondsinnet formål.<br/>  Data kommer fra vårt Azure miljø å blir oppdatert ved neste datainnsamling. (Historiske data viser de siste 30 dagene) (Oppdatert 17. August) 

[![made-with-Markdown](https://img.shields.io/badge/Made%20with-Markdown-1f425f.svg)](http://commonmark.org) [![GitHub commits](https://img.shields.io/github/commits-since/Naereen/StrapDown.js/v1.0.0.svg)](https://github.com/trusselsky/trusselsky.github.io/commits/)

### Feilet pålogging via RDP - Land ###
Tabellen under viser påloggingsforsøk mot Windows Honeypot miljøet, basert på spesifikk EventID og hvilken IP addresser som er oftest brukt. Denne viser blant annet påloggingsforsøk via RDP og er filtrert etter topp 15 IP-addresser. 

{{< table "" >}}

### Feilet pålogging via RDP - UPN ###
Tabellen under viser påloggingsforsøk mot Windows Honeypot miljøet, basert på mest brukte kontonavn (UPN).

{{< tableaccount "" >}}

### Trafikk port - Land ###
Tabellen under viser påloggingsforsøk mot Windows Honeypot miljøet, basert på mest brukte kontonavn (UPN).

{{< tableprocess "" >}}