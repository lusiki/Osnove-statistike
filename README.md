# Osnove statistike

Web stranica kolegija "Osnove statistike" na HKS-u.

## Tehnički stack

- [Quarto](https://quarto.org) website
- R + tidyverse za analitički kod
- GitHub Pages za hosting
- GitHub Actions za automatski deployment

## Lokalno pokretanje

```bash
quarto preview
```

## Renderiranje za produkciju

```bash
quarto render
```

## Struktura

```
├── _quarto.yml          # Konfiguracija stranice
├── index.qmd            # Početna stranica
├── syllabus.qmd         # Silabus kolegija
├── schedule.qmd         # Tjedni raspored
├── lectures/            # Predavanja (week-01 do week-15)
├── resources/           # Literatura, alati, dataseti
├── projects/            # Praktični projekt
├── assets/              # Slike i slajdovi
├── styles.css           # Prilagođeni CSS
└── .github/workflows/   # GitHub Actions
```

## Licenca

Sadržaj kolegija je vlasništvo autora. Strukturalni pristup inspiriran knjigom "Learning Statistics with R" (Danielle Navarro, CC BY-SA 4.0).
