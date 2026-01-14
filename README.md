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
## Konfiguracija rutera
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
<em>Slika 4: Postavke rutera </em>
</p>

## PLMN Managment
**PLMN Management :** omogućava upravljanje povezivanjem uređaja na mobilne mreže. Uređaj može automatski birati dostupnu mrežu ili omogućiti ručni odabir operatera.

  PLMN Auto Selection – automatski ili ručni izbor mreže

  Scan – pretraga dostupnih mobilnih mreža

  Available – mreža je dostupna za povezivanje

  Forbidden – mreža nije dozvoljena za trenutnu SIM karticu

  Type – tehnologija mreže (NR5G, LTE, UMTS)

  PLMN – jedinstveni identifikator mobilne mreže

Odabrana mreža se potvrđuje klikom na Apply, dok Cancel poništava izmjene.
<p align="center">
<img alt="Scenarij1 drawio" src="Slike/Ruter konfiguracija 3.png" />
<br>
<em>Slika 5: Postavke rutera </em>
</p>

---
## Konfiguracija WireGuard tunela 
# WireGuard manual setup (wg70)

Ovaj dio pokazuje **ručno kreiranje WireGuard tunela** na Linuxu,
korak-po-korak, koristeći interfejs `wg70`.

> Napomena: Ovo je edukativni / testni setup.  
> Za produkciju se preporučuje `/etc/wireguard/wg70.conf`.

---

## 1. Instalacija WireGuard-a

```bash
sudo apt update
sudo apt install wireguard
```
## 2. Generisanje privatnog ključa (ili ključeva)
```bash
wg genkey > private
chmod 600 private
```
Generiše se privatni ključ koji identifikuje WireGuard interfejs.
Permisije se ograničavaju radi sigurnosti.

## 3. Kreiranje WireGuard interfejsa
```bash
sudo ip link add wg70 type wireguard
```
Kreira se virtualni mrežni interfejs tipa WireGuard sa imenom wg70.

## 4. Dodjela IP adrese interfejsu
```bash
sudo ip addr add 100.100.129.70/16 dev wg70
```
Dodjeljuje se interna VPN IP adresa interfejsu, ova adresa se koristi unutar WireGuard mreže.

## 5. Postavljanje privatnog ključa na interfejs
```bash
sudo wg set wg70 private-key ./private
```
WireGuard interfejs dobija privatni ključ koji se koristi za autentikaciju i kriptografiju.

## 6. Podizanje (aktivacija) interfejsa
```bash
sudo ip link set wg70 up
```
Interfejs se aktivira i postaje spreman za komunikaciju.

## 7. Provjera WireGuard statusa
```bash
sudo wg
interface: wg70
  public key: LgfO7g2vT/yN2QcyuDV8WUBRXTj2rB/sBvK0dvo1vFA=
  private key: (hidden)
  listening port: 58713
```
Prikazuje informacije o WireGuard interfejsu, uključujući public key i listening port.

<p align="center">
<img alt="WireGuard tunel" src="Slike/WireGuard kreiranje.png" />
<br>
<em>Slika 6: WireGuard tunel  </em>
</p>

<p align="center">
<img alt="WireGuard tunel" src="Slike/WireGuard tunel.png" />
<br>
<em>Slika 7: WireGuard .conf fajl  </em>
</p>

Ova slika prikazuje aktivni WireGuard klijentski tunel koji je uspješno importovan iz konfiguracionog *.conf* fajla i pokrenut na Windows uređaju, naziv interfejsa odgovara imenu konfiguracionog fajla, dok su VPN IP adresa i DNS server definisani unutar *[Interface-a]* tog fajla.
Prikazani public key predstavlja jedinstveni identitet klijenta i mora biti dodat na WireGuard server kao odgovarajući peer kako bi komunikacija bila omogućena.
Jednom kreiran, ovaj *.conf* fajl može se sigurno distribuirati i koristiti na drugim uređajima i operativnim sistemima (Windows, Linux, macOS, mobilni), bez dodatnih izmjena.

<p align="center">
<img alt="Ping test" src="Slike/Provjera WireGuard tunela.png" />
<br>
<em>Slika 7: ICMP provjera  </em>
</p>

Pinganje služi za provjeru da li je tunel aktivan i da li postoji mrežna povezanost između dva kraja. Slanjem ping paketa na IP adresu tunela provjerava se da li druga strana odgovara, što znači da je tunel ispravno uspostavljen. Ako se dobije odgovor (reply), tunel radi; ako nema odgovora, postoji problem u konfiguraciji ili mrežnoj vezi.











---




























