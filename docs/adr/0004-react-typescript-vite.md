# 0004 – React, TypeScript in Vite

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Košarica, pregled ponudbe in prikaz statusov potrebujejo interaktiven vmesnik. Pomembno mi je tudi, da hitro vidim spremembe med razvojem.

## Obravnavane možnosti

- React + TypeScript + Vite
- React z navadnim JavaScriptom
- Osnovni HTML in JavaScript brez ogrodja

## Odločitev in utemeljitev

Za frontend bom uporabil React s TypeScriptom, lokalni razvoj pa bo tekel prek Vite. Tipi bodo opisovali izdelke, naročila in statusne vrednosti.

## Posledice

- **Pozitivne:** Ponovno uporabljive komponente, hitre razvojne posodobitve in zgodnejše odkrivanje tipnih napak.
- **Negativne:** Potrebni so odvisnosti, začetna nastavitev in prevajanje; TypeScript ne preverja samodejno podatkov, prejetih med izvajanjem.
