# Uporabniške zgodbe – KmetDirekt

Pri drugi nalogi sem iz funkcionalnosti KmetDirekt pripravil uporabniške zgodbe. Upošteval sem tudi popravek iz prve naloge: izračun cene je del oddaje naročila, priprava in prevzem pa sta ločeni funkcionalnosti.

V prvi nalogi je 13 funkcionalnosti, tukaj pa 15 zgodb. Javni pregled ponudbe in prijavo sem opisal posebej, prav tako dodajanje in spreminjanje izdelkov. Sedem funkcionalnosti spada v MVP, preostale so načrtovane za pozneje.

## Osnovna pravila

- KmetDirekt je namenjen eni kmetiji. Izdelke prodaja v paketih, količine so cela števila. Plačila prek spleta in dostave za zdaj ne bo.
- Naročilo gre običajno skozi stanja `ODDANO → POTRJENO → PRIPRAVLJENO → PREVZETO`. Zaposleni lahko novo naročilo tudi zavrne, kupec pa ga lahko pred začetkom priprave prekliče.
- Prosto zalogo dobimo tako, da od fizične zaloge odštejemo že rezervirane pakete. Ob oddaji naročila se količina rezervira; ob preklicu ali zavrnitvi se sprosti. Ob prevzemu se odšteje še od fizične zaloge.
- Ponudbo lahko vidi tudi neprijavljen obiskovalec. Prijavljeni uporabniki imajo eno od treh vlog: kupec, zaposleni ali lastnik.
- Za zdaj predvidevam, da zaposleni ob potrditvi določi termin prevzema, med pripravo preveri vse postavke in ob prevzemu izroči celotno naročilo. To so predpostavke projekta, ne potrjena pravila dejanske kmetije.

Pogoje sprejema sem zapisal tako, da jih je mogoče preveriti s konkretnim primerom. Pri tem sem se oprl na predavanje o uporabniških zgodbah, predvsem na opozorilo, da nejasna poslovna pravila hitro vodijo do različnih razlag.

## Povezava z nalogo 1

| Zgodba | Funkcionalnost | Faza |
|---|---|---|
| US-01 – Oddaja naročila | F01 | MVP |
| US-02 – Preverjanje in rezervacija zaloge | F02 | MVP |
| US-03 – Potrditev ali zavrnitev | F03 | MVP |
| US-04 – Priprava naročila | F04 | MVP |
| US-05 – Evidentiranje prevzema | F05 | MVP |
| US-06 – Preklic naročila | F06 | MVP |
| US-07 – Javni pregled ponudbe | F07 | MVP |
| US-08 – Prijava in omejitev dostopa | F07 | MVP |
| US-09 – Pregled zalog | F08 | Kasneje |
| US-10 – Dodajanje paketa v ponudbo | F09 | Kasneje |
| US-11 – Sprememba ali umik ponudbe | F09 | Kasneje |
| US-12 – Izbira termina prevzema | F10 | Kasneje |
| US-13 – Zgodovina naročil | F11 | Kasneje |
| US-14 – Statistika prodaje | F12 | Kasneje |
| US-15 – Ročni popravek zaloge | F13 | Kasneje |

## Uporabniške zgodbe

### US-01 – Oddaja naročila

- **Funkcionalnost:** F01 (MVP)
- **Vloga:** Kupec
- **Zgodba:** Kot kupec želim oddati naročilo z več mesnimi paketi, da lahko izdelke prevzamem v enem obisku.
- **Pogoji sprejema:**
  1. Ko prijavljen kupec odda naročilo z vsaj eno postavko in pozitivnimi celoštevilskimi količinami, sistem mora ustvariti naročilo s statusom `ODDANO` ter postavke naročila.
  2. Če je naročilo prazno ali vsebuje količino 0, negativno ali necelo vrednost, sistem mora oddajo zavrniti in ne sme ustvariti naročila.
  3. Ko kupec oddaja naročilo, backend mora iz veljavnih cen izdelkov izračunati skupno vrednost in shraniti ceno posamezne postavke ob oddaji.
  4. Ko se po oddaji spremeni trenutna cena izdelka, mora že shranjena cena postavke in skupna vrednost obstoječega naročila ostati nespremenjena.
  5. Pred oddajo lahko kupec spremeni količino posamezne postavke ali jo odstrani; povzetek nato pokaže posodobljeno vrednost.

