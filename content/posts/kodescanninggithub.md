---
title: "Sårbarhetsscanning med GitHub mot kjente rammeverk"
date: 2021-07-29T13:20:04+02:00
draft: false
tags: ["GitHub", "Terraform", "GitHub CodeScanning"]
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

Den (28/07) Annonserte GitHub at som en del av Code Scanning tjenesten de leverer at de nå har kommet med 15 nye integrasjoner med åpne kildekode rammeverk som dekker rammeverk som Ruby, PHP, Switch, Terraform, PowerShell og Kubernetes YAML. 

Code Scanning funksjonen ble lansert i 2020 som er tilgjengelig for alle offentelige repositories samt for Private repositories (Krever GitHub Advanced) men gjør at man kan se igjennom kildekoden etter sårbarheter. 

## Hvordan sette opp Code Scanning ##
Code Scanning kan aktiveres ved å gå inn på et **Repository --> Security --> Overview --> Code Scanning** 

![Code Scannning](/githubcodescanning.JPG)

Deretter må man velge basert på hvilken rammeverk man benytter. Man kan benytte seg av de innebydge arbeidsflyten som er egen basert på definert rammeverk eller man kan bruke CodeQL Analysis

## GitHub Actions med CodeScanning med Terraform ## 

Med et eksempel her, skal vi vise hvordan man kan bruke Code Scanning sammen med tfsec for å scanne et Github repository som inneholder Terraform kode for å se etter ikke-sikker konfigurasjon. 
Code Scanning benytter GitHub Actions, hvor tjenesten vil via en Ubuntu-Worker laste ned innholdet i GitHub repositoriet.  Som et eksempel her har vi laget følgende.

* Fork innholdet i repositoriet her --> https://github.com/snyk/terraform-goof
* Gå inn på **Security --> Overview --> Code Scanning --> Velg tfsec fra listen** klikk Setup this workflow. 
![TFSEC](/tfsec.JPG)  Dette vil da lage en Github Actions Workflow i ditt repository som vil kjøres hver gang ny kode sjekkes inn. Konfigurasjon vil du kunne se under ./guthub/workflows mappen.  Du kan se et eksempel på det her --> (https://github.com/trusselsky/terraform-goof)

* Om du vil sette opp workflow direkte fra lokale IDE og pushe konfigurasjon via Git kan du bruke følgende template. 
```
name: tfsec

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]  
  schedule:
    - cron: '15 13 * * 5'

jobs:
  tfsec:
    name: Run tfsec sarif report
    runs-on: ubuntu-latest
    permissions:
      actions: read
      contents: read
      security-events: write

    steps:
      - name: Clone repo
        uses: actions/checkout@v2

      - name: Run tfsec
        uses: tfsec/tfsec-sarif-action@9a83b5c3524f825c020e356335855741fd02745f
        with:
          sarif_file: tfsec.sarif         

      - name: Upload SARIF file
        uses: github/codeql-action/upload-sarif@v1
        with:
          # Path to SARIF file relative to the root of the repository
          sarif_file: tfsec.sarif  
```
**NB:** Tfsec har en del innebygget sjekker mot ulike providere i Terraform, mer informasjon kan finnes her (https://tfsec.dev/docs/installation/)

Når flyten er implementert vil den gå igjennom kildekoden å laste opp eventuelle resultat inn i en SARIF fil. Github vil lese innholdet i den genererte SARIF filen for å vise alarmer som kommer frem. Du kan se resultatet under Security --> Code Scanning Alerts

![CodeScanning](/codescanningalerts.JPG)

