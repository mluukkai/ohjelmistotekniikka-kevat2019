## Bugi OpenJDK:n uusimmassa versiossa (marraskuu 2018)

OpenJDK:n uusimmassa versiossa on bugi, joka vaikuttaa mavenia käyttäviin sovelluksiin esim. estämällä sovelluksen/testien ajamisen. 

Tällä hetkellä ongelmaan ei ole tiedossa mitään järkevää korjausta, joka toimisi käyttöympäristöstä riippumatta, joten kannattaa pitäytyä käyttämästä OpenJDK:ta ja turvautua vaihtoehtoisiin ratkaisuihin (esim. Oracle JDK). 

Jos kuitenkin kaikesta huolimatta haluat käyttää OpenJDK:ta, lisää pom.xml tiedostoon maven-surefire-plugin:

```
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <version>2.16</version>
  <configuration>
    <argLine>-Djdk.net.URLClassPath.disableClassPathURLCheck=true</argLine>
  </configuration>
</plugin>
```

Jos olet jo määrittänyt ko. pluginin, lisää sen `<configuration>` -tagien sisään seuraava rivi yo. esimerkin mukaisesti:

`<argLine>-Djdk.net.URLClassPath.disableClassPathURLCheck=true</argLine>`

Nämä lisäykset saattavat kuitenkin rikkoa Jacocon testikattavuusraportin, joten niitä kannattaa käyttää harkiten.
