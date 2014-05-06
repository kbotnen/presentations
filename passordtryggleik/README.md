## Introduksjon
Året 2013 har gått inn i historien som "The year of stolen credentials", og vi har allereie hatt stort fokus på sikkerhet i 2014 grunna blant anna #heartbleed [1] og #gotofail [2].

- **mars 2013**: 50 millionar brukarar må skifte passord på skytjenesten Evernote grunna lekkasje av brukarnavn, epost-adresse og passord [3].
- **oktober 2013**: 150 millionar brukarid og passord blir stjelt fra Adobe [4].

Med dette som bakteppe vil eg prøve å forklare nokre grunnleggande begrep rundt emnet passordtryggleik.
Noko av det eg vil belyse er:
- korleis vert passord lagra?
- korleis gjeng ein fram for å knekke eit passord?
- viktigheten av å ikkje bruke samme passord på fleire stadar.
- forskjellen på eit svakt og eit sterkt passord.

## Kva er eit passord?
Dei fleste kjenner eit passord som en sekvens av tegn. Dette kan vere bokstavar, tal, spesialtegn eller ein kombinasjon av dei tre. 

Dette gir oss eit sett med 97 verdiar. Merk at teknet for mellomrom er endel av settet:

"0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~ "

- a-z, 27
- A-Z, 27
- 0-9, 10
- spesialtekn, 33

Passordet er det vi brukar for å fortelle eit system at vi er  den vi gir oss ut for å vere (autentisering). Sidan passordet ditt er personlig og hemmeleg kan vi anta at dersom nokon brukar ditt passord ein stad, så kan det berre vere deg.
Ein kan diskutere om dette er den beste måten å autentisere på, men akkurat no er det passord som er den klart mest utbredte  autentiseringsmetoden.

## Lagring av passord
For å forstå korleis ein går fram for å knekke eit passord er det nødvendig å seie nokre ord om korleis eit passord vert lagra  på server.
Når du skriv inn ønska passord i ei boks etterfulgt av "Lagre" vert sekvensen du skreiv gjort om til det som kallast ein hashverdi. Dette gjerast ved hjelp av ein kryptografisk hashfunksjon, der inndataene er passordet vårt, og resultatet er ein hashverdi.
- hashverdien har lik lengde uavhengig av lengden på passordet.
- gitt ein hashverdi så skal det vere veldig vanskelig å finne ut kva passordet var, det vil sei at vi har ein enveisfunksjon.
- hashverdien skal vere tilnærma unik, det vil sei at for eit stort antall passord skal vere veldig sikre på at to ulike passord ikkje endar opp med samme hashverdi.

For å illustrere tar eg to passord og generer sha-1 hashverdien for dei [5]:
"test"     -> a94a8fe5ccb19ba61c4c0873d391e987982fbbd3
"test1234" -> 9bc34549d565d9505b287de0cd20ac77be1d3f2c

Som vi ser så har passorda forskjellig lengde, men hashverdien er like lang. Det er altså denne hashverdien som vert lagra i passorddatabasen.

Når du no kjem attende til websida og skal logge inn vert passordet du skriv inn hashet, og resultatet vert sammenligna med hashverdien som er lagra i passorddatabasen.

Eit resultat av denne hashinga er at dersom du gløymer passordet ditt må det nullstillast. Mange har kanskje opplevd å få tilsendt ein nullstill-passord lenke dersom ein har har gløymt passordet sitt på ein nettstad. Det er rett og slett ikkje mulig å hente ut passordet ditt i klartekst når det først er hashet og lagra, så det må settast eit nytt passord.

## Korleis tenker dei som prøver å utnytte passorda våre?
Eit passord vil gi angriparen tilgang til eit system dei i utgangspunktet ikkje har tilgang til. 
Ofte er det tilgangen til systemet som er verdifull, og ikkje sjølve dataene til den som eiger passordet. Dette betyr at argumenter som "men ingen har interesse av å stjele mitt passord", og "eg har ingenting å skjule", ikkje er gyldige, sidan det ikkje nødvendigvis er dine ting dei er ute etter, men systema du har tilgang til.

