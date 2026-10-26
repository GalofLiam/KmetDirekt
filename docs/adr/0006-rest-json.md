# 0006 – REST API in JSON

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Frontend in backend morata izmenjevati podatke o izdelkih in naročilih, API pa želim preprosto preizkusiti v Postmanu.

## Obravnavane možnosti

- REST in JSON
- GraphQL
- Strežniško izrisane strani brez ločenega API-ja

## Odločitev in utemeljitev

Uporabil bom REST poti, npr. GET /api/products in POST /api/orders, s telesi zahtev in odgovorov v JSON.

## Posledice

- **Pozitivne:** HTTP metode in statusne kode olajšajo dokumentiranje in testiranje; frontend je ločen od podatkovne baze.
- **Negativne:** Za bolj zapletene poglede je lahko potrebnih več zahtev ali posebne API poti.
