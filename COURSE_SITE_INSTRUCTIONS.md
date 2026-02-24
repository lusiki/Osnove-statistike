# Upute za izradu stranice kolegija

## Što želim

Quarto web stranicu za sveučilišni kolegij koja se renderira lokalno u Positronu i objavljuje na GitHub Pages. Struktura, stil i radni tok moraju biti identični onima opisanim ispod.

## Tehnički stack

Quarto website projekt (`project: type: website` u `_quarto.yml`). Renderira se s `quarto preview` lokalno i automatski se objavljuje na GitHub Pages putem GitHub Actions workflowa. Sve je markdown (.qmd datoteke) s ugrađenim R code chunkovima koji se izvršavaju tijekom renderiranja.

## Struktura repozitorija

```
ime-kolegija/
├── _quarto.yml              # Konfiguracija stranice
├── index.qmd                # Početna stranica s pregledom kolegija
├── syllabus.qmd             # Cjelokupni silabus
├── schedule.qmd             # Tjedni raspored s praćenjem statusa
├── lectures/
│   ├── _metadata.yml         # Zajedničke postavke za predavanja
│   ├── week-01.qmd          # Jedno predavanje po datoteci
│   ├── week-02.qmd
│   └── ...
├── resources/
│   ├── reading-list.qmd     # Popis literature po tematskim klasterima
│   ├── tools.qmd            # Alati i platforme s informacijama o pristupu
│   └── datasets/            # Primjeri podataka za vježbe
├── projects/
│   └── practical-project.qmd # Upute za projekt s rubrikom
├── assets/
│   ├── images/
│   └── slides/
├── .github/
│   └── workflows/
│       └── publish.yml       # GitHub Actions za automatski deployment
├── .gitignore
├── styles.css                # Prilagođeni CSS (statusne oznake, stilovi)
├── CLAUDE.md                 # Konvencije projekta za Claude Code
└── README.md
```

Nema mape seminara. Seminarske aktivnosti opisuju se kao stupac u tablici rasporeda (schedule.qmd), ali ne dobivaju zasebne stranice ni navigacijski tab.

## Navigacija (navbar)

Gornja navigacija ima sljedeće tabove: Početna, Silabus, Raspored, Predavanja (dropdown s tjednima), Resursi (dropdown s Popis literature i Alati), Projekt. Nema taba Seminari.

## Konfiguracija (_quarto.yml)

Jezik: hr. Tema: cosmo (light) / darkly (dark). TOC uključen s dubinom 3. Pretraga uključena. Navbar pozadina: #1a1a2e, tekst: #e6e6e6. Footer: naziv kolegija | HKS godina, desno "Izrađeno pomoću Quarto". Ne koristiti `subtitle` pod `website` blokom jer starije verzije Quarta to ne podržavaju. Umjesto toga spojiti naslov i šifru u `title` polje. Ne koristiti `drafts: mode: visible` jer starije verzije to ne podržavaju.

## Predavanja (_metadata.yml i week-NN.qmd)

Zajedničke postavke u `lectures/_metadata.yml`:

```yaml
toc: true
toc-depth: 3
number-sections: true
format:
  html: default
  pdf:
    lang: en
  docx: default
```

`lang: en` pod pdf formatom je namjerno jer babel-croatian LaTeX paket ima problema s instalacijom na nekim sustavima. Tekst ostaje na hrvatskom, samo se zaobilazi LaTeX hyphenation problem.

Svaka datoteka predavanja ima YAML zaglavlje:

```yaml
---
title: "Tjedan N: Naslov"
subtitle: "Podnaslov koji objašnjava sadržaj"
date: 2025-02-01
categories: [kategorija1, kategorija2]
draft: false
---
```

Sve datoteke predavanja imaju `draft: false` od početka kako bi se renderirale. Placeholder datoteke (tjedni čiji sadržaj još nije napisan) sadrže minimalan tekst s napomenom da će sadržaj biti dodan.

## Stil pisanja predavanja

