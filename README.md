# InkTime Smartwatch - Hardware Design

Acest repository contine fisierele de design hardware pentru proiectul InkTime, un smartwatch open-source. Sunt incluse fisierele pentru etapele EVT si DVT, schemele electrice, PCB-ul, fisierele de fabricatie si modelul mecanic.

## Specificatii si Functionalitate Hardware
Platforma este construita in jurul microcontroller-ului Nordic nRF52840.

* Microcontroller: nRF52840 gestioneaza logica principala si comunicatia Bluetooth.
* Alimentare: Baterie LiPo de 3.7V (model AKY0106). Bateria este lipita direct pe pad-urile placii pentru a economisi spatiu, renuntandu-se la conectorul JST. Incarcarea se face prin portul USB-C. Tensiunea sistemului este coborata la 3.3V folosind un convertor DC/DC.
* Interfata utilizator: Ecran E-Paper conectat prin SPI (consum redus de energie), 3 butoane fizice pentru navigare si un motor de vibratii (shaker DC) pentru feedback haptic.
* Senzori: Modul IMU conectat prin I2C pentru detectarea miscarii.

## Mapare Pini nRF52840
Tabelul de mai jos detaliaza pinii folositi pentru fiecare componenta:

| Pin nRF52840 | Functie | Componenta Conectata | Rol |
| :--- | :--- | :--- | :--- |
| [Completati pinul] | I2C SDA | IMU | Date senzor miscare |
| [Completati pinul] | I2C SCL | IMU | Clock senzor miscare |
| [Completati pinul] | SPI MOSI | Ecran E-Paper | Date catre display |
| [Completati pinul] | SPI SCK | Ecran E-Paper | Clock display |
| [Completati pinul] | GPIO | Buton SW1 | Intrerupere meniu (Sus) |
| [Completati pinul] | GPIO | Buton SW2 | Intrerupere meniu (Selectie) |
| [Completati pinul] | GPIO | Buton SW3 | Intrerupere meniu (Jos) |
| [Completati pinul] | PWM | Shaker | Control vibratii |

## Bill of Materials (BOM)
Lista principalelor componente folosite in proiect:

| Referinta | Componenta | Capsula |
| :--- | :--- | :--- |
| U1 | nRF52840 | AQFN73 |
| B1 | Baterie LiPo AKY0106 | Custom |
| M1 | Shaker DF-FIT0774 | Custom |
| DISP | Ecran E-Paper WSH-12561 | Custom |
| R, C | Pasive standard | 0201 / 0402 |

## Design Log si Compromisuri
Urmatoarele decizii au fost luate in procesul de proiectare pentru a respecta constrangerile mecanice si electrice:

* Grosimea placii: PCB-ul a fost proiectat cu o grosime de 1 mm pentru a respecta dimensiunile carcasei. Toate componentele sunt amplasate pe layer-ul TOP.
* Design antena: Antena a fost plasata pe marginea exterioara. Zona de sub antena a fost decupata, fara trasee sau plan de masa, pentru a asigura transmisia radio. A fost adaugat via-stitching intre planurile de masa in zona circuitului radio.
* Reguli de rutare: Traseele de alimentare au latimea de 0.3 mm, iar cele de date de minim 0.15 mm. Condensatoarele de decuplare de 100nF au fost amplasate cat mai aproape de pinii de alimentare.
* Erori asumate: Erorile de "Dimension" semnalate de DRC pentru cele 3 butoane si mufa USB au fost ignorate intentionat, deoarece amplasarea lor a fost dictata de alinierea mecanica cu decupajele carcasei. Eroarea "Only INPUT pins on NET ID" a fost de asemenea ignorata, fiind un comportament acceptat.
