# 0007 – PostgreSQL

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Uporabniki, naročila, postavke in izdelki so povezani. Ob naročilu moram dosledno spremeniti več tabel in zalogo.

## Obravnavane možnosti

- PostgreSQL
- MongoDB
- MySQL

## Odločitev in utemeljitev

Izbral sem PostgreSQL zaradi relacij, tujih ključev, omejitev in transakcij. Tak model ustreza naročilom s postavkami.

## Posledice

- **Pozitivne:** Referenčna integriteta in transakcije pomagajo preprečevati nekonsistentne podatke.
- **Negativne:** Za spremembe podatkovne strukture so potrebne migracije; dokumentni model bi bil pri zelo spremenljivih podatkih prilagodljivejši.
