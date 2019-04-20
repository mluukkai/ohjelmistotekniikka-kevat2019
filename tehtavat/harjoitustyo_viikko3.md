# Harjoitustyö, viikko 3

**Palautuksen deadline ti 2.4. klo 23:59**

Muista pushata  harjoitustyöhön liittyvät asiat GitHubiin ennen viikkodeadlinea.

- Klo 00 jälkeen tulevia repositorion päivityksiä ei huomioida pisteytyksessä, eli ne tuovat 0 pistettä.

Palautuksesta on tarjolla 2 kurssipistettä.

Arvostelussa kiinnitetään huomiota seuraaviin seikkoihin
- Repostitorion juuresta löytyy Maven-projekti
  - [ohje](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/tyon_aloitus.md#harjoitusty%C3%B6n-aloitus) projektin luomiseen ja sen  sijoittamiseen palautusrepositorioon
- Projektin koodin pystyy suorittamaan NetBeansin vihreällä napilla _tai/ja_ komennolla <code>mvn compile exec:java -Dexec.mainClass=pakkaus.Paaohjelma</code>
  - komennon parametrina on metodin _main_ sisältävän luokan täydellinen, eli myös pakkauksen sisältämä nimi
  - [referenssisovelluksen](https://github.com/mluukkai/OtmTodoApp) tapauksessa parametri olisi <code>-Dexec.mainClass=todoapp.ui.TodoUi</code>
- Edellytys pisteille suoritettavissa oleva versio, joka toteuttaa ainakin osan jostain viikolla 2 tekemäsi määrittelydokumentin toiminnallisuudesta
  - pelkät getterietä ja settereitä sisältävät, täysin ilman toiminnallisuutta olevat luokat eivät tuo pisteitä
- Sovelluksella on oltava _vähintään yksi testi_ jonka voi suorittaa komennolla <code>mvn test</code>
  - Testin tulee olla mielekäs, eli sen on testattava jotain ohjelman kannalta merkityksellistä asiaa
  - Testin tulee mennä läpi
- Sovellukselle tulee pystyä generoimaan testikattavuusraportti komennolla <code>mvn test jacoco:report</code>
- Tuntikirjanpito on ajantasalla
  - Tuntikirjanpitoon ei merkitä laskareihin käytettyä aikaa
- Repositorion README.md kunnossa
  - tiedosto on kurssin tämän vaiheen osalta relevantin sisällön suhteen samankaltainen  kuin [referenssisovelluksen](https://github.com/mluukkai/OtmTodoApp) README.md
  - kaikki ylimääräinen, mm linkit laskareihin on poistettu 
- Repositorio siisti
  - ei ylimääräistä tavaraa (mm. hakemistoa target/ tai tietokantatiedostoja)
  - laskarit jätetään hakemiston _laskarit_ alle
  - järkevä .gitignore-tiedosto olemassa

Ohjelman tulee edistyä jokaisella viikolla tasaisesti. Jos ohjelma tulee valmiiksi jo ennen loppupalautusta valmistaudu laajentamaan sitä saadaksesi ohjelman edistymisestä pisteet. Tarkoitus on edistää projektia tasaisesti kurssiviikkojen aikana.
