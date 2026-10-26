# 0009 – Strežniške seje za prijavo

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Gre za klasično brskalniško aplikacijo, kjer želim omogočiti odjavo in preklic aktivne prijave.

## Obravnavane možnosti

- Strežniške seje z express-session in PostgreSQL shrambo
- JWT, shranjen pri odjemalcu

## Odločitev in utemeljitev

Po uspešni prijavi bo backend ustvaril strežniško sejo. Brskalnik prejme samo identifikator v piškotku HttpOnly; gesla bodo zgoščena z Argon2id.

## Posledice

- **Pozitivne:** Sejo je mogoče razveljaviti na strežniku; brskalnik ne upravlja vsebine seje.
- **Negativne:** Potrebna je shramba sej in zaščita pred CSRF; v produkciji je potreben HTTPS ter primerne nastavitve piškotkov.