### US-02 – Preverjanje in rezervacija zaloge

- **Funkcionalnost:** F02 (MVP)
- **Vloga:** Kupec
- **Zgodba:** Kot kupec želim naročiti samo razpoložljive pakete, da moje naročilo ne rezervira več izdelkov, kot jih ima kmetija.
- **Pogoji sprejema:**
  1. Ko kupec odda naročilo, sistem mora preveriti prosto količino vseh izbranih izdelkov (`fizična − rezervirana`).
  2. Če prosta količina kateregakoli izdelka ne zadošča, sistem mora zavrniti celotno naročilo in ne sme spremeniti nobene rezervacije.
  3. Ko je zaloge dovolj, sistem mora v eni transakciji ustvariti naročilo in rezervirati količine vseh njegovih postavk.
  4. Če dva kupca hkrati zahtevata zadnji razpoložljivi paket, mora uspeti največ eno naročilo; prosta zaloga ne sme postati negativna.
  5. Ko naročilo zaradi premajhne zaloge ni sprejeto, kupec vidi obvestilo, katera postavka nima dovolj prostih paketov.

### US-03 – Potrditev ali zavrnitev

- **Funkcionalnost:** F03 (MVP)
- **Vloga:** Zaposleni
- **Zgodba:** Kot zaposleni želim pregledati novo naročilo ter ga potrditi ali zavrniti, da lahko kmetija načrtuje pripravo.
- **Pogoji sprejema:**
  1. Ko zaposleni odpre naročilo s statusom `ODDANO`, sistem mora prikazati njegove postavke, količine in skupno vrednost.
  2. Ko zaposleni potrdi naročilo ter vnese predviden termin prevzema, sistem mora status spremeniti v `POTRJENO` in shraniti termin.
  3. Če termin ni veljaven prihodnji datum in ura, sistem mora potrditev zavrniti in status mora ostati `ODDANO`.
  4. Ko zaposleni zavrne naročilo s statusom `ODDANO`, sistem mora nastaviti `ZAVRNJENO` in natanko enkrat sprostiti njegove rezervirane količine.
  5. Če je naročilo že `POTRJENO`, `ZAVRNJENO` ali v poznejšem stanju, sistem mora ponovljeno odločitev zavrniti brez spremembe zaloge.

### US-04 – Priprava naročila

- **Funkcionalnost:** F04 (MVP)
- **Vloga:** Zaposleni
- **Zgodba:** Kot zaposleni želim preveriti pakete potrjenega naročila in označiti zaključeno pripravo, da je jasno, kaj je pripravljeno za prevzem.
- **Pogoji sprejema:**
  1. Ko zaposleni odpre `POTRJENO` naročilo, sistem mora prikazati kontrolni seznam postavk z nazivi in količinami.
  2. Dokler niso vse postavke označene kot preverjene, mora biti zaključek priprave onemogočen.
  3. Ko zaposleni označi vse postavke in potrdi pripravo, sistem mora status spremeniti iz `POTRJENO` v `PRIPRAVLJENO`.
  4. Če naročilo nima statusa `POTRJENO`, sistem mora poskus priprave zavrniti in ne sme spremeniti zaloge.

### US-05 – Evidentiranje prevzema

- **Funkcionalnost:** F05 (MVP)
- **Vloga:** Zaposleni
- **Zgodba:** Kot zaposleni želim evidentirati izročitev pripravljenega naročila, da so prevzemi in fizična zaloga pravilno zaključeni.
- **Pogoji sprejema:**
  1. Ko zaposleni potrdi izročitev naročila s statusom `PRIPRAVLJENO`, sistem mora nastaviti status `PREVZETO`.
  2. Ob prehodu v `PREVZETO` sistem mora v eni transakciji zmanjšati fizično in rezervirano zalogo za količine postavk; prosta zaloga zato ostane nespremenjena.
  3. Če naročilo ni v statusu `PRIPRAVLJENO`, sistem mora poskus prevzema zavrniti brez sprememb.
  4. Če zaposleni ponovi zahtevo za že prevzeto naročilo, sistem ne sme še enkrat zmanjšati zaloge.

### US-06 – Preklic naročila

