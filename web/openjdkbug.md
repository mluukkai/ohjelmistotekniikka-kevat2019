## Bugi OpenJDK:ssa (marraskuu 2018, päivitetty maaliskuu 2019)

Ainakin OpenJDK:n versiossa 1.8.0_181 on bugi, joka vaikuttaa mavenia käyttäviin sovelluksiin esim. estämällä sovelluksen ja testien ajamisen tai testikattavuusraportin luomisen. 

Sovelluksen ja testien ajamisen estävä bugi on ilmeisesti korjattu uudemmissa versioissa, mutta jacocon testikattavuusraportti ei välttämättä toimi. Tämä saattaa korjaantua päivittämällä pom.xml jacocon versio 0.8.0 => 0.8.3.
