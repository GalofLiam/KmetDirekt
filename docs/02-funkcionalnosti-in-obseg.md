# Funkcionalnosti in obseg – KmetDirekt

## Uporabniške vloge

| Vloga | Kaj lahko počne | Omejitve |
|---|---|---|
| **Neprijavljen obiskovalec** | Brez prijave pregleduje javno ponudbo, kategorije, cene in prikaz proste zaloge. | Ne oddaja naročil, ne vidi naročil drugih in ne dostopa do administracije. |
| **Kupec** | Pregleduje ponudbo, odda naročilo, vidi svoja naročila in jih pred začetkom priprave lahko prekliče. | Ne vidi naročil drugih kupcev in ne spreminja cen, zalog ali statusov priprave. |
| **Zaposleni** | Pregleduje prispela naročila, jih potrdi ali zavrne, določi termin prevzema ter označi pripravo in prevzem. | Ne ureja cen in uporabniških računov ter ne spreminja zaloge ročno. |
| **Lastnik (administrator)** | Ima pregled nad naročili, upravlja ponudbo, zalogo, cene in uporabniške račune. | Ne more poljubno popravljati zgodovine zaključenih naročil. |

Neprijavljen obiskovalec ni četrta shranjena vloga v bazi: pomeni zahtevo brez veljavne prijavljene seje. V tabeli `users` ostanejo tri vloge (`CUSTOMER`, `EMPLOYEE`, `ADMIN`). Backend bo preverjal prijavo, vlogo in po potrebi lastništvo naročila. Skrivanje gumbov na spletni strani ni varnostni ukrep. Za MVP bodo uporabniški računi in izdelki pripravljeni vnaprej, brez javne registracije in administrativnih obrazcev.

## Predvidene funkcionalnosti

Prvih sedem funkcionalnosti predstavlja **MVP**, torej prvo delujočo različico. Pri naročilih je poudarek na preverjanju in izvajanju pravil, ne samo na shranjevanju podatkov.

| # | Funkcionalnost | Opis | MVP |
|---|---|---|---|
| 1 | Oddaja naročila | Kupec izbere več vrst paketov in količine. Sistem preveri pozitivne cele količine, na backendu izračuna skupno ceno iz veljavnega cenika in ob oddaji shrani tudi ceno vsake postavke, da poznejša sprememba cenika ne spremeni naročila. | **MVP** |
| 2 | Preverjanje in rezervacija zaloge | Sistem ob oddaji naročila preveri prosto zalogo vseh naročenih izdelkov ter v isti podatkovni transakciji rezervira količine in ustvari naročilo. Če katerikoli izdelek ni na voljo, naročilo ni ustvarjeno. | **MVP** |
| 3 | Potrditev ali zavrnitev naročila | Zaposleni pregleda novo naročilo, ga potrdi in določi predviden termin prevzema ali ga zavrne. Ob zavrnitvi se rezervirane količine sprostijo. | **MVP** |
| 4 | Priprava naročila za prevzem | Zaposleni pri potrjenem naročilu vidi seznam izdelkov in količin, preveri pripravljene pakete ter označi naročilo kot `PRIPRAVLJENO`. Ne more pripraviti zavrnjenega, preklicanega ali že prevzetega naročila. | **MVP** |
| 5 | Evidentiranje osebnega prevzema | Zaposleni lahko naročilo označi kot `PREVZETO` samo, če je že `PRIPRAVLJENO`. Sistem zaključi naročilo in rezervirane količine dokončno evidentira kot porabljeno fizično zalogo, brez dvojnega odštevanja. | **MVP** |
| 6 | Preklic naročila | Kupec lahko prekliče svoje naročilo v stanju `ODDANO` ali `POTRJENO`, ne pa po označitvi priprave. Sistem sprosti rezervirane količine natanko enkrat. | **MVP** |
| 7 | Prijava in preverjanje pravic | Neprijavljen obiskovalec vidi javno ponudbo, za oddajo naročila pa je potrebna prijava. Backend s strežniško sejo preverja uporabniško vlogo in lastništvo naročila. | **MVP** |
| 8 | Podrobnejši pregled zalog | Ločen prikaz fizične, rezervirane in proste zaloge po izdelkih. | Ne |
| 9 | Upravljanje ponudbe | Lastnik dodaja in spreminja mesne pakete, cene in aktivnost ponudbe. | Ne |
| 10 | Izbira termina prevzema | Zaposleni pripravi seznam terminov, kupec pa izbere enega od njih. | Ne |
| 11 | Zgodovina naročil | Kupec vidi pretekla naročila, zaposleni pa tista, ki jih je obravnaval. | Ne |
| 12 | Statistika prodaje | Lastnik preveri, koliko paketov je bilo prevzetih in kateri izdelki so bili najbolj naročani. | Ne |
| 13 | Ročni popravki zaloge | Lastnik ob popravku zaloge vnese tudi razlog spremembe. | Ne |

Za MVP bo v podatkovni bazi že nekaj testnih izdelkov in uporabnikov vseh treh vlog. Zato lahko aplikacija deluje tudi brez administrativnih obrazcev, ki jih načrtujem za pozneje.

## Potek naročila v MVP

1. Obiskovalec lahko najprej pregleda ponudbo brez prijave. Za oddajo naročila se prijavi in izbere pakete.
2. Backend preveri količine, izračuna ceno ter v eni podatkovni transakciji shrani naročilo in rezervira pakete.
3. Zaposleni naročilo potrdi ali zavrne. Če ga zavrne, se rezervacija sprosti.
4. Ob potrditvi določi predviden termin prevzema. Pri pripravi zaposleni preveri seznam paketov in naročilo označi kot `PRIPRAVLJENO`. Ob izročitvi izdelkov evidentira stanje `PREVZETO`.
5. Kupec lahko naročilo do začetka priprave prekliče. Sistem mora paziti, da se rezervacija ne sprosti dvakrat.

Stanja `PREVZETO`, `ZAVRNJENO` in `PREKLICANO` so končna. Ob prevzemu se rezervirani paketi dokončno odštejejo od fizične zaloge.

## Možne nadgradnje

- E-poštna obvestila o spremembah statusa.
- Spletno plačevanje.
- Dostava na naslov kupca.
- Povezava z računovodskim sistemom.
- Napovedovanje povpraševanja po mesnih paketih.
- Podrobnejša poročila in izvoz podatkov.

## Izven obsega

- Reja, zakol, razsek ali predelava mesa.
- Spletna plačila in vračila denarja.
- Organizacija dostave in hladne verige.
- Namenska aplikacija za Android ali iOS.
- Prodaja več različnih kmetij na skupni platformi.
- Nadomeščanje zakonsko predpisanih evidenc ali integracija z davčno blagajno.