No vil eg oppsummere nokre av dei passordangrepa vi kan verte utsett for.

**Ordbok angrep (eng: dictionary attack)**
Som navnet tilseier baserer denne framgangsmåten seg på å gjette seg igjennom alle oppføringar i ei ordbok. Ordbøkene kan variere i størrelse alt etter kor lange ord angriparen ønskar å gjette på.
Det finnes ordlister tilgjengelig på blant anna Afrikaans, Kroatisk, Tjekkisk, Dansk, Nederlandsk, Engelsk, Finsk, Fransk, Tysk, Ungarsk, Italiensk, Japansk, Latin, Norsk, Polsk, Russisk, Spansk, Swahili, Svensk, Tyrkisk, og Yiddish. I tillegg har ein ordbøker som inneheld dei mest brukte passorda (fleire millionar  "mest brukte passord"). Ordbøker for bruk med passordcracking programvare kjøpes enkelt på nett for 20 Euro [6].
For å cracke ein passordhash på denne måten tar man ei oppføring frå ordboka, hasher den, og sammenligner hashverdien med det passordet ein prøver å cracke. Dersom hashverdiane er lik, veit ein med veldig stor sansynlighet at ein har rett passord.
**Optimalisert ordbokangrep (eng: precomputed dictionary attack)**
Dette angrepet er ein optimalisert variant av ordbok angrep. Sidan det å generere ein kryptografisk hashverdi er tidkrevande,  har ein gjort denne jobben på forhånd og lagra resultata i det som kallast rainbowtables. Dette er altså ordbøker, men ferdig hashet sånn at angriperen slepp å bruke tid / prosessorkraft på å beregne alle hashverdiane sjølv. Rainbowtables kan du laste ned gratis frå nettet [7].
**Brute force angrep**
Dersom ingen av ordbok angrep variantane fungerar er brute force eit alternativ. Dette baserer seg på å generere hashverdien for alle mulige kombinasjoner av små bokstavar, store bokstavar, tal og tekn.
**Phishing angrep**
Dette er eit vanlig åtak som baserer seg på å lure brukaren til å besøke ei bestemt nettside for deretter å taste inn passordet sitt. Nettsida angriparen prøver å lure brukaren til er ofte kopiar av kjente sider som facebook, outlook eller liknande, men kontrollerast av angriparen. Når du skriv inn passordet ditt på disse falske sidene har du i praksis gitt det til angriparen.
**Sosial manipulering (eng: social engineering)**
Dette er når nokon ber deg oppgi passordet ditt uten å ha nokon legitim grunn til det. Dette er den mest treffsikre måten å stjele passord på, men er vanskelig å utføre i stor skala. Eit angrep som ofte er retta mot navngitte personer.
- - -
Dei tre første angrepa er såkalla offline angrep, der angriparen har fått tak i ein kopi av databasen med passord. Offline angrep har den egenskapen at angriparen kan sitte i ro og mak å gjette passord uten at nokon veit at passorda deira er under angrep.

No har vi sett på nokon av måtane ein angripar kan gå fram for å  stele passordet vårt, men kva skjer vidare?
Ein database med stjålne passord er handelsvare i kriminelle miljøer. [kan vi finne noke prisinformasjon her?]. Passord som gir tilgang til kraftige system prisast ofte høgare en passord til ei gjenomsnittlig heimedatamaskin.


## Kva kjennetegner eit sterkt passord?
Eit sterkt passord har den egenskapen at det er vanskelig å knekke. No som vi veit korleis nokon av teknikkane for å knekke passord fungerar kan vi også tenke oss nokon egenskapar som passordet vårt bør ha.
1. passordet vårt må ikkje kunne finnast i nokon ordliste
2. passordet vårt må vere tilstrekkelig langt
3. passordet vårt må vere tilstrekkelig komplekst, det vil sei at det må inneholde små bokstavar, store bokstavar, tal og tekn.
4. passordet vårt må vere unikt.

