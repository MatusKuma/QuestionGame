# Slovohra — denná hra s otázkami

## Ako to funguje
Hráč vidí slovo a nápovedu. Napíše otázku, o ktorej si myslí, že jej odpoveďou je zobrazené slovo. Hra porovná význam jeho otázky so skrytou otázkou pomocou viacjazyčného embedding modelu spusteného v prehliadači.

## Pridávanie nových dní
Uprav iba `catalog.json`. Do poľa `days` pridaj ľubovoľný počet objektov:

```json
{
  "date": "2026-10-29",
  "word": "OCEÁN",
  "hint": "Je väčší než more.",
  "question": "Aká rozsiahla vodná plocha pokrýva väčšinu zemského povrchu?"
}
```

- `date`: dátum výzvy vo formáte `YYYY-MM-DD`
- `word`: slovo, ktoré hráč vidí
- `hint`: nápoveda, ktorú hráč vidí
- `question`: tajná otázka, s ktorou sa porovnáva hráčov vstup

Pridaj ďalšie dni do toho istého poľa `days`. Dátumy musia byť jedinečné a formát JSON musí ostať platný. Aplikácia vyberie výzvu s dnešným dátumom; ak dnešný dátum chýba, zobrazí najnovšiu výzvu z minulosti. Pri vývoji môžeš zmeniť dátum v `catalog.json` na dnešný.

## Spustenie na počítači
Vyžaduje sa Python 3 alebo iný lokálny HTTP server. V priečinku s `index.html` a `catalog.json` spusti:

```bash
python -m http.server 8000
```

Potom otvor `http://localhost:8000`.

Nepoužívaj priame otvorenie `index.html` cez `file://`, pretože prehliadač môže blokovať načítanie JSON súboru.

## Bezplatné zverejnenie
Nahraj `index.html` a `catalog.json` do GitHub repozitára a zapni GitHub Pages. Model sa sťahuje z verejného CDN pri prvom použití a potom ho prehliadač môže uložiť do cache.

## Limity prototypu
- Skóre je hrubý odhad sémantickej podobnosti, nie presná kontrola správnosti.
- Bez backendu je tajná otázka viditeľná v `catalog.json` a zdrojovom kóde; vhodné na prototyp a testovanie, nie na súťaž s odmenami.
- Pokusy sa ukladajú len lokálne v konkrétnom prehliadači.
- Na prvé spustenie treba internet na stiahnutie modelu a knižnice. Následné vyhodnocovanie prebieha lokálne.
