# Viikon 2 laskarit

Tehtävät on tarkoitus tehdä joko pajassa tai omatoimisesti. Tehtävien palautuksen deadline on ti 26.3. klo 23:59

Tehtävät palautetaan GitHubin avulla Labtoolin rekisteröimääsi repositorioon.

Muista pushata tehtävät GitHubiin ennen viikkodeadlinea.
  
 - Klo 00 jälkeen tulevia repositorion päivityksiä ei huomioida pisteytyksessä, eli ne tuovat 0 pistettä.

Tee palautuksia varten repositorion sisällä olevaan hakemistoon _laskarit_ uusi alihakemisto _viikko2_.

Viikon palautuksista on tarjolla 2 pistettä. Pisteytys arvioidaan palautuksen laadun perusteella.

Huomaa, että tällä viikolla on myös harjoitustyöhön liittyviä [tavoitteita](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/tehtavat/harjoitustyo_viikko2.md)

## 1 

* tutustu [JUnit-ohjeeseen](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/junit.md)
* lukiessasi tee testit myös itse
* lisää lopuksi maksukortille seuraavat testit:
  * maukkaan lounaan syöminen ei vie saldoa negatiiviseksi, ota tähän mallia testistä syoEdullisestiEiVieSaldoaNegatiiviseksi
  * negatiivisen summan lataaminen ei muuta kortin saldoa
  * kortilla pystyy ostamaan edullisen lounaan, kun kortilla rahaa vain edullisen lounaan verran (eli 2.5e)
  * kortilla pystyy ostamaan maukkaan lounaan, kun kortilla rahaa vain maukkaan lounaan verran (eli 4e)

**HUOM1** on suositeltavaa, että yksi testi testaa vain "yhtä asiaa" kerrallaan. Tee siis jokaisesta ylläolevasta oma testinsä.

**HUOM2** Kirjoita assertEquals-komennot aina siten, että ensimmäisenä parametrina on odotettu tulos ja toisena parametrina testatun metodin antama tulos.

## 2 Maksukortti ja kassapääte: testit kortille

**HUOM** tämä tehtävä tehdään **eri projektiin** kuin edellinen, ja vaikka molemmissa tehtävissä on saman niminen luokka, eli _Maksukortti_ ovat luokat erilaiset, eli **älä** copypastaa edellisen tehtävän koodia tai tehtäviä tähän tehtävään.

Tämän tehtävän projekti _ladataan internetistä_ hieman alempana olevan ohjeen mukaan.

