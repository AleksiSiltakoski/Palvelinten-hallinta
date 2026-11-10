# H1 Voileipä

## Tiivistykset kappaleista
- Sudo käyttäjä luodaan komennolla "sudo adduser"


## a) osa
Menin terminaalissa ansible kansiooni komennolla "cd ansible/"
Siellä loin uuden käyttäjän komennolla "sudo adduser aleksi2"
Tein myös "sudoless" ryhmän komennolla "sudo groupadd sudoless"
lisäsin aleksi 2 sinne komennolla "sudo adduser aleksi2 sudoless".
Tämän jälkeen avasin uuden terminaali ikkunan ja kirjoitin sinne komennon "sudo -i" ja olin roottina sisällä.
Tämän jälkeen menin takaisin aiempaan terminaaliin, jossa olin kirjautuneena vielä sudona ja kirjoitin komennon "sudo visudo /etc/sudoers.d/sudoless" ja sinne lisäsin rivin tekstiä: "%sudoless ALL = (ALL) NOPASSWD: ALL"
Tämä lisäsi sudoers säännön, missä kaikki sudoless ryhmän käyttjät voivat käyttää sudoa ilman salasanaa.
![sudo](sudo.png)


## Lähteet
Tero Karvinen 2026: Sudo without password: https://terokarvinen.com/passwordless-sudo/ Luettu 10.11.2026
Tero Karvinen 2026: Passwordless Sudo with Ansible: https://terokarvinen.com/passwordless-sudo-with-ansible/ Luettu 10.11.2026
Munroe 2006: xkcd Sandwich: https://xkcd.com/149/ Luettu 10.11.2026
