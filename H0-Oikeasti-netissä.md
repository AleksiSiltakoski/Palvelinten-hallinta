# H0 - Oikeasti netissä 

Ensimmäisenä tehtävä tuli tiiviistää kahden eri sivun asiat esimerkiksi ranskalaisin viivoin. Kyseiset sivut on merkitty lähteisiin.
 ## Ensimmäisen sivun (Niemi 2025: H4 Tehtävät) tiivistys
- vuokrataan oikea virtuaalipalvelin esim. upcloud
- valitaan serveri mahdollisimman läheltä (Suomi, Eurooppa)
- valitaan halvin 1gigan muistin omaava palvelin
- "Operating system" kohdassa valitse Debian GNU/Linux 13 (Trixie)
- Login methodiksi valitse SSH-avain. Luo ne virtulLinuxin terminaalissa komennolla "ssh-keygen"
- Kopioi tämän jälkeen public keyn rivi ja lisää se upcloudin sivulle.
- Ota yhteys virtuaalipalvelimeen komennolla root + @ + virtuaalipalvelimen ip-osoite (sen näkee upcloudin sivulta) oikea komento voi olla siis esim: ssh root@193.11.11.10
- Lisää käyttäjä komennolla "adduser omanimi sudo". Tämä tarkoittaa, että käyttäjä luodaan nimellä omanimi ja se saa sudo-oikeudet.
- Mene käyttäjän kotihakemistoon ja luo .ssh kansio "(mkdir -p /home/omanimi/.ssh)". Anna oikeudet (chmod 700 /home/omanimi/.ssh).
- Sitten lisää nano /home/omanimi/.ssh/authorized_keys tiedostoon public key yhdelle riville. Public key löytyy virtuaalilinuxin .ssh kamsiosta nimeltä (id_ed255519.pub).
- Aseta oikeudet komennolla chmod 600 /home/omanimi1/.ssh/authorized_keys
- Omistajuus komennolla: chown -R omanimi:omanimi /home/omanimi/.ssh
-Palomuurin asennus: "apt-get update" & "apt-get install ufw".
- Tee reikä palomuuriin porttiin 22 komenoolla: "ufc allow 22/tcp"
- Aktivoi palomuuri komennolla: "ufc enable"
- Komennolla: "ufw status" voi tarkistaa palomuurin tilan.
- HUOMIO! koska kyseessä on tiivistys "omanimi" on keksitty nimi.
- Ota ssh-yhteys pilveen ja päivitä järjestelmä terminaalissa komennolla sudo apt update
- Apache2 asennetaan komennolla "sudo apt-get install apache2"

## Toisen sivun a) kohdan tiivistys (Partanen 2025: Harjoitus 5 Nimekäs a) kohta)
- Tarvitaan oma domain-nimi (mahdollisimman halpa, koska ei omaan käyttöön)
- Namecheap yksi mahdollisista tarjoajista
- Valitse domain privacy suojaus päälle
- Rekisteröidy ja syötä korttitiedot ja osta nimi
- Laita osoite osoittamaan omaan koneeseen
- Valitse advanced DNS ja lisää oma A record kohta, joka osoittaa virtuaalipalvelimelle.
- Host kohtaan laita www 

## a) Debianin asennus
Tässä tehtävässä tarkoituksena oli asentaa Debian 13 tietokoneelle. Koko asennuksen sain tehtyä seuraamalla terokarvinen.com "Vinkit" kohdassa olevaa ohjetta. 
Itse ohje on myös merkittynä lähteisiin. Latasin aluksi sivulta: https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/ oikean Debian version mikä oli tässä tapauksessa "debian-live-13.7.0-amd64-xfce.iso".
Debianin lataamisen jälkeen avasin virtualboxin managerin ja painoin sieltä kohtaa "New" ja aloin debianin alustamisen virtuaaliboxiin. Nimesin sen Debianiksi ja ISO imageen laitoin juuri sen polun missä ISO tiedosto on.
Kohdan "OS Version" vaihdoin 64-bittiseksi ja klickasin täplän "Proceed with Unattended installation" pois.
Muistiin laitoin 4090 MB, ytimiin 2 ja disk size 50 GB. 
Tämän jälkeen käynnistin Debianin asetuksella "Start with GUI".
Kävin testaamassa Debianin internet yhteydet avaamalla sen ja applications kohdasta painoin "web browser" ja hain wikipediaa ja katsoin aukeaako se ja se aukesi.
Käynnistin Debianin uudelleen terminalista komenolla "sudo reboot". Ja Live boot menusta valitsin kohdan "start installer". Ja tämän jälkeen aloin asentamaan Debiania. 
Kieleksi valitsin engalnnin, mutta näppäimistön kieleksi laitoin suomen. Configure locales kohtaan laitoin: "en_US.UTF-8". "Root password" kohdan jätin tyhjäksi.
Uuden käyttäjän nimeksi oman nimeni ja käyttäjänimeksi etunimeni. Partion disks: Guided - use entire disk ja sitten heti perään valinta "SCI3" ja vielä loppuun "Partion disks": All files in one portion.
Tämän jälkeen debian asensi ja valittiin continue ja debian käynnisti itsensä uudelleen. Tämän jälkeen kirjauduin sisään juuri tekemillä käyttäjänimellä ja salasanalla.

