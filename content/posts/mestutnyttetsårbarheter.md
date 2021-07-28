---
title: "Vanligste sårbarhetene i 2020/2021"
date: 2021-07-28T15:09:25+02:00
draft: false
tags: [""]
author: "Me"
# author: ["Me", "You"] # multiple authors
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
U.S. Cybersecurity og Infrastructure Security Agency (CISA) har sammen laget en liste med de (top 30) vanligste sårbarhetene som blir utnyttet i angrep, basert på historiske data fra 2020 (samt sålangt i 2021) 

Du kan se listen over de ulike sårbarheten her --> https://us-cert.cisa.gov/ncas/alerts/aa21-209a PDF utgave her --> https://us-cert.cisa.gov/sites/default/files/publications/AA21-209A_Joint%20CSA_Top%20Routinely%20Exploited%20Vulnerabilities.pdf 

Sårbarhetene kommer fra en ulike rekke leverandører. Basert på historikk data fra 2020, er følgende de meste utnyttet sårbarhetene: 

* Citrix - CVE-2019-19781 - arbitrary code execution
* Pulse - CVE 2019-11510 - arbitrary file reading
* Fortinet - CVE 2018-13379 - path traversal
* F5- Big IP - CVE 2020-5902 - remote code execution (RCE)
* MobileIron - CVE 2020-15505 - RCE
* Microsoft - CVE-2017-11882 - RCE
* Atlassian - CVE-2019-11580 - RCE
* Drupal - CVE-2018-7600 - RCE
* Telerik - CVE 2019-18935 - RCE
* Microsoft - CVE-2019-0604 - RCE
* Microsoft - CVE-2020-0787 - elevation of privilege
* Microsoft - CVE-2020-1472 - elevation of privilege

Vi så blant annet at Citrix sårbarheten alene kunne påvirke opptil 850 organisasjoner i Norge. Samt blant annet CVE-2021-26855 (Microsoft Exchange) som ble utnyttet mot Stortinget som gjorde det mulig for angripere å hente ut Epost kontoer fra den lokale Exchange databasen ved å kjøre egendefinert kode mot OWA/EXC. 

I 2021 fortsetter angripere å benytte seg av målrettet sårbarheter mot enheter/tjenester som er offentlig tilgjengelig. Blant de som er svært utnyttet så langt i 2021, er sårbarheter i Microsoft, Pulse, Accellion, VMware og Fortinet.

De har også kompilert en liste over de ulike CVEene med tiltak man kan gjøre for å fikse opp i de ulike sårbarhetene. 




