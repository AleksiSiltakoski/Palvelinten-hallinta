# H1 Voileipä

## Tiivistykset kappaleista
- käyttäjä luodaan komennolla "sudo adduser"
- Ryhmä luodaan komennolla "sudo groupadd"
- "sudo visudo /etc/sudoers.d/sudoless" ja "sinne %sudoless ALL = (ALL) NOPASSWD: ALL" antaa kaikkien sudoless ryhmän jäsenten käyttää sudoa ilman salasanaa.


## a) osa
Seurasin tehtävässä Tero karvinen "Sudo without password" ohjeita.

Menin terminaalissa ansible kansiooni komennolla "cd ansible/"
Siellä loin uuden käyttäjän komennolla "sudo adduser aleksi2"
Tein myös "sudoless" ryhmän komennolla "sudo groupadd sudoless"
lisäsin aleksi 2 sinne komennolla "sudo adduser aleksi2 sudoless".
Tämän jälkeen avasin uuden terminaali ikkunan ja kirjoitin sinne komennon "sudo -i" ja olin roottina sisällä.
Tämän jälkeen menin takaisin aiempaan terminaaliin, jossa olin kirjautuneena vielä sudona ja kirjoitin komennon "sudo visudo /etc/sudoers.d/sudoless" ja sinne lisäsin rivin tekstiä: "%sudoless ALL = (ALL) NOPASSWD: ALL"
Tämä lisäsi sudoers säännön, missä kaikki sudoless ryhmän käyttjät voivat käyttää sudoa ilman salasanaa.

![sudo](sudo.png)

## b) osa 
Tässä tehtävässä seurasin Tero Karvinen "Passwordles Sudo with Ansible" ohjeita.
Aluksi loin tiedoston mkdir -p roles/aleksi2/tasks
Tämän jälkeen komennolla "nano roles/aleksi2/tasks/main.yml
Ja lisäsin sinne ohjeiden mukaisesti. Muutin nimet aleksi2 ja key kohdan. <img width="895" height="480" alt="image" src="https://github.com/user-attachments/assets/30de2ad7-48f6-41a9-82f1-53548854f553" /> ylhäällä oleva kuva ohjeesta Tero Karvinen 2026 "Passwordles Sudo with Ansible".
Sitten menin "nano site.yml" ja sinne kohdan "hosts" alle kohdan "become: true" & "roles" kohtaan "aleksi2".
Tämän jälkeen ajoin terminaalissa komennon "ansible-playbook site.yml" ja tuli virhe ilmmoitus, jossa sanottiin, että sudo tarvitsee salasanan. <img width="901" height="262" alt="image" src="https://github.com/user-attachments/assets/1976b720-4e2a-4d3e-8c76-c147aaea8ec1" />

Joten ajoin komennpn "ansible-playbook site.yml -K" ja syötin salasanan ja tämä oli lopputulos. <img width="1536" height="502" alt="image" src="https://github.com/user-attachments/assets/f9f6d634-0bac-4835-a3f7-d57da5da3ed2" />

## c) osa
Asensin kaksi pakettia seuraavaksi ansiblella. Nämä olivat tree ja htop. 
Ensiksi loin uuden roolin komennolla "mkdir -p roles/packages/tasks"
Tämän jälkeen menin nanoon "nano roles/packages/tasks/main.yml"
Nanoon lisäsin:
---
- name: Install packages
  apt:
    name:
      - tree
      - htop
    state: present
    update_cache: yes

  name: ne paketit, jotka asennan
  state: present eli paketin pitää olla asennettu
  updatet_cache: yes = päivittää pakettilistan ennen asennusta
Tämän jälkeen lisäsin roolin site.yml komennolla "nano site.yml". Ja lisäsin rooli kohdassa "aleksi2" alapuolelle juuri luomani "packages" roolin.
Sitten ajoin komennon: "ansible-playbook site.yml --ask-become-password"
<img width="1519" height="702" alt="image" src="https://github.com/user-attachments/assets/220f5212-272c-44dd-8ea7-ea6d36f6dd35" />

## d) osa 
Loin ensiksi roolin nimeltä file komennolla "mkdir -p roles/file/tasks"
Tämän jälkeen kirjoitin terminaaliin komennon "nano roles/file/tasks/main.yml"
Ja sisällöksi laitoin: 
---
- name: Create text file
  copy:
    dest: /home/aleksi2/ansible.txt
    content: |
      Nimeni on aleksi moro!
      Käyn tätä kurssia tällä hetkellä kolmatta viikkoa.
      Ja joo öö joo.
    owner: aleksi2
    group: aleksi2
    mode: "0600"
Eli omistaja on "aleksi2".

Tämän jälkeen lisäsin "filen" site.yml komennolla "nano site.yml" ja laitoin siellä packages alapuolelle "file".
Ajoin komennon "ansible-playbook site.yml --ask-become-pass" ja syötin salasanan.
Tämän jälkeen vielä koitin tarkistaa tiedostoa komennolla "ls -l /home/aleksi2/ansible.txt", mutta koska tiedoston omistaja oli "aleksi2" ei se auennut.
Tämän takia jouduin ajamaan komennon "sudo ls -l /home/aleksi2/ansible.txt" ja tämän jälkeen syötin salasanan ja se toimi.
<img width="1516" height="748" alt="image" src="https://github.com/user-attachments/assets/6cbc0e7f-b961-40b9-aa30-ed094f23ed96" />
Kuvan alalaidassa näkyy -rw-------
Koska käytin mode "0600" on käyttäjällä "aleksi2" nyt oikeudet r (lukea) & w (kirjoittaa) tiedostoa. Eli "aleksi2" on ainoa kuka voi lukea ja muokata tiedostoa. 

## e) osa
Aloitin luomalla roolin "debug" komennolla "mkdir -p roles/debug/tasks"
Sitten kirjoitin jälleen komennon "nano roles/debug/tasks/main.yml"
Ja sinne kirjoitin:
---
- name: Show message
  debug:
    msg: "Ansible toimii!"

Menin "nano site.yml" ja sinne kirjoitin roolien perään - debug
Ajoin terminaalissa jälleen komennon "ansible-playbook site.yml --ask-become-pass".
Ja tässä on lopputulos: <img width="742" height="383" alt="image" src="https://github.com/user-attachments/assets/bd7aea63-50aa-4d1a-9f86-16995f6784af" />
Debugin tehtävä oli näyttää viesti "Ansible toimii" ja se toimi





## Lähteet
Tero Karvinen 2026: Sudo without password: https://terokarvinen.com/passwordless-sudo/ Luettu 10.11.2026
Tero Karvinen 2026: Passwordless Sudo with Ansible: https://terokarvinen.com/passwordless-sudo-with-ansible/ Luettu 10.11.2026
Munroe 2006: xkcd Sandwich: https://xkcd.com/149/ Luettu 10.11.2026
Docs.Ansible.com: ansible.builtin.debug.module : https://docs.ansible.com/ansible/latest/collections/ansible/builtin/debug_module.html luettu 10.11.2026
