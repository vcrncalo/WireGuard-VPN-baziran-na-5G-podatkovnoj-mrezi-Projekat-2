# Sistemi i servisi mobilnih telekomunikacija
## Projekat 2 : WireGuard VPN baziran na 5G podatkovnoj mreži 

Grupa : Vedad Crnčalo, Harun Dedović, Džejlana Konjalić, Amna Bumbul, Amila Čengić, Emrah Dragolj, Denin Mehanović

## Postavka projekta : 

• RP1: Dizajn WireGuard VPN-a baziranog na 5G podatkovnoj mreži, a koji uključuje različite scenarije:  
  (1) jedan WireGuard peer se nalazi unutar, a drugi izvan 5G mreže i  
  (2) oba WireGuard peer-a se nalaze unutar 5G mreže.

• RP2: Implementacija podatkovne usluge u 5G SA mreži korištenjem AMARI Callbox Classic rješenja i 5G modema.

• RP3: Implementacija VPN-a za scenarij (1).

• RP4: Implementacija VPN-a za scenarij (2).

• RP5: Eksperimentalna analiza signalizacijskih tokova za scenarije (1) i (2).

• RP6: Izrada projektne dokumentacije i održavanje GitHub repozitorija.

---

## Arhitektura sistema
<p align="center">
<img alt="Scenarij1 drawio" src="Slike/Scenarij1.drawio.png" />
<br>
<em>Slika 1: Scenarij 1 </em>
</p>

**Scenarij 1 :** Ovaj dijagram prikazuje komunikaciju između klijenta (UE1) i udaljenog servera (UE2). Klijent je povezan na 5G modem, koji dalje komunicira sa AMARI Callbox uređajem. AMARI Callbox uspostavlja siguran WireGuard tunel preko interneta prema serveru, omogućavajući pouzdanu i zaštićenu razmjenu podataka između krajnjih tačaka, bez obzira na javnu mrežnu infrastrukturu.

<p align="center">
<img alt="Scenarij2 drawio" src="Slike/Scenarij2.drawio.png" />
<br>
<em>Slika 2: Scenarij 2 </em>
</p>

**Scenarij 2 :** Ovaj dijagram prikazuje dvosmjernu, sigurnu komunikaciju između klijenta (UE1) i servera (UE2), gdje su obje krajnje tačke povezane putem 5G modema. Svaka strana uspostavlja WireGuard tunel prema AMARI Callbox uređaju, koji djeluje kao centralna tačka za sigurno rutiranje saobraćaja. Na ovaj način je omogućena pouzdana i enkriptovana razmjena podataka između UE1 i UE2 preko mobilne mreže i interneta, uz izolaciju i zaštitu komunikacije.

---
## 18.12.2025
Tokom vježbe uspostavljena je 5G SA mreža korištenjem AMARI Callbox Classic sistema i 5G modema. Najprije je ostvaren pristup 5G modemu kako bi se provjerila njegova IP adresa i osnovni status mrežne konekcije.

Nakon toga analizirani su konfiguracijski fajlovi bazne stanice (gNB) u AMARI okruženju. Posebna pažnja posvećena je postavkama vezanim za podatkovni saobraćaj, kao što su mrežni interfejsi, IP adresiranje i način uspostavljanja korisničke podatkovne sesije u 5G SA mreži.

Kroz web interfejs rutera provjerene su i LAN i WiFi postavke, uključujući aktivne mreže, DHCP opseg i status 5G NR-SA veze. Na taj način je potvrđeno da je korisnička oprema uspješno povezana na mrežu i da se podaci pravilno razmjenjuju.
<p align="center">
<img alt="Scenarij1 drawio" src="Slike/Ruter konfiguracija 2.jpg" />
<br>
<em>Slika 3: Postavke rutera </em>
</p>

<p align="center">
<img alt="Scenarij1 drawio" src="Slike/Ruter konfiguracija 1.jpg" />
<br>
<em>Slika 3: Postavke rutera </em>
</p>
---
