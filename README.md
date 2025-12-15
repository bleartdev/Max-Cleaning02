# Max Cleaning 02 – Web Aplikacion për Larje Tepiha

## Përshkrimi
Max Cleaning 02 është web-aplikacion për menaxhimin e porosive të larjes së tepiha,
i ndërtuar për përdorim në Kosovë dhe në gjuhën Shqipe.

Biznesi ka lokacion fizik në **Klinë e Epërme**,
ndërsa shërbimi i **marrjes dhe dorëzimit të tepiheve** ofrohet në:
- **Mitrovicë**
- **Skenderaj**

---

## Rolet në Aplikacion
- Klient
- Admin

---

## Autentikimi
- Autentikimi bëhet me **numër telefoni**
- Nëse numri i telefonit ekziston në databazë si admin,
  llogaria krijohet automatikisht si **ADMIN**
- Fjalëkalimet ruhen të **hash-uara** në databazë (`password_hash`)
- Përdoret **session-based authentication**

---

## Siguria
- Session-based authentication
- Kontroll i aksesit sipas rolit (Klient / Admin)
- Mbrojtje nga qasja direkte në faqet e Adminit (route/guard)
- (Opsionale) CSRF token për format kritike:
  - login
  - register
  - porosi
  - update statusi / çmimi

---

## Teknologjia
- Backend: PHP
- Database: MySQL
- Server lokal: XAMPP (Apache + MySQL)
- Frontend: HTML, CSS, JavaScript
- SMS: SMS Gateway (njoftime automatike)
- Maps: Share Location / Google Maps

---

# AUTENTIKIMI (Kyçu & Regjistrohu)

## Kyçu (Login)
- Faqja e kyçjes është e përbashkët për Klient dhe Admin

### Fushat
- Numri i telefonit
- Fjalëkalimi
- Butoni Kyçu

### Linke
- Regjistrohu
- Kam harruar fjalëkalimin

### Sjellja pas Kyçjes
- Nëse numri është ADMIN → ridrejtohet te **Admin Panel**
- Nëse numri është KLIENT → ridrejtohet te **Faqja Kryesore (Klient)**

---

## Regjistrohu (Register)
- Regjistrimi bëhet vetëm me numër telefoni

### Fushat
- Emri
- Mbiemri
- Numri i telefonit
- Fjalëkalimi
- Konfirmo fjalëkalimin

### Logjika
- Nëse numri ekziston në listën e adminëve → krijohet si **ADMIN**
- Përndryshe → krijohet si **KLIENT**
- Fjalëkalimi ruhet i **hash-uar**

---

## Kam harruar fjalëkalimin
- Shkruan numrin e telefonit
- Vendos fjalëkalimin e ri
- Fjalëkalimi ruhet i hash-uar
- Kyçet automatikisht

---

# PJESA E KLIENTIT (KLIENT)

## Header Klient
- Faqja Kryesore
- Forma e Porosisë
- Qmimore
- Porositë e Mia
- Logout

> Nëse klienti nuk është i kyçur,
> qasja në këto faqe e ridrejton te Kyçu.

---

## Faqja Kryesore (Klient)
- Përshkrim i shërbimit
- Lokacioni i biznesit: **Klinë e Epërme**
- Zonat e shërbimit për marrje dhe dorëzim:
  - Mitrovicë
  - Skenderaj
- Butona për krijim porosie dhe informata

---

## Forma e Porosisë
Klienti krijon porosi duke zgjedhur mënyrën e dorëzimit:
- E sjell vetë në lokacion (**Klinë e Epërme**)
- Kompania vjen për marrje në adresë (**Mitrovicë / Skenderaj**)

### Marrje në adresë
- Klienti zgjedh qytetin:
  - Mitrovicë
  - Skenderaj
- Buton **Share Location**
- Lokacioni ruhet dhe shfaqet në hartë për Adminin

---

### Tepihat
- Sasia e tepiheve
- Për çdo tepih:
  - Gjerësia (cm)
  - Gjatësia (cm)
- Buton: Shto tepih tjetër

---

## Validimi i të Dhënave
- Validim frontend (JavaScript)
- Validim backend (PHP)
- Nuk lejohet:
  - gjerësi/gjatësi 0 ose negative
  - sasi 0
  - qytet jashtë Mitrovicë / Skenderaj (kur zgjedhet marrje në adresë)

