# Muutamia toteutukseen liittyviä vihjeitä

## Sovelluksen käyttöliittymä

Voit siis tehdä sovelluksellesi tekstikäyttöliittymän tai graafisen käyttöliittymän. Tekstikäyttöliittymän tekeminen on toki useimmiten huomattavasti helpompaa, mutta se voi olla hieman tylsää ja graafisen käyttöliittymän tekemättömyys saattaa [vaikuttaa arvosanaan](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/arvosteluperusteet.md).

Pääasia on joka tapauksessa, että pyrit _eriyttämään mahdollisimman hyvin sovelluslogiikan käyttöliittymästä_. Käyttöliittymän roolin tulee siis olla ainoastaan käyttäjän kanssa tapahtuva interaktio, varsinaisen logiikan tulee tapahtua muissa oliossa. 

### Eräs malli tekstikäyttöliittymälle

Ohjelmoinnin jatkokurssin viikon 9 tehtävän [numerotiedustelu](https://materiaalit.github.io/ohjelmointi-s17/part9/) malliratkaisu tarjoaa erään kohtuullisen hyvän mallin tekstikäyttöliittymälle.

Pääohjelma ei tee mitään muuta kuin luo ja käynnistää luokan _Numerotiedustelu_ instanssin:

```java
public class Paaohjelma {
 
    public static void main(String[] args) {
        Scanner lukija = new Scanner(System.in);
 
        Numerotiedustelu numerotiedustelu = new Numerotiedustelu(lukija);
        numerotiedustelu.kaynnista();
    }
}
```

_Numerotiedustelu_ on oikeastaan sovelluksen tekstikäyttöliittymä. Varsinainen sovelluslogiikka on luokan _NumeroJaOsoitepalvelu_ vastuulla. 

Osa luokan _Numerotiedustelu_ koodia seuraavassa:

```java
public class Numerotiedustelu {
 
    private Scanner lukija;
    private Map<String, String> komennot;
    private NumeroJaOsoitepalvelu palvelu;
 
    public Numerotiedustelu(Scanner lukija) {
        this.lukija = lukija;
        palvelu = new NumeroJaOsoitepalvelu();
 
        komennot = new TreeMap<>();
        
        komennot.put("x", "x lopeta");
        komennot.put("1", "1 lisää numero");
        komennot.put("2", "2 hae numerot");
        komennot.put("3", "3 hae puhelinnumeroa vastaava henkilö");
        komennot.put("4", "4 lisää osoite");
        komennot.put("5", "5 hae henkilön tiedot");
        komennot.put("6", "6 poista henkilön tiedot");
        komennot.put("7", "7 filtteröity listaus");
        komennot.put("x", "x lopeta");
    }
 
    public void kaynnista() {
        System.out.println("numerotiedustelu");
        tulostaOhje();
        while (true) {
            System.out.println();
            System.out.print("komento: ");
            String komento = lukija.nextLine();
            if (!komennot.keySet().contains(komento)) {
                System.out.println("virheellinen komento.");
                tulostaOhje();
            }
 
            if (komento.equals("x")) {
                break;
            } else if (komento.equals("1")) {
                lisaaNumero();
            } else if (komento.equals("2")) {
                haeNumerot();
            } else if (komento.equals("3")) {
                haeHenkilo();
            } else if (komento.equals("4")) {
                lisaaOsoite();
            } else if (komento.equals("5")) {
                haeTeidot();
            } else if (komento.equals("6")) {
                poistaHenkilo();
            } else if (komento.equals("7")) {
                listaus();
            }
 
        }
    }
 
    private void haeNumerot() {
        System.out.print("kenen: ");
        String nimi = lukija.nextLine();
        Collection<String> numerot = palvelu.haeNumerot(nimi);
        if (numerot.isEmpty()) {
            System.out.println("  ei löytynyt");
            return;
        }
 
        for (String numero : numerot) {
            System.out.println(" " + numero);
        }
    }
 
    private void lisaaNumero() {
        System.out.print("kenelle: ");
        String nimi = lukija.nextLine();
        System.out.print("numero: ");
        String numero = lukija.nextLine();
        palvelu.lisaaNumero(nimi, numero);
    }
 
    // lisää käyttöliittymäfunktioita...
}
```

Koodi tulostaa ruudulle komentojen nimet, kysyy käyttäjän syötettä ja suorittaa halutun toimenpiteen:

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/j-1.png" width="700">

Koodi haarautuu käyttäjän valinnan mukaan if:ssä valitun toimenpiteen suorittavaan metodiin. Esim. jos valinta on 1, suoritetaan tiedot luetteloon lisäävä metodi:

```java
private void lisaaNumero() {
    System.out.print("kenelle: ");
    String nimi = lukija.nextLine();
    System.out.print("numero: ");
    String numero = lukija.nextLine();
    palvelu.lisaaNumero(nimi, numero);
}
```

Metodi ei kuitenkaan itse tiedä puhelinluettelosta mitään, luettelointitehtäviä eli *sovelluslogiikkaa* hoitaa muuttujaan _palvelu_ talletettu _NumeroJaOsoitepalvelu_-olio, jonka metodia _lisaaNumero_ käyttöliittymä kutsuu käyttäjän antama syöte parametrina.

Koska sovelluslogiikka tapahtuu kokonaan erillään käyttöliittymästä, voidaan sen toimivuus
 testata helposti JUnitin avulla automatisoidusti.

## Riippuvuuden injektointi

Mallivastauksen koodi ei kuitenkaan ole ihan optimaalinen ja sitä saa parannettua helposti pienellä kikalla. Muutetaan _Numerotiedustelu_ muotoon

```java
public class Numerotiedustelu {
 
    private Scanner lukija;
    private Map<String, String> komennot;
    private NumeroJaOsoitepalvelu palvelu;
 
    public Numerotiedustelu(Scanner lukija, NumeroJaOsoitepalvelu palvelu) {
        this.lukija = lukija;
        this.palvelu = palvelu;
        palvelu = new NumeroJaOsoitepalvelu();
 
        komennot = new TreeMap<>();
        
        komennot.put("x", "x lopeta");
        // ...
    }

    // ...
}    
```

Pääohjelmaa täytyy nyt muuttaa seuraavasti:

```java
public class Paaohjelma {
 
    public static void main(String[] args) {
        Scanner lukija = new Scanner(System.in);
        NumeroJaOsoitepalvelu palvelu = new NumeroJaOsoitepalvelu();
 
        Numerotiedustelu numerotiedustelu = new Numerotiedustelu(lukija, palvelu);
        numerotiedustelu.kaynnista();
    }
}
```

Ero on hyvin pieni, nyt sovelluslogiikasta huolehtiva _NumeroJaOsoitepalvelu_-olio luodaan pääohjelmassa ja annetaan käyttöliittymänä toimivalle _Numerotiedustelu_-oliolle konstruktorin parametrina.

Tästä tekniikasta käytetään nimitystä [riippuvuuden injektointi](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/materiaali.md#riippuvuuksien-injektointi), sillä  _NumeroJaOsoitepalvelu_-olio on _Numerotiedustelu_-olion riippuvuus, joka tässä myöhemmässä versiossa injetoidaan konstruktoriparametrin avulla riippuvuutta tarvitsevalle oliolle. Aiemmassa versiossahan numerotiedustelu loi riippuvuuden itse.

Riippuvuuksien injektoinnista on monia etuja, eräs näistä on laajennettavuus.

Voisimme luoda uuden parannellun version numero- ja osoitepalvelusta perinnän avulla:

```java
public class ParanneltuNumeroJaOsoitepalvelu extends NumeroJaOsoitepalvelu {
  // ...
}
```

Laajennettu palvelu voisi käyttää vanhaa käyttöliittymää sellaisenaan:

```java
public class Paaohjelma {
 
    public static void main(String[] args) {
        Scanner lukija = new Scanner(System.in);
        ParanneltuNumeroJaOsoitepalvelu palvelu = new ParanneltuNumeroJaOsoitepalvelu();
 
        Numerotiedustelu numerotiedustelu = new Numerotiedustelu(lukija, palvelu);
        numerotiedustelu.kaynnista();
    }
}
```

Toinen merkittävä etu on testauksen helpottaminen. Se onkin syynä sille, miksi _Scanner_ injektoidaan _Numerotiedustelu_-oliolle.

Testit toimivat seuraavaan tyyliin:

```java
public class NumerotiedusteluTest {
 
    public void numeronLisays() 
        Scanner lukija = new TestausSkanner(
          "1",
          "Arto Hellas",
          "040-123456",
          "x"
        );

        NumeroJaOsoitepalvelu palvelu = new NumeroJaOsoitepalvelu();
 
        Numerotiedustelu numerotiedustelu = new Numerotiedustelu(lukija, palvelu);
        numerotiedustelu.kaynnista();

        // varmista assert-lauseella että ohjelman tulostus oli se halutun kaltainen
    }
}
```

Eli testi antaa _Numerotiedustelu_-oliolle simuloidun syötteen, joka toimii numerotiedustelun kannalta normaalin Scannerin tavoin. Suorituksen jälkeen testi varmistaa, että ohjelman tulostus on halutun kaltainen. 

### Java FX

Graafisen käyttöliittymän toteuttamiseen kannattaa oletusarvoisesti käyttää JavaFX:ää, jonka käytön perusteet esitellään [Ohjelmoinnin jatkokurssilla](https://materiaalit.github.io/ohjelmointi-s17/part11/)

Myös graafista käyttöliittymää käytettäessä tulee periaatteen olla se, että käyttöliittymän koodi ei sisällä sovelluslogiikkaa.

Mallia voi ottaa esimerkiksi kurssin referenssisovelluksen [TodoApp:in](https://github.com/mluukkai/OtmTodoApp/) koodista ja [arkkitehtuurikuvauksesta](https://github.com/mluukkai/OtmTodoApp/blob/master/dokumentaatio/arkkitehtuuri.md).

### Sovelluksen alustaminen ja sulkeminen

Kuten jatkokurssin materiaalissa kerrotaan, JavaFX-sovelluksen käyttöliittymästä vastaava pääluokka on peritty luokasta _Application_.

_main_-metodi ei yleensä tee mitään muuta kuin kutsuu metodia _launch_ joka taas saa aikaan sen, että pääluokasta luodaan instanssi ja instanssin metodeita _init_ ja _start_ kutsutaan.

Metodi _start_ on pakko toteuttaa ja sen suorituksen aikana muodostetaan käyttöliittymä. Metodin _init_ toteutus on vapaaehtoinen ja se on erinomainen paikka alustaa projektin riippuvuudet sillä metodi suoritetaan ennen start:ia. Teknisten rajoitteiden takia JavaFX-sovelluksille on hankalaa antaa riippuvuuksia samaan tapaan konstruktori-injektiolla kuin mitä aiemmassa esimerkissä teimme.

Seuraavassa ote Todo-sovelluksen käyttöliittymän koodista:

```java
public class TodoUi extends Application {
    // sovelluslogiikka  
    private TodoService todoService;
    
    @Override
    public void init() {
        FileUserDao userDao = new FileUserDao("users.txt");
        FileTodoDao todoDao = new FileTodoDao("todos.txt", userDao);
        // alustetaan sovelluslogiikka 
        todoService = new TodoService(todoDao, userDao);
    }

    @Override
    public void start(Stage primaryStage) {   
      // muodosta käyttöliittymä täällä
  
      Button createTodo = new Button("create");
      // käyttöliittymä kutsuu todoService-olioa hoitamaan sovelluslogiikkaan liittyvät toimet
      createTodo.setOnAction(e->{
          todoService.createTodo(newTodoInput.getText());
          newTodoInput.setText("");       
          redrawTodolist();
      });

      primaryStage.setOnCloseRequest(e->{
        System.out.println("sovellus on aikeissa sulkeutua");
        if (enHaluaEttaSovellusSulkeutuu) {
          e.consume();   
        }
      });
    }    

    @Override
    public void stop() {
      // tee lopetustoimenpiteet täällä
      System.out.println("sovellus sulkeutuu");
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

Koodi havainnollistaa myös tapaa, miten lambda-funktiona määritelty _createTodo_-napin tapahtumankäsittelijä kutsuu sovelluslogiikan metodia _todoService.createTodo_. 

Koodissa on myös metodi [stop](https://docs.oracle.com/javase/8/javafx/api/javafx/application/Application.html#stop--) joka suoritetaan aina viimeisenä ennen sovelluksen sulkeutumista. Metodissa voidaan suorittaa tarvittavia lopetustoimia, esim. tiedostojen tallentamista.

Metodin _start_ loppuun on rekisteröity tapahtumankuuntelija, joka suoritetaan juuri ennen sovelluksen sulkemista. If-haara demonstroi miten sulkemisen voi vielä estää tapahtumankuuntelijassa. 

### FXML

Ohjelmoinnin jatkokurssilla ja [esimerkkisovelluksessa](https://github.com/mluukkai/OtmTodoApp) käyttöliittymät luodaan ohjelmallisesti, eli luomalla ja yhdistelemällä käyttöliittymäkomponentteja muodostavia olioita. 

JavaFX tarjoaa myös tavan käyttöliittymän ulkoasun määrittelemiseen läheisesti HTML:ää muistuttavassa [FXML-formaatissa](https://docs.oracle.com/javase/8/javafx/fxml-tutorial/why_use_fxml.htm).

Tarkastellaan yksinkertaista esimerkkiä, graafista noppaa:

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/j-2.png" width="400">

Esimerkin koodi on kokonaisuudessaan GitHubissa <https://github.com/mluukkai/FXMLExample>

Käyttöliittymän rakenteen määrittelee tiedosto _Scene.fxml_:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.control.Button?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.layout.AnchorPane?>

<AnchorPane id="AnchorPane" prefHeight="200" prefWidth="320" xmlns="http://javafx.com/javafx/9" xmlns:fx="http://javafx.com/fxml/1" fx:controller="otm2018.FXMLController">
    <children>
        <Label fx:id="display" alignment="CENTER" layoutX="84.0" layoutY="47.0" minHeight="16" minWidth="69" prefHeight="17.0" prefWidth="146.0" />    
        <Button fx:id="button" layoutX="134.0" layoutY="113.0" onAction="#handleButtonAction" text="roll" />
    </children>
</AnchorPane>
```

Layout on nyt muodostettu [AnchorPanen](https://docs.oracle.com/javase/8/javafx/api/javafx/scene/layout/AnchorPane.html) avulla. Toisin kuin muissa layouteissa, AnchorPanessa jokaiselle siihen sijoitettavalle komponentille annetaan absoluuttinen sijainti. Käyttöliittymä siis koostuu kahdesta komponentista, Labelista ja Buttonista. Molemmilla on joukko _attribuutteja_, joista osa liittyy komponentin sijainnin määrittelemiseen, ja osa taas on oleellinen ohjelman toiminnallisuuden kannalta. 

AnchorPanen attribuuteista erityisen mielenkiintoinen on _fx:controller_, se määrittelee luokan, joka toimii näkymän _kontrollerina_. Luokka on määritelty seuraavasti:

```java
package otm2018;

import java.net.URL;
import java.util.ResourceBundle;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.Initializable;
import javafx.scene.control.Label;

public class FXMLController implements Initializable {
    private Dice dice;

    public FXMLController() {
        dice = new Dice();
    }
     
    @FXML
    private Label display;
    
    @FXML
    private void handleButtonAction(ActionEvent event) {
        dice.roll();
        label.setText("you got "+dice.getValue());
    }
    
    @Override
    public void initialize(URL url, ResourceBundle rb) {
        label.setText("dice not rolled yet...");
    }    
}
```

Kontrollerin oliomuuttuja _display_ on nyt sidottu näkymän labeliin, sillä muuttujan nimi on sama kuin labelin attribuutin _fx:id_ arvo:

```xml
<Label fx:id="display" ... />  
```

Kontrollerin metodi _handleButtonAction_ toimii näkymän napin tapahtumankuuntelija, sillä nappi viittaa siihen attribuutin _onAction_ avulla:

```xml
<Button fx:id="button" onAction="#handleButtonAction" text="roll" .../>
```

Sovelluslogiikkaa, eli nopan toiminnallisuutta mallintava luokka näyttää seuraavalta:

```java
package otm2018;

public class Dice {
    private int value;

    public int getValue() {
        return value;
    }
    
    public void roll() {
        value = (int)(Math.random()*6+1);
    }
}
```

Pääohjelman _start_-metodin rooliksi jää nyt ladata fxml:n määrittely ja muodostaa sen perusteella näkyville asetettava Scene: 

```java
package otm2018;

import javafx.application.Application;
import static javafx.application.Application.launch;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class MainApp extends Application {

    @Override
    public void start(Stage stage) throws Exception {
        Parent root = FXMLLoader.load(getClass().getResource("/fxml/Scene.fxml"));
        
        Scene scene = new Scene(root);
        
        stage.setTitle("JavaFX and Maven");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }

}
```

### Scenebuilder

FXML-muotoiset käyttöliittymien näkymät on mahdollista tehdä käsin editoimalla fxml-tiedostoja. Toinen mahdollisuus on käyttää graafista [Scenebuilder](http://gluonhq.com/products/scene-builder/)-editoria käyttöliittymän rakentamiseen.

<img src="https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/j-3.png" width="800">

Scenebuilder integroitui ainakin OSX:ssä automaattisessti NetBeansiin.

### Riippuvuuksien injektointi JavaFX-kontrollereille
 
Kurssin referenssisovelluksen [FXML](https://github.com/mluukkai/FxmlTodoApp)-versiossa muutama vihje tilanteeseen, jossa FXML:llä luotujen näkymien kontrollereille pitää injektoida riippuvuuksia, esim. sovelluslogiikkaolio. Linkin takaa näet myös erään tavan, miten FXML:llä tehtyjä näkymiä on mahdollista vaihtaa.

### JavaFX-aiheisia linkkejä

Ohjelmoinnin jatkokurssilla tehdään JavaFX:n ainoastaan matala pintaraapaisu, jatkokurssin materiaali kannattaa kuitenkin ehdottomasti kerrata jos olet aikeissa käyttää JavaFX:ää. 

Jos käyttöliittymäsi on vähänkin epätriviaali, joudut suurella todennäköisyydellä etsimään itse lisää tietoa. Omatoimisen tiedonhaun harjoittelu onkin tämän kurssin eräs tärkeimmistä oppimistavoitteista. Seuraavassa muutamia linkkejä auttamaan alkuunpääsemistä. Jos löydät internetistä hyvää materiaalia, tee sivulle [pull request](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/materiaali.md#kirjoitusvirheitä-materiaalissa)

- [Getting started](https://docs.oracle.com/javase/8/javafx/get-started-tutorial/index.html)
- [API](https://docs.oracle.com/javase/8/javafx/api/toc.htm)
- Oraclen JavaFX-tutoriaalit
  - [layoutit](https://docs.oracle.com/javase/8/javafx/layout-tutorial/index.html)
  - [käyttöliittymäkomponentit](https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/ui_controls.htm)
  - [diagrammit](https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/charts.htm)
  - [FXML](https://docs.oracle.com/javafx/2/get_started/fxml_tutorial.htm)
- [FXML getting started](https://docs.oracle.com/javafx/2/fxml_get_started/jfxpub-fxml_get_started.htm)  
- [Scenebuilder](http://gluonhq.com/products/scene-builder/)
- [JavaFX dialogit](http://code.makery.ch/blog/javafx-dialogs-official/)
- OtmTodoApp:in [FXML](https://github.com/mluukkai/FxmlTodoApp)-versio (ei sisällä koko toiminnallisuutta)

Youtubesta löytyy runsaasti vaihtelevanlaatuisia videoita aihepiiristä. Hyväksi havaittuja:

- [Bucky Robertsin JavaFX-videosarja (lopussa myös FXML ja Scene Builder)](https://www.youtube.com/playlist?list=PL6gx4Cwl9DGBzfXLWLSYVy8EbTdpGbUIG)

## Tietojen talletus

Arvosteluperusteet [kannustavat](https://github.com/mluukkai/Ohjelmistotekniikka2018/blob/master/web/arvosteluperusteet.md) siihen, että ohjelmasi käsittelisi johonkin muotoon pysyväistalletettua tietoa. Kannattaa kuitenkin pitää talletettavan tiedon määrä kohtuullisena, eeppisimmät tietoa käsittelevät aiheet sopivat paremmin kurssille [Tietokantasovellus](https://courses.helsinki.fi/fi/tkt20011).

### DAO-suunnittelumalli

Riippumatta mihin tiedon tallennat, kannattaa tiedon tallentaminen eristää sovelluksen muista osista esim. tietokantojen perusteista tutun [DAO](https://materiaalit.github.io/tikape-k18/part3/)-suunnittelumallin avulla.

[Esimerkkisovelluksella](https://github.com/mluukkai/OtmTodoApp) on Tikapenkin mallia noudattelevat DAO:t sekä sovelluksen käsittelemille käyttäjille että käyttäjien todoille eli työtehtäville.

Molemmat DAO:t on piilotettu sovelluslogiikalta rajapintojen taakse:  

```java
public interface UserDao {
    User create(User user);
    User findByUsername(String username);
    List<User> getAll();
}

public interface TodoDao {
    Todo create(Todo todo);
    List<Todo> getAll();
    void setDone(int id);
}
```

Esimerkkisovelluskessa on DAO:ista tiedostoon tallettavat versiot. Toteukset ovat melko suoraviivaisia ja epämielenkiintoisia:

```java
public class FileUserDao implements UserDao {
    private List<User> users;
    private String file;

    public FileUserDao(String file) {
        users = new ArrayList<>();
        this.file = file;
        load();   
    }

    private void load() {
        try {
            Scanner reader = new Scanner(new File(file));
            while (reader.hasNextLine()) {
                String[] parts = reader.nextLine().split(";");
                User u = new User(parts[0], parts[1]);
                users.add(u);
            }
        } catch(Exception e){
            e.printStackTrace();
        }
    }
    
    private void save() {
        try {
            FileWriter writer = new FileWriter(new File(file));
            for (User user : users) {
                writer.write(user.getUsername()+";"+user.getName()+"\n");
            }
            writer.close();
        } catch(Exception e){
            e.printStackTrace();
        }
    }
    
    @Override
    public List<User> getAll() {
        return users;
    }
    
    @Override
    public User findByUsername(String username) {
        return users.stream().filter(u->u.getUsername().equals(username)).findFirst().orElse(null);
    }
    
    @Override
    public User create(User user) {
        users.add(user);
        save();
        return user;
    }    
}
```

TodoDao:n toteutukseen liittyy pieni mielenkiintoinen detalji. Koska Todo tuntee käyttäjänsä, tarvitsee _FileTodoDao_ linkitystä varten _UserDao_:n:

```java
public class FileTodoDao implements TodoDao {
    public List<Todo> todos;
    private String file;

    public FileTodoDao(String file, UserDao userDao) {
        todos = new ArrayList<>();
        this.file = file;
        try{
            Scanner reader = new Scanner(new File(file));
            while (reader.hasNextLine()) {
                String[] parts = reader.nextLine().split(";");
                int id = Integer.parseInt(parts[0]);
                boolean done = Boolean.parseBoolean(parts[2]);
                User user = userDao.getAll().stream().filter(u->u.getUsername().equals(parts[3])).findFirst().orElse(null); 
                Todo todo = new Todo(id, parts[1], done, user);
                todos.add(todo);
            }
        } catch(Exception e){
            e.printStackTrace();
        }
        
    }

    // ...
}
```

Sovelluksen _todoService_ ei siis tunne _DAO_-olioiden todellista luonnetta, sovelluksen alustusmetodi _init_ luo käytettävät DAO:t ja injektoi ne sovelluslogiikalle:

```java
@Override
public void init() {
    String userFile = "users.txt";
    String todoFile = "todos.txt";

    FileUserDao userDao = new FileUserDao(userFile);
    FileTodoDao todoDao = new FileTodoDao(todoFile, userDao);
    todoService = new TodoService(todoDao, userDao);
}
```

## Sovelluksen konfiguraatiot

Sovelluksen koodiin ei ole syytä kovakoodata mitään konfiguraatioita, kuten sen käyttämien tiedostojen tai tietokantojen nimiä. Edellä esitetyssä alustusmetodissa _init_ syyllistytään juuri tähän. Eräs syy tähän on se, että jos konfiguraatiot ovat koodissa, ei ohjelman normaalin käyttäjän (jolla ei ole pääsyä koodiin) ole mahdollista tehdä muutoksia konfiguraatioihin.

Konfiguraatiot on syytä määritellä ohjelman ulkopuolella, esim. erillisissä konfiguraatiotiedostoissa.

Esimerkkisovelluksen konfiguraatiot on määritelty sovelluksen juuressa olevaan tiedostoon 
_config.properties_:

<pre>
userFile=users.txt
todoFile=todos.txt
</pre>

Koodi käsittelee konfiguraatioita [Property](https://docs.oracle.com/javase/7/docs/api/java/util/Properties.html)-olion avulla:

```java
@Override
public void init() throws Exception {
    Properties properties = new Properties();

    properties.load(new FileInputStream("config.properties"));
    
    String userFile = properties.getProperty("userFile");
    String todoFile = properties.getProperty("todoFile");
        
    FileUserDao userDao = new FileUserDao(userFile);
    FileTodoDao todoDao = new FileTodoDao(todoFile, userDao);
    todoService = new TodoService(todoDao, userDao);
}
```

Lisää konfiguraatioiden käsittelyyn Property-olioiden avulla esim. [täällä](https://www.mkyong.com/java/java-properties-file-examples/) tai [täällä](https://docs.oracle.com/javase/tutorial/essential/environment/properties.html)

Toinen hyvä paikka konfiguraatioille ovat [ympäristömuuttujat](https://docs.oracle.com/javase/tutorial/essential/environment/env.html).

## Uuden tekniikan harjoittelu ja käyttöönotto

Kun olet toteuttamassa jotain itsellesi uudella tekniikalla, esim. JavaFX:llä, _sqlite_-tietokantaa hyödyntäen, tai teet ohjelmaasi laajennuksen hyödyntämällä kirjastoa, jota et vielä tunne, kannattaa ehdottomasti tehdä uudella tekniikalla erillisiä kokeiluja varsinaisen ohjelmasi ulkopuolella, omassa pienessä koesovelluksessa.

Jos yrität "montaa asiaa yhtäaikaa" eli ottaa esim. FXML-tekniikan käyttöön omassa jo pitkälle edenneessä ohjelmassasi, on aika varmaa, että saat ainoastaan aikaan suuren määrän ongelmia. Silloin kun koodia ja liikkuvia osia on paljon, ei ole koskaan varmuutta missä ongelma on, ja sen takia on erittäin hyödyllistä, että teet harjoittelun ja kokeilut erillisessä "proof of concept"-sovelluksessa ja kun saat esim. FXML:n toimimaan kokeilusovelluksessa, on usein sen jälkeen helppoa "copypasteta" koodi varsinaiseen sovellukseen.

