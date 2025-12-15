# Max Cleaning 02 – Web Aplikacion per Larje Tepiha

## Pershkrimi
Max Cleaning 02 eshte web-aplikacion per menaxhimin e porosive te larjes se tepiha,
i ndertuar per perdorim ne Kosove dhe ne gjuhen Shqipe.

## Rolet ne Aplikacion
- Klient (User)
- Admin

## Autentikimi
- Autentikimi behet me numer telefoni
- Nese numri i telefonit ekziston ne databaze si admin,
  llogaria krijohet automatikisht si ADMIN

## Teknologjia
- Backend: PHP
- Database: MySQL
- Server lokal: XAMPP (Apache + MySQL)
- Frontend: HTML, CSS, JavaScript
- SMS: SMS Gateway (njoftime automatike)

# AUTENTIKIMI (Kyçu & Regjistrohu)

## Kyçu (Login)
- Faqja e kyçjes eshte e perbashket per Klient dhe Admin

### Fushat
- Numri i telefonit
- Fjalekalimi
- Butoni Kyçu

### Linke
- Regjistrohu
- Kam harruar fjalekalimin

### Sjellja pas Kyçjes
- Nese numri eshte ADMIN → ridrejtohet te Admin Panel
- Nese numri eshte CLIENT → ridrejtohet te Faqja Kryesore (User)

## Regjistrohu (Register)
- Regjistrimi behet vetem me numer telefoni

### Hapat
- Emri
- Mbiemri
- Numri i telefonit
- Vendos fjalekalimin
- Konfirmo fjalekalimin
- Regjistrohu

- Nese numri eshte ne listen e adminëve ne DB → krijohet si ADMIN
- Perndryshe → krijohet si CLIENT

## Kam harruar fjalekalimin
- Shkruan numrin e telefonit
- Vendos fjalekalimin e ri
- Ruaj dhe kyçu

# PJESA E KLIENTIT (CLIENT)

## Header Klient
- Faqja kryesore
- Forma e porosise
- Qmimore
- Porosite e bera
- Logout

- Nese klienti nuk eshte i kyçur,
  klikimi ne keto faqe e con te Kyçu

## Faqja Kryesore (User)
- Pershkrim i sherbimit
- Lokacionet e biznesit
- Butona per porosi dhe informata

## Forma e Porosise
Klienti krijon porosi duke zgjedhur menyren e dorezimit:
- E sjell vete ne lokacion
- Kompania vjen per marrje ne adrese

### Marrje ne adrese
- Buton Share Location
- Vendndodhja ruhet ne harte per adminin

### Tepihat
- Sasia
- Gjeresia (cm)
- Gjatesia (cm)

### Pas dergimit
- Mesazh ne web:
  "Porosia juaj eshte derguar dhe eshte ende e pa pranuar."
- SMS me te njejtin mesazh dergohet automatikisht

## Qmimore
- Cmimet jane orientuese
- Cmimi final konfirmohet nga admini pas matjes reale

## Porosite e Bera
Klienti sheh:
- Numrin e porosise
- Statusin
- Tepihat (sasia dhe permasat)
- Cmimin final (nese ekziston)

- Cdo perditesim shfaqet ne web
- Cdo perditesim dergohet me SMS

# PJESA E ADMINIT (ADMIN PANEL)

## Header Admin
- Faqja kryesore
- Menaxhim i porosive
- Nisje
- Porosite / Klientet
- Buxheti
- Logout

## Faqja Kryesore (Admin)
Admini sheh:
- Pershendetje personale
- Butona:
  - Menaxhim i porosive
  - Nisje
  - Buxheti
- (Opsionale) Porosi sot

## Menaxhim i Porosive
Admini sheh:
- Emrin e klientit
- Numrin e telefonit
- Lokacionin
- Share Location (harte)
- Sasinë e tepiheve

### Detajet e Porosise
- Tepihat me gjeresi dhe gjatesi
- Mundesi per korrigjim te permasave
- Cmimi llogaritet automatikisht

- Cmimi standard: 0.89 € / m2

### Veprimet
- Prano porosine
- Vendos Gati me / Dorezim me
- Anulo porosine

- Cdo veprim perditeson statusin
- Cdo veprim dergon SMS te klienti

## Nisje (Marrje & Dorezim)
- Admini niset per marrje ose dorezim
- Statusi perditesohet

### SMS
- "Sot do vijme me i marre tepihat."
- "Tepihu vjen sot."

## Porosite / Klientet (Vetem shikim)
- Lista e porosive dhe klienteve
- Renditje nga me e reja
- Shfaq statusin dhe cmimin
- Pa mundesi menaxhimi

## Buxheti
- Llogaritet vetem nga porosite e dorezuara

### Filter
- Sot
- Jave
- Muaj

- Shfaq fitimin bruto

## Statuset e Porosive
- Pa pranuara
- Te pranuara
- Te nisura
- Te dorezuara
- Te anuluara

- Cdo status perditesohet ne web
- Cdo status njoftohet me SMS
