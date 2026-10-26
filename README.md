# KmetDirekt

KmetDirekt je načrtovana spletna aplikacija za naročanje vnaprej pripravljenih mesnih paketov pri eni lokalni kmetiji. Kupec izdelke izbere v brskalniku in naročilo osebno prevzame na kmetiji. Zaposleni skrbi za obravnavo naročil, lastnik pa za ponudbo in zaloge.

## Tehnologije

- **Frontend:** React, TypeScript, Vite
- **Backend:** Node.js, Express, TypeScript; REST API in JSON
- **Baza:** PostgreSQL (`pg`, parametriziran SQL)
- **Prijava:** strežniške seje, piškotki HttpOnly in nadzor pravic
- **Lokalni razvoj (predvideno):** Docker Compose za backend in bazo, Vite za frontend

Projekt je trenutno v fazi načrtovanja. Mapi `frontend/` in `backend/` sta pripravljeni, implementacija bo dodana kasneje.

## Dokumentacija

- [Zasnova rešitve](docs/01-zasnova-resitve.md)
- [Funkcionalnosti in obseg](docs/02-funkcionalnosti-in-obseg.md)
- [Podatkovni model](docs/03-podatkovni-model.md)
- [Arhitektura in tehnologije](docs/04-arhitektura-in-tehnoloski-sklad.md)
- [Uporabniške zgodbe](docs/05-uporabniske-zgodbe.md)
- [Wireframe-i](docs/06-wireframes.md)
- [Arhitekturne odločitve (ADR)](docs/adr/README.md)

## Sodelovanje

Spremembe se pripravljajo na ločenih vejah in združujejo v `main` prek pull requestov (GitHub Flow). Ob novi pomembni arhitekturni odločitvi dodamo ADR, ob spremembi sprejete odločitve pa novega, ki navede prejšnjega.

Dokumentacija projekta vključuje zasnovo, uporabniške zgodbe, wireframe-e in zapise arhitekturnih odločitev.