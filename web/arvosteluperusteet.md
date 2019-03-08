# Kurssin suorittaminen ja arvostelu

Kurssilla jaossa 60 pistettä. Pisteet jakautuvat seuraavasti

- Viikkodeadlinet 17p
- Koodikatselmointi 2p
- Dokumentaatio	12p   
  - Määrittely		
  - Arkkitehtuuri		
  - Käyttö/asennusohje	
  - Testidokumentti	
  - JavaDoc	
- Testaus	5p	
  - Testit			
- Lopullinen ohjelma 24p
  - Toiminnallisuus		
  - Koodin laatu 		

Arvosanaan 1 riittää 30 pistettä, arvosanaan 5 tarvitaan noin 55 pistettä.

Läpipääsyyn vaatimuksena on lisäksi vähintään 10 pistettä lopullisesta ohjelmasta.

## Lopullisesta ohjelmasta annettavat pisteet

Pisteet (yht 24) jakautuvat seuraavasti
- Käyttöliittymä 4p
  - 0p yksinkertainen tekstikäyttöliittymä
  - 1-2p monimutkainen tekstikäyttöliittymä
  - 2-3p yksinkertainen graafinen käyttöliittymä
  - 4p laaja graafinen käyttöliittymä
- Talletetun tiedon käyttö ja tiedon tallettaminen 4p
  -	ei pysyväistallennusta
  - 1-2p tiedosto (1p jos ohjelma ainoastaan lukee tiedostoja)
  - 3-4p tietokanta (3p jos ohjelma ainoastaan lukee tietokannasta dataa)
  - 3-4p internet (esim. google docs tai joku muu talletusratkaisu)
  - Pisteytys riippuu käsiteltävän tiedon monimutkaisuudesta
- Sovelluslogiikan kompleksisuus 3p
- Ohjelman laajuus 5p
- Ulkoisten kirjastojen hyödyntäminen 1p
  - ks https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/maven.md#ulkoisten-kirjastojen-k%C3%A4ytt%C3%A4minen-mavenin-avulla
- Suorituskelpoinen jar-tiedosto 1p
  - Tiedosto generoitavissa tai löytyy repositoriosta _loppupalautus_-nimisestä releasesta
- Koodin laatu 6p
  - Kooste [laatuvaatimuksista](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/koodin_laatuvaatimukset.md)
  - 5p hyvät abstraktiot (esim. Design patternien kuten DAO hyödynnys), hyvä luokkarakenne, helposti testattava ja laajennettava
  - 3p ei ilmeistä copypastea, ok luokkarakenne
  - +1p checkstylesäännöt kunnossa (muutama checkstyletyylin rikkomus saatetaan katsoa läpi sormien, jos tyylirikon poisto esim. huonontaisi muuten koodin laatua)
  - **Älä jätä sovellukseesi poiskommentoitua koodia**, tai koodia jota sovellus ei käytä (esim. refaktoroinnin myötä turhaksi muuttuneet metodit/luokat)
    - jos jätät, vähenevät koodin laadun pisteet -1 tai -2p riippuen kommentoidun/turhan koodin määrästä

### Laajuus ja sovellusogiikan kompleksisuus

- Miten laaja on laaja?
- Kurssin [referenssisovellus](https://github.com/mluukkai/OtmTodoApp) olisi laajuudeltaan juuri ja juuri 2 pisteen arvoinen, sovelluslogiikaltaan se on aika suoraviivainen ja ansaitsisi vain yhden pisteen
- Laajuutta ei voida määritellä tarkasti esim. luokkien tai metodien määrällä, laajuus on aina suhteellinen sovelluksen tyyppiin ja kompleksisuuteenkin
- Eräs tapa laajentaa sovellusta ja lisätä sen kompleksisuutta on tehdä siitä _parametrein konfiguroitava ja laajennettava_, esim:
  - Sovelluksen käyttämän tietokantatiedoston nimi ei ole kirjoitettu koodiin vaan on käyttäjän määriteltävissä
  - Pelissä eri vaikueustasojen pelimaailmat eivät ole määritelty koodissa vaan luodaan erillisten tiedostojen perusteella
  - Pacmanissa hirviöiden määrä ei ole ohjelmakoodiin kovakoodattu vakio vaan valittavissa käyttöliittymästä
  - Konfiguroitavuus voidaan toteuttaa joko käyttöliittymän tai [konfiguraatiotiedostojen](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/java.md#sovelluksen-konfiguraatiot) avulla
  
  
## Testauksesta annettavat pisteet

Täysien pisteiden (5p) edellytys:
- Testattu kattavasti: rivi- ja haarautumakattavuus korkea (noin 70%)
  - Testien pitää testata hyödyllisiä asioita, pelkät testikattavuutta nostavat hyödyttömät (esim. assert-komentoja sisältämättömät) testit eivät tuo pisteitä
- Testaus riittävää sekä yksikkö- että integraatiotasolla
  - eli yksittäisten luokkien lisäksi on testattava myös monen luokan yhdistelmän tuottavaa toiminnallisuutta 
- Sovelluslogiikkaa testataan realistisilla skenaarioilla
- Testit testaavat mielekkäitä asioita
  - jos testit on tehty ainoastaan testauskattavuuden kasvattamiseksi, ei pisteitä ole montaa odotettavissa
- Riippuvuudet käsitelty järkevästi
  - tietokantaa käyttävissä sovelluksissa testeissä käytössä "testitietokanta"
  - myös valekomponentit ovat hyviä joissain tilanteissa, ks. esim [referenssisovellus](https://github.com/mluukkai/OtmTodoApp/blob/master/src/test/java/todoapp/domain/TodoServiceUserTest.java#L8)

## Dokumentaation pisteet

Dokumentaatio tuo yhteensä maksimissaan 12 pistettä, jotka jakautuvat seuraavasti

- Määrittelydokumentti 2p
  - **päivitetty vastaamaan lopullisen ohjelman toiminnallisuutta**
  - päivittämätön määrittelydokumentti tuo 0 pistettä
- Arkkitehtuurikuvaus 4p
- Käyttö/asennusohje 1p
  - arvostelijan tulee pystyä asentamaan ohjelma ja käyttämään sitä ohjeen avulla
- Testausdokumentti 2p
- JavaDoc 2p
  - Suoraviivaisia gettereitä, settereitä ja konstruktoreja ei tarvitse dokumentoida
- Repositorio ja README 1p
  - Repositorion ja README:n oletetaan olevan aiempien viikkojen vaatimusten mukainen
  - Repositoriossa on _loppupalautus_-niminen release, joka sisältää suoritettavissa olevan jar-tiedoston ja muut ohjelman mahdollisesti tarvitsemat tiedostot

[Referenssisovellus](https://github.com/mluukkai/OtmTodoApp) toimii hyvänä esikuvana dokumentaation suhteen. JavaDoc tosin on sovelluksessa osittain puutteelinen.

**HUOM** älä copypastea referenssisovelluksen dokumentaation tekstiä omaan dokumentaatioosi, kirjoita teksti omin sanoin. Tekstin suora kopiointi johtaa hylkäämiseen.