# Viikon 1 tehtävät

Tehtävät on tarkoitus tehdä joko pajassa tai omatoimisesti. Tehtävien palautuksen deadline on tiistai 19.3 klo 23:59

Tehtävät palautetaan Githubin ja Labtoolin avulla. Lisää palautuksesta myöhemmin. Osa tehtävistä ei näy palautuksesta mitenkään. Niiden tekemättä jättäminen näkyy puuttuvana osaamisena ja saattaa aiheuttaa myöhemmin hankaluuksia.

Viikon palautuksista on tarjolla 2 pistettä. Pisteytys arvioidaan palautuksen laadun perusteella.

Muista pushata tehtävät GitHubiin ennen viikkodeadlinea. Myöhässä tehty palautus ei tuo pisteitä.

## Komentorivin harjoittelua

Graafisten käyttöliittymien olemassaolosta huolimatta ohjelmistoalalla on edelleen erittäin tärkeää hallita komentorivin eli terminaalin käyttö. 

## osa 1

Opettele käyttämään "riittävästi" komentoriviä (ks. alla oleva lista). Opettelu käy ehkä helpoiten tekemällä osoitteessa [https://www.codecademy.com/learn/learn-the-command-line](https://www.codecademy.com/learn/learn-the-command-line) olevan onlinekurssin kaksi ensimmäistä osaa _Navigating the File System_ ja _Viewing and Changing the File System_ (maksullisista pro-episodeista ei kannata välittää).

**HUOM. Codecademy vaatii kirjautumisen Facebook, Google tai GitHub -tunnuksella. Kurssilla käytetään muutenkin GitHubia, niin se tunnus pitäisi kaikilla olla vähintään olla olemassa, jotta pääsee kirjautumaan.**

Tämän tehtävän jälkeen sinun tulisi hallita seuraavat asiat:
* käsitteet
  * root directory
  * home directory
  * parent directory
  * child directory
  * working directory
  * .. ja *
* ja osata käyttää komentoja
  * pwd
  * cd
  * ls, ls -a, ls -l, ls -t
  * mkdir
  * touch
  * cp
  * rm, rm -r
  * mv

Tulet tarvitsemaan komentorivin käyttötaitoja tällä kurssilla ja muutenkin opinnoissasi.

## osa 2

Ota ssh-yhteys linuxpalvelimeen _melkki.cs.helsinki.fi_, _melkinpaasi.cs.helsinki.fi_ tai _melkinkari.cs.helsinki.fi_. Linuxilla ja macilla yhteys otetaan komentoriviltä komennolla _ssh kayttajatunnus@palvelimenosoite_. Windowsilla ssh-yhteyden ottaminen onnistuu esimerkiksi [putty:llä](http://www.putty.org).

Kirjauduttuasi laitoksen palvelimelle, tee seuraavat toimenpiteet:
* luo kotihakemistoosi hakemisto _kurssit_
  * **HUOM** joidenkin kohdalla melkillä on ollut ongelmia kotihakemiston asetuksissa ja esim. hakemiston luomisen seurauksena on virhe 'permission denied'. Jos törmäät ongelmaan, lähetä viesti osoitteeseen _it-support@cs.helsinki.fi_ ja raportoi ongelmaksi "ei oikeuksia kotihakemistoon melkillä"
  * kokeile myös jos kirjaantuminen toiselle koneelle, esim. _melkinpaasi.cs.helsinki.fi_ tuottaisi paremman tuloksen
* luo hakemistolle _kurssit_ alihakemisto _ot2019_
* ja luomallesi hakemistolle alihakemisto _viikko1_
* mene kotihakemistoosi ja luo sen alle hakemisto _temp_
* mene hakemistoon _temp_
* hae osoitteessa _https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/misc/Unicafe.zip_ oleva tiedosto [wget](https://en.wikipedia.org/wiki/Wget)-ohjelmalla
  * wget toimii siten, että sille annetaan ladattava tiedosto parametriksi
* haettu tiedosto on _zip-paketti_, pura se _unzip_-ohjelmalla
  * myös unzip toimii siten, että sille annetaan purettava tiedosto parametriksi
* komennon suorittamisen jälkeen hakemistoon on ilmestynyt hakemisto _Unicafe_
* siirrä hakemisto hakemiston _kurssit/ot2019/viikko1_ alihakemistoksi
* poista zip-paketti
* poista hakemisto _temp_
* mene nyt uudessa paikassa olevaan hakemistoon _Unicafe_
* suorita komento _mvn clean_
  * jos näet rivien joukossa ilmoituksen _BUILD SUCCESS_ on tehtävä tehty

**Mene tämän jälkeen _kotihakemistoon_ ja anna komento _tree kurssit_. Copypastea komennon tulostus talteen, tarvitset sitä myöhemmin.**

## tab complete

Komentoriviä käyttäessä kannattaa ehdottomasti totutella _tab-completen_ käyttöön. _Tab_ on näppäin, joka näyttää suunnilleen seuraavalta

![](https://github.com/mluukkai/otm2016/raw/master/img/tab.jpg)

Tab:ia painamalla voit komentorivillä täydentää kirjoittamasi komennon nimen tai parametrin. Esim. jos olet siirtymässä hakemistoon nimeltään _ohjelmistotekniikka-kevat-2019_, riittää, että kirjoitat <code>cd oh</code> ja painat tabia. Jos hakemistossasi ei ole muita tiedostoja tai hakemistoja, jotka alkavat merkeillä _oh_, nimi täydentyy. Jos on, niin voit joutua kirjoittamaan merkin tai kaksi lisää. Jos tiedostoja on useampia etkä ole varma oikeasta nimestä, painamalla tabia useamman kerran näet mahdolliset vaihtoehdot.

Myös komentojen nimet voi täydentää tab-completella. Esim. haluat avat _chromium-browser_ web-selaimen komentoriviltä, riittää että kirjoitat <code>chro</code> ja painat tabia. Komennon nimi täydentyy.

Ei pidä myöskään unohtaa _nuolta ylöspäin_. Sen avulla voit selata aiemmin kirjoittamiasi komentoja.

## yhtäaikaiset terminaalit / terminaalin tabit

Aloitteleva komentorivin käyttäjä pitää usein ainoastaan yhtä terminaali-ikkunaa kerrallaan auki. Useimmissa tilanteissa työtehosi moninkertaistuu, jos avaat useita terminaaleja näytöllä tai avaat yhteen terminaaliin useita "tabeja" eli välilehtiä. Uuden tabin saat avautumaan painamalla yhtä aikaa _ctrl_, _shift_ ja _t_ tai sovelluksen valikosta (joka laitoksen Linuxeissa sijaitsee ruudun yläreunassa).
  
## Versionhallinta

Tutustumme seuraavaksi versionhallintaan. 

Mitä tarkoitetaan versionhallinnalla? Lainaus sivulta [https://www.atlassian.com/git/tutorials](https://www.atlassian.com/git/tutorials)

> Version control systems are a category of software tools that help a software team manage changes to source code over time. Version control software keeps track of every modification to the code in a special kind of database. If a mistake is made, developers can turn back the clock and compare earlier versions of the code to help fix the mistake while minimizing disruption to all team members.

Vaikka ylläoleva puhuu versionhallinnasta ohjelmistotiimien yhteydessä, kannattaa versionhallintaa käyttää oikeastaan yhdenkin hengen projekteissa ja muunkinlaisen materiaalin, kuin koodin hallinnoimiseen. Esim. tämän kurssin kaikki materiaali on talletettu versionhallintaan.

Nykyään suosituin versionhallintaohjelmisto on [git](https://git-scm.com). Tutustumme tänään gitin alkeisiin. 

**HUOM** tämä tehtävä tulee tehdä Linuxilla tai Macilla, jolle on asennettu Git. Helpointa lienee tehdä tehtävä laitoksen koneella. Git kannattaa joka tapauksessa asentaa omalle koneelle. Gitin voi asentaa myös Windowsille.

## Gitin alkeet

### konfiguraatioita

Avaa terminaali omalla koneellasi. **Seuraavat tehtävät tehdään siis paikallisesti, ei melkillä!**

Määrittele gitille **oma nimesi** sekä **käyttämäsi email-osoite** antamalla komennot:

```
 git config --global user.name "Your Name"
 git config --global user.email you@example.com
```

Varmista komennolla <code>git config -l</code>, että määrittelyt menivät oikein.

Määritellään vielä git käyttämään sopivia värejä komennolla <code>git config --global color.ui</code> ja **vaihdetaan gitin käyttämäksi oletuseditoriksi** _nano_ komennolla <code>git config --global core.editor nano</code>
* jos käytät vimiä, voit jättää oletuseditorin muuttamatta

Tee vielä seuraava konfiguraatio

```
git config --global push.default matching
```

Tämä liittyy _git push_ -komennon oletusarvoiseen toiminnallisuuteen. Komennosta lisää myöhemmin.

### repositorio

Tee nyt sopiva hakemisto gitin harjoittelua varten ja mene hakemistoon, eli anna esim. komennot:
* mkdir ot_viikko1
* cd ot_viikko1

**HUOM:** varmista nyt että olet luomassasi hakemistossa, eli jos suoritat komennon _ls_, ei hakemistossa pitäisi olla mitään.

Luodaan hakemistosta paikallinen _git-repositorio_ antamalla komento <code>git init</code>

Git ilmoittaa alustaneensa repositorion:

<pre>
mluukkai@melkinpaasi:~/ot_viikko1$ git init
Initialised empty Git repository in /home/ad/fshome4/u4/m/mluukkai/Linux/ot_viikko1/.git/
</pre>

Jos katsot hakemiston sisältöä komennolla <code>ls -la</code> huomaat, että hakemiston sisälle on ilmestynyt hakemisto <code>.git</code>. Git käyttää luotua hakemistoa pitääkseen kirjaa repositorioon talletetuista tiedostoista.

**HUOM** koska hakemiston nimi (_.git_) alkaa pisteellä, ei komento _ls_ näytä sitä oletusarvoisesti. Parametri _a_ näyttää myös pisteellä alkavat tiedostot ja hakemistot. Kokeile, miten _ls -a_ ja _ls -la_ eroavat toisistaan!

Pysy edelleen repositorion sisältävässä hakemistossasi _ot_viikko1_.

Luo hakemistoon tiedosto nimeltään _tiedosto.txt_, esim. komennolla <code>touch</code>. Luotuasi tiedoston, suorita komento <code>git status</code>:

<pre>
mluukkai@melkinpaasi:~/ot_viikko1$ touch tiedosto.txt
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	tiedosto.txt

nothing added to commit but untracked files present (use "git add" to track)
mluukkai@melkinpaasi:~/ot_viikko1$
</pre>

Git ilmoittaa, että on olemassa tiedosto, joka on tilassa _untracked_, eli tiedostoa ei ole lisätty versionhallinnan pariin.

Kuten komennon tuloste kertoo, tiedoston lisääminen gitin alaisuuteen (...to include in what will be committed) tapahtuu komennolla <code>git add tiedosto.txt</code>

Suorita lisäys ja sen jälkeen komento <code>git status</code>:

<pre>
mluukkai@melkinpaasi:~/ot_viikko1$ git add tiedosto.txt
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   tiedosto.txt
</pre>

Git kertoo nyt, että _tiedosto.txt_ on niiden muutosten joukossa, jotka voidaan _commitoida_.

### commit

Commitoimisella tarkoitetaan tiedostojen ja hakemistojen sekä niihin liittyvien muutosten tallentamista _git-repositorioon_.

Suoritetaan commitointi antamalla komento <code>git commit -m "tiedosto.txt luotu"</code>

<pre>
mluukkai@melkinpaasi:~/ot_viikko1$ git commit -m "tiedosto.txt luotu"
[master (root-commit) 0e12cfa] tiedosto.txt luotu
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 tiedosto.txt
</pre>

Suorita jälleen komento <code>git status</code>

<pre>
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master
nothing to commit, working directory clean
</pre>

Git ilmoittaa, että _working directory clean_, eli hakemistosi on samassa tilassa kuin git-repositorio.

### working directory, index/staging,  repository  

**Muista käyttää tab-completea tehtäviä tehdessäsi!**

Kun teet muutoksia hakemistosi alla oleviin tiedostoihin (tai hakemistoihin), kohdistuvat muutokset _working directoryyn_ eli työhakemistoon. 
* Tee jokin muutos tiedostoon tiedosto.txt 
  * käytä tiedostojen editointiin _nano_-editoria. Editori käynnistyy komentoriviltä komennolla _nano tiedosto.txt_
  * saat tallennettua nanossa tiedoston painamalla yhtä aikaa _ctrl_ ja _o_
  * editori sulkeutuu painamalla _ctrl_ ja _x_
* Luo hakemistoon uusi tiedosto, nimeltään _toinen.txt_

Suorita jälleen <code>git status</code>

<pre>
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   tiedosto.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	toinen.txt

no changes added to commit (use "git add" and/or "git commit -a")
</pre>

Git ilmoittaa nyt, että uusi tiedosto on _untracked_ ja että aiemmassa tiedostossa on muutoksia, jotka eivät ole _staged for commit_.

Toimitaan ohjeen mukaan eli lisätään muutokset ja uusi tiedosto commitoitavien joukkoon. Molempien tiedostojen yhtäaikainen "addaaminen" onnistuu komennolla <code>git add .</code>

Tarkistetaan taas tilanne komennolla <code>git status</code>

<pre>
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   tiedosto.txt
	new file:   toinen.txt
</pre>

Sekä muutos että uusi tiedosto ovat nyt valmiina committoitavaksi. 

Committointi onnistuu komennolla _git commit_. Kuten edelliselläkin kerralla, annetaan komennolle parametrina _commit-viesti_, eli merkkijono, joka kuvaa mitä muutoksia uusi commit tuo edelliseen nähden:

<code>git commit -m"muutos ja lisäys"</code>

Tarkasta committoinnin jälkeen jälleen tilanne komennolla _git status_.

**HUOM** jos suoritat commitoinnin vahingossa ilman commit-viestiä, eli parametria _-m_, avaa git tekstieditorin ja olettaa että haluat kirjoittaa commit-viestin editoriin. Jos et määritellyt alun ohjeen mukaan gitille editoriksi nanoa, avautuu oletusarvoinen editori _vim_ ja joudut kenties googlaamaan, miten pääset pois editorista.

Tiedostot ja niihin tehdyt muutokset voivat siis olla gitin suhteen _kolmessa eri tilassa_. 
* Aluksi tiedostot (tai niihin tehdyt muutokset) ovat vain _working directoryssä_ ja git ei noteeraa niitä ennen kuin ne lisätään komennolla <code>git add</code>
* Tämän jälkeen tiedostot ovat valmiina commitoitavaksi. Gitin terminologian mukaan valmiina committoitavaksi olevat tiedostot ovat _staging_-alueella
*  Komento <code>git commit</code> siirtää stagingissa olevat muutokset repositorioon eli luo uuden _commitin_

Seuraava kuva havainnollistaa sitä, miten tiedoston _tila_ vaihtuu git-komentoja tekemällä.

![](https://github.com/mluukkai/otm2016/raw/master/img/lh3-2.png)

Kun tiedosto luodaan, menee se gitin _working directoryyn_. Komennolla _git add_ tiedosto siirtyy _staging_-alueelle, eli valmiiksi committointia varten. Stagingissa oleva tiedosto viedään (eli "commitoidaan") repositorioon komennolla _git commit_. Kun committoitua tiedostoa taas editoidaan, menevät muutokset jälleen _working directoryyn_.

## git commit

Jokainen komennon _git commit_ suorittaminen siis synnyttää repositorioon uuden commitin, eli uuden "tilan". Komennolla <code>git log</code> on mahdollista nähdä, mitä committeja repositorio sisältää:

<pre>
mluukkai@melkinpaasi:~/ot_viikko1$ git log
commit 6aff75ab51d14d7cb9a72867ba13d9782d06c7ff (HEAD -> master)
Author: Matti Luukkainen <mluukkai@iki.fi>
Date:   Sun Oct 7 19:33:32 2018 +0300

    muutos ja lisäys

commit 9e6a83d058c9564e8a390f8766845d45b365f360
Author: Matti Luukkainen <mluukkai@iki.fi>
Date:   Sun Oct 7 19:32:12 2018 +0300

    tiedosto.txt luotu
mluukkai@melkinpaasi:~/ot_viikko1$
</pre>

Gitin logi kertoo jokaisen commitin ajan, tekijän, viestin ja _tunnisteen_. Tunnisteita käytetään, jos on esim. tarvetta palata johonkin vanhan commitin tilaan. 


Voit selata logia nuolinäppäimillä. Pääset ulos _git log_:ista painamalla _q_.

## lisää harjoittelua

Muista käyttää komentoa _git status_ mahdollisimman usein. Älä myöskään unohda tab-completea!

* Luo tiedosto _kolmas.txt_
* Lisää se commitoitavaksi ja commitoi 
* Muuta tiedostojen _toinen.txt_ ja _kolmas.txt_ sisältöä ja commitoi muutokset
* Luo hakemisto _stuff_ ja sen sisälle jokin tiedosto
* Lisää muutokset committoitavaksi ja committoi
  * Huomaa, että hakemiston lisääminen riittää, sen sisältämät tiedostot tulevat automaattisesti lisätyksi
* Katso miltä git-logi näyttää

## gitk

Gitin committeja voi tarkastella myös graafisella _gitk_-komennolla (OSX:lle ja Windowsille vastaava työkalu on [Sourcetree](https://www.sourcetreeapp.com)). Suorita komento repositoriossa:

![](https://github.com/mluukkai/otm2016/raw/master/img/lh3-1.png)

Vasemmalla yläkulmassa näet kaikki commitit. Uusin tilanne ylimpänä. Uusimman commitin nimi on *master*. Klikkaamalla commitia, näet muissa ikkunoissa commitiin liittyviä tietoja. Oikealla alakulmassa näet ne tiedostot, jotka ovat muuttuneet commitissa (jos valinta on _patch_) tai ne tiedostot, joita repositoriossa oli olemassa commitin aikana (jos valinta on _tree_). Vasemmassa alakulmassa pystyt tarkastelemaan commitin tiedostoihin tekemiä muutoksia tai tiedostojen tilaa commitin aikana.  Valinnat ovat hieman hämäävät, sillä ne toimivat eri tavoin riippuen oikean puolen moodista.

Vastaava näkymä OSX:n [Sourcetree](https://www.sourcetreeapp.com)-ohjelmalla tarkasteltaessa:

![](https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/web/images/lh1-1a.png)

Seuraavaa tehtävää tekiessäsi kannattaa terminaaliin avata uusi välilehti, jotta voit pitää gitk:ta käynnissä.

* Kopioi tiedostoon _tiedosto.txt_ jostain paljon tekstiä ja commitoi tiedosto
* Poista nyt osa tiedoston tekstistä ja lisää tiedostoon hieman lisää tekstiä
* commitoi muutosten jälkeen
* Päivitä gitk:n näkymä (file/update) ja katso miten muutokset näkyvät (tarkastele kahta ylintä committia) 
  * valitse oikeasta alakulmasta _patch_ ja vasemmasta _diff_
  * näin näet commitin aiheuttamat muutokset [diff](https://fi.wikipedia.org/wiki/Diff)-muodossa
  * jos oikealta on valittuna _tree_, näkyy vasemmalla puolella (valinnasta riippumatta) tiedostojen commitin aikainen tilanne 
* Jos käytät sourcetreetä, sen pitäisi päivittyä automaattisesti ja näyttää muutos _diff_-muodossa

## tiedoston poistaminen ja uudelleennimentä

* Poista tiedosto _toinen.txt_
* suorita _git status_
* commitoi muutos
  * poista ensin tiedosto gitin alaisuudesta komennolla _git rm_
* varmista komennolla _git status_, että kaikki on niinkuin kuuluukin
* muuta tiedoston _tiedosto.txt_ nimeksi _eka.txt_
  * uudelleennimentä tapahtuu komennolla _mv_
* suorita _git status_
  * miten git käsittelee uudelleennimennän?
* commitoi muutos

## git add -p

* Tee jotain muutoksia tiedostoihin _eka.txt_ ja _kolmas.txt_
  * tee sekä lisäyksiä että poistoja
* lisää ne commitoitavaksi komennolla _git add -p_
  * git näyttää nyt jokaisen tekemäsi muutoksen _patch_-muodossa ja pyytää varmistamaan lisätäänkö muutos commitoivaksi
  * hyväksy painamalla _y_ ja enter
* commitoi muutokset
* tee tiedostoihin tehtyjen muutosten commitoitavaksi lisääminen *aina* komennolla _git add -p_, näin pääset tarkastamaan, että muutokset ovat juuri ne mitä oletat olevasi lisäämässä
* Huomaa, että kokonaan uudet tiedostot eivät siirry committoitavaksi komennolla _git add -p_ 

## muutosten peruminen

Joskus tiedostoihin tulee tehtyä muutoksia, jotka on tarpeen perua 
* tee nyt joku muutos tiedostoon _eka.txt_, **älä** lisää tiedostoa committoitavaksi
* suorita komento *git status*

```bash
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   eka.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Kuten oletettua, git kertoo että olemme tehneet muutoksia, jotka eivät ole "staged for commit", eli lisättyjä commitoitavaksi. 
* Päätetäänkin perua muutokset. Se onnistuu komennolla <code>git checkout -- eka.txt</code>
* Kun suoritat uudelleen komennon _git status_ huomaat, että working directory ei enää sisällä muutoksia:

```bash
mluukkai@melkinpaasi:~/ot_viikko1$ git checkout -- eka.txt
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master
nothing to commit, working directory clean
```

* Varmista vielä, että tiedoston sisältö on sama kuin ennen muutoksia

Myös stagingiin viety eli valmiina committoitavaksi oleva muutos voidaan perua. 
* Tee muutoksia tiedostoon _kolmas.txt_ ja lisää se committoitavaksi. **Älä** kuitenkaan committoi. 
* git statuksen pitäisi näyttää seuraavalta

``` bash
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   kolmas.txt

mluukkai@melkinpaasi:~/ot_viikko1$
```

Ohje muutoksen perumiseen löytyy git statuksen tulosteesta.
* suorita muutokset peruva komento <code>git reset HEAD kolmas.txt</code>
* katsotaan jälleen _git status_

``` pre
mluukkai@melkinpaasi:~/ot_viikko1$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   kolmas.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Tiedosto ei siis enää ole _staged_-tilassa, muutokset ovat kuitenkin _working directoryssä_, eli jos katsot tiedoston sisällön, muutokset ovat vielä olemassa
* pääset perumaan muutokset kokonaan antamalla komennon <code>git checkout -- kolmas.txt</code>
* varmista, että tiedosto on palannut muutoksia edeltävään tilaan

Seuraavassa tiedoston tilaa kuvaava kaavio täydennettynä, eli jos tiedosto on lisätty committoitavaksi, eli se on  _staged_, voidaan muutos perua komennolla _git reset HEAD_. Tällöin muutokset kuitenkin vielä jäävät tiedostoon, eli ovat _working directoryssä_. Tiedosto saadaan palautettua repositoriossa olevaan edellisen commitin tilaan komennolla _git checkout_.

![](https://github.com/mluukkai/otm2016/raw/master/img/lh3-3.png)

## Harjoittelua

- luo repositiosi sisälle hakemisto _tiedostoja_ ja hakemiston sisälle tiedostot _file1_, _file2_ ja _file3_
- commitoi muutokset
  - muista miten pystyt lisäämään kokonaisen hakemiston sisällön committoitavaksi yhdellä komennolla
- muuta tiedoston _file1_ sisältöä ja poista tiedosto _file2_
- peru muutokset!
- muuta tiedoston _file3_ sisältöä, lisää commitoitavaksi
- peru muutokset!
- poista tiedosto _file1_ ja uudelleennimeä tiedosto _file2_ tiedostoksi _file22_
- committoi 

Suorita repositoriossa komento _git log --stat | cat_ ja **ota komennon tulos talteen**, tulet tarvitsemaan sitä myöhemmin!


## GitHub 

Gitin käytöstä on toki hyötyä jo harjoittelemallammekin tavalla, eli muodostamalla paikallisen koneen hakemistosta repositorio. Pääsemme kuitenkin nauttimaan kertaluokkaa suuremmista hyödyistä liittämällä repositoriomme internetissä olevaan _etärepositorioon_. Etärepositorion kautta repositorion tiedostot on helppo jakaa useiden koneiden tai/ja useiden käyttäjien kesken.

Internetin johtava paikka etärepositorioiden tallettamiseen on [GitHub](https://github.com)

Ennen GitHubin käytöönottoa, tee uusi git-repositorio paikalliselle koneelle, seuraavassa oletetaan että hakemiston nimi on _ot-harjoitustyo_. 

**HUOM: älä luo uutta repositoriota aiemmin tekemäsi harjoitusrepositorion sisälle!**

Esim. seuraavat komennot siirtyvät kotihakemistoon, luovat sen alle hakemiston _ot-harjoitustyo_, siirtyvät hakemistoon, alustavat sen git-repositorioksi sekä lisäävät ja commitoivat yhden tiedoston repositorioon:

<pre>
cd 
mkdir ot-harjoitustyo
cd ot-harjoitustyo
git init
touch README.md
git add .
git commit -m"initial commit"
</pre>

Siirrytään sitten GitHubin käyttöön

* Luo itsellesi tunnus GitHubiin (ellei sinulla jo ole tunnusta)
* Luo uusi repositorio
  * uuden repositorion luomistoiminto löytyy vasemman ylänurkan plus-symboolin alta
* **Älä laita rastia** kohtaan *Initialize this repository with a README*

![](https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/web/images/lh1-2a.png)

* luo repositorio painamalla vihreää _Create repository_ -nappia

Seuraavaksi haluamme liittää GitHubiin luodun repositorion juuri luodun paikallisen koneen repositorion _ot-harjoitustyo_ etärepositorioksi.

* etärepositorion lisääminen onnistuu GitHubiin avautuvan näkymän ohjeiden mukaan 
* varmista, että kohdasta "Quick setup..." on valittu **SSH**

![](https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/web/images/lh1-3a.png)

- kopioi ylempi rivi kohdasta *...or push an existing repository from the command line*
- omassa esimerkissäni rivi on

``` bash 
git remote add origin git@github.com:mluukkai/ot-harjoitustyo.git
```

- pastea rivi komentoriville ja suorita komento painamalla enter
- suorita komento _git remote -v_
- tulostus kertoo, että githubin etärepositorio on liitetty paikalliseen repositorioosi nimellä _origin_

```bash
mluukkai@melkki:~/ot-harjoitustyo$ git remote  -v
origin	git@github.com:mluukkai/ot-harjoitustyo.git (fetch)
origin	git@github.com:mluukkai/ot-harjoitustyo.git (push)
```

- _origin_ on etärepositorion oletusarvoinen nimi. Nimi voi olla mikä tahansa ja etärepositorioitakin voi olla useita
- voimme siirtää paikallisen repositoriomme tilan etärepositorioon komennolla _git push_
  - saatat joutua tekemään ensimmäisen pushin pidemmässä muodossa _--set-upstream origin master_
- kokeillaan

```bash
mluukkai@melkki:~/ot-harjoitustyo$ git push --set-upstream origin master
Warning: Permanently added the RSA host key for IP address '192.30.253.112' to the list of known hosts.
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

## Julkinen avain

Jos olet jo asettanut julkisen avaimen esim. Tietokantojen perusteissa, pushauksen pitäisi toimia ja voit siirtyä [seuraavaan kohtaan](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/tehtavat/viikko1.md#kertausta).

Pushaus ei toimi. Nyt kyse on siitä, että git haluaisi suorittaa [julkisen avaimen](https://the.earth.li/~sgtatham/putty/0.55/htmldoc/Chapter8.html) autentikoinnin. Se ei kuitenkaan onnistu koska emme ole kertoneet gitille julkista salausavaintamme.

* luo salausavain antamalla komentoriviltä komento _ssh-keygen_
  * voit vastata kaikkiin kysymyksiin enterillä
* syntyy kaksi salausavainta, salainen ja julkinen. Ne sijoitetaan kotihakemistosi alla olevaan hakemistoon _.ssh_
* mene hakemistoon ja katso hakemiston sisältöä
* tiedosto _id_rsa.pub_ sisältää julkisen avaimen, se on tarkoitus kopioida githubiin jotta avaimeen perustuva kirjautuminen onnistuisi
  * näet tiedoston sisällön komennolla _cat id_rsa.pub_
* anna komentoriviltä komento _ssh-add_  
* mene GitHubin asetussivulle klikkaamalla oikean yläkulman symbolista ja valitsemalla _settings_
* valitse settingseistä _SSH and GPG keys_
* luo uusi _SSH-avain_ 
  * anna avaimelle joku _title_ (esim. laitos) ja kopioi tiedoston id_rsa.pub sisältö kohtaan _key_  
* Suorita uudelleen push:

```
mluukkai@melkki:~/ot-harjoitustyo$ git push
Counting objects: 3, done.
Writing objects: 100% (3/3), 213 bytes | 106.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/mluukkai/ot-harjoitustyo/pull/new/master
remote:
To github.com:mluukkai/ot-harjoitustyo.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
``` 

* nyt kaikki näyttää toimivan

## Lisää tiedostoja

* tee juuri luodun repositorion sisälle hakemisto _laskarit_
  * ja sen sisälle hakemisto _viikko1_
  * Komentorivitehtävien lopussa oli kehotus: Mene tämän jälkeen kotihakemistoon ja anna komento tree kurssit. _Copypastea komennon tulostus talteen, tarvitset sitä myöhemmin_
  * Tee hakemiston _laskarit/viikko1_ sisälle tiedosto _komentorivi.txt_ ja kopioi sinne komennon _tree_ tulos
  * Edellisen tehtäväsarjan lopussa kehoitettiin tallentamaan harjoitusrepositoriossa annetun komennon _git log --stat | cat_ tulos
  * Tee hakemiston _laskarit/viikko1_ sisälle tiedosto _gitlog.txt_ ja kopioi sinne githarjoittelun tulos
* Kirjoita jotain tekstiä hakemiston juuressa olevaan tiedostoon README.md
  * muotoile tekstisi [markdown-notaatiota](https://guides.github.com/features/mastering-markdown/) käyttäen
  * tee tiedostoon esim. jokin otsikko, tavallista tekstiä, joka sisältää lihavoituja ja kursivoituja osuuksia
  * näemme pian tekstin ruudulla muotoiltuna
* commitoi muutokset
  * muista aina commitoinnin yhteydessä _lisätä_ tiedosto/muutokset commitoitavaksi
* pushaa koodi githubiin komennolla _git push_

## Tiedostot GitHubissa

* mene GitHub-repositoriosi sivulle
  * käytännössä tämä tapahtuu uudelleenlataamalla repositorion luomisen jälkeen avautunut sivu
* huomaat että tiedostot näkyvät nyt repositorion sivulla. Sivulle renderöityy repositorion juuressa olevan README.md:n sisältö markdown-muotoiltuna
* voit editoida repositoriossa olevia tiedostoja suoraan GitHubin editorilla menemällä tiedoston sivulle ja painamalla kynäsymbolia
* tee README.md:hen linkit repositorion hakemistossa _laskarit/viikko1/_ oleviin tiedostoihin _komentorivi.txt_ ja _gitlog.txt_
  * ohje linkin muodostamiseen löytyy [täältä](https://guides.github.com/features/mastering-markdown/)
  * tiedostojen urlin saat navigoimalla GitHubissa tiedostoon ja kopioimalla osoitteen selaimen osoiteriviltä 
* Repositoriosi tulee näyttää suunnilleen seuraavalta

![](https://raw.githubusercontent.com/mluukkai/ohjelmistotekniikka-kevat2019/master/web/images/lh1-4a.png)

* jos teit kaiken oikein, pääset README.md:ssä olevia linkkejä klikkaamalla näkemään linkitettyjen tiedostojen sisällön

## Paikallisen repositorion ajantasaistaminen

* GitHubissa tekemämme muutokset ovat tehneet etärepositorioon uuden commitin
* Etärepositorio on nyt _edellä_ paikallista repositorioamme
* Saamme tuotua muutokset paikalliselle koneelle komennolla _git pull_
* Kokeile komentoa ja varmista, että muuttunut sisältö on nyt paikallisessa repositoriossa

## Lisää githubia

* Tee paikallisella koneella jokin muutos esim. tiedostoon README.md
* Lisää ja committaa muutos
* Vie muutokset GitHubiin komennolla _git push_
* Varmista GitHubista että muutokset näkyvät
* Paikallinen repositoriosi ja GitHubin etärepositorio ovat jälleen samassa tilassa. 

## Paikallisen ja etärepositorion epäsynkrooni

* joskus käy niin, että paikallinen ja etärepositorio menevät epäsynkroniin, siten että molempiin tehdään yhtäaikaa uusi commit
* luodaan tälläinen tilanne
* tee paikalliseen repositorioon muutos tiedostoon _README.md_, lisää ja committoi muutos
  * **älä** pushaa muutosta GitHubiin
* tee GitHubiin muutos **johonkin muualle** kuin README.md-tiedostoon
  * editoi siis esim. tiedostoa _gitlog.txt_ hieman suoraan GitHubissa
* yritä nyt pushata paikallisen repositorion muutokset githubiin
* seurauksena on virheilmoitus

``` 
mluukkai@melkki:~/ot-harjoitustyo$ git push
To git@github.com:mluukkai/ot-harjoitustyo.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:mluukkai/ot-harjoitustyo.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
mluukkai@melkki:~/ot-harjoitustyo$
``` 

* Tulet törmäämään tähän varmaan useasti jatkossakin.
* Ongelma ei ole paha. Koska paikalliset ja GitHubin muutokset ovat kohdistuneet **eri tiedostoihin**, selviämme helpolla 
* ensin pullaamme muutokset paikalliseen repositorioon komennolla _git pull_
  * pullaaminen synnyttää ns. merge commitin, jolle joudumme määrittelemään commit-viestin avautuvaan editoriin
  * oletusarvoinen viesti käy, eli riittää että poistut editorista tallentaen muutokset
* ja pushaamme ne uudelleen githubiin
* nyt paikallinen ja etärepositorio ovat taas synkroonissa
* katso repositorion tilaa nyt komennolla _gitk_
* näet, että repositorion uusimmalla commitilla on nyt kaksi edeltäjää, paikallinen commit ja etärepositorion commit

<img src="https://github.com/mluukkai/otm2016/raw/master/img/lh5-3.png" alt="alt text" width="800">

Jos muutokset olisivat kohdistuneet samaan tiedostoon, olisi syntynyt hieman vakavampi tilanne, eli _merge-konflikti_. Konfliktit on pakko selvittää itse editorin avulla. On toki olemassa työkaluja, mergetooleja, jotka auttavat konfliktin selvittämisessä. Emme kuitenkaan mene tällä kurssilla merge-konflikteihin.

Nyrkkisääntönä kannattaa pitää aina sitä, että kun rupeat työskentelemään paikallisessa repositoriossa, pullaa ensin kaikki muutokset etärepositoriosta. Ja kun lopetat työskentelyn, pushaa muutokset etärepositorioon. Näin konflikteja ei yhden ihmisen työskentelyssä todennäköisesti tule.

## Labtool

Rekisteröi nyt omat tietosi ja luomasi repositorio [Labtooliin](https://studies.cs.helsinki.fi/labtool/courses/TKT20002.2019.K.K.1). Valitse kurssiksi _Ohjelmistotekniikka_ jos joudut tekemään valinnan. 

Labtool kysyy myös harjoitustyön aihetta, jos et ole vielä varma aiheestasi voit muuttaa aiheen nimeä myöhemmin.

## Lisää gitiä

Gitin peruskäyttö tulee varmasti tutuksi kurssin aikana. Gitin edistyneempien piirteiden opiskelua kannattaa ilman muuta jatkaa myös omin päin. Internetistä löytyy suuri määrä enemmän tai vähemmän hyviä tutoriaaleja. Seuraavassa muutama linkki
* <https://www.atlassian.com/git/tutorials/>
* <http://learngitbranching.js.org>
* <http://ohshitgit.com>
