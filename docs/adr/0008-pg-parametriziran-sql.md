# 0008 – pg in parametriziran SQL

- **Status:** Sprejeto (za načrtovano rešitev)
- **Datum:** 2026-10-24
- **Nadomešča:** —

## Kontekst in problem

Pri manjši aplikaciji želim razumeti dejanske SQL poizvedbe, posebej transakcije za zalogo.

## Obravnavane možnosti

- Knjižnica pg in neposreden parametriziran SQL
- ORM, na primer Prisma

## Odločitev in utemeljitev

Do PostgreSQL bom dostopal prek pg. Vrednosti v poizvedbah bom vezal s parametri, za transakcijo pa uporabljal isto povezavo od BEGIN do COMMIT oziroma ROLLBACK.

## Posledice

- **Pozitivne:** Nadzor nad SQL in zaklepanjem vrstic ter manj dodatnih abstrakcij.
- **Negativne:** Več ročnega SQL in preslikovanja rezultatov; napake v poizvedbah je treba posebej testirati.
