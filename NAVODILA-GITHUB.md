# Koraki za objavo in preizkus GitHub Flow

To so praktična navodila za študentsko nalogo, ne del aplikacije.

## 1. GitHub Education

Na https://github.com/education/students oddaj zahtevek za Student Developer Pack. GitHub lahko zahteva preverjanje aktualnega vpisa. Odobritve ni mogoče predpostaviti.

## 2. Ustvari repozitorij

Na GitHubu izberi **New repository**, ime `KmetDirekt`, **public** (ali private, če ti profesor dovoli in imaš ustrezen načrt) in ga po možnosti ustvari brez samodejno dodanega README, ker ga paket že vsebuje.

Za izpolnitev zahteve po kloniranju najprej kloniraj ustvarjeni repozitorij, nato vanj prenesi vsebino te mape `KmetDirekt_GitHub_naloga3` (ne celotne mape kot podmapo).

```bash
git clone https://github.com/TVOJ-UPORABNIK/KmetDirekt.git
cd KmetDirekt
# Tu kopiraj pripravljene datoteke, vključno z docs/ in .gitignore
git add .
git commit -m "docs: dodana zasnova, zgodbe, wireframe-i in ADR"
git push -u origin main
```

Če repozitorij še nima veje `main` ali lokalni Git zahteva inicializacijo identitete, to uredi pred commitom (`git config user.name` / `user.email`). Če GitHub ob ustvarjanju doda README, datoteke pred začetnim commitom uskladi in ne prepiši obstoječega dela na slepo.

## 3. Zaščiti main

Na GitHubu odpri **Settings → Branches → Add branch protection rule** (oziroma ustrezno možnost v novejšem prikazu pravil). Ciljna veja: `main`.

- Vklopi `Require a pull request before merging`.
- Ne zahtevaj odobritve druge osebe: možnost `Require approvals` naj bo izklopljena oziroma naj bo zahtevano število 0.
- `Allow force pushes`: izklopljeno.
- `Allow deletions`: izklopljeno.
- `Do not allow bypassing the above settings`: vklopljeno.

Nastavitve in razpoložljivost so odvisne od GitHubovega načrta in vrste repozitorija; pri opozorilu o neaktivnih pravilih preveri načrt in po potrebi uporabljaj javni repozitorij.

## 4. Izvedi poskusni PR

Po zaščiti `main` naredi najmanjšo smiselno spremembo na novi veji.

```bash
git switch -c docs/preverjanje-github-flow
# Uredi npr. eno poved v README.md
git add README.md
git commit -m "docs: pojasnjen opis projekta"
git push -u origin docs/preverjanje-github-flow
```

Na GitHubu izberi **Compare & pull request**, nastavi `base: main` in `compare: docs/preverjanje-github-flow`, ustvari PR in ga združi z **Merge pull request**. Nato lokalno: 

```bash
git switch main
git pull origin main
```

Preveri, da se PR pojavi na zavihku **Pull requests → Closed**, da ima stanje merged in da je veja `main` zaščitena. Po potrebi naredi posnetke zaslona za dokazilo.

## 5. Pred oddajo

Preveri povezave iz README, da se tri slike odprejo, da se izpiše vseh 15 ADR-jev, da je glavna veja zaščitena, in da je en PR res združen. Spletnih korakov ta paket ne more izvesti namesto tebe.
