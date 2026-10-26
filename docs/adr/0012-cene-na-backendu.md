# 0012 – Izračun cen na backendu in zgodovinska cena

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Cena v brskalniku ni zaupanja vredna, poznejša sprememba cenika pa ne sme spreminjati preteklih naročil.

## Obravnavane možnosti

- Ponoven izračun na backendu in snapshot cene v postavki
- Zanašanje na izračun v brskalniku
- Izračun pretekle cene iz trenutnega cenika

## Odločitev in utemeljitev

Ob oddaji backend iz baze prebere veljavne cene, izračuna znesek in shrani ceno posamezne postavke naročila.

## Posledice

- **Pozitivne:** Uporabnik ne more določiti cene prek zahtevka, stara naročila pa ohranijo svojo vrednost.
- **Negativne:** Podatki o ceni so podvojeni med cenikom in postavko; spremembe cene med ogledom košarice in oddajo zahtevajo jasen odziv vmesnika.
