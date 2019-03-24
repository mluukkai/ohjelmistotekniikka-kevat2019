# Viikon 3 laskarit

Tehtävät on tarkoitus tehdä joko pajassa tai omatoimisesti. Tehtävien palautuksen deadline on *tiistaina 2.4. klo 23:59*

Tehtävät palautetaan Githubin avulla Labtoolin rekisteröimääri repositorioon.

Muista pushata tehtävät GitHubiin ennen viikkodeadlinea.
  
- Klo 00 jälkeen tulevia repositorion päivityksiä ei huomioida pisteytyksessä, eli ne tuovat 0 pistettä.

Tee palautuksia varten repositorion sisällä olevaan hakemistoon _laskarit_ uusi alihakemisto _viikko3_. Kukin tehtävä palautetaan lisäämällä hakemiston sisälle sopivasti nimettyjä kuvia.

Viikon palautuksista on tarjolla yksi kurssipiste. Pisteytys arvioidaan palautuksen laadun perusteella.

Huomaa, että tällä viikolla on myös harjoitustyöhön liittyviä [tavoitteita](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/tehtavat/harjoitustyo_viikko3.md)

## Luokkakaaviot

Kertaa luokkakaavioihin liittyvät asiat [kurssimateriaalista](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/materiaali.md#luokkakaaviot).

Luokkakaavioiden piirtoon helpoin työkalu on <http://yuml.me/>, jos haluat  ammattimaisempaa jälkeä on <https://draw.io/> hyvä (tätä tehtävää varten se ei kuitenkaan liene vaivan arvoista). Myös valokuva käsin piirretyistä kaavioista riittää.

### 1

Monopoli ks. esim. http://fi.wikipedia.org/wiki/Monopoli_(peli) on varmasti kaikkien tuntema lautapeli. 

Tehdään luokkakaavio, joka kuvaa pelissä olevia asioita ja niiden suhteita.

Tässä tehtävän osassa tehdään alustava luokkakaavio, joka ei kuvaa peliä vielä kokonaisuudessaan vaan sisältää vasta seuraavat elementit: 

Monopolia pelataan käyttäen kahta noppaa. Pelaajia on vähintään 2 ja enintään 8. Peliä pelataan pelilaudalla joita on yksi. Pelilauta sisältää 40 ruutua. kukin ruutu tietää, mikä on sitä seuraava ruutu pelilaudalla. Kullakin pelaajalla on yksi pelinappula. Pelinappula sijaitsee aina yhdessä ruudussa. 

### 2 

Laajennetaan edellisen tehtävän luokkakaaviota tuomalla esiin seuraavat asiat:

Ruutuja on useampaa eri tyyppiä:
* aloitusruutu
* vankila
* sattuma ja yhteismaa
* asemat ja laitokset
* normaalit kadut (joihin liittyy nimi)

Monopolipelin täytyy tuntea sekä aloitusruudun että vankilan sijainti.

Jokaiseen ruutuun liittyy jokin toiminto. 

Sattuma- ja yhteismaaruutuihin liittyy kortteja, joihin kuhunkin liittyy joku toiminto. 

Toimintoja on useanlaisia. Ei ole vielä tarvetta tarkentaa toiminnon laatua.

Normaaleille kaduille voi rakentaa korkeintaan 4 taloa tai yhden hotellin. Kadun voi omistaa joku pelaajista. Pelaajilla on rahaa. 

## Sekvenssikaaviot

Kertaa sekvenssikaavioihin liittyvät asiat [kurssimateriaalista](https://github.com/mluukkai/ohjelmistotekniikka-kevat2019/blob/master/web/materiaali.md#sekvenssikaaviot).

Sekvenssikaavioiden piirtoon paras työkalu lienee <https://www.websequencediagrams.com/>. Myös valokuva käsin piirretyistä kaavioista riittää.

### 3

Tarkastellaan bensatankista ja moottorista koostuvan koneen Java-koodia.

Piirrä sekvenssikaaviona tilanne, jossa kutsutaan (jostain koodin ulkopuolella olevasta metodista) ensin _Machine_-luokan konstruktoria ja sen jälkeen luodun Machine-olion metodia _drive()_.

Muista, että sekvenssikaaviossa tulee tulla ilmi kaikki mainin suorituksen aikaansaamat olioiden luomiset ja metodien kutsut!


```java
public class Machine {
  private FuelTank tank;
  private Engine engine;

  public Machine() {
      tank = new FuelTank();
      tank.fill(40);
      engine = new Engine(tank);
  }

  void drive() {
      engine.start();
      boolean running = engine.isRunning();
      if ( running ) engine.useEnergy();          
  }
}

public class FuelTank {
  private int fuelContents;

  FuelTank() {
      fuelContents = 0;
  }
  
  void fill(int amount) {
      fuelContents = amount;
  }
  
  int contentsLeft() {
      return fuelContents;
  }
  
  void consume(int amount) {
      fuelContents = fuelContents - amount;
  }
}
    
public class Engine {
  private FuelTank fuelTank;

  Engine(FuelTank tank) {
      fuelTank = tank;
  }

  void start() {
      fuelTank.consume(5);
  }

  boolean isRunning() {
      return fuelTank.contentsLeft() > 0;
  }

  void useEnergy() {
      fuelTank.consume(10);
  }
}
```    
    
### 4

Tarkastellaan kurssin Ohjelmoinnin perusteet jo eläkkeelle jääneen HSL-aiheisen tehtävän mallivastausta.

Kuvaa _sekvenssikaaviona_ main-metodin suorituksen aikaansaama toiminnallisuus. 

Muista, että sekvenssikaaviossa tulee tulla ilmi kaikki mainin suorituksen aikaansaamat olioiden luomiset ja metodien kutsut!

```java
public class Kioski {
    public Matkakortti ostaMatkakortti(String nimi) {
        Matkakortti uusiKortti = new Matkakortti(nimi);                        
        return uusiKortti;
    }
    
    public Matkakortti ostaMatkakortti(String nimi, int arvo) {
        Matkakortti uusiKortti = new Matkakortti(nimi);                      
        uusiKortti.kasvataArvoa(arvo);
        return uusiKortti;
    }       
}


public class Matkakortti {
    String omistaja;
    double arvo;
    int pvm;
    int kk;
    
    public Matkakortti(String n){
        omistaja = n;  
        pvm = 0;  
        kk = 0;  
        arvo = 0;
    }         
    
    public void kasvataArvoa(double a){ 
        arvo += a; 
    }
    
    public void vahennaArvoa(double a){ 
        arvo -= a; 
    }
    
    public double getArvo(){ 
        return arvo; 
    }   

    public void uusiAika(int p, int k){
        kk = k;
        pvm = p;
    }    
}


public class Lataajalaite {
    public void lataaArvoa(Matkakortti k, double a) {
        k.kasvataArvoa(a);
    }
    
    public void lataaAikaa(Matkakortti k, int pvm, int kk) {
        k.uusiAika(pvm, kk);
    }
}



public class Lukijalaite {
    private double RATIKKA = 1.5;
    private double HKL = 2.1;
    private double SEUTU = 3.5;
    
    public boolean ostaLippu(Matkakortti k, int tyyppi){
        double hinta = 0;
        if ( tyyppi == 0 ) {
            hinta = RATIKKA;
        } else if ( tyyppi ==1 ) {
            hinta = HKL;
        } else {
            hinta = SEUTU;
        }                        
        
        if ( k.getArvo()<hinta ) { 
            return false;
        }
        k.vahennaArvoa(hinta);
        
        return true;
    }     
}

public class HKLLaitehallinto { 
        ArrayList<Lataajalaite> lataajat = new ArrayList();
        ArrayList<Lukijalaite> lukijat = new ArrayList();

        void lisaaLataaja(Lataajalaite lataaja){ lataajat.add(lataaja); }

        void lisaaLukija(Lukijalaite lukija){ lukijat.add(lukija); }
}

public class Main {
    public static void main(String[] args) {
        HKLLaitehallinto laitehallinto = new HKLLaitehallinto();

        Lataajalaite rautatietori = new Lataajalaite();
        Lukijalaite ratikka6 = new Lukijalaite();
        Lukijalaite bussi244 = new Lukijalaite();   

        laitehallinto.lisaaLataaja(rautatietori);
        laitehallinto.lisaaLukija(ratikka6);
        laitehallinto.lisaaLukija(bussi244);
        
        Kioski lippuLuukku = new Kioski();
        Matkakortti artonKortti = lippuLuukku.ostaMatkakortti("Arto");

        rautatietori.lataaArvoa(artonKortti, 3);
        
        ratikka6.ostaLippu(artonKortti, 0);
        bussi244.ostaLippu(artonKortti, 2);   
    }
}
```
