# 0014 – Docker Compose za lokalni razvoj

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Backend potrebuje PostgreSQL, ponovljiv zagon pa je pomemben pri študijskem delu na različnih napravah.

## Obravnavane možnosti

- Docker Compose za PostgreSQL in backend
- Ročna namestitev obeh storitev
- Kubernetes

## Odločitev in utemeljitev

PostgreSQL in Express bom lokalno zagnal s Compose, frontend pa med razvojem z Vite. Za podatke baze bom uporabil trajni volume.

## Posledice

- **Pozitivne:** Enostavnejši ponovljiv zagon in manj odvisnosti od lokalne konfiguracije baze.
- **Negativne:** Potrebujem Docker in razumeti moram omrežja, volumne in okoljske spremenljivke; konfiguracijo je treba vzdrževati.
