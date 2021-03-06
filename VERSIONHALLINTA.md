# 3. Versionhallinta

**a) Markdown**

Viikolla 16 Palvelinten hallinta -kurssilla oli aiheena versionhallinta. Tämän kotitehtävän raportti tehdään Markdown-formaatilla. GitHub muotoilee Markdownin nätin näköiseksi. Risuaita tekee otsikon, tyhjä rivi kappaleenvaihdon, sisennyksellä koodin muotoilu ja kuvatkin voi laittaa nätisti suoraan repositorystä. Alla koodi kuvan laittamiseen.
~~~~
![Kuvan kuvaus](/relative/path/to/img.jpg?raw=true "Valinnainen otsikko")
Neljä tildeä, rivinvaihto ja koodi siihen väliin ja taas rivinvaihto ja neljä tildeä, niin saa nätin näköistä koodia.
~~~~
Aloitin tehtävän tekemisen luomalla Githubiin repositoryn. Minulla oli jo valmiiksi tunnus Githubiin, mutta ei yhtään repoa siellä. Githubiin rekisteröityminen on melko helppo operaatio, sisään kirjautumisen jälkeen vain klikataan ylhäältä oikealta + merkkiä ja sitten "New repository". Repoa luodessa on muutamia vaihtoehtoja, jotka selitän screenshotin alapuolella.

![Repon luonti](/images/21-reponluonti.png?raw=true "Repon luonti Githubissa")

Ensiksi valitaan tietysti repolle nimi ja kuvaus. Repon näkyvyyden voi asettaa julkiseksi tai yksityiseksi. Repo kannattaa alustaa READMElla, jotta sen voi saman tien kloonata omalle koneelle ja aloittaa repon käytön. .gitignorelle ei vielä tässä vaiheessa ole käyttöä, sitä käytetään ohjelmistokehitysprojekteissa esimerkiksi sitä varten, ettei jo valmiiksi käännetyt (already compiled) ohjelmakoodit mene turhaan repoon, koska siellä on tietysti tarkoitus säilöä vain lähdekoodia. Lisäksi gitignoreen voi laittaa esim. kehittäjäkohtaiset IDEn (Integrated Development Environment, koodieditori) mahdollisesti luomat asetustiedostot, joita ei luonnollisesti myöskään ole tarkoitus upata yhteiseen repositoryyn.

![Repon kloonaus](/images/22-gitkloonaus.png?raw=true "Repon kloonaus omalle koneelle")

Kunhan olet asentanut Gitin omalle Linux-koneellesi (sudo apt-get install git), voit kloonata repon gitistä yhdellä komennolla. Repo kloonataan oletuksena alikansioon, joka nimetään repon nimellä. Kun repo on onnistuneesti kloonattu, voit tutustua git status -komentoon, joka näyttää tämänhetkisen Gitin tilan (onko sinulla paikallisia muutoksia, joita ei ole vielä commitattu).

~~~~
apt-get install git
git clone https://github.com/jumajale/juhonph.git
git status
~~~~

Loin repoon images-kansion kuvia varten ja kopioin sinne ottamani screenshotin raporttia varten. Kopioin README.md tiedoston VERSIONHALLINTA.md tiedostoksi ja lisäsin tiedostoon tekstiä.

![Git add, commit ja push](/images/23-gitpushaus.png?raw=true "Git add, commit ja push")

Git status-komento näyttää nyt, että minulla on tiedostoja, joita ei seurata versionhallinnassa. git add . -komennolla saan ne lisättyä versionhallinnan seurantaan. git commit -komennolla luodaan committi, jolle annetaan commit message. Käytäntönä on käyttää commit messagessa preesens-muotoa, esim "Add driver for Windows". Git status -komento on hyvä ajaa ennen git add . -komentoa, jotta voit varmistua siitä, mitä olet lisäämässä versionhallintaan (jotta et vahingossakaan committaa julkiseen repositoryyn mitään typerää!). Git push -komentoa käytettäessä Git kysyy käyttäjätunnuksen ja salasanan, kun olet pushaamassa sisältöäsi Github-repositoryyn. Github-käyttäjälläsi tulee olla lupa tehdä committeja kyseiseen repositoryyn, muuten tämä ei onnistu.