**Punkt 1** vil motvirke ordbok angrep som gjerne er den første angrepsvektoren som vert forsøkt. Merk at ordlistene som vert brukt utvidar seg stadig, og kan sjåast meir som på ei samling av ord og frasar istadenfor ei rein ordbok. Det finst døme på passordangrep som har brukt Shakespeare, og deler av Wikipedia som "ord" det har blitt testa mot [her må referanse på plass].

Eksempel: "Love all, trust a few, do wrong to none."
Dette er eit passord som er tilstrekkelig langt, har små bokstavar, store bokstavar, og tekn. Problemet med dette passordet er at vi vil finne det i ei "ordbok", og det vil derfor vere lett å knekke.

**Punkt 2** vil motvirke brute force angrep som er en angrepsvektor som vi sikrar oss best mot ved å la antall mulige kombinasjoner vere tilstrekkelig høgt.

**Punkt 3** tilsvarar punkt 2. For kvar ny gruppe (store bokstavar, små bokstavar, tal og tekn) vi innfører i passordet vårt, jo meir øker vi antall mulige kombinasjoner som angriparen må teste.

**Punkt 4** vil ikkje  motvirke sjølve angrepet, men er meir et begrensande tiltak som trer i kraft når passordet har blitt kompromittert.

## Litt meir om passordkompleksitet
I dette avsnittet vil eg prøve å vise med tal kvifor punkt 2 og punkt 3 i førre avsnittet er så viktige.

Eg vil vise antall mulige passord, og kor lang tid det vil ta å knekke med brute force angrep. Antall forsøk pr.sekund vil vere avhengig av maskina ein utfører brute force angrep på, og tala eg har brukt i utrekningane er henta frå [8].

- 27 lovlige tekn (a-z), lengde 4, 361 forsøk i sekundet:
531 441 mulige passord, 1472 sekunder, **ca 24.5 minutter**.
- 27 lovlige tekn (a-z), lengde 6, 361 forsøk i sekundet:
387 420 489 mulige passord, 1073186 sekunder, **ca 12.42 dagar**.
- 27 lovlige tekn (a-z), lengde 8, 361 forsøk i sekundet:
282 429 536 481 mulige passord, 782353287 sekunder, **ca 24.7 år**.

Fleire utrekningar kan du sjå her: [lenke til pdf eller noke med resten av utrekningane]

Disse tala viser oss at lengde og kompleksitet faktisk er avgjerande for om eit passord er sikkert eller ikkje.
Merk også at for korte passord (6-8 tekn) vil det ofte vere ferdig genererte rainbowtables som gjer at antall forsøk pr.sekund er langt høgare en dei som er brukt i utrekningane over [7].

## UiB sin passord politikk

## Oppsummering
Dette var eit forsøk på å forklare nokon av mekanismane som trer i kraft når det gjeld passord. Mykje av dette er kjent for mange, men eg håpar at ei lita oppfrisking kan vere nyttig.

No som vi har ei oversikt over utfordringane rundt passordtryggleik vil eg presentere forslag til løysingar. Dette vil komme i ein egen post om kort tid.

... og husk, dersom nokon spør deg om passordet ditt på epost så  skal du ikkje svare. Dette er eit eksempel på phishing angrep.

## Referanser

1. http://heartbleed.com
2. http://support.apple.com/kb/HT6147
3. http://blog.evernote.com/blog/2013/03/02/security-notice-service-wide-password-reset/
4. http://krebsonsecurity.com/2013/10/adobe-breach-impacted-at-least-38-million-users/
5. http://www.sha1-online.com
6. http://www.openwall.com/wordlists/
7. http://ophcrack.sourceforge.net/tables.php
8. http://resources.infosecinstitute.com/password-cracking-evolution/