Tämän jälkeen minulla tuli sama ongelma kuin Punnalalla ja toimin hänen ohjeiden mukaansa seuraavasti: 
1. Avasin source.listin komennolla: "sudo nano /etc/apt/sources.list"
2. Source.listiin syötin seuraavat komennot:
    deb https://deb.debian.org/debian trixie main non-free-firmware
deb-src https://deb.debian.org/debian trixie main non-free-firmware

deb https://security.debian.org/debian-security trixie-security main non-free-firmware
deb-src https://security.debian.org/debian-security trixie-security main non-free-firmware

deb https://deb.debian.org/debian trixie-updates main non-free-firmware
deb-src https://deb.debian.org/debian trixie-updates main non-free-firmware
3. Tallensin ne painamalla Ctrl & O + enter ja poistuin sieltä painamalla ctrl + X.

Sitten asensin palomuurin laittamlla seuraavat komennot terminaaliin: 
1. sudo apt-get update
2. sudo apt-get -y dist-upgrade
3. sudo apt-get -y install ufw
4. sudo ufw enable

Tämän jälkeen sain tekstin terminaliin, että palomuuri on asennettu ja aktivoitu.

## Copy pasten toimintaan laitto debianissa
Jatkoin Punnalan ohjeiden seuraamista ja seuraavaksi laitettiin Copy paste toimimaan Debianissa.
1. Avasin ylhäällä olevasta valikosta kohdan "Devices" auki ja sieltä kohdan "Insert Guest Additions CD image"
2. Avasin "Applications"- kohdan ja sieltä "file manager" ja sieltä klickasin CD:n auki.
3. Avasin jälleen "Applications" ja sieltä tällä kertaa "Terminal Emulator"
4. Terminaliin laitoin seuraavat komennot ohjeen mukaisesti järjestyksessä:
   cd /media/cdrom0
   ls
   sudo bash VBoxLinuxAdditions.run
5. Sitten käynnistin Debianin uudelleen sulkemalla sen oikealta ylhäältä "X:Stä" ja käynnistin sen manuaalisesti itse uudelleen.
6. Copy paste alkoi toimia, kun valittiin "Devices" ja sieltä "shared Clipboard ja sieltä vaihtoehto "Bidirectional"
7. Tämän jälkeen testasin copypastea itse ja se toimi

Tämän jälkeen olin saanut Debianin asennettua ja laitettua palomuurin päälle sekä saanut onnistuneesti copy pasten toi
mimaan.


## F) Vaihtoehtoinen tehtävä
Koska en valinnut vuokrata omaa virtuaalipalvelinta valitsin tehtävänannosta tehtäväksi kohdan f) "Vaihtoehto tehtävän", joka oli kokonaan ilmainen.
Tehtävänä oli lisätä weppipalvelimen Debianiin. 
Aloitin laittamalla virtuaalilinuxin terminaaliin komennon "sudo apt-get install apache2"
Tämän jälkeen avasin virtuaalikoneen "web browserin" ja osoiteriville kirjoitin "https://localhost". Firefox avasi apachen sivun eli apache2 toimi. 
Sitten menin takaisin virtuaalikoneen terminaaliin ja laitoin sinne komennon "ip addr" ja katsoin oman ip-osoitteeni riviltä jossa oli kohta "inet".
Kun sain tietää oman ip-osoitteeni avasin "web browser" ja firefoxiin kirjoitin "http:/" ja perään juuri se äsken katsomani ip-osoite. Painoin ENTER ja sama apachen sivu aukesi eli sekin toimi.

Sitten testasin vielä kotisivuja. Menin aluksi kotihakemistoon terminaalissa komennolla "cd"
Tämän jälkeen kirjoitin terminaliin komennon: "mkdir public_html". Tämä loi "public_html"-kansion.
Tässä välissä annoin oikeudet komennolla: "chmod 700 /home/aleksi".
Avasin virtuaalikoneen firefoxilla nettisivun: "http://localhost/aleksi".
Tämän jälkeen firefoxiin avautui juuri tekemäni "public_html". Se oli tyhjä, koska itse kansioon ei olla vielä luotu mitään tiedostoja.

Tässä tehtävässä käytin ohjeena Tero karvisen 2008: Install Apache Web server on ubuntu, minkä löysin terokarvinen.com sivulta aika ylhäältä "Esitiedot" kohdasta. Kyseinen sivu on merkittynä lähteisiin.
## Lähteet
Tero Karvinen 2008: Install Apache Web Server on Ubuntu: https://terokarvinen.com/2008/05/02/install-apache-web-server-on-ubuntu-4/index.html
Punnala 2025: Linux asennus virtuaalikoneelle: https://github.com/punnalathomas/linux-course/blob/main/h1-installing-linux.md
Alla ne sivut joista, "a) kohdan" tiivistys tuli tehdä:
Niemi 2025: H4 Tehtävät: https://github.com/AONCODES/linux-course/blob/main/h4.md
Partanen 2025: Harjoitus 5 Nimekäs a) kohta: https://partanennn.github.io/linux-servers/practices/fifth-week.html
