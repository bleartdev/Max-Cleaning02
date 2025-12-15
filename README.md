# Max Cleaning 02 – Web Aplikacion për Larje Tepiha

## Përshkrimi
Max Cleaning 02 është web-aplikacion për menaxhimin e porosive të larjes së tepiha,
i ndërtuar për përdorim në Kosovë dhe në gjuhën Shqipe.

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
- Lokacionet e biznesit
- Butona për krijim porosie dhe informata

---

## Forma e Porosisë
Klienti krijon porosi duke zgjedhur mënyrën e dorëzimit:
- E sjell vetë në lokacion
- Kompania vjen për marrje në adresë

### Marrje në adresë
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

---

## Menaxhim i Porosive
Admini sheh:
- Emrin e klientit
- Numrin e telefonit
- Lokacionin
- Share Location (hartë)
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
- Admini shënon nisjen për marrje ose dorëzim
- Statusi i porosisë përditësohet

### SMS automatike
- "Sot do vijmë për marrjen e tepiheve."
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

## Statuset e Porosive
- Të pa pranuara
- Të pranuara
- Në transport
- Të dorëzuara
- Të anuluara

- Çdo status përditësohet në web
- Çdo status njoftohet me SMS
