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
Linkki uutiseen: https://news.ycombinator.com/item?id=39983536 
- Uutisessa käsitellään Ansiblea keskitetyn hallinnan työkaluna palvelimien ja infrastruktuurin ylläpidossa
- IaC -> auttaa asioissa, mitkä ennen tehtiin käsin
- CMS -> auttaa asioissa, mihin kukaan ei voi käsin koskea ja runnaa IaC elementtien sisällä.
- Huomio: uutisessa käsiteltiin eroa infrastruktuurin automatisoinnin ja konfiguraation väillä.


# a) Kohta apache2 
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

# b) kohta Nginx
Aloitin pysäyttämällä apachen komennolla "sudo systemctl stop apache2". Ja tarkistin, että se on varmasti pysähtynyt komennolla "systemctl status apache2".
Tämän jälkeen poistin apachen käynnistymästä automaattisesti komennolla "sudo systemctl disable apache2"
Sitten latasin Nginx: sudo apt update, sudo apt install nginx.
Käynnistin Nginx: sudo systemctl enable nginx, sudo systemctl start nginx.
Ja katsoin että se oli käynnissä komennolla: "systemctl status nginx".

Tein uuden hakemiston komennollmkdir ~/nginxsivu"
Siirryin nano ~/nginxsivu/index.html ja kirjoitin sinne nginx-sivuni.
Tämän jälkeen avasin nginx oletussivuston asetukset: "sudo nano /etc/nginx/sites-available/default" ja etsin sieltä rivin "root /var/www/html;" ja muutin sen muotoon: root /home/aleksi/nginxsivu;.
Tallensin muutokset ja testasin ne komennolla "sudo nginx -t".
Sitten käynnistin nginx uudelleen komennolla "sudo systemctl restart nginx" ja avasin firefoxin ja kirjoitin sinne: http://localhost.
Sivusto näytti oikean tuloksen: 
<img width="2880" height="2160" alt="image" src="https://github.com/user-attachments/assets/fe746a9a-511d-44f3-bff4-1bebc99d697a" />

# c) kohta Nginx automatisointi ansiblella
Tässä tehtävässä tuli automatisoida Nginx asennus Ansiblella.
Siirryin ansible kansiooni komennolla "cd ~/ansible".
Tämän jälkeen loin kyseiseen kansioon uuden roolin "nginx" komennolla: "mkdir -p roles/nginx/tasks".
Ja siirryin: "nano roles/nginx/tasks/main.yml".
Tässä kohdassa seurasin Karvinen 2026: Apache installwd with Ansible -quick notes ohjeita soveltaen. (merkitty lähteisiin). 
Nanoon kirjoitin: 
<img width="1245" height="522" alt="image" src="https://github.com/user-attachments/assets/ac7498f8-f1a3-4d24-8f49-0fab221a735f" />
Tämän jälkeen talensin tuttuun tapaan tekemäni muutokset ja poistuin nano-tiedostosta.
Avasin seuraavaksi nano site.yml ja kirjoitin alimmaiseksi "- nginx". Tämä oli minulle tuttua h2-tehtävästä.
Tämän jälkeen ajoin terminaalissa komennon: "ansible-playbook -i hosts.ini site.yml -K" ja syötin salasanani. 
Palybook suoritettiin onnistuneesti: 
<img width="1512" height="778" alt="image" src="https://github.com/user-attachments/assets/b1a7a36e-e9c6-46cc-839e-bbc7517899dc" />





# Läheet
Nginx https://wiki.debian.org/Nginx luettu 17.11.2026
Karvinen 2026: Apache installed with Ansible -quick notes: https://terokarvinen.com/apache-ansible/ luettu 17.11.2026
Ansbile community documentation https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html luettu 17.11.2026
Ansible- Infrastructure as Code for building up my Homelab: https://news.ycombinator.com/item?id=39983536 Luettu 17.11.2026






