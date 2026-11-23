# Postgresql

# a) Tässä tehtävässä latasin demonin Postgresql.
Aloitin demonin lataamisen kirjoittamalla linuxin terminaliin komennon "sudo apt-get update". 
Tämän jälkeen heti perään kirjoitin komennon "sudo apt-get -y install postgresql", mikä latasi itse demonin. 
Tämän jälkeen testasin demonin toimivuuden alla olevan kuvan mukaisesti.
<img width="479" height="134" alt="image" src="https://github.com/user-attachments/assets/98b7fad1-828a-4131-a0c4-ea52aee2fe06" />

# b) Automatisointi ansiblella
Tässä tehtävässä siirryin alussa ansible kansiooni komennolla "cd ~/ansible". 
Sitten loin postgresql roolin komennolla "mkdir -p roles/postgresql/tasks".
Tämän jälkeen siirryin "nano roles/postgresql/tasks/main.yml". Ja sinne muokkasin seuraavasti: <img width="454" height="166" alt="image" src="https://github.com/user-attachments/assets/79df51f8-45f5-4795-8bc8-5bc397366335" />.

Sitten siirryin "nano site.yml" ja lisäsin sinne alimmaiselle riville "- postgresql", muiden roolien jatkoksi. 
Tämän jälkeen ajoin ansible-playbookin kommennolla "ansible-playbook -i hosts.ini site.yml -K". 
<img width="1512" height="148" alt="image" src="https://github.com/user-attachments/assets/7af32973-322c-4b86-ae40-c5233c4f51dc" />

# c) Seuraavakai vuorossa oli Asetusten muuttaminen "master modella" ja ansbilen uudestan ajo
Aloitin tehtävän tarkistamalla, mikä PostgreSQL-versio minulla oli lataamalla kirjoittamalla terminaaliin komennon ls /etc/postgresql". Tulos oli 17.
Tämän jälkeen jatkoin siirtymällä "nano roles/postgresql/tasks/main.yml". Tämän jälkeen muokkasin tiedostoa lisäämällä PostgrreSql:n latauksen alapuolelle uuden set log_connectionsin: <img width="628" height="291" alt="image" src="https://github.com/user-attachments/assets/af2f729a-27d2-4189-8fee-30b71175c5f4" />

Se siis avaa PostgreSQL:n asetustiedoston postgresql.conf ja etsii rivin joka alkaa log_connections. Jos rivi löytyy ansible korvaa sen arvoilla "log_connections = on". Ja jos riviä ei löydy ansible puolestaan lisää sen tiedostonn.
"Log_connections = on" kirjaa jokaisen uuden yhteyden tietokantaan.

Seuraavaksi ajoin ansible-playbookin komennolla "ansible-playbook -i hosts.ini site.yml -K".
<img width="1467" height="141" alt="image" src="https://github.com/user-attachments/assets/bff636ad-01d7-44eb-a0be-ef29a470aa50" />

Lopuksi ajoin vielä komennon "grep log_connections /etc/postgresql/17/main/postgresql.conf". Mikä näyttää, että tekemäni muutokset asetuksiin olivat tulleet voimaan. <img width="940" height="90" alt="image" src="https://github.com/user-attachments/assets/96972d1e-50e9-4cce-acea-7d3ede15ddb5" />
Tehtävän tekemiseen käytin apuna seuraavaa lähdettä https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/lineinfile_module.html

# Lähteet:
Ansible Community Documentation - ansible.builtin.lineinfile module – Manage lines in text files: https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/lineinfile_module.html luettu 23.11.2026
University of Westminster - Configuration Management of Distributed Systems over Unreliable and Hostile Networks: https://westminsterresearch.westminster.ac.uk/item/w7vvz/configuration-management-of-distributed-systems-over-unreliable-and-hostile-networks luettu 23.11.2026