- **Funkcionalnost:** F06 (MVP)
- **Vloga:** Kupec
- **Zgodba:** Kot kupec želim pravočasno preklicati lastno naročilo, da ne zasedam zaloge, ki je ne bom prevzel.
- **Pogoji sprejema:**
  1. Ko kupec zahteva preklic lastnega naročila s statusom `ODDANO` ali `POTRJENO`, sistem mora nastaviti `PREKLICANO` in sprostiti vse njegove rezervacije.
  2. Če kupec zahteva preklic tujega naročila, sistem mora zavrniti dostop brez spremembe naročila.
  3. Če je naročilo `PRIPRAVLJENO`, `PREVZETO`, `ZAVRNJENO` ali že `PREKLICANO`, sistem mora nov preklic zavrniti brez spremembe zaloge.
  4. Ponovljen preklic ne sme drugič povečati proste zaloge.

### US-07 – Javni pregled ponudbe

- **Funkcionalnost:** F07 (MVP)
- **Vloga:** Neprijavljen obiskovalec
- **Zgodba:** Kot neprijavljen obiskovalec želim pregledati razpoložljive mesne pakete, da vidim ponudbo pred prijavo.
- **Pogoji sprejema:**
  1. Brez prijave sistem mora prikazati aktivne izdelke z imenom, ceno, kategorijo in prosto količino paketov.
  2. Neaktivni izdelki ne smejo biti vključeni v javni seznam.
  3. Ko neprijavljen obiskovalec poskusi oddati naročilo, backend mora vrniti HTTP `401` in ne sme ustvariti naročila.
  4. Če ni aktivnih izdelkov, sistem mora prikazati jasno sporočilo, da trenutno ni ponudbe.
  5. Če je prosta zaloga izdelka enaka nič, sistem to prikaže in onemogoči njegovo dodajanje v košarico.

### US-08 – Prijava in omejitev dostopa

- **Funkcionalnost:** F07 (MVP)
- **Vloga:** Kupec
- **Zgodba:** Kot kupec želim varno uporabljati svoj račun, da lahko naročam in vidim le lastne podatke.
- **Pogoji sprejema:**
  1. Ko uporabnik vnese pravilna prijavna podatka, backend mora preveriti geslo in ustvariti strežniško sejo.
  2. Če so prijavni podatki napačni, sistem mora prijavo zavrniti s splošnim sporočilom brez razkritja, kateri podatek je napačen.
  3. Za zaščiteno pot brez veljavne seje backend mora vrniti `401`, za prijavljenega uporabnika brez zahtevane vloge pa `403`.
  4. Ko kupec zahteva tuje naročilo, backend mora zavrniti vpogled tudi ob poznavanju ID-ja naročila.

### US-09 – Pregled zalog

- **Funkcionalnost:** F08 (Kasneje)
- **Vloga:** Lastnik
- **Zgodba:** Kot lastnik želim videti fizično, rezervirano in prosto količino vsakega paketa, da lahko ocenim razpoložljivo ponudbo.
- **Pogoji sprejema:**
  1. Sistem mora za vsak izdelek prikazati fizično, rezervirano in prosto količino.
  2. Prosta količina mora biti enaka fizični minus rezervirana in ne sme biti negativna.
  3. Pregled mora biti omejen na vlogo `ADMIN`.

### US-10 – Dodajanje paketa v ponudbo

- **Funkcionalnost:** F09 (Kasneje)
- **Vloga:** Lastnik
- **Zgodba:** Kot lastnik želim dodati nov mesni paket v ponudbo, da ga lahko kupci naročajo.
- **Pogoji sprejema:**
  1. Ko lastnik vnese ime, obstoječo kategorijo, nenegativno ceno in nenegativno količino, sistem mora ustvariti izdelek.
  2. Če manjka ime, kategorija ne obstaja ali je cena oziroma zaloga negativna, sistem mora zavrniti zapis.
  3. Ko je ustvarjeni izdelek aktiven, mora biti prikazan v javni ponudbi.
  4. Uporabnik brez vloge `ADMIN` ne sme dodajati izdelkov.

### US-11 – Sprememba ali umik ponudbe