~~~~
git status
git add .
git commit
git push
~~~~

Gitin perusteet hallinnassa. Jos kaikki on yksinkertaista (esim yhden hengen projektissa), pelkästään näillä pärjää pitkälle.

**d) Git log, git diff ja git blame**

~~~~
jupstejuho@jvl-830g5:~/Documents/palvelintenhallinta/juhonph$ git log
commit fcdb28af6221f5f96c4692c6deec1a0909ddb02f (HEAD -> master, origin/master, origin/HEAD)
Author: Jupstejuho <jupstejuho@hotmail.com>
Date:   Thu Apr 23 00:44:40 2020 +0300

    Complete step a) from homework, add screenshots

commit b0f421169dad902d3449a9f08737ffe0224c1020
Author: Jupstejuho <jupstejuho@hotmail.com>
Date:   Thu Apr 23 00:22:53 2020 +0300

    Fix code block

commit a19ce2eed4116fb6d502eb58ed7ecb1f9f64e906
Author: Jupstejuho <jupstejuho@hotmail.com>
Date:   Thu Apr 23 00:18:24 2020 +0300

    Add rivinvaihto

commit 7be310068947e14f3b3fe04fc85227e3c61849e8
Author: Jupstejuho <jupstejuho@hotmail.com>
Date:   Thu Apr 23 00:16:21 2020 +0300

    Remove initial crap from homework, test markdown formatting

commit d0e1dddaf30e6497e7c92c7c5ebaa108c1b8dfb4
Author: Jupstejuho <jupstejuho@hotmail.com>
Date:   Wed Apr 22 23:57:55 2020 +0300

    Add markdown file for homework

commit 11d113da63fbf302b99dce84aad3709e8e79b3c9
Author: Juho Lepp<C3><A4>nen <49460603+jumajale@users.noreply.github.com>
Date:   Wed Apr 22 23:39:55 2020 +0300

    Initial commit
~~~~

Git log -komento näyttää gitin lokikirjan; gitin tapauksessa tämä tarkoittaa siis historiaa repositoryyn tehdyistä commiteista. Tämä on sellaisenaan aina paikallista - mikäli työskentelisit vaikkapa kymmenhenkisessä projektissa, git log näyttäisi lokin commit-historiasta, joka on sinun koneellasi tiedossa. Jotta tähän päivittyy muiden tekemät muutokset, sinun tulee tehdä git pull ja vetää muutokset koneellesi, jolloin myös tiedostot päivittyvät. Git fetch -komento taasen ainoastaan tsekkaa muutosten tilan, mutta ei päivitä tiedostoja. Oikeissa ohjelmistoprojekteissa gittiä käytettäessä on ihan tyypillistä, että joudut välillä ratkomaan ristiriitaisuuksia palvelimen versionhallinnassa olevan version ja omalla koneellasi sijaitsevan version välillä.

Yllä näkyvässä git log -komennon ajamisen tuloksessa commitin perässä näkyvä mystinen numerosarja on commitille annettava yksilöllinen id. Tämä on tärkeä, koska sen perusteella voidaan jäljittää tietty muutos yksittäiseen committiin tai vaikkapa kätevästi palauttaa versionhallinnan tiedostojen tila siihen, mitä se oli esim. 5 committia sitten. Author-kohta taas kertoo commitin pushaajan nimen ja sähköpostiosoitteen ja Date-kohta paljastaa, milloin commit on pushattu. Tämän jälkeen sisennettynä näkyvä teksti on commitin kuvaus, joka annetaan yksilöllisesti jokaiselle commitille. Jokaisella commitilla on oltava kuvaus ja mielestäni sen tulee olla mahdollisimman lyhyt ja ytimekäs. Esimerkiksi "fixed stuff" ei missään mimessä kelpaa commit-messageksi!

