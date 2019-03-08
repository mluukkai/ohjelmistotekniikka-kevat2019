# Ohjeita Maveniin

## Projektin luominen

Ohje maven-muotoisen projektin luomiseen NetBeansilla [täällä](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/tyon_aloitus.md#maven-projektin-luominen)

Vaikka käyttäisit JavaFX:ää, kannattaa projektia varten silti luoda ohjeen mukaan "normaali" maven-projekti.

## Testit ja Testikattavuus

Lisää tiedostoon _pom.xml_ seuraavat

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
<build>
    <plugins>
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

Huomaa, että määrittelyt on lisättävä _Project_-tagien sisälle:

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/m-0.png" width="700">

Voit nyt suorittaa testauskattavuuden mittaamisen komennolla

```xml
mvn test jacoco:report
```

Katso lisää [viikon 2 laskareista](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/tehtavat/viikko2.md#3-testauskattavuus).

### Koodin huomiotta jättäminen kattavuusraportissa

Joskus haluamme jättää osan koodista, esim. käyttöliittymän huomioimatta kattavuusraportissa. 

Oletetaan, että projekti näyttää seuraavalta

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/m-1.png" width="700">

oletusarvoisesti testauskattavuus raportoidaan kaikesta koodista

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/m-2.png" width="700">

Yksittäisen pakkauksen koodit on helppo poistaa raportin alaisuudesta lisäämällä jacoco-pluginin määrittelyyn _excludes_-osa seuraavasti:

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.0</version>
    <configuration>
        <excludes>
            <exclude>pokemontietokanta/ui/*</exclude>
        </excludes>
    </configuration>                
    <executions>
        <execution>
            <id>default-prepare-agent</id>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
    </executions>
</plugin>  
```

Excludesin alle voi lisätä tarvittaessa myös useampia excludeja. Lisää tietoa exclude-syntaksista internetissä, esim. [täältä](https://stackoverflow.com/questions/27799419/maven-jacoco-configuration-exclude-classes-packages-from-report-not-working).

## Maven-komentojen suorittaminen NetBeansista

Ohje [täällä](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/tehtavat/viikko2.md#maven-komentojen-suorittaminen-netbeansista).

## Ulkoisten kirjastojen käyttäminen Mavenin avulla

Mavenin avulla omassa koodissa on erittäin helppo ottaa käyttöön muiden ohjelmoijien toteuttamia apukirjastoja.

Internet on täynnä erilaisiin tilanteisiin sopivia apukirjastoja. 

Oletetaan, että haluamme tehdä sovelluksessa tilastotieteellistä analyysiä. Googlella 
Löydämme [Apache Commons](https://commons.apache.org) -projektista löytyvän [matematiikkakirjaston](http://commons.apache.org/proper/commons-math/), jonka tarjoamat [tilastotieteen työvälineet](http://commons.apache.org/proper/commons-math/userguide/stat.html) vaikuttavat lupaavalta.

Apache Commonsin dokumentaatio ei suoraan kerro, miten koodi saadaan liitettyä Maven-muotoiseen projektiin. Se on kuitenkin helppoa, tarvitsemme tiedon siitä miten projekti löytyy Mavenin repositorioista eli "koodisäiliöistä".

Googlaamalla "Apache Commons Math Maven" löytyy sivu <https://mvnrepository.com/artifact/org.apache.commons/commons-math3/3.6> joka näyttää seuraavalta

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/m-4.png" width="950">

Saamme liitettyä kirjaston projektiimme, kopioimalla sivulla olevan _dependency_-määritelmän projektin _pom.xml_-tiedoston osan _dependencies_ alle:

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/m-5.png" width="800">

Kirjastosta on nyt otettu uusin versio 3.6.1, minkä olemassaolosta _mvnrepository.com_ antoi vihjeen.

Suorittamalla NetBeansissa _Clean and Build_ lataa Maven kirjaston koodin. 
NetBeans-projektin _Dependencies_-kansio varmistaa asian:

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/m-6.png" width="400">

Voimme nyt käyttää kirjaston luokkia koodissamme:

```java
import org.apache.commons.math3.stat.descriptive.DescriptiveStatistics;
import pokemontietokanta.domain.Pokemon;

public class Main {
    public static void main(String[] args) {
        Pokemon p = new Pokemon("arto");
        p.go();
        
        DescriptiveStatistics stats = new DescriptiveStatistics();

        int[] strengthOfPokemons = { 58, 5, 10, 45, 17};

        for( int i = 0; i < strengthOfPokemons.length; i++) {
            stats.addValue(strengthOfPokemons[i]);
        }

        double mean = stats.getMean();
        double std = stats.getStandardDeviation();
        double median = stats.getPercentile(50);
        
        System.out.println("mean "+mean);
        System.out.println("standar deviation "+std);
        System.out.println("median "+median);
    }
}
```

Apache Commonsissa olevat kirjastot ovat varsin hyvin dokumentoituja. Jos ja kun löydät googlaamalla projektiisi sopivia kirjastoja, niiden dokumentaation taso vaihtelee. Sekään ei ole ennenkuulumatonta, että kirjastojen koodissa on bugeja. Nykyään melkein kaikkien kirjastojen koodi löytyy GitHubista. Kirjastojen GitHub-sivuilta selviää mm. se onko kirjasto edelleen aktiivisen ylläpidon alaisena. Jos kirjaston GitHubissa ei ole ollut päivityksiä pitkään aikaan, esim. vuoteen, kannattaa kirjastoon suhtautua suurella skeptisyydellä. Useimpien kirjastojen dokumentaatiotkin ovat GitHubissa. Apache Commons on tämän suhteen poikkeus, sen kirjastojen koodia ei edes hallinnoida gitin vaan jo hieman esihistoriallisen svn-versionhallintajärjestelmän avulla.

## Checkstyle

Katso lisää [täältä](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/checkstyle.md)

## JavaDoc

Katso lisää [täältä](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/javadoc.md)

## Jarin generointi

Maven-muotoinen projekti voidaan helposti paketoida [jar-paketiksi](https://en.wikipedia.org/wiki/JAR_(file_format)), jolloin ohjelmaa voidaan suorittaa NetBeansin ulkopuolelta.

Jarin generoimiseen tarvitaan seuraava konfiguraatio:

```xml
    <build> 
       <plugins>
            // muut pluginit ovat tässä välissä
           <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>1.6</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <transformers>
                                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <mainClass>pokemontietokanta.ui.Main</mainClass>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>        
``` 

Huomaa, että kohdan _mainClass_ on oltava **täsmälleen sama** kuin pääohjelman sisältävän luokan täydellinen nimi:

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/m-3.png" width="700">

* Saat nyt luotua jar-tiedoston antamalla komentoriviltä komennon _mvn package_
* komento luo hakemiston _target_ sisälle kaksi jar-päätteistä tiedostoa, niistä oikea on se, jonka nimessä *ei* ole sanaa original
* ohjelman voi nyt suorittaa komennolla <code>java -jar jartiedoston_nimi.jar</code>

Jar-tiedosto on mahdollista suorittaa millä tahansa koneella, olettaen että koneelle on asennettu Javan versio 1.8

