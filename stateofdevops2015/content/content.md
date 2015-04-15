### Tittel og ingress

- Tittel: Devops ved ITA

- Ingress: Vi skal snakke litt om hva devops-metodikk betyr for oss, hva vi har
gjort til nå og hvordan vi ser for oss veien videre. Vi vil også vise et
praktisk eksempel på hvordan devops brukes i vår hverdag.

### Om dette dokumentet

- Skriv i Markdown
- Tre blanke linjer gir en ny slide
- UTF8 æøå
- Presentasjonen kan styles annerledes etterhvert om ønskelig

[http://notat.devapp.uib.no:9001/p/stateofdevopsuib](http://notat.devapp.uib.no:9001/p/stateofdevopsuib)



### Hva ønsker vi å oppnå

- kontinuerlig forbedring
- kontinuerlig levering
- stabilt driftsmiljø
- bedre samarbeid mellom seksjoner og grupper
- mindre personavhengighet



#### Hvordan ønsker vi å oppnå målene nevnt over?



Alle bruker en felles verktøykasse!



- git (versjonshåndtering)
- puppet (konfigurasjonsmanagement)
- ansible (orkestrering)
- jenkins (kontinuerlig integrasjon: bygging, testing, overvåking)
- python, php, ruby, bash (programmeringsspråk)
- vagrant, virtualbox, vmware (virtualisering)



#### Treng tittel

- dev / test / prod -miljø
- infrastruktur som kode
- deling av informasjon



#### Hva har vi gjort til nå?



Historietime!



- klientdrift har fungert som en sandkasse for utprøving av konsepter fra ca. 2012
- siden 2014 har alle nye servere blitt satt opp med puppet
- har "tatt av" siste året



#### Veien videre?



Mye gjenstår!



- automatiserte tester
- måling
- automatisert pakking
- rhel 7 blir brekkstang for å komme videre



#### Utfordringer?



Kultur og endring av kultur!



- krever en "team tankegang" for å lykkes
- krever at en jobber / forstår på tvers av etablerte faggrupper
- krever at en bryr seg om helheten, det vil si at en må ha holistisk tilnærming til utvikling og infrastruktur!
- endring av hvordan folk arbeider
- puppet brukes også på applikasjonsdriftsnivå



#### Hva skal til for at devops skal fungere på en institusjon som UiB IT?
### Denne må vi snakke mer om!



- en må finne ut hvordan en skal få folk med på laget
- en må bygge kompetanse der det går an



#### Eksempel tatt fra virkeligheten
### Dette må klargjøres


Scenario: Vi vil ha en prosjekt side, og vi vil ha den igår!



#### Infrastruktur
- Provisjonerer en ny RHEL7 server med puppet og de riktige rollene satt
- - base EL7 (default sikkerhet, repoer og litt annet tjafs)
- - webserver (apache m mod_passenger)
- - databaseklient (postgres bindinger)
- - ruby appstack (ruby, rails)


#### Fordeler
- Når man har satt opp en instans er det kjappt å sette opp flere
- Når man ønsker å endre kan man endre i koden, kjøre i test, og videre i dev.
Man er da sikker på at det er samme endringen som er gjort både i test og dev.
- Når man skal oppgradere applikasjoner kan man kjøre opp en ny instans med den
nye versjonen og bytte fra den gamle til den nye, og så kaste den gamle. Mye bedre
en å prøve å inplace oppgradere den eksisterende applikasjoner.
- - Dette kan gi oss mindre / ingen nedetid ved oppgradering av applikasjoner.




#### Applikasjon
- Det bestilles og opprettes en postgresql database (manuelt steg)



#### Drift
- Alle er happy



#### Sky / CLoud
- UH-Sky
- IAAS


#### Spørsmål?