<details>
  <summary>Klikkaa tästä nähdäksesi Git diff -komennon outputin</summary>

Kokeillaan spoiler-tägin käyttöä.

```
diff --git a/VERSIONHALLINTA.md b/VERSIONHALLINTA.md
index 9c569e9..7a68579 100644
--- a/VERSIONHALLINTA.md
+++ b/VERSIONHALLINTA.md
@@ -37,3 +37,49 @@ git push
 ~~~~
 
 Gitin perusteet hallinnassa. Jos kaikki on yksinkertaista (esim yhden hengen projektissa), pelkästään näillä pärjää pitkälle.
+
+**d) Git log, git diff ja git blame**
+
+~~~~
+jupstejuho@jvl-830g5:~/Documents/palvelintenhallinta/juhonph$ git log
+commit fcdb28af6221f5f96c4692c6deec1a0909ddb02f (HEAD -> master, origin/master, origin/HEAD)
+Author: Jupstejuho <jupstejuho@hotmail.com>
+Date:   Thu Apr 23 00:44:40 2020 +0300
+
+    Complete step a) from homework, add screenshots
+
+commit b0f421169dad902d3449a9f08737ffe0224c1020
+Author: Jupstejuho <jupstejuho@hotmail.com>
+Date:   Thu Apr 23 00:22:53 2020 +0300
+
+    Fix code block
+
+commit a19ce2eed4116fb6d502eb58ed7ecb1f9f64e906
+Author: Jupstejuho <jupstejuho@hotmail.com>
+Date:   Thu Apr 23 00:18:24 2020 +0300
+
+    Add rivinvaihto
+
+commit 7be310068947e14f3b3fe04fc85227e3c61849e8
+Author: Jupstejuho <jupstejuho@hotmail.com>
+Date:   Thu Apr 23 00:16:21 2020 +0300
+
+    Remove initial crap from homework, test markdown formatting
+
+commit d0e1dddaf30e6497e7c92c7c5ebaa108c1b8dfb4
+Author: Jupstejuho <jupstejuho@hotmail.com>
+Date:   Wed Apr 22 23:57:55 2020 +0300
+
+    Add markdown file for homework
+
+commit 11d113da63fbf302b99dce84aad3709e8e79b3c9
+Author: Juho Lepp<C3><A4>nen <49460603+jumajale@users.noreply.github.com>
+Date:   Wed Apr 22 23:39:55 2020 +0300
+
+    Initial commit
+~~~~
+
+Git log -komento näyttää gitin lokikirjan; gitin tapauksessa tämä tarkoittaa siis historiaa repositoryyn tehdyistä commiteista. Tämä on sellaisenaan aina paikallista - mikäli työskentelisit vaikkapa kymmenhenkisessä projektissa, git log näyttäisi lokin commit-historiasta, joka on sinun koneellasi tiedossa. Jotta tähän päivittyy muiden tekemät muutokset, sinun tulee tehdä git pull ja vetää muutokset koneellesi, jolloin myös tiedostot päivittyvät. Git fetch -komento taasen ainoastaan tsekkaa muutosten tilan, mutta ei päivitä tiedostoja. Oikeissa ohjelmistoprojekteissa gittiä käytettäessä on ihan tyypillistä, että joudut välillä ratkomaan ristiriitaisuuksia palvelimen versionhallinnassa olevan version ja omalla koneellasi sijaitsevan version välillä.
+
+Yllä näkyvässä git log -komennon ajamisen tuloksessa commitin perässä näkyvä mystinen numerosarja on commitille annettava yksilöllinen id. Tämä on tärkeä, koska sen perusteella voidaan jäljittää tietty muutos yksittäiseen committiin tai vaikkapa kätevästi palauttaa versionhallinnan tiedostojen tila siihen, mitä se oli esim. 5 committia sitten. Author-kohta taas kertoo commitin pushaajan nimen ja sähköpostiosoitteen ja Date-kohta paljastaa, milloin commit on pushattu. Tämän jälkeen sisennettynä näkyvä teksti on commitin kuvaus, joka annetaan yksilöllisesti jokaiselle commitille. Jokaisella commitilla on oltava kuvaus ja mielestäni sen tulee olla mahdollisimman lyhyt ja ytimekäs. Esimerkiksi "fixed stuff" ei missään mimessä kelpaa commit-messageksi!
+
```
</details>

