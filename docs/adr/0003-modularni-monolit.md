# 0003 – Modularni monolit

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Aplikacijo razvijam sam, obseg pa je omejen na eno kmetijo. Moduli za uporabnike, izdelke in naročila so povezani, posebej pri zalogi.

## Obravnavane možnosti

- En backend, razdeljen na module auth, products in orders
- Samostojne mikrostoritve za posamezna področja

## Odločitev in utemeljitev

Odločil sem se za modularni monolit. Logiko bom razdelil po področjih, vendar bo to ena Express aplikacija.

## Posledice

- **Pozitivne:** Manj potrebnih nastavitev, preprostejše iskanje in odpravljanje napak ter lažje vzdrževanje projekta manjšega obsega.
- **Negativne:** Posameznih modulov ni mogoče neodvisno nameščati ali skalirati; pri rasti projekta bo treba paziti na meje med moduli.
