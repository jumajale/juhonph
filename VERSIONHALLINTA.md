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