Git diff -komennolla voidaan näyttää tiedostokohtaiset muutokset kahden eri version välillä. Oletuksena pelkkä "git diff" komennon ajaminen näyttää muutokset edellisen commitin jälkeen. Ylläolevasta git diff -komennon outputista näen, että ero edellisen commitin ja nykyisen version välillä on "-37,3 +37,49". Tämä luetaan suomeksi näin: "Riviltä 37 alkaen on poistettu 3 riviä, riviltä 37 alkaen on lisätty 49 riviä". Seuraavissa riveissä näkyy tiedostoon tehdyt varsinaiset muutokset. Git diff -komennon avulla voidaan myös esimerkiksi näyttää ero kahden commitin tai branchin (haaran) välillä. Seuraavaksi käsitellään git blame.

<details>
  <summary>Klikkaa tästä nähdäksesi git blamen outputin</summary>

```
jupstejuho@jvl-830g5:~/Documents/palvelintenhallinta/juhonph$ git blame README.md
^11d113d (Juho Lepp<C3><A4>nen 2020-04-22 23:39:55 +0300 1) # juhonph
^11d113d (Juho Lepp<C3><A4>nen 2020-04-22 23:39:55 +0300 2) Palvelinten hallintaa Saltilla
jupstejuho@jvl-830g5:~/Documents/palvelintenhallinta/juhonph$ git blame VERSIONHALLINTA.md
d0e1ddda (Jupstejuho 2020-04-22 23:57:55 +0300   1) # 3. Versionhallinta
d0e1ddda (Jupstejuho 2020-04-22 23:57:55 +0300   1) # 3. Versionhallinta
d0e1ddda (Jupstejuho 2020-04-22 23:57:55 +0300   2) 
7be31006 (Jupstejuho 2020-04-23 00:16:21 +0300   3) **a) Markdown**
a19ce2ee (Jupstejuho 2020-04-23 00:18:24 +0300   4) 

```
**Omittasin outputista paljon turhaa tekstiä pois, koska tarkoituksena on vain lyhyesti näyttää esimerkki siitä, mitä git blame tekee**
</details>

Git blamen avulla voidaan tarkistaa yksittäiseen tiedostoon tehdyt muutokset commitin tarkkuudella niin, että voidaan nähdä myös, kuka kyseiset muutokset on tehnyt.

**e) Git reset --hard**

Apua, tuli tehtyä tyhmä muutos. Ylikirjoitin vahingossa koko tämän kotitehtävän sisällön niin, että koko sisältönä oli vain "MINÄ VAHINGOSSA KOKO TIEDOSTON, ONKO TÄMÄ PAHA?", jonka jälkeen lisäsin tiedoston versionhallintaan git add . komennolla. En kuitenkaan tehnyt committia, joten hei, tämähän on vielä fiksattavissa. Ajetaan komento "git reset --hard", jonka jälkeen versionhallinta palauttaa kaiken tekstini takaisin! Näppärää.

![Git reset --hard](/images/24-gitresethard.png?raw=true "Git reset --hard")

**f) Uusi salt-moduuli**

Päätin tehdä salt-tilan, joka asentaa Gitin ja konfiguroi sen pitämään orjakoneella ajantasaisen version Git-repositorystäni /tmp/gittirepo hakemistossa. Lisäksi kyseiselle repolle asetetaan paikallisesti käyttäjän nimeksi Testi Kayttaja ja sähköpostiosoitteeksi testi@kayttaja.com. Päätin tehdä tämän perus package-file rakenteen sijaan hyödyntämällä Saltin sisäänrakennettua Gitin konffaamiseen tarkoitettua tilaa.