---

### Pas dërgimit të porosisë
- Mesazh në web:
  "Porosia juaj është dërguar dhe është ende e pa pranuar."
- SMS automatik me të njëjtin mesazh

---

## Qmimore (Klient)
- Çmimet janë **orientuese**
- Çmimi final konfirmohet nga Admini pas matjes reale

---

## Porositë e Mia
Klienti sheh:
- Numrin e porosisë
- Statusin
- Tepihat (sasia dhe përmasat)
- Çmimin final (nëse ekziston)

- Çdo përditësim shfaqet në web
- Çdo përditësim njoftohet me SMS

---

## Historiku i Porosisë
- Çdo ndryshim statusi ruhet si histori
- Klienti mund të shohë:
  - statusin
  - datën
  - orën

---

## Orari i Punës (Opsionale)
- Porositë jashtë orarit shënohen si "Në pritje"
- Admini i konfirmon ditën tjetër

---

# PJESA E ADMINIT (ADMIN PANEL)

## Header Admin
- Faqja Kryesore
- Menaxhim i Porosive
- Transporti
- Porosi / Klientë
- Qmimore
- Buxheti
- Logout

---

## Faqja Kryesore (Admin)
Admini sheh:
- Përshëndetje personale
- Butona kryesorë:
  - Menaxhim i Porosive
  - Transporti
  - Buxheti
- (Opsionale) Porositë e ditës
- (Opsionale) Njoftime për porosi të reja

---

## Menaxhim i Porosive
Admini sheh:
- Emrin e klientit
- Numrin e telefonit
- Qytetin (Mitrovicë / Skenderaj) ose “E sjell vetë”
- Lokacionin në hartë (Share Location)
- Sasinë e tepiheve

### Detajet e Porosisë
- Tepihat me gjerësi dhe gjatësi
- Mundësi për korrigjim të përmasave reale
- Çmimi llogaritet automatikisht

---

### Veprimet e Adminit
- Prano porosinë
- Vendos statusin (në transport / gati / dorëzuar)
- Anulo porosinë

- Çdo veprim:
  - përditëson statusin në web
  - dërgon SMS te klienti

---

## Qmimore (Admin)
- Admini menaxhon çmimin për metër katror (€/m²)
- Çmimi mund të ndryshohet në çdo kohë

### Shembull
- Çmimi aktual: 0.89 € / m²
- Në të ardhmen mund të bëhet: 1.20 € / m²
- Çdo porosi llogaritet sipas çmimit aktiv në momentin e konfirmimit

---

## Transporti (Marrje & Dorëzim)
- Transporti realizohet vetëm në:
  - Mitrovicë
  - Skenderaj
- Admini shënon nisjen për marrje ose dorëzim
- Statusi i porosisë përditësohet

### SMS automatike
- "Sot do vijmë për marrjen e tepiheve në Mitrovicë / Skenderaj."
- "Tepihat do të dorëzohen sot."

---

## Porosi / Klientë (Vetëm shikim)
- Lista e të gjitha porosive dhe klientëve
- Renditje nga më e reja
- Shfaq statusin dhe çmimin
- Pa mundësi menaxhimi

---

## Buxheti
- Llogaritet vetëm nga porositë e **dorëzuara**

### Filtra
- Sot
- Javë
- Muaj

- Shfaq fitimin bruto

---

## Raporte (Opsionale)
- Eksport i porosive në:
  - PDF
  - Excel
- Raport mujor i fitimit

---

## Audit Log (Admin)
- Regjistrohen veprimet e Adminit:
  - pranim porosie
  - ndryshim çmimi (€/m²)
  - anulim porosie
  - dorëzim porosie
- Çdo veprim ruhet me datë dhe orë

---

## Fshirje Logjike (Soft Delete)
- Porositë nuk fshihen fizikisht nga databaza
- Shënohen si:
  - të anuluara
  - të arkivuara (opsionale)

---

## Backup
- Backup i databazës rekomandohet rregullisht
- (Opsionale) Backup automatik ditor/javor

---

## Statuset e Porosive
- Të pa pranuara
- Të pranuara
- Në transport
- Të dorëzuara
- Të anuluara

- Çdo status përditësohet në web
- Çdo status njoftohet me SMS
