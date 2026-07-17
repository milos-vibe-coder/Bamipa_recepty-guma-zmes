# BAMIPA — Recepty gumových zmesí

Webová aplikácia na kalkuláciu materiálových nákladov gumárenských zmesí. Beží čisto v prehliadači — žiadny server, žiadna databáza, žiadna inštalácia.

## Funkcie

- **Viac receptov** — vytváranie, duplikovanie, premenovanie a mazanie receptov
- **Editovateľná tabuľka** — materiál, množstvo (g), cena €/kg; kg a súčty sa počítajú automaticky
- **Priemerná cena zmesi** €/kg a indikátor koľko položiek je už ocenených
- **Automatické ukladanie** do prehliadača (localStorage) + tlačidlo Uložiť (Ctrl+S)
- **Uložiť / Načítať súbor** — prenos receptu ako .json medzi zariadeniami a ľuďmi
- **Export CSV** (slovenský formát, otvoríš v Exceli) a **Tlač / PDF**
- Funguje na mobile aj počítači, offline

## Lokálne spustenie

Stačí otvoriť `index.html` v prehliadači. Hotovo.

## Nasadenie na web (zadarmo)

### Variant A — GitHub Pages (odporúčané)

1. Vytvor repozitár na github.com (napr. `bamipa-recepty`)
2. V priečinku projektu:
   ```
   git init
   git add .
   git commit -m "Prvá verzia"
   git branch -M main
   git remote add origin https://github.com/TVOJE_MENO/bamipa-recepty.git
   git push -u origin main
   ```
3. Na GitHube: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root) → Save**
4. Do pár minút beží na `https://TVOJE_MENO.github.io/bamipa-recepty/`

### Variant B — Netlify (najrýchlejšie)

1. Choď na app.netlify.com → **Add new site → Deploy manually**
2. Pretiahni celý priečinok projektu do okna
3. Hotovo — dostaneš adresu typu `nazov.netlify.app`

### Variant C — Vercel

1. vercel.com → **Add New → Project** → prepoj GitHub repozitár
2. Framework: **Other**, žiadny build príkaz — deploy

## Ako fungujú dáta

Každý používateľ má **vlastné dáta vo svojom prehliadači** (localStorage). Web samotný dáta nezdieľa — na výmenu receptov slúži **Uložiť do súboru / Načítať súbor** (.json). Ak by si v budúcnosti chcel spoločnú databázu pre celý tím (všetci vidia tie isté recepty a ceny), treba doplniť backend — pozri `CLAUDE.md`, sekcia Roadmap.

## Štruktúra projektu

```
index.html    # celá aplikácia (HTML + CSS + JS v jednom súbore)
README.md     # tento súbor
CLAUDE.md     # inštrukcie pre vibe coding s Claude / Claude Code
.gitignore
```

## Licencia

Interné použitie BAMIPA s.r.o.