Jälleen kerran aloitin kirjautumalla saltmaster-palvelimelle SSH-yhteydellä. Loin /srv/salt kansioon oman kansion gitsaltilla-nimistä tilaa varten. Kansion sisälle loin init.sls tiedoston, johon laitoin sisällöksi: 


```
git:
  pkg.installed

gitinkloonaus:
  git.latest:
    - name: https://github.com/jumajale/juhonph.git
    - target: /tmp/gittirepo

gitemail:
  git.config_set:
    - name: user.email
    - value: testi@kayttaja.com
    - repo: /tmp/gittirepo

gitname:
  git.config_set:
    - name: user.name
    - value: Testi Kayttaja
    - repo: /tmp/gittirepo

```

Tämän jälkeen otin tilan käyttöön. Lopputulos vaikuttaisi onnistuneen.
<details>
  <summary>Outputti salt '*' state.apply gitsaltilla -komennon ajamisesta</summary>

```
root@jvl-saltmaster:~# salt '*' state.apply gitsaltilla
uusixubuntu:
----------
          ID: git
    Function: pkg.installed
      Result: True
     Comment: The following packages were installed/updated: git
     Started: 00:10:09.583648
    Duration: 6796.929 ms
     Changes:   
              ----------
              git:
                  ----------
                  new:
                      1:2.17.1-1ubuntu0.7
                  old:
              git-completion:
                  ----------
                  new:
                      1
                  old:
              git-core:
                  ----------
                  new:
                      1
                  old:
----------
          ID: gitinkloonaus
    Function: git.latest
        Name: https://github.com/jumajale/juhonph.git
      Result: True
     Comment: https://github.com/jumajale/juhonph.git cloned to /tmp/gittirepo
     Started: 00:10:16.403949
    Duration: 2242.736 ms
     Changes:   
              ----------
              new:
                  https://github.com/jumajale/juhonph.git => /tmp/gittirepo
              revision:
                  ----------
                  new:
                      63b1d6960385074d7c4acc226323fc9e32d1fdab
                  old:
                      None
----------
          ID: gitemail
    Function: git.config_set
        Name: user.email
      Result: True
     Comment: 'user.email' was added as 'testi@kayttaja.com'
     Started: 00:10:18.646903
    Duration: 23.562 ms
     Changes:   
              ----------
              user.email:
                  ----------
                  new:
                      - testi@kayttaja.com
                  old:
                      None
----------
          ID: gitname
    Function: git.config_set
        Name: user.name
      Result: True
     Comment: 'user.name' was added as 'Testi Kayttaja'
     Started: 00:10:18.670679
    Duration: 18.499 ms
     Changes:   
              ----------
              user.name:
                  ----------
                  new:
                      - Testi Kayttaja
                  old:
                      None

Summary for uusixubuntu
------------
Succeeded: 4 (changed=4)
Failed:    0
------------
Total states run:     4
Total run time:   9.082 s
```
</details>

Testasin Saltin ajamien muutosten toimivuutta siirtymällä Xubuntu-machinella /tmp/gittirepo hakemistoon ja ajamalla git status -komennon. Onnistui.

![Testaus Salt-tilan ajamisen jälkeen](/images/25-testaftersaltapply.png?raw=true "Testaus Salt-tilan ajamisen jälkeen")

Tämän jälkeen testasin vielä, onnistuiko Salt muuttamaan myös Git käyttäjän nimen ja sähköpostiosoitteen paikallisesti repositoryyn. Tein tämän luomalla uuden tiedoston, committaamalla ja pushaamalla sen, jonka jälkeen tarkistin git logilla, kuka näkyi uusimman commitin tekijänä. Great success!

![Testaus Salt-tilan ajamisen jälkeen](/images/26-testafterediting.png?raw=true "Testaus Salt-tilan ajamisen jälkeen")

