# JavaDoc

Osa ohjelmiston dokumentointia on lähdekoodin API:n eli käytännössä luokkien julkisten metodien kuvaus. Javassa lähdekoodi dokumentoidaan käyttäen JavaDoc-työkalua. 

Sovelluksen JavaDocia voi tarkastella selaimen avulla

![](https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/l-7.png)


Myös NetBeans osaa näyttää ohjelmoidessa koodiin määritellyn javadocin:

![](https://raw.githubusercontent.com/mluukkai/Ohjelmistotekniikka2018/master/web/images/l-14.png)


Dokumentointi tapahtuu kirjoittamalla koodin yhteyteen sopivasti muotoiltuja kommentteja.

Seuraava metodi on kommentoitu vapaamuotoisesti.  Kommentista käy ilmi mitä metodi tekee, mutta muotoiltua dokumentointisivua siitä ei saa tehtyä automaattisesti.
``` java
/* 
 * Kertoo kuinka todennäköistä onnistuminen on käyttäjän syötteellä.
 * HUOM: käyttää yläluokan metodia ja palauttaa arvon vähennettynä kalibroinnilla
 */
public int onnistumistodennakoisyys(int syote) {
    int tn = super.laskeTn(syote) - this.kalibrointi;
    return tn;
}
```

JavaDoc-dokumentoinnilla sama kuvaus olisi seuraavaa:
``` java
/**
 * Metodi kertoo mikä on onnistumistodennäköisyys syöteluvulla
 * ottaen huomioon olion konstruktorissa asetetun kalibrointiarvon.
 *
 * @param   syote   Käyttäjän antama syöte
 * 
 * @return todennäköisyys kalibroituna
 */
public int onnistumistodennakoisyys(int syote) {
    int tn = super.laskeTn(syote) - this.kalibrointi;
    return tn;
}
```

JavaDocin @param jne. avainsanoja ei onneksi tarvitse opetella ulkoa, koska NetBeans osaa täydentää myös JavaDoc-dokumentointia.  Private & package -näkyvyydellä olevat metodit eivät tule dokumentointiin.

Myös luokkia voi ja kannattaa dokumentoida. Se tapahtuu samalla tavoin kuin metodienkin dokumentointi.
``` java
/**
 * Luokka tarjoaa useita todennäköisyyslaskentaan tarvittavia metodeita.
 */
public class Todennakoisyyslaskin {
    /* ... */
}
```

JavaDocista saa luotua HTML-version suorittamalla komennon _mvn javadoc:javadoc_

Generoitu JavaDoc löytyy hakemistosta _target/site/apidocs/_

### Oliomuuttujien dokumentointi

Oliomuuttujille ei yleisesti ottaen tarvitse kirjoittaa JavaDoc-kommentteja, sillä ne ovat usein yksityisiä ja täten eivät kuulu luokan JavaDocilla kuvattavaan APIin. Jos sinulla on koodissasi julkisia (public) muuttujia, ne suositellaankin ensisijaisesti muutettavaksi yksityisiksi (private), jolloin JavaDoc-kommentteja voidaan kirjoittaa niiden setteri- ja getterimetodeille.

Jos sinulla kaikesta huolimatta on julkisia muuttujia, JavaDoc-syntaksin mukaan niiden dokumentointi tehdään kuten metodienkin: 
``` java
/**
 * Kalibrointiarvo todennäköisyyden laskemiseen.
 */
public int kalibrointi = 20;
```
 
## Tarkempi dokumentointi

Laajennetaan vielä alussa esiteltyä esimerkkiä.  Metodille annetaan toinen parametri ja tämä dokumentoidaan omana @param-rivinä.  Lisäksi dokumentointiin lisätään "See Also" -kohta, jonka kautta HTML-dokumentissa liikkuminen laskukone-pakkauksen Laskenta-luokan laskeTn(int)-metodiin on helppoa.  Tämä ilmaistaan muodossa laskukone.Laskenta#laskeTn(int).  NetBeanssin control+space osaa täydentää projektin koodin mukaan tämän polun!
``` java
/**
 * Metodi kertoo mikä on onnistumistodennäköisyys syöteluvulla
 * ottaen huomioon olion konstruktorissa asetetun kalibrointiarvon.
 *
 * @param   syote   Käyttäjän antama syöte
 * @param   kayttajanKorjaus    Käyttäjän antama korjausarvo
 * 
 * @see    laskukone.Laskenta#laskeTn(int)
 *
 * @return todennäköisyys kalibroituna
 */
public int onnistumistodennakoisyys(int syote, int kayttajanKorjaus) {
    int tn = super.laskeTn(syote) - this.kalibrointi - kayttajanKorjaus;
    return tn;
}
```

Lisää ohjeita löydät [JavaDocin Wikipedia-sivulta](http://en.wikipedia.org/wiki/Javadoc).

## Pakkausten dokumentointi

Myös pakkaukselle voi antaa JavaDoc-kuvauksen sijoittamalla pakkaukseen tiedoston _package-info.java_, mallia voi ottaa [referenssisovelluksesta](https://github.com/mluukkai/OtmTodoApp/blob/master/src/main/java/todoapp/dao/package-info.java).