- **Funkcionalnost:** F09 (Kasneje)
- **Vloga:** Lastnik
- **Zgodba:** Kot lastnik želim spremeniti ceno ali umakniti paket iz ponudbe, da javna ponudba ustreza dejanskemu stanju.
- **Pogoji sprejema:**
  1. Ko lastnik spremeni ceno izdelka v nenegativno vrednost, sistem mora shraniti novo ceno za prihodnja naročila.
  2. Sprememba trenutne cene ne sme spremeniti shranjenih cen v postavkah oddanih naročil.
  3. Ko lastnik deaktivira izdelek, mora ta izginiti iz javne ponudbe in ga ni več mogoče dodati v novo naročilo.
  4. Deaktiviranje izdelka ne sme izbrisati postavk že obstoječih naročil.

### US-12 – Izbira termina prevzema

- **Funkcionalnost:** F10 (Kasneje)
- **Vloga:** Kupec
- **Zgodba:** Kot kupec želim izbrati razpoložljiv termin za prevzem, da lahko svoj obisk kmetije načrtujem vnaprej.
- **Pogoji sprejema:**
  1. Sistem mora prikazati samo prihodnje termine, ki jih je objavil zaposleni.
  2. Ko kupec izbere še razpoložljiv termin za svoje potrjeno naročilo, sistem mora izbiro shraniti in jo prikazati v podrobnostih naročila.
  3. Če izbrani termin ni več na voljo, sistem mora izbiro zavrniti in zahtevati novo izbiro.
  4. Izbira termina za tuje naročilo ne sme biti dovoljena.

### US-13 – Zgodovina naročil

- **Funkcionalnost:** F11 (Kasneje)
- **Vloga:** Kupec
- **Zgodba:** Kot kupec želim pregledati svoja prejšnja naročila, da lahko preverim, kaj sem naročil in prevzel.
- **Pogoji sprejema:**
  1. Seznam mora vsebovati samo naročila prijavljenega kupca.
  2. Za vsako naročilo sistem mora prikazati datum oddaje, skupno vrednost in status.
  3. Ko kupec odpre posamezno lastno naročilo, sistem mora prikazati postavke in njihove količine.
  4. Če kupec zahteva tuje naročilo, sistem mora zavrniti dostop.

### US-14 – Statistika prodaje

- **Funkcionalnost:** F12 (Kasneje)
- **Vloga:** Lastnik
- **Zgodba:** Kot lastnik želim preveriti količine dejansko prevzetih paketov, da vidim, po katerih izdelkih je največ povpraševanja.
- **Pogoji sprejema:**
  1. Statistika mora za izbrano obdobje šteti samo naročila s statusom `PREVZETO`.
  2. Za vsak izdelek mora prikazati vsoto količin prevzetih postavk.
  3. Zavrnjena in preklicana naročila ne smejo povečevati količin prevzete prodaje.
  4. Pregled mora biti dostopen samo vlogi `ADMIN`.

### US-15 – Ročni popravek zaloge

- **Funkcionalnost:** F13 (Kasneje)
- **Vloga:** Lastnik
- **Zgodba:** Kot lastnik želim popraviti fizično zalogo z obrazložitvijo, da lahko evidentiram odstopanja pri štetju paketov.
- **Pogoji sprejema:**
  1. Popravek mora zahtevati novo celoštevilsko nenegativno količino in neprazen razlog.
  2. Če bi bila nova fizična zaloga manjša od rezervirane, sistem mora popravek zavrniti.
  3. Ko je popravek uspešen, sistem mora shraniti novo zalogo, razlog in čas spremembe.
  4. Popravek mora biti dovoljen samo vlogi `ADMIN`.

## Kaj še ni določeno

Pri MVP ne načrtujem javne registracije, spletnega plačevanja, dostave ali samostojne izbire termina prevzema. Izdelki in testni računi bodo za začetek že vneseni.

Pred izvedbo bi bilo treba razjasniti še nekaj stvari:

- Ali mora zaposleni pri potrditvi vedno določiti termin prevzema in ali lahko izbira samo med določenimi urami?
- Ali mora pri pripravi označiti vsako postavko posebej?
- Ali kmetija dovoljuje delni prevzem naročila? Trenutno je predviden samo prevzem vseh paketov skupaj.

Ta vprašanja sem pustil zapisana, ker bi drugačni odgovori vplivali na obnašanje aplikacije. Tudi na predavanju *USERSTORY.MD – Ena zahteva, dva bralca* je bilo poudarjeno, da je bolje jasno pokazati odprto vprašanje, kot pa neopazno ugibati.
