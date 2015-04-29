#### Hva ønsker vi å oppnå

- Kontinuerlig forbedring
- Kontinuerlig levering
- Stabilt driftsmiljø
- Samarbeid mellom seksjoner og grupper
- Mindre personavhengighet
- Økt gjennomsiktighet



#### Hvordan ønsker vi å oppnå målene nevnt over?



### En felles verktøykasse



- Git (versjonshåndtering)
- Puppet (konfigurasjonsmanagement)
- Ansible (orkestrering)
- Jenkins (kontinuerlig integrasjon)
- Python, Php, Ruby, Bash (programmeringsspråk)
- Vagrant, Virtualbox, Vmware, Openstack, libvirt (virtualisering)
- Logstash (logging)



### Jobbe smartere



#### Egne miljøer for utvikling, test og produksjon

- Gjør det enklere å styre endringer
- ITIL (Endringsprosessen)
- Mer stabilt driftsmiljø
- På klienter og servere, i pakker og applikasjoner



#### Infrastruktur som kode

- Programmatisk definerte tilstander på systemer
- Koden dokumenterer systemet; systemdokumentasjonen er dynamisk
- Enklelt å implementere miljøer for utvikling, test og produksjon
- Konfigurasjonsdata er versjonerbare



- Unngår manuelle feil
- Unngår avvik mellom konfigurasjon og dokumentasjon
- Unngår konfigurasjonsdrift
- Gjør det lettere å rulle tilbake endringer
- Ekstremt tidsbesparende!



#### Deling av informasjon

- Infrastruktur som kode i Git gir økt gjennomsiktighet
- Dokumentere oppsett, fremgangsmåter med mer, slik at flere kan
lære mer
- Mindre personavhengighet



### Hva har vi gjort til nå?



- Vi har ikke hatt et styrt DevOps løp
- Vokst seg gradvis frem
- Endret  måten vi jobber på
- Endret verktøyene vi bruker
- Ikke kommet ovenfra og ned
- Behov for å være smartere når det gjelder versjonskontroll, serverkonfig,
orkestrering, deling av informasjon med mer



### Historietime



#### Versjonshåndtering

![Image Alt](http://folk.uib.no/kbo041/devops/images/timeline_versjonshaendtering.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/553e947b-1558-453e-8826-0b310a00c609/image.png)-->



#### Konfigurasjonsmanagement med Puppet

![Image Alt](http://folk.uib.no/kbo041/devops/images/timeline_konfigurasjonsmanagement.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/553ea0dc-5ae4-4554-adb5-18a80a004a17/image.png)-->



### Deling av informasjon

![Image Alt](http://folk.uib.no/kbo041/devops/images/timeline_delingavinformasjon.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/553eb0ab-0bf4-4f04-a9ad-64330a005c11/image.png)-->



### Utfordringer?



### Kultur og endring av kultur!



- Krever at en bryr seg om helheten, det vil si at en må ha en holistisk tilnærming til utvikling og infrastruktur!
- Krever en teamtankegang for å lykkes
- Krever at en jobber og forstår på tvers av etablerte faggrupper
- Endring av hvordan folk arbeider



## Empati



- Mellom utviklere og driftere
- Med de som konsumerer tjenestene



#### Devops i praksis



#### Eksempel: Utrulling av en applikasjon

- Provisjoner en ny server med Puppet
- RHEL-base med appstack
- Selve applikasjonen




#### Provisjonering av server

![Image Alt](http://folk.uib.no/kbo041/devops/images/provisjonering_av_server.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/55395b6c-2f2c-40a9-88d8-6c960a00d7d7/image.png)-->



#### Fordeler

- Provisjoner mye, raskt
- Serveren har akkurat den tilstanden vi ønsker den skal ha
- Endringer i tilstanden kan spores i Git og RTS
- Samme endring i test og produksjon



#### Utrulling av applikasjonen

![Image Alt](http://folk.uib.no/kbo041/devops/images/deployment_av_pakke.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/55395146-f988-4aea-96ae-474f0a0052f5/image.png)-->



#### Hva ønsker vi å gjøre videre?

- Vi ønsker at flere skal jobbe smartere og ta i bruk verktøy fra verktøykassen
- Automatisert testing av infrastruktur kode
- Automatisert pakking av applikasjoner, f.eks: om en utvikler lager en ny tag i
Git så pakkes og deployes det en ny versjon av applikasjonen



#### Kan devops fungere i en større offentlig institusjon?

- Hvordan skal en få folk med på laget
- Hvordan kan en bygge kompetanse
- Hvordan kan en ta hensyn til at folk har ulik bakgrunn
- Hvordan ta hensyn til at vi er en offentlig bedrift

Er det noen som har innspill så diskuterer vi det gjerne senere idag.



#### Konklusjon

- Devops for oss er å samarbeide på tvers av grupper og seksjoner
- Devops for oss er å automatisere så mye som mulig
- Devops for oss er å ha versjonskontroll på så mange elementer som mulig
- Devops for oss er å ha gjennomsiktighet, samt dele så mye som mulig
- Devops for oss er å ha empati



#### Spørsmål?

- Interessert i å bruke noen av verktøyene fra verktøykassen?
- Har du noen gode ideer om hvordan IT-Avdelingen kan utvikle seg videre?
- Kan Devops brukes andre steder på UiB?
