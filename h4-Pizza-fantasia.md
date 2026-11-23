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

# c) 
