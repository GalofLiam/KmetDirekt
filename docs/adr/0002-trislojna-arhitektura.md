# 0002 – Trislojna arhitektura

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Cene, dostopne pravice in zaloge ne smejo biti prepuščene brskalniku, hkrati pa želim preprosto spreminjati uporabniški vmesnik.

## Obravnavane možnosti

- Ločene predstavitvena, aplikacijska in podatkovna plast
- Odjemalec z neposrednim dostopom do baze

## Odločitev in utemeljitev

Uporabil bom React za prikaz, Express za REST API in poslovna pravila ter PostgreSQL za shranjevanje. Brskalnik ne dostopa neposredno do baze.

## Posledice

- **Pozitivne:** Odgovornosti so jasne in preverjanje pravic ostane na strežniku.
- **Negativne:** Vzdrževati je treba dogovor med frontendom in API-jem ter tri različne dele aplikacije.
