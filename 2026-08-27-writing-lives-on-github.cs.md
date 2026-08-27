---
nazev: Texty žijí na GitHubu, web si pro ně chodí sám
typ: clanek
druh: POZNÁMKA
popis: Zdrojem je jeden veřejný repozitář. Web si ho při sestavení přečte a vysází. Žádné administrační rozhraní, žádná databáze.
---

# Texty žijí na GitHubu, web si pro ně chodí sám

Zdrojem je jeden veřejný repozitář. Web si ho při sestavení přečte a vysází.

## Proč ne redakční systém

Redakční systém řeší problém, který nemám. Znamenal by databázi, přihlašování,
zálohy a aktualizace — celou vrstvu, která musí běžet, aby se dala přečíst
stránka s textem. Za to dostanu editační okno v prohlížeči.

Repozitář má proti tomu tři vlastnosti, kterých si cením víc. Historie změn je
v něm zadarmo a je úplná. Text jde otevřít v čemkoli, co umí otevřít soubor.
A když se web rozbije, texty tím netrpí — leží jinde, ve formátu, který přežije
kdejakou technologii, na které zrovna stojí sazba.

## Co je v repozitáři

Články jsou obyčejné soubory Markdown. Název souboru nese slug, jazyk a datum:

```
2026-08-27-writing-lives-on-github.en.md
2026-08-27-writing-lives-on-github.cs.md
```

Dva soubory se stejným slugem jsou tentýž text ve dvou jazycích. Můžou mít úplně
jiný nadpis, spojuje je ta část mezi datem a příponou jazyka. Když existuje jen
jedna verze, web ji nabídne i v druhém jazyce a nad textem přizná, že překlad
zatím není.

Nahoře v souboru je hlavička — název, druh, perex. Zbytek je text.

## Obrázky

Obrázky leží vedle textů a odkazuje se na ně relativní cestou:

<figure>
  <img src="images/flow.webp"
       alt="Tři kroky vedle sebe: repozitář, sestavení, hotová stránka"
       width="1600" height="300" loading="lazy" />
  <figcaption>Krok uprostřed proběhne při každém sestavení. Mezi ním a hotovou stránkou už nic neběží.</figcaption>
</figure>

Relativní cesta má jednu výhodu, kvůli které to takhle je: obrázek se ukáže
i přímo na GitHubu. Článek je čitelný na obou místech, nejen na webu. Při
sestavení se cesta přepíše na adresu, ze které si ji stáhne prohlížeč.

## Co se stane při sestavení

Web se zeptá GitHubu na seznam souborů, stáhne je, ověří hlavičky a vysází
statické stránky. Když v hlavičce chybí povinný údaj, sestavení spadne — což je
záměr, lepší než tiše vydat stránku s dírou.

Hotový výstup je pak jenom HTML. Žádný požadavek na GitHub už z prohlížeče
neodchází.
