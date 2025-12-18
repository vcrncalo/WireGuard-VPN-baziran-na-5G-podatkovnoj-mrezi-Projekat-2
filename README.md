# Sistemi i servisi mobilnih telekomunikacija
# Projekat 2 : WireGuard VPN baziran na 5G podatkovnoj mreži 

Grupa : Vedad Crnčalo, Harun Dedović, Džejlana Konjalić, Amna Bumbul, Amila Čengić, Emrah Dragolj, Denin Mehanović

Postavka projekta : 

• RP1: Dizajn WireGuard VPN-a baziranog na 5G podatkovnoj mreži, a koji uključuje različite scenarije:  
  (1) jedan WireGuard peer se nalazi unutar, a drugi izvan 5G mreže i  
  (2) oba WireGuard peer-a se nalaze unutar 5G mreže.

• RP2: Implementacija podatkovne usluge u 5G SA mreži korištenjem AMARI Callbox Classic rješenja i 5G modema.

• RP3: Implementacija VPN-a za scenarij (1).

• RP4: Implementacija VPN-a za scenarij (2).

• RP5: Eksperimentalna analiza signalizacijskih tokova za scenarije (1) i (2).

• RP6: Izrada projektne dokumentacije i održavanje GitHub repozitorija.

# Arhitektura sistema
<p align="center">
<img width="1036" height="187" alt="Scenarij1 drawio" src="https://github.com/user-attachments/assets/26bdc36d-c368-482d-abd9-78c74ea138d8" />
<br>
<em>Slika 1: Scenarij 1 </em>
</p>

**Scenarij 1 :** Ovaj dijagram prikazuje komunikaciju između klijenta (UE1) i udaljenog servera (UE2). Klijent je povezan na 5G modem, koji dalje komunicira sa AMARI Callbox uređajem. AMARI Callbox uspostavlja siguran WireGuard tunel preko interneta prema serveru, omogućavajući pouzdanu i zaštićenu razmjenu podataka između krajnjih tačaka, bez obzira na javnu mrežnu infrastrukturu.

<p align="center">
<img width="1161" height="761" alt="Scenarij2 drawio" src="https://github.com/user-attachments/assets/15e0c591-2e8a-42b1-9afa-9b848df29488" />
<br>
<em>Slika 2: Scenarij 2 </em>
</p>

**Scenarij 2 :** Ovaj dijagram prikazuje dvosmjernu, sigurnu komunikaciju između klijenta (UE1) i servera (UE2), gdje su obje krajnje tačke povezane putem 5G modema. Svaka strana uspostavlja WireGuard tunel prema AMARI Callbox uređaju, koji djeluje kao centralna tačka za sigurno rutiranje saobraćaja. Na ovaj način je omogućena pouzdana i enkriptovana razmjena podataka između UE1 i UE2 preko mobilne mreže i interneta, uz izolaciju i zaštitu komunikacije.
