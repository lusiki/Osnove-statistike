# Dataseti za vježbe

Svi dataseti su simulirani ali s realističnim vrijednostima iz komunikološkog konteksta. Nazivi stupaca su na engleskom jer je to standard u R-u.

## social_media_survey.csv (N=500)

Anketa o korištenju društvenih mreža.

| Stupac | Opis |
|--------|------|
| respondent_id | ID ispitanika |
| age | Dob (18–65) |
| gender | Spol (M, F, Other) |
| platform | Najkorištenija platforma |
| daily_minutes | Dnevno vrijeme na platformi (minute) |
| trust_score | Povjerenje u informacije s platforme (1–7) |
| education | Razina obrazovanja |

## article_engagement.csv (N=1000)

Angažman čitatelja na web portalu.

| Stupac | Opis |
|--------|------|
| article_id | ID članka |
| headline_type | Tip naslova (clickbait, informative, question, listicle) |
| word_count | Broj riječi u članku |
| has_image | Ima li članak sliku (0/1) |
| time_on_page | Vrijeme na stranici (sekunde) |
| shares | Broj dijeljenja |
| comments | Broj komentara |

## media_trust.csv (N=300)

Istraživanje povjerenja u medije.

| Stupac | Opis |
|--------|------|
| respondent_id | ID ispitanika |
| age_group | Dobna skupina |
| media_source | Izvor medija (TV, web_portal, social_media, radio, print) |
| credibility_score | Ocjena vjerodostojnosti (1–7) |
| frequency_of_use | Učestalost korištenja |

## newsletter_campaign.csv (N=5000)

Rezultati email kampanja.

| Stupac | Opis |
|--------|------|
| campaign_id | ID kampanje |
| subject_line_type | Tip predmetne linije (promotional, informational, personalized, urgent) |
| send_time | Vrijeme slanja (morning, afternoon, evening, night) |
| open_rate | Stopa otvaranja (0–1) |
| click_rate | Stopa klikanja (0–1) |
| unsubscribe | Stopa odjave (0–1) |

## ab_test_headlines.csv (N=2000)

A/B test naslova na web portalu.

| Stupac | Opis |
|--------|------|
| observation_id | ID opservacije |
| variant | Varijanta testa (A, B) |
| headline_style | Stil naslova (emotional, factual, question, number) |
| clicks | Broj klikova |
| impressions | Broj prikaza |
| ctr | Click-through rate |
| time_of_day | Doba dana |