Ovo je najvažniji dio. Predavanja se pišu kao poglavlja knjige, ne kao bilješke ili slajdovi.

**Ton.** Tekuća proza koja se čita kao priča. Svaka sekcija gradi se na prethodnoj. Primjeri su konkretni i relevantni za studente komunikologije. Tehnički koncepti objašnjavaju se kroz analogije i svakodnevna iskustva. Pretpostavljati da su studenti inteligentni ali nemaju tehničko predznanje. Stil je jednostavan, zabavan i akademski istovremeno. Pomislite na ton Danielle Navarro u "Learning Statistics with R": prijateljski, iskren o tome što je teško, pun konkretnih primjera, s povremenim humorom, ali uvijek intelektualno pošten.

**Struktura jednog predavanja:**

1. Ishodi učenja (callout-note blok)
2. Uvodni hook koji objašnjava zašto je tema važna za komunikologe
3. Glavne sekcije sadržaja pisane kao tekuća proza s podnaslovima
4. Praktični savjeti uokvireni u callout-tip blokove
5. Važne napomene u callout-important blokovima
6. R code chunkovi ugrađeni u narativ (ne odvojeni od teksta, nego isprepleteni s objašnjenjima)
7. Ključni zaključci (callout-important blok, numerirana lista)
8. Priprema za sljedeći tjedan (callout-warning blok s konkretnim zadacima)
9. Dodatno čitanje (obavezno + preporučeno, s linkovima)
10. Pojmovnik (tablica s pojmovima i objašnjenjima)

**Formatiranje.** Koristiti Quarto callout blokove (.callout-note, .callout-tip, .callout-important, .callout-warning). Blockquote (>) za ključne metafore. Horizontalne crte (---) kao vizualne separatore između velikih sekcija. Pisati u odlomcima, ne u nabrajanjima. Izbjegavati pretjerano korištenje dvotočki, crtica i navodnika u tekstu.

## Silabus (syllabus.qmd)

Sadrži kontekst kolegija (studij, godina, ECTS, opterećenje), narativ kolegija koji objašnjava logiku rasporeda tema, zatim opis svakog tjedna predavanja kao jednog odlomka tekuće proze koji objašnjava što se obrađuje, zašto je to bitno i kako se nadovezuje na prethodne tjedne. Na kraju tablica seminarskih aktivnosti, popis literature organiziran po tematskim klasterima i opis ocjenjivanja.

## Raspored (schedule.qmd)

Tablica s kolonama: Tjedan, Datum, Tema predavanja (link na lectures/week-NN.qmd), Seminarska aktivnost (samo tekst, bez linka), Status. Status koristi CSS klase: .badge-upcoming, .badge-current, .badge-completed. Datumi su inicijalno TBD. Ispod tablice sekcija s datumima ocjenjivanja i prostor za bilješke sa sesija.

## Početna stranica (index.qmd)

Kratki opis kolegija, osnovni podaci u callout-note bloku (studij, semestar, ECTS, opterećenje, nositelj s email linkom, konzultacije), opis strukture kolegija u tri cjeline, tablica s brzim pristupom (linkovi na silabus, raspored, literaturu, alate, projekt) i sekcija za obavijesti.

## Resursi

**reading-list.qmd** organiziran po tematskim klasterima, ne kronološki. Obavezna literatura označena s [O]. Svi obavezni izvori besplatno dostupni online ili putem knjižnice.

**tools.qmd** sadrži tablice alata organiziranih po kategorijama s kolonama: Alat, Namjena, Pristup. Na kraju callout-tip o studentskim računima i besplatnim razinama.

## Projekt (practical-project.qmd)

Pregled zadatka, scenariji (2 do 3 opcije), popis onoga što se predaje (4 do 5 stavki), rubrika kao tablica s kriterijima i opisima za izvrsno/zadovoljavajuće/nedovoljno, rokovi kao tablica, FAQ sekcija.

## CSS (styles.css)