Ohjelmoinnin perusteiden viikolla [5 tehtävissä 101](https://www.cs.helsinki.fi/group/java/s16-materiaali/viikko5/#101maksukortti_ja_kassapaate) toteutettiin "tyhmä" Maksukortti ja Kassapääte. 

Rahan käsittely double-tyyppisenä on hiukan ongelmallista. Seuraavassa rahaa käsitellän kokonaislukuna ja kaikki rahamäärät talletetaan eurojen sijasta sentteinä.

Ohjelmointiuransa aloittelevan tuttavasi vastaus seuraavassa:

``` java
public class Maksukortti {
 
    private int saldo;
 
    public Maksukortti(int saldo) {
        this.saldo = saldo;
    }
 
    public int saldo() {
        return saldo;
    }
 
    public void lataaRahaa(int lisays) {
        this.saldo += lisays;
    }
 
    public boolean otaRahaa(int maara) {
        if (this.saldo < maara)
            return false;
 
        this.saldo = this.saldo - maara;
        return true;
    }

    @Override
    public String toString() {
        int euroa = saldo/100;
        int senttia = saldo%100;
        return "saldo: "+euroa+"."+senttia;
    }    
}
```

Kassapäätteelle on lisätty metodit, jotka mahdollistavat myytyjen lounaiden määrän ja kassassa olevan rahamäärän kysymisen, toString()-metodi on poistettu:

``` java
public class Kassapaate {
 
    private int kassassaRahaa;
    private int edulliset;
    private int maukkaat;
 
    public Kassapaate() {
        this.kassassaRahaa = 100000;
    }
 
    public int syoEdullisesti(int maksu) {
        if (maksu >= 240) {
            this.kassassaRahaa = kassassaRahaa + 240;
            ++this.edulliset;
            return maksu - 240;
        } else {
            return maksu;
        }
    }
 
    public int syoMaukkaasti(int maksu) {
        if (maksu >= 400) {
            this.kassassaRahaa = kassassaRahaa + 400;
            this.maukkaat++;
            return maksu - 400;
        } else {
            return maksu;
        }
    }
 
    public boolean syoEdullisesti(Maksukortti kortti) {
        if (kortti.saldo() >= 240) {
            kortti.otaRahaa(240);
            this.edulliset++;
            return true;
        } else {
            return false;
        }
    }
 
    public boolean syoMaukkaasti(Maksukortti kortti) {
        if (kortti.saldo() >= 400) {
            kortti.otaRahaa(400);
            this.maukkaat++;
            return true;
        } else {
            return false;
        }
    }
 
    public void lataaRahaaKortille(Maksukortti kortti, int summa) {
        if (summa >= 0) {
            kortti.lataaRahaa(summa);
            this.kassassaRahaa += summa;
        } else {
            return;
        }
    }
 
    public int kassassaRahaa() {
        return kassassaRahaa;
    }
 
    public int maukkaitaLounaitaMyyty() {
        return maukkaat;
    }
 
    public int edullisiaLounaitaMyyty() {
        return edulliset;
    }
}
```

**Hae nyt projektin koodi koneellesi**.

Avaa terminaali, mene palautusrepositoriosi hakemistoon _laskarit/viikko2_ ja suorita seuraavat komennot:

```bash
wget https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/misc/Unicafe.zip
unzip Unicafe.zip
rm Unicafe.zip
```

**HUOM** jos käytät Windowsia ja koneellasi ei ole käytössä komentoa _wget_ lataa tehtävän koodi klikkaamalla yo. linkkiä. Muista siirtää projekti repositorion alle oikeaan hakemistoon!

Lisää ja commitoi hakemisto repositorioon.

Varmista komennolla _git status_, että working directory on puhdas ja kaikki on commitoitu:

```bash
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean
```

Olemme tähän asti suorittaneet testit NetBeansilla. Kokeillaan nyt miten testit voidaan suorittaa _komentoriviltä_.
* mene hakemistoon, jossa projekti sijaitsee
  * **Huom** seuraavassa oletetaan että koneellesi on asennettu [maven](https://maven.apache.org/), laitoksen koneilla ja fuksikannettavissa maven löytyy valmiiksi, Linuxiin sekä OSX:n se on helppo asentaa, kenties myös Windowsiin
  * jos et jostain syystä saa mavenia toimimaan komentoriviltä, niin voit käyttää sitä NetBeansin kautta [tämän](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/tehtavat/viikko2.md#maven-komentojen-suorittaminen-netbeansista) ohjeen avulla
* suorita testit antamalla komento _mvn test_
  * huomaa, että komento _mvn_ tulee antaa aina projektin juurihakemistossa, eli samassa hakemistossa, jossa sijaitsee tiedosto _pom.xml_
  * muista, että näet hakemiston sisällön komennolla _ls_

Jos kaikki on hyvin, saat raportin läpimenneistä testeistä

<pre>
Running com.mycompany.unicafe.MaksukorttiTest
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.248 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.046 s
[INFO] Finished at: 2018-02-27T15:59:21+02:00
[INFO] Final Memory: 19M/311M
[INFO] ------------------------------------------------------------------------
</pre>

### .gitignore

Kun testien jälkeen suoritat komennon _git status_, huomaat että projektin juureen on ilmestynyt uusi hakemisto _target_, joka ei ole gitin alaisuudessa

```bash
On branch master
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	target/

nothing added to commit but untracked files present (use "git add" to track)
```
maven-projektien hakemisto _target_, joka sisältää maven-komentojen aikaansaannoksia on tyypillisesti sellainen, jota emme halua versionhallinnan pariin.

git-repositorion juureen on mahdollista lisätä tiedosto [.gitignore](https://www.atlassian.com/git/tutorials/gitignore) jossa voidaan määritellä, mitä tiedostoja ja hakemistoja git jättää huomioimatta eli _ignoroi_.

Mene **repositoriosi juureen**, luo tiedosto _.gitignore_, avaa se editorilla ja lisää tiedostoon seuraava rivi:

<pre>
/laskarit/viikko2/Unicafe/target
</pre>

Kun nyt teet komennon _git status_ pitäisi tuloksen olla seuraava:

<pre>
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore
</pre>

Eli vaikka hakemistossa _/laskarit/viikko2/Unicafe_  on alihakemisto _target_, ei git niitä huomioi

### Takaisin testeihin

Avaa nyt projekti NetBeansilla.

*Tee valmiiseen testiluokkaan _MaksukorttiTest_ testit, jotka testaavat ainakin seuraavia asioita*:

* kortin saldo alussa oikein
* rahan lataaminen kasvattaa saldoa oikein
* rahan ottaminen toimii
  * saldo vähenee oikein, jos rahaa on tarpeeksi
  * saldo ei muutu, jos rahaa ei ole tarpeeksi
  * metodi palauttaa _true_, jos rahat riittivät ja muuten _false_

Voit suorittaa testit NetBeansilla tai komentoriviltä.

### Maven

Suoritimme testit komentoriviltä komennolla _mvn test_. Mistä on kyse? Maksukortin sisältämä projekti on määritelty [maven](https://maven.apache.org)-formaatissa. Maven on työkalu, jonka avulla voidaan hallita Javalla tehtyjen ohjelmien kääntämistä, testien suorittamista ja paljon muitakin työvaiheita, kuten pian tulemme näkemään. Kurssin ohjelmoinnin perusteet tehtäviä ei ole määritelty mavenilla, vaan hieman vanhemmassa [ant](http://ant.apache.org)-formaatissa. Ohjelmoinnin jatkokurssilla ainakin myöhemmillä viikoilla on käytössä maven, se ei tosin juurikaan näy normaalille NetBeans-käyttäjälle.

Maven-projektien juuressa on tiedosto _pom.xml_, joka sisältää projektin konfiguraatiot. Katso miltä tiedosto näyttää. Tiedosto löytyy NetBeansista kohdan _project files_ alta.

Tiedostossa on määritelty, että projektilla on testejä suoritettaessa _riippuvuutena_ JUnit-kirjaston versio 4.12:

``` java
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

Tiedostossa _plugin_-osiossa on määritelty, että koodi käännetään Javan versiota 8 käyttäen. Maven käyttää Java kasista numeroa 1.8 (kohdat _source_ ja _target_):

``` java
<build>
    <plugins>
        <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            <version>2.5</version>
        </plugin>
        ...
    </plugins>
</build>
``` 

## 3 Testauskattavuus

Olemme tyytyväisiä, uskomme että testitapauksia on nyt tarpeeksi. Onko tosiaan näin? Onneksi on olemassa työkaluja, joilla voidaan tarkastaa testien rivi- ja haarautumakattavuus. __Rivikattavuus__ mittaa mitä koodirivejä testien suorittaminen on tutkinut. Täydellinen rivikattavuuskaan ei tietenkään takaa että ohjelma toimii oikein, mutta on parempi kuin ei mitään. __Haarautumakattavuus__ taas mittaa mitä eri suoritushaaroja koodista on käyty läpi. Suoritushaaroilla tarkoitetaan esim. if-komentojen valintatilanteita. 

Projektiin on valmiiksi konfiguroitu käytettäväksi [Jacoco](http://www.eclemma.org/jacoco/) joka mittaa sekä lause- että haarautumakattavuuden. Määrittely on tiedoston pom.xml osiossa _plugins_:

``` java
<build>
    <plugins>
        // ...
        <plugin>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.0</version>
            <executions>
                <execution>
                    <id>default-prepare-agent</id>
                    <goals>
                        <goal>prepare-agent</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>  
    </plugins>
</build>
``` 

_jacoco_ suoritetaan komentoriviltä (projektihakemistossa ollessasi) komennolla <code>mvn test jacoco:report</code>

Tulokset tulevat projektihakemistosi alihakemistoon __target/site/jacoco/index.html__. Avaa tulokset web-selaimella:

<img src="https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/web/images/v2-4.png" width="800">

Useilla selaimilla tämä tapahtuu komennolla __open file__. Laitoksen koneella voit myös avata selaimen terminaalissa menemällä ensin projektihakemistoon ja antamalla komennon __chromium-browser target/site/jacoco/index.html__ 

**Jos maksukortin koodissa on vielä rivejä tai haarautumia (merkitty punaisella) joille ei ole testiä, kirjoita sopivat testit.**

## Maven-komentojen suorittaminen NetBeansista

Maven-komentoja on mahdollista suorittaa myös NetBeansin kautta. Tämä tapahtuu klikkaamalla projektin kohdalla hiiren oikealla napilla: 

<img src="https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/web/images/v2-6.png" width="600">

"Remember as"-toiminnolla voit tallettaa konfiguroidun maven-komentosarjan:

<img src="https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/web/images/v2-5.png" width="600">

## 4 Maven-projektin hakemistorakenne

Maven-projektien hakemiston rakenne noudattaa aina samaa logiikkaa. Hakemiston juuressa on projektin konfiguraatiot sisältävä tiedosto _pom.xml_. Ohjelman lähdekoodi on hakemistossa _src/java_ ja testit hakemistossa _src/test_. Hakemistoon _target_ generoituvat kaikki maven-komentojen aikaansannokset. 

Suorita komento _mvn clean_. Komento poistaa hakemiston _target_. 

Suorita projektin koodin käännöksen suorittava komento _mvn compile_. Tutki mitä hakemiston _target_ sisälle syntyy.

Suorita testit komennolla _mvn test_. Tutki mitä hakemistosta _target_ löytyy komennon suorittamisen jälkeen.

## 5 Kassapäätteen testit

Laajennetaan Unicafen testaus kattamaan myös kassapääte.

*Tee testiluokka _KassapaateTest_ ja tee testit jotka testaavat ainakin seuraavia asioita:*
* luodun kassapäätteen rahamäärä ja myytyjen lounaiden määrä on oikea (rahaa 1000, lounaita myyty 0)
* käteisosto toimii sekä edullisten että maukkaiden lounaiden osalta
  * jos maksu riittävä: kassassa oleva rahamäärä kasvaa lounaan hinnalla ja vaihtorahan suuruus on oikea
  * jos maksu on riittävä: myytyjen lounaiden määrä kasvaa
  * jos maksu ei ole riittävä: kassassa oleva rahamäärä ei muutu, kaikki rahat palautetaan vaihtorahana ja myytyjen lounaiden määrässä ei muutosta
* _seuraavissa testeissä tarvitaan myös Maksukorttia jonka oletetaan toimivan oikein_
* korttiosto toimii sekä edullisten että maukkaiden lounaiden osalta
  * jos kortilla on tarpeeksi rahaa, veloitetaan summa kortilta ja palautetaan true
  * jos kortilla on tarpeeksi rahaa, myytyjen lounaiden määrä kasvaa
  * jos kortilla ei ole tarpeeksi rahaa, kortin rahamäärä ei muutu, myytyjen lounaiden määrä muuttumaton ja palautetaan false
  * kassassa oleva rahamäärä ei muutu kortilla ostettaessa
* kortille rahaa ladattaessa kortin saldo muuttuu ja kassassa oleva rahamäärä kasvaa ladatulla summalla

Huomaat että kassapääte sisältää melkoisen määrän "copypastea". Nyt kun kassapäätteellä on automaattiset testit, on sen rakennetta helppo muokata eli refaktoroida siistimmäksi koko ajan kuitenkin varmistaen, että testit menevät läpi. Tulemme tekemään refaktoroinnin myöhemmin kurssilla.

## 6

Varmista jacocon avulla, että kassapäätteen testeillä on 100% lause- ja haarautumakattavuus.

## 7 

Talleta kohdassa [testikattavuus](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/tehtavat/viikko2.md#3-testauskattavuus) olevan kuvan tyylinen [screenshot](https://www.take-a-screenshot.org/) projektisi kattavuusraportista palautusrepositoriosi hakemistoon _laskarit/viikko2_. 

**Muista tallentaa tekemäsi muutokset gitiin ja työntää ne Githubiin (_git push_).**
