# 0010 – Javni obiskovalec in RBAC

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Obiskovalec mora videti ponudbo brez prijave, kupec pa ne sme upravljati naročil drugih kupcev ali spreminjati ponudbe.

## Obravnavane možnosti

- Javni gost brez seje in vloge CUSTOMER, EMPLOYEE, ADMIN
- Enake pravice za vse prijavljene uporabnike
- Podroben sistem pravic za vsako operacijo

## Odločitev in utemeljitev

Uporabil bom tri shranjene vloge in ločeno dovoljenje za javne poti. Express middleware preveri sejo in vlogo, za kupčeva naročila pa še lastništvo.

## Posledice

- **Pozitivne:** Preprost pregled pravic in varovanje dejanj na backendu.
- **Negativne:** Spremembe pravil zahtevajo posodobitev kode in teste; samo skrivanje elementov v Reactu ni dovolj.
