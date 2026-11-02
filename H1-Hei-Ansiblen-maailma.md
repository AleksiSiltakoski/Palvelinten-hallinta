# H1-Hei-Ansiblen-Maailma

## Tehtävänä oli asentaa SSH-demoni ja katsoa että se toimii. Tämän jälkeen automatisoida SSH-kirjautuminen julkisella avaimella. Ja tämän jälkeen tehdä hei maailma ansiblella.

## SSH-demonin lataus
Ensiksi kirjauduin sudo-käyttäjälleni komennolla "Sudo whoami", jonka jälkeen syötin salasanani ja olin sudo-käyttäjälläni kirjautuneena. 
Ajoin uusimmat päivitykset komennolla "sudo apt-get update". 
Latasin sitten SSH:n komennolla "sudo apt-get -y install ssh". 
Seuraavaksi laitoin komennon "sudo systemctl enable --now ssh". Tämä komento teki sen, että SSH-demoni käynnistyy aina virtuaalikoneen käynnistyessä ja se laitettiin myös samalla hetkellä päälle.
Nyt ssh-demoni on ladattu ja asetettu käynnistymään aina virtuaalikoneen käynnistymisen yhteydessä

## SSH-demonin testaus
Aloitin laittamalla komennon "ssh localhost" virtuaalikoneen terminaaliin. 
Tämän jälkeen laitoin terminaalin komento riville "w" ja näin, että olin kirjautuneena kaksi kertaa. Toinen on läppärini ja toinen SSH:n kautta muodostettu yhteys.
Terminaaliin laitoin komennon "exit" ja toinen yhteyksistä disconnectasi
Seuraavaksi generoin keypair:in komennolla "ssh-keygen". Tässä vaiheessa terminaalissa piti painaa 3 kertaa enteriä, mikä hyväksyi kaikki oletusasetukset. 
Sitten juuri tehty keypair kopioitiin localhostiin komennolla "ssh-copy-id localhost". Tämän jälkeen tuli salasana antaa vielä viimeisen kerran. Kyseinen komento lisäsi public key:n ssh/authorized_keys ja nyt kirjautuminen onnistuu SSH:n kautta ilman salasanaa.
Seuraavaksi kirjoitin virtuaalikoneen terminaaliin komennon: "ssh localhost" ja pystyin kirjautumaan ilman salasanan käyttöä.
![ssh-copy-id localhost](ssh.png)

## Ansiblen lataus ja Hei maailman teko ja kokeileminen SSH:n yli
Ajoin uusimmat päivitykset jälleen komennolla "sudo apt-get update".
Tämän jälkeen asensin ansiblen laittamalla virtuaalikoneen terminaaliin komennon "sudo apt-get install ansible". Tämän jälkeen kesti hetken ja ansible oli asentunut. 
Seuraavaksi loin kansion ansiblen configurationille komennolla "mkdir ansible". Tämän jälkeen siirryin kansioon komennolla "cd ansible/"
Tämän jälkeen loin tiedoston hosts.ini sisälle laittamalla terminaaliin komennon "nano hosts.ini". Kirjoitin tämän jälkeen nanoon "localhost" ja tallensin muutokseni ctrl + o + enter ja poistuin nanosta ctrl + x.
Tarkistin tämän jälkeen hosts.ini sisällön komennolla "cat hosts.ini" ja tuloste oli juuri laittamani "localhost". 
Seuraavaksi laitoin terminaaliin komennon "ansible all -a 'uptime' -i hosts.ini". Se suoritti uptime-komennon Ansible:n kautta.
![ansible-uptime-komento](ansible1.png)
Nyt ansible pystyy käyttämään SSH-yhteyttä. 

Seuraavaksi otin turhan virhe viestin python versiosta pois, joka on kuvassa pinkillä. 
Ensiksi menin takaisin "nano hosts.ini" ja liitin nanossa localhostin alapuolelle yhden rivin väliä, jonka jälkeen tekstit: "[all:vars]
ja seuraavalle riville ansible_python_interpreter=/usr/bin/python3". Tämän jälkeen tallennuksen jälkeen kijroitin terminaaliin komennon "ansible all -a 'uptime' -i hosts.ini" uudestaan ja pinkki error-viesti oli poistunut.
![ansible-uptime-komento-uusi](ansible2.png)

Tämän jälkeen avasin "nano ansible.cfg" ja kirjoitin sinne ensimmäiselle riville [defaults] ja toiselle riville: inventory = hosts.ini. Tallensin ctrl + o ja enter ja poituin ctrl + x.
Tarkistin, että kaikki oli oikein komennolla "cat ansible.cfg".
Tämän jälkeen riiti, että terminaaliin kirjoitti komennon "ansible all -a 'uptime' ja edellisessä komennossa mukana olleen kohdan: "-i hosts.ini" pystyy tästä lähtien jättämään pois kokonaan, kun käytetään komentoja "ansible" & "ansible-playbook".

Tämän jälkeen kirjoitin komennon "nano site.yml" ja sinne lisättiin: 
- hosts: all
  roles:
    - hello
Site.yml listaa mitkä tietokoneet saavat mitkä konfiguraatiot eli roolit. Kyseinen komento laitettiin, koska halutaan että kaikki koneet saavat roolin "hello".
Tämän jälkeen terminaalissa ajettiin komento: "ansible-playbook site.yml".
Näytölle tuli punainen error-viesti, jossa sanottiin, että roolia "hello" ei ole olemassa, joten se pitää tehdä. Lisäksi tuli varmistus kuitenkin siitä, että ansible-playbook lukee tiedoston site.yml, mikä on hyvä tieto.

Seuraavaksi loin kyseisen "hello"- roolin. 
Loin tarvittavat kansiot laittamalla komennon "mkdir -p roles/hello/tasks/" virtuaalikoneen terminaaliin. 
Tämän jälkeen avastin tiedoston "nano roles/hello/tasks/main.yml" ja kirjoitin sinne: 
- copy:
    dest: /tmp/hello-ansible
    content: "See you at TeroKarvinen.com!\n"
  Tämän jälkeen ajoin komennon "ansible-playbook site.yml"
  ![ansible-playbook-site.yml-komento](ansible3.png)

  Tämän jälkeen ajoin vielä varmistukseksi toisen komennon: "ssh localhost 'cat /tmp/hello-ansible'", mikä tulosti "See you at Terokarvinen.com" (näkyy ylhäällä olevassa kuvassa. Tässä kohtaa testasin hello ansiblea SSH:n yli.

## Lähteet
Tero karvinen 2026: Hello Ansible: https://terokarvinen.com/hello-ansible/ luettu: 2.11.2026
Tero Karvinen 2026: SSH public key - Login without password: https://terokarvinen.com/ssh-public-key-login-without-password/ Luettu 2.11.2026
