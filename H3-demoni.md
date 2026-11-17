## Demoni

# X) tiivistykset
- apache2 ladataan komennolla "sudo apt-get install apache2"
- Muutokset confioguraatio tiedostoihin tapahtuvat vasta, kun demonia "kickataan".
- apache2 käynnistetään uudelleen komennolla "sudo systemctl restart apache2".

- Kun halutaan tehtävän tapahtuman vain, kun muutos on tehty laitteeseen. Esim halutaan restarttaa laite päivtysten jälkeen, eikä ennen kun muutoksia on tehty.
- Ansible käyttää tähän "Handlersseja". Ne ovat taskeja, jotka ajavat vain kun niille on ilmoitettu.
- Taskit voivat ohjeistaa yhtä tai enempää "handlersia" toimimaan, kun käytetään "notify".
- "Handlersit" toteutetaan siinä järjestyksessä, missä ne on annettu "handlersseissa", eikä siinä missä ne on kerrottu "notify" kohdassa.

# Artikkelin tiivistys


# a) Kohta apache2 asennus
Olin jo ladannut aiemmissa tehtävissä apachen, joten tässä kohtaa tein vain uuden hakemiston komennolla "mkdir -p ~/public_html". 
Tämän jälkeen terminaaliin laitoin komennon "nano ~/public_html/index.html" ja sinne kirjoitin "Testi sivu harjoitus".
Tämän jälkeen ajoin komennon "sudo a2enmod userdir". 
Seuraavaksi annoin nämä oikeudet: chmod 755 ~ chmod 755 ~/public_html chmod 644 ~/public_html/index.html.
chmod  755 = saan lukea, siirtyä ja kirjoittaa hakemistoon. Muut saavat lukea & apache pääsee kulkemaan kotihakemiston läpi public_html.
chmod 755 ~/public_html = apache saa lukea hakemiston sisällön
chmod 644 ~/public_html/index.html = Voin muokata tiedostoa & apache ja muut saavat lukea tiedostoa.

Tämän jälkeen tarkastin apachen statuksen komennolla "systemctl status apache2". <img width="2880" height="2160" alt="image" src="https://github.com/user-attachments/assets/d0bdf956-a284-43ce-98eb-90ed9057666b" />
Ja lopuksi avasin virtuaalikoneella firefoxin ja kirjoitin sinne "http://localhost/~aleksi/" ja sivu näkyi siellä. 
<img width="2880" height="2160" alt="image" src="https://github.com/user-attachments/assets/3a1abab1-9323-42d6-a48f-8deffb08e291" />




