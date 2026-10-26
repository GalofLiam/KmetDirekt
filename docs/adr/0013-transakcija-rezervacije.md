# 0013 – Transakcijska rezervacija zaloge

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Dva kupca lahko skoraj istočasno oddasta naročilo za zadnje proste pakete. Naročilo in rezervacija morata ostati usklajena.

## Obravnavane možnosti

- Enotna PostgreSQL transakcija z zaklepanjem ali atomskim preverjanjem
- Ločene neodvisne posodobitve naročila in zaloge

## Odločitev in utemeljitev

V eni transakciji bom preveril prosto zalogo, rezerviral pakete ter shranil naročilo in postavke; ob napaki naredil ROLLBACK.

## Posledice

- **Pozitivne:** Preprečevanje dvojne rezervacije in delno shranjenih naročil.
- **Negativne:** Daljše transakcije lahko povzročijo čakanje na zaklenjene vrstice; paziti je treba tudi na sprostitev rezervacije samo enkrat.