Prilagođeni stilovi za statusne oznake (.badge-completed zelena, .badge-upcoming siva, .badge-current plava s pulse animacijom), stilove za stranice predavanja (.learning-objectives, .key-takeaways, .next-week-preview s lijevim borderima u boji) i općenite prilagodbe (šire područje sadržaja, ljepše tablice).

## GitHub Actions (.github/workflows/publish.yml)

```yaml
on:
  workflow_dispatch:
  push:
    branches: main

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pages: write
      id-token: write
    steps:
      - name: Check out repository
        uses: actions/checkout@v4
      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2
      - name: Render and Publish
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
          render: true
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## .gitignore

```
/.quarto/
/_site/
/_freeze/
.Rproj.user
.Rhistory
.RData
.Ruserdata
*.Rproj
.DS_Store
Thumbs.db
```

## CLAUDE.md

Sadrži opis projekta, tip projekta (Quarto website), konvencije za sadržaj (organizacija datoteka, stil pisanja, ton kolegija, životni ciklus predavanja, git radni tok, objava) i ovisnosti.

---

# Specifične upute za kolegij statistike

## Izvorni sadržaj (pozadinska infrastruktura)

Knjiga **"Learning Statistics with R: A tutorial for psychology students and other beginners"** (Version 0.6) autorice Danielle Navarro služi kao sadržajna okosnica kolegija. Knjiga je objavljena pod CC BY-SA 4.0 licencom što znači da se smije slobodno adaptirati uz navođenje izvora.

Knjiga se NE prevodi doslovno. Koristi se kao strukturalni i konceptualni temelj: redoslijed tema, logika objašnjavanja, pedagogija postupnog građenja znanja. Sadržaj se piše iznova na hrvatskom, s primjerima iz komunikologije i modernih medija, u tidyverse stilu. Autorica i knjiga navode se u popisu literature i u uvodu kolegija kao inspiracija i preporučeno čitanje na engleskom.

## Mapiranje knjige na 15 tjedana

Izvorni sadržaj knjige (18 poglavlja) komprimira se u 15 tjedana kolegija. Ovdje je mapiranje:

| Tjedan | Tema predavanja | Poglavlja iz knjige | Fokus za komunikologe |
|:------:|-----------------|--------------------|-----------------------|
| 1 | Zašto statistika? Uvod u istraživački dizajn | Ch 1, Ch 2 | Zašto komunikolog treba podatke. Simpsonov paradoks na primjeru medijskih anketa. Mjerenje, skale, pouzdanost. Eksperimentalni vs neeksperimentalni dizajn na primjerima iz medijskih istraživanja. |
| 2 | Uvod u R i tidyverse | Ch 3 (adaptirano) | Instalacija R i Positrona. Umjesto base R konzole, odmah krenuti s tidyverse pristupom. tibble umjesto data.frame, pipe operator, readr za učitavanje. Primjer: učitavanje dataseta o korištenju društvenih mreža. |
| 3 | Rad s podacima u tidyverse | Ch 4, Ch 7 (adaptirano) | dplyr (filter, select, mutate, summarise, group_by), tidyr (pivot_longer, pivot_wider), readr/readxl za učitavanje. Primjer: čišćenje podataka iz ankete o medijskim navikama studenata. |
| 4 | Deskriptivna statistika | Ch 5 | Mjere centralne tendencije i varijabilnosti. Sve kroz summarise() i group_by(). Korelacije. Primjer: opisivanje distribucije vremena provedenog na TikToku po dobnim skupinama. |
| 5 | Vizualizacija podataka s ggplot2 | Ch 6 (potpuno prepisano) | ggplot2 umjesto base R grafike. Histogrami, boxplotovi, scatterplotovi, bar chartovi. Gramatika grafike (aes, geom, facet, theme). Primjer: vizualizacija rezultata medijske ankete. |
| 6 | Programiranje u R (osnove) | Ch 8 (skraćeno) | Skripte, funktije, uvjetne naredbe. Koliko programiranja komunikolog treba? Fokus na pisanje čistih, ponovljivih analiza, ne na programerske vještine. |
| 7 | Uvod u vjerojatnost | Ch 9 | Što je vjerojatnost? Frekvencijski i bayesijanski pristup. Binomna i normalna distribucija. Primjer: vjerojatnost viralnog sadržaja, distribucija broja dijeljenja objava. |
| 8 | Kolokvij | | Provjera znanja iz prvih 7 tjedana. |
| 9 | Uzorkovanje, procjena i intervali pouzdanosti | Ch 10 | Uzorci i populacije. Zakon velikih brojeva. Centralni granični teorem. Intervali pouzdanosti. Primjer: anketiranje publike, margina pogreške u istraživanjima medija, zašto su online ankete problematične. |
| 10 | Testiranje hipoteza | Ch 11 | Nulta i alternativna hipoteza. Greške tipa I i II. P-vrijednost. Veličina učinka i snaga testa. Primjer: testiranje razlike u angažmanu između dva formata objave na Instagramu. |
| 11 | Kategorički podaci: hi-kvadrat testovi | Ch 12 | Goodness-of-fit i test nezavisnosti. Fisherov egzaktni test. Primjer: postoji li veza između tipa medija (TV, web, podcast) i dobne skupine publike? |
| 12 | Usporedba prosjeka: t-testovi | Ch 13 | Jednosmjerni, dvosmjerni, upareni t-test. Welchova korekcija. Veličina učinka (Cohenov d). Provjera normalnosti. Primjer: usporedba vremena čitanja članaka s i bez vizuala. |
| 13 | Usporedba više grupa: ANOVA | Ch 14 | Jednosmjerna ANOVA. Post-hoc testovi (Tukey). Provjera pretpostavki (homogenost varijance, normalnost). Primjer: razlika u percipiranoj vjerodostojnosti vijesti ovisno o izvoru (TV, portal, društvena mreža). |
| 14 | Linearna regresija | Ch 15 | Jednostavna i višestruka regresija. R-kvadrat. Dijagnostika modela. Primjer: predviđanje angažmana objave na temelju duljine teksta, vremena objave i broja hashtagova. |
| 15 | Prezentacije projekata i pogled naprijed | Ch 16 (skraćeno), Ch 17 (pregled), Ch 18 | Kratki pregled faktorske ANOVE. Bayesijanska statistika kao alternativni pristup (samo pregled, bez tehničkih detalja). Studentske prezentacije. Što dalje? |

## R i tidyverse konvencije

Ovo je kritično. Sav R kod u predavanjima mora koristiti **tidyverse** pristup. Izvorni book koristi base R. MI NE KORISTIMO BASE R osim kada je neizbježno (npr. `t.test()`, `chisq.test()`, `aov()`, `lm()` jer tidyverse nema zamjene za statističke testove).

Konkretno:

**Učitavanje podataka.** Koristiti `readr::read_csv()` ili `readxl::read_xlsx()`, nikada `read.csv()`.

**Manipulacija podacima.** Koristiti `dplyr` (filter, select, mutate, summarise, group_by, arrange, count, across), `tidyr` (pivot_longer, pivot_wider, drop_na, separate, unite), pipe operator `|>` (base R pipe, ne magrittr `%>%`).

**Vizualizacija.** Isključivo `ggplot2`. Nikada base R `plot()`, `hist()`, `boxplot()`. Koristiti teme poput `theme_minimal()` ili `theme_bw()`. Grafike moraju biti čiste, čitljive i prilagođene za tisak (bez pretjeranog korištenja boja).

**Tibbleovi.** Koristiti `tibble` umjesto `data.frame`. Koristiti `glimpse()` umjesto `str()`.

**Paketi koji se koriste na kolegiju.** tidyverse (uključuje ggplot2, dplyr, tidyr, readr, tibble, stringr, forcats, purrr), broom (za pretvaranje statističkih modela u tidy tablice), janitor (za clean_names i tabyl), scales (za formatiranje osi grafika), patchwork (za kombiniranje grafika). Za statističke testove: base R funkcije (t.test, chisq.test, aov, lm) s broom::tidy() za izvlačenje rezultata u tidy format.

**Obrazac koda u predavanjima.** Svaki code chunk mora imati:

```r
#| label: opisno-ime-chunka
#| echo: true
#| message: false
#| warning: false
```

Kod se objašnjava u tekstu PRIJE chunka (što ćemo napraviti i zašto) i POSLIJE chunka (što vidimo u rezultatu i što to znači). Chunk nikada ne stoji sam bez konteksta.

## Primjeri i dataseti

Svi primjeri moraju biti iz domene komunikologije i modernih medija. NE koristiti psihologijske primjere iz izvorne knjige. Zamijeniti ih:

**Umjesto psihologijskih eksperimenata** koristiti: A/B testove na web stranicama, analize angažmana na društvenim mrežama, istraživanja medijskih navika, ankete o povjerenju u medije, analize sadržaja vijesti, metrike web analitike.

**Umjesto kliničkih podataka** koristiti: podatke o korištenju platformi (TikTok, Instagram, YouTube), metriku newsletter kampanja (open rate, click rate), rezultate anketa o konzumaciji medija, podatke o gledanosti/slušanosti, web traffic podatke.

**Umjesto laboratorijskih eksperimenata** koristiti: online eksperimente (A/B testovi naslova članaka), ankete provedene putem Google Forms, analizu komentara na portalima, analizu hashtagova.

**Dataseti.** Za svaki tjedan pripremiti CSV datoteku u `resources/datasets/` s podacima relevantnim za temu tjedna. Podaci mogu biti simulirani ali moraju biti realistični. Svaki dataset mora imati:

- Smislene nazive stupaca na engleskom (jer je to standard u R-u)
- Dokumentaciju u obliku komentara ili README datoteke u datasets/ mapi
- Realistične vrijednosti za komunikološki kontekst

Primjeri dataseta:

- `social_media_survey.csv` (anketa o korištenju društvenih mreža, N=500, varijable: age, gender, platform, daily_minutes, trust_score, education)
- `article_engagement.csv` (angažman čitatelja na portalu, N=1000, varijable: article_id, headline_type, word_count, has_image, time_on_page, shares, comments)
- `media_trust.csv` (istraživanje povjerenja u medije, N=300, varijable: respondent_id, age_group, media_source, credibility_score, frequency_of_use)
- `newsletter_campaign.csv` (rezultati email kampanje, N=5000, varijable: campaign_id, subject_line_type, send_time, open_rate, click_rate, unsubscribe)
- `ab_test_headlines.csv` (A/B test naslova na portalu, N=2000, varijable: variant, headline_style, clicks, impressions, ctr, time_of_day)

## Stil pisanja za statistički kolegij

Stil se oslanja na ton Danielle Navarro ali prilagođen za hrvatski i za komunikologe.

**Jednostavno.** Statistički koncepti objašnjavaju se svakodnevnim jezikom prije nego što se uvede formalna terminologija. Svaki pojam se uvodi tako da čitatelj intuitivno razumije o čemu se radi prije nego što vidi formulu ili R kod.

**Zabavno.** Dopušteni su humor, pop-kulturne reference, anegdote iz stvarnog medijskog svijeta. Ali humor nikad ne smije biti na račun studenata koji se muče sa statistikom. Poruka je uvijek: ovo je teško svima na početku, ali je savladivo i korisno.

**Akademski.** Unatoč laganom tonu, sadržaj mora biti točan i precizan. Formule se ne izbjegavaju ali se uvijek objašnjavaju riječima. Ograničenja metoda se uvijek navode. P-vrijednosti se ne tretiraju kao magični prag nego se objašnjava što zapravo znače (i ne znače).

**Pošteno o teškoćama.** Kada je nešto konceptualno teško (npr. p-vrijednost, centralni granični teorem, stupnjevi slobode), to se otvoreno kaže. Ne pretvarati se da je jednostavno. Umjesto toga objasniti zašto je teško i ponuditi intuiciju koja pomaže.

**Relevantno.** Svaki statistički koncept mora imati jasan odgovor na pitanje "zašto bi komunikologa ovo trebalo zanimati?". Ako ne možete odgovoriti na to pitanje za konkretan koncept, ili ga preskočite ili eksplicitno kažite da je ovo tehnički detalj koji se javlja u pozadini.

## R code u predavanjima

Svako predavanje koje uključuje R kod mora:

1. Na početku učitati potrebne pakete u jednom setup chunku:

```r
#| label: setup
#| echo: true
#| message: false
library(tidyverse)
library(broom)
# i drugi paketi po potrebi
```

2. Učitati podatke odmah nakon setupa i pokazati prvih nekoliko redova:

```r
#| label: ucitavanje-podataka
podaci <- read_csv("../resources/datasets/ime_dataseta.csv")
glimpse(podaci)
```

3. Graditi analizu korak po korak, od jednostavnijeg prema složenijem
4. Svaki chunk mora proizvesti vidljiv output (tablica, grafika ili tekstualni rezultat)
5. Grafike moraju imati naslove i oznake osi na hrvatskom

## Što trebam od AI-ja

Kada dajem upute za novi kolegij, trebam sljedeće:

1. Ime kolegija, šifra, studij, godina, semestar, ECTS, opterećenje (sati predavanja + seminara), nositelj
2. Popis od 15 tjedana s naslovima predavanja i kratkim opisom sadržaja
3. Popis seminarskih aktivnosti za svaki tjedan (kratki opis)
4. Eventualni naglasak ili bias koji treba utkati kroz primjere

Na temelju toga AI treba generirati:

- Kompletni zip s cijelom strukturom repozitorija, spreman za raspakiravanje u prazan folder i pokretanje s `quarto preview`
- Sve datoteke na hrvatskom jeziku
- Sve lecture datoteke s `draft: false`
- Barem jedno predavanje (Week 1) napisano kao potpuno poglavlje u narativnom stilu s R kodom
- Ostala predavanja kao placeholderi
- Popunjen silabus s opisima svih tjedana
- Popunjen raspored
- Popunjen popis literature i alata relevantan za tematiku kolegija
- Popunjen opis praktičnog projekta s rubrikom
- Simulirane datasete u resources/datasets/

## Poznati problemi i rješenja

**Dropbox lock conflict.** Ako je projekt u Dropbox mapi, `.quarto/idx` datoteka može biti zaključana. Rješenje: `Remove-Item -Recurse -Force .quarto` pa ponoviti, ili premjestiti projekt izvan Dropboxa.

**babel-croatian LaTeX error.** PDF rendering pada jer se babel-croatian paket ne može instalirati. Rješenje: koristiti `lang: en` pod pdf formatom u _metadata.yml. Tekst ostaje na hrvatskom.

**subtitle pod website blokom.** Starije verzije Quarta ne podržavaju `subtitle` u `website` bloku `_quarto.yml`. Rješenje: spojiti naslov i šifru u `title` polje.

**drafts: mode: visible.** Starije verzije ne podržavaju ovu sintaksu. Rješenje: staviti `draft: false` na sve datoteke.

**quarto preview ne generira PDF/Word.** `quarto preview` renderira samo HTML. Za PDF i Word pokrenuti `quarto render lectures/week-NN.qmd` ili `quarto preview --render all`.

**R code chunkovi i GitHub Actions.** GitHub Actions runner nema instalirane R pakete. U `publish.yml` treba dodati korak za instalaciju R-a i paketa, ili koristiti `freeze: auto` u `_quarto.yml` da se R chunkovi izvršavaju samo lokalno a GitHub koristi zamrznute rezultate:

```yaml
execute:
  freeze: auto
```

Ovo je preporučeni pristup jer izbjegava kompleksnost instaliranja R paketa u CI/CD pipelineu. Lokalno renderirate, rezultati se zamrzavaju u `_freeze/` direktoriju koji se commitira u git, i GitHub Actions samo kopira zamrznute rezultate.
