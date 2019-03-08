# Github release

Eräs tapa julkaista ohjelmasta stabiili versio on tehdä GitHubiin release, eli julkaistu versio.

* klikkaa repositorion GitHub-sivulta kohtaa "0 releases"
* valitse *Draft a new release*
* määrittele julkaisun tiedot 
* lisää jar-tiedosto klikkaamalla kohtaa "Attach binaries..."
  * jar-tiedosto kannattaa ehkä uudelleennimetä, mavenin generoima tiedostonimi on hieman ikävä
* jos sovelluksen suorituksessa edellytetään muita tiedostoja, lisää ne tarvittaessa mukaan ja mainitse niistä tekstissä

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/release.png" width="700">

Nyt koodi on kenen tahansa ladattavissa menemällä GitHub-repositorioosi, ja klikkaamalla repositoriosivusi kohtaa "1 release" ja suoritettavissa komennolla <code>java -jar tiedostonnimi.jar</code> olettaen että koneelle on asennettu Javan versio 1.8
