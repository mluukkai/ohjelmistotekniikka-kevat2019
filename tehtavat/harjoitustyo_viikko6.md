# Harjoitustyö, viikko 6

Palautuksen deadline **perjantai 26.4. klo 23:59**. 

**Muutama huomio**

- **Viikon 6 aikana tapahtuu koodikatselmointi**, tarkemmat ohjeet katselmointiin [täällä](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/koodikatselmointi.md)
- Kannattaa pitää mielessä, että kurssin loppu alkaa lähestyä ja myös loppupalautuksen deadline.

  - Nyt kannattaa kerrata loppupalautuksen [arvosteluperusteet](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/arvosteluperusteet.md)
  - Viimeiselläkin viikolla ohjelmaa ehtii vielä kasvattamaa, mutta myös dokumentoinnille kannattaa jättää aikaa

Arvostelussa kiinnitetään huomiota seuraaviin seikkoihin

- Ohjelma on kasvanut edellisestä viikosta (0.75p)
  - Ohjelmasta pystyy tekemään suorituskelpoisen [jar](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/maven.md#jarin-generointi)-tiedoston komennolla _mvn package_
   - Ohjelman suoritettavissa oleva versio on kasvanut edellisestä viikosta _ja_ toteuttaa edellisen viikon versiota suuremman osan määrittelydokumentin toiminnallisuudesta eli jotain käyttäjälle näkyvää hyödyllistä toiminnallisuutta
  - Ohjelman suoritettavissa olevasta versiosta on tehty uusi [GitHub-release](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/release.md), joka sisältää suoritettavan version jar-tiedoston ja muut mahdolliset ohjelman suorituksessa tarvittavat tiedostot
- Koodin laatu (0.5p)
  - Ohjelma ei sisällä suurta määrää toisteista koodia eli copy pastea
  - Ohjelman luokkarakenne on järkevä
    - luokkien tulee pyrkiä noudattamaan ns. [single responsibility](https://materiaalit.github.io/ohjelmointi-s17/part6/) -periaatetta, eli yhden luokan ei tulisi tehdä liian montaa asiaa
    - liian suuret luokat tulee siis jakaa useiksi luokiksi
  - Metodit ovat järkevän pituisia ja yhteen asiaan keskittyviä 
    - myös liian suuret metodit tulee jakaa useiksi metodeiksi 
- Testaus on edennyt (0.5p)
  - Sovellukselle tulee pystyä generoimaan testikattavuusraportti komennolla <code>mvn test jacoco:report</code>
    - käyttöliittymän rakentava koodi [jätetään pois](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/maven.md#koodin-huomiotta-jättäminen-kattavuusraportissa) testikattavuusraportista
  - Sovelluksen testien rivikattavuuden tulee olla vähintään 60%
  - Testien tulee testata järkevällä tavalla ohjelman toiminnallisuutta
    - jos testit on tehty pelkästään rivikattavuuden saavuttamiseksi, ei testeistä saa pisteitä
- JavaDoc aloitettu (0.5p)
  - JavaDoc tulee olla generoitavissa komennolla _mvn javadoc:javadoc_
  - Ainakin osalle ohjelman luokista ja niiden metodeista on tehty JavaDoc-kuvaukset
    - edellytyksenä pisteille on vähintään 5 luokan ja niiden julkisten metodien dokumentointi
      - gettereitä ja settereitä (jotka eivät tee mitään muuta kuin asettavat/palauttavat oliomuuttujan arvon) ei tarvitse dokumentoida
  - [Ohje](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/javadoc.md) JavaDocin käyttöön
- Alustava arkkitehtuurikuvaus (0.5p)
  - Dokumentti sisältää sovelluksen korkean tason (esim. pakkausten tasolla) rakenteen kuvauksen, sekä alustavan kuvauksen sovelluslogiikasta
  - Dokumentissa voi hyödyntää edellisten viikkojen luokka- ja sekvenssikaavioita
  - Mallia voi ottaa [referenssisovelluksesta](https://github.com/mluukkai/OtmTodoApp/blob/master/dokumentaatio/arkkitehtuuri.md#sovelluslogiikka)
  - Dokumentin alustavan version sopiva pituus on noin 1-2 sivua
- Alustava käyttöohje (0.25p)
  - Ohje voi olettaa, että sovellusta suoritetaan palautusrepositoriosta käsin, eli asentamiseen ja konfigurointiin ei ole vielä tarvetta ottaa kantaa
  - Alustavan käyttöohjeen sopiva pituus on noin sivu
  - Mallina voi jälleen toimia [referenssisovellus](https://github.com/mluukkai/OtmTodoApp/blob/master/dokumentaatio/kayttoohje.md)

**Seuraavien kohtien puutteet vähentävät pisteitä**

- Koodin laatu
  - Pakkausrakenne järkevä (esim. kaikki koodi oletuspakkauksessa)
  - Sovelluslogiikkaa on eriytetty riittävästi käyttöliittymästä
  - Checkstyle on käytössä
    - Ohjelmassa on alle 5 Checkstyle-virhettä
    - Käyttöliittymän rakentavan koodin ei tarvitse olla Checkstyle-tarkastelun alla
- Tuntikirjanpito on ajantasalla
  - **Tuntien summan tulee olla merkittynä**
  - Tuntikirjanpitoon ei merkitä laskareihin käytettyä aikaa
- Repositorion README.md kunnossa
  - Tiedosto on kurssin tämän vaiheen osalta relevantin sisällön suhteen samankaltainen kuin [referenssisovelluksen](https://github.com/mluukkai/OtmTodoApp) README.md, eli se sisältää ainakin seuraavat
    - harjoitustyön aiheen lyhyt kuvas
    - linkit vaatimusmäärittelyyn, arkkitehtuuridokumenttiin, käyttöohjeeseen ja tuntikirjanpitoon 
    - linkki releaseihin
    - ohjeet komentoriviltä suoritettaviin toimenpiteisiin (testaus, testiraportin suoritus, suoritettavan jarin generointi, checkstyletarkastuksen suorittaminen, JavaDocin generointi)
- Repositorio siisti
  - ei ylimääräistä tavaraa (mm. hakemistoa target)
  - laskarit jätetään hakemiston _laskarit_ alle
  - järkevä .gitignore-tiedosto olemassa
