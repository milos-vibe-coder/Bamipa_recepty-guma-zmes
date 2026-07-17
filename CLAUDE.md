# CLAUDE.md — inštrukcie pre AI asistenta (vibe coding)

Tento súbor číta Claude Code / AI asistent pri práci na projekte. Drž sa ho.

## Čo je tento projekt

Jednosúborová webová aplikácia (`index.html`) na kalkuláciu materiálových nákladov gumárenských zmesí pre firmu BAMIPA. Používatelia sú nie-technickí pracovníci vo výrobe — UI musí zostať jednoduché a v slovenčine.

## Architektúra — dôležité pravidlá

1. **Všetko v jednom súbore.** HTML, CSS aj JS žijú v `index.html`. Nezavádzaj build systém, npm, frameworky ani externé závislosti, pokiaľ to používateľ výslovne nežiada. Dôvod: nasadenie = nakopírovanie jedného súboru, funguje offline.
2. **Žiadne CDN závislosti.** Aplikácia musí fungovať bez internetu.
3. **Slovenčina všade** — UI texty, hlášky, potvrdenia, formát čísel (`toLocaleString("sk-SK")`), desatinná čiarka na vstupe (funkcia `num()` akceptuje `,` aj `.`).
4. **Spätná kompatibilita dát.** Dáta sú v localStorage pod kľúčom `bamipa-recepty-v1`:
   ```js
   { recipes: [{ id, title, rows: [[nazov, gramy, cenaEurKg], ...], updatedAt }], activeId }
   ```
   Riadok = pole troch stringov. Pri zmene schémy vždy napíš migráciu (vzor: `load()` migruje starý kľúč `spotrebovany-material-v1`). Nikdy nesmieš používateľovi zmazať dáta.
5. **JSON súbory** (Uložiť/Načítať súbor) majú formát `{ app: "bamipa-recepty", version: 1, title, rows, savedAt }`. Pri zmene zvýš `version` a zachovaj čítanie starších verzií.

## Konvencie v kóde

- Vanilla JS, `"use strict"`, žiadne triedy — jednoduché funkcie
- Stav drží objekt `store`, aktívny recept vracia `active()`
- Po každej zmene dát volaj `save()` (debounced autosave + indikátor na tlačidle Uložiť)
- Prepočty: `recalcRow()` v rámci `render()`, súčty `recalcTotals()`
- CSS je v `<style>` v hlavičke, farby: primárna `#1f4e78`, nebezpečné akcie `#c0392b`, needitované ceny žlté `#fff8e1`
- Deštruktívne akcie (mazanie riadku/receptu) vždy s `confirm()`

## Ako testovať

Otvor `index.html` v prehliadači (alebo `npx serve .`). Manuálny checklist:
- pridanie/úprava/odstránenie materiálu, prepočet súčtov
- prepnutie receptu, nový, duplikát, vymazanie (posledný recept sa nesmie dať vymazať)
- Ctrl+S, reload stránky → dáta ostali
- Uložiť do súboru → Načítať súbor → recept sa pridal
- Export CSV otvoriteľný v Exceli (oddeľovač `;`, desatinná čiarka, BOM)
- mobil (šírka ~380 px) a tlač (Ctrl+P — skryjú sa tlačidlá)

## Roadmap (námety, len na požiadanie používateľa)

- Cenník materiálov zdieľaný medzi receptami (materiál → cena sa dopĺňa automaticky)
- Prepočet receptu na cieľovú šaržu (kg) — škálovanie množstiev
- Porovnanie nákladov dvoch receptov vedľa seba
- Zdieľaná databáza pre tím (napr. Supabase/Firebase) — až keď localStorage prestane stačiť
- História zmien cien materiálov

## Čoho sa vyvarovať

- Nepremenovávaj localStorage kľúče bez migrácie
- Nemeň formát CSV (ľudia naň môžu mať nadviazané Excel postupy)
- Nepridávaj login/účty, pokiaľ to nie je výslovne žiadané
- Neprekladaj UI do angličtiny
