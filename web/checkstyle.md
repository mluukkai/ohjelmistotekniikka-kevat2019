# Checkstyle

Koodin testauksen lisäksi koodin luettavuuden ylläpitäminen on tärkeää. Tässä hyvänä apuvälineenä on staattisen analyysin työkalu Checkstyle. ks. [http://checkstyle.sourceforge.net/](http://checkstyle.sourceforge.net/). Kurssilla käytetään *Ohjelmoinnin Perusteista* ja *Ohjelmoinnin Jatkokurssista* tuttua checkstyleä, [koodin laatuvaatimuksien](koodin_laatuvaatimukset.md) seurannassa.

> Checkstyle is a development tool to help programmers write Java code that adheres to a coding standard. It automates the process of checking Java code to spare humans of this boring (but important) task. This makes it ideal for projects that want to enforce a coding standard.

## Checkstylen tuominen projektiin

Checkstyle on helppo ottaa käyttöön Maven-projektissa, lisäämällä sopiva konfiguraatio  _pom.xml_-tiedostoon. Jotta Checkstylen raporteista pääsisi helposti tarkastelemaan lähdekoodissa olevaa ongelmakohtaa, on hyvä käyttää Checkstyleä yhdessä [jxr:n](http://maven.apache.org/plugins/maven-jxr-plugin/) kanssa. 

Lisää **pom.xml** tiedostoon seuraavat

```xml
<build>
  <plugins>
    // muita plugineja
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-checkstyle-plugin</artifactId>
      <version>2.17</version>
      <configuration>
        <configLocation>checkstyle.xml</configLocation>
      </configuration>
    </plugin>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-jxr-plugin</artifactId>
      <version>2.5</version>
    </plugin>
  </plugins>
</build>
```

Checkstylen tarkkailemien virheiden joukko on konfiguroitavissa erillisen konfiguraatiotiedoston avulla, luo nyt tätä varten projektiin uusi **XML**-tiedosto _checkstyle.xml_.

Avaa tiedosto ja korvaa tiedoston sisältö seuraavalla: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE module PUBLIC "-//Puppy Crawl//DTD Check Configuration 1.3//EN" "http://www.puppycrawl.com/dtds/configuration_1_3.dtd">
<module name='Checker'>

    <!-- asetetaan kieliasetukset englanniksi. -->
    <property name="localeCountry" value="EN"/>
    <property name="localeLanguage" value="en"/>

    <module name='TreeWalker'>

        <property name='tabWidth' value='4' />
        
        <!-- Block Checks -->

        <module name='EmptyBlock' />
        <module name='LeftCurly' />
        <module name='NeedBraces' />
        <module name='RightCurly' />
        <module name='AvoidNestedBlocks' />
        <module name="NestedIfDepth">
          <property name="max" value="2"/>
        </module>
        <module name="NestedForDepth">
          <property name="max" value="2"/>
        </module>
        <module name="NestedTryDepth"/>

        <!-- Miscellaneous -->

        <module name='Indentation' />
        <module name="OneStatementPerLine"/>
        <module name="MethodLength">
            <property name="tokens" value="METHOD_DEF"/>
            <property name="max" value="20"/>
            <property name="countEmpty" value="false"/>
        </module>

        <!--- Naming Conventions -->

        <module name='ClassTypeParameterName' />
        <module name='ConstantName' />
        <module name='LocalFinalVariableName' />
        <module name='LocalVariableName' />
        <module name='MemberName' />
        <module name='MethodName' />
        <module name='MethodTypeParameterName' />

        <module name='PackageName'>
            <property name='format' value='^[a-z]+(\.[a-z][a-z0-9]*)*$' />
        </module>

        <module name='ParameterName' />
        <module name='StaticVariableName' />
        <module name='TypeName' />

        <!-- Whitespace -->

        <module name='GenericWhitespace' />
        <module name='EmptyForInitializerPad' />
        <module name='EmptyForIteratorPad' />
        <module name='MethodParamPad' />

        <module name='NoWhitespaceAfter'>
            <property name='tokens' value='BNOT, DEC, DOT, INC, LNOT, UNARY_MINUS, UNARY_PLUS' />
        </module>

        <module name='NoWhitespaceBefore'>
            <property name='tokens' value='SEMI, DOT, POST_DEC, POST_INC' />
            <property name='allowLineBreaks' value='true' />
        </module>

        <module name='ParenPad' />
        <module name='TypecastParenPad' />
        <module name='WhitespaceAfter' />

        <module name='WhitespaceAround'>
            <property name='allowEmptyConstructors' value='true' />
            <property name='allowEmptyMethods' value='true' />
        </module>
    </module>

    <!-- File Length -->

    <module name='FileLength'>
        <property name='max' value='500' />
    </module>


</module>
```

Voit suorittaa Checkstylen komentoriviltä komennolla <code>mvn jxr:jxr checkstyle:checkstyle</code>

Muista, että maven-komentoja on mahdollista suorittaa myös suoraan [NetBeansista](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/tehtavat/viikko2.md#maven-komentojen-suorittaminen-netbeansista).

Generoituasi Checkstyle-raportin löydät sen polusta **/target/site/checkstyle.html**.

Käytetyistä tarkistuksista löydät tarkempaa tietoa [täältä](http://checkstyle.sourceforge.net/checks.html). 

## Luokkien jättäminen Checkstylen ulkopuolelle

Kurssilla ei ole tarpeen kirjoittaa ehdottoman siistiä käyttöliittymäkoodia, ja siksi emme vaadikaan että käyttöliittymäluokkia testataan ollenkaan Checkstylen avulla. Muutetaan siis vielä raportointi niin, että tietyt tiedostot jätetään pois. 

Lisää seuraava määritys ```<module name='TreeWalker'>```-tagin ulkopuolelle (!!) esimerkiksi siis ```<module name='FileLength'>```-tagin ylä- tai alapuolelle, mutta kuitenkin niin, että se on ```<module name='Checker'>```-
tagin alaisuudessa:

```xml
<module name="SuppressionFilter">
  <property name="file" value="skipped_files.xml" />
</module>
```

Seuraavassa siis esimerkki checkstyle.xml-tiedostosta: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE module PUBLIC "-//Puppy Crawl//DTD Check Configuration 1.3//EN" "http://www.puppycrawl.com/dtds/configuration_1_3.dtd">
<module name='Checker'>

    <module name='TreeWalker'>

        <property name='tabWidth' value='4' />
	      
	    <!-- Paljon moduuleja välissä -->
        
    </module>

    <!-- File Length -->


    <module name='FileLength'>
        <property name='max' value='200' />
    </module>

    <module name="SuppressionFilter">
    	<property name="file" value="skipped_files.xml" />
    </module>

</module>
```

Tämän jälkeen tarvitaan vielä tiedosto _skipped_files.xml_, joka määrittelee mitkä tiedostot checkstyle voi jättää huomiotta.. 

Luo siis samaan kansioon missä checkstyle.xml-tiedostosi sijaitsee tiedosto `skipped_files.xml` ja anna sen sisällöksi seuraava:

```xml
<?xml version="1.0"?>

<!DOCTYPE suppressions PUBLIC
    "-//Puppy Crawl//DTD Suppressions 1.1//EN"
    "http://www.puppycrawl.com/dtds/suppressions_1_1.dtd">

<suppressions>
    <suppress files="todoapp.ui.TodoUi.java" checks="[a-zA-Z0-9]*"/>
    <suppress files="todoapp.ui.GuiHelper.java" checks="[a-zA-Z0-9]*"/>
</suppressions>
```

Korvaamalla `todoapp.ui.TodoUi.java` ja `todoapp.ui.GuiHelper.java` niiden tiedostojen nimillä (huomaa, että nimet ovat täydellisiä, pakkauksen sisältäviä nimiä!), joita et halua checkstylen huomioivan. 

Älä jätä huomioimatta mitään muita kuin JavaFX-käyttöliittymän komponenttien rakentamisessa käyttämiäsi tiedostoja!

Korjaa ohjelmastasi kaikki checkstylen ilmoittavat virheet.

## JavaDoc-Checkstyle

Siinä vaiheessa kun lisäät projektiisi JavaDoc:n voit lisätä Checkstyleen moduulin, jolla tarkistetaan JavaDocin oikeellisuus. Moduulit lisätään TreeWalker-moduulin tägien väliin.

```xml
  <module name="JavadocMethod">
    <property name="scope" value="public"/>
    <property name="allowMissingParamTags" value="false"/>
    <property name="allowMissingPropertyJavadoc" value="true"/>
    <property name="allowMissingThrowsTags" value="false"/>
    <property name="allowMissingReturnTag" value="false"/>
    <property name="allowThrowsTagsForSubclasses" value="true"/>
  </module>
        
  <module name="JavadocStyle">
    <property name="scope" value="public"/>
    <property name="checkEmptyJavadoc" value="true"/>
  </module>
```

Tämän seurauksena uusia virheitä tulee ilmestymään paljon, sillä Checkstylen tarkistus on nyt kattavampi. 
