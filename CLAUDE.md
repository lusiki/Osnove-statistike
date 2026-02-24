# Osnove statistike — Quarto Website

## Opis projekta

Ovo je web stranica kolegija "Osnove statistike" na HKS-u, izrađena u Quartu. Stranica se renderira lokalno s `quarto preview` i automatski objavljuje na GitHub Pages putem GitHub Actions.

## Tip projekta

Quarto website (`project: type: website`).

## Konvencije za sadržaj

### Organizacija datoteka

- Predavanja: `lectures/week-NN.qmd` (jedno po tjednu, 15 ukupno)
- Resursi: `resources/` (reading-list.qmd, tools.qmd, datasets/)
- Projekt: `projects/practical-project.qmd`
- Slike: `assets/images/`
- Slajdovi: `assets/slides/`

### Stil pisanja

- Jezik: hrvatski
- Ton: narativni, poput poglavlja knjige (ne slajdovi, ne bilješke)
- Uzor: Danielle Navarro, "Learning Statistics with R"
- Primjeri: iz komunikologije i modernih medija (ne psihologija)
- Statistički koncepti se objašnjavaju svakodnevnim jezikom prije formalnih definicija

### R kod konvencije

- **Isključivo tidyverse** pristup (ne base R, osim za statističke testove)
- Pipe operator: `|>` (base R pipe, ne magrittr `%>%`)
- Vizualizacija: ggplot2 (nikad base R plot funkcije)
- Podatkovne strukture: tibble (ne data.frame)
- Svaki code chunk mora imati `#| label:`, `#| echo: true`, `#| message: false`, `#| warning: false`

### Životni ciklus predavanja

1. Placeholder sa `draft: false` i napomenom "sadržaj dolazi uskoro"
2. Pisanje punog narativnog sadržaja s R kodom
3. Revizija i poliranje

### Git radni tok

- Main branch za produkciju
- `freeze: auto` za zamrzavanje R code outputa lokalno
- `_freeze/` direktorij se commitira u git
- GitHub Actions koristi zamrznute rezultate (ne izvršava R)

### Objava

- Automatska via GitHub Actions na push u main
- Ručna via `workflow_dispatch`

## Ovisnosti

- Quarto (>= 1.3)
- R (>= 4.3) s paketima: tidyverse, broom, janitor, scales, patchwork
