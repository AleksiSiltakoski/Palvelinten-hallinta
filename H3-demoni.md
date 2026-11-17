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
