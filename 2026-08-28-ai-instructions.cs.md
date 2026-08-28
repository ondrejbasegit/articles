---
nazev: Jak úspěšně spolupracovat s AI
typ: clanek
druh: NÁVOD
popis: Nejužitečnější instrukce, které pro AI mám, nemají s kódem nic společného.
---

Žádný web by dnes nemohl být kompletní bez návodu, jak napsat CLAUDE.md. Zkusím to ale udělat trochu jinak (i když to také říká každý, vím). Místo klasického copy + paste obsahu se pokusím popsat, jak na to běžně jdu, a na co si dát pozor. Nejužitečnější instrukce, které pro AI mám, nemají nic společného s technickou stránkou ani kódem.

Nejdřív trochu teoretických znalostí, od základů a bez pokročilejších věcí (jako je tvorba vlastních agentů, skills, MCP — o tom až příště).

Jakmile dáš AI agentovi přístup ke svému počítači, a je jedno, o kterého agenta se přesně jedná (Codex, Cursor, Copilot, Gemini, Claude Code…), jsou obvykle dvě hlavní cesty, odkud bere své „trvalé informace“, neboli instrukce:

- **Globální** — v domovském adresáři aktuálního uživatele, např. `~/.claude/`
- **Projektová** — ve složce s projektem, ve kterém je AI aktuálně otevřená,
  např. `~/projekty/fakturace/.claude/`

Obojí si AI agent obvykle založí sám a uchovává v nich, co uzná za vhodné. Nás především zajímá jeden soubor v obou složkách, který může být nazvaný různě, a jehož obsah se automaticky nalepí před každý ručně napsaný prompt:

| nástroj | soubor |
|---|---|
| kdokoli | `AGENTS.md` |
| Claude Code | `CLAUDE.md` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Cursor | `.cursor/rules/*.mdc` (dřív `.cursorrules`) |
| Gemini CLI | `GEMINI.md` |

Je nutné mít na paměti, že tento soubor si AI agent z domovského adresáře uživatele načítá vždy a z adresáře projektu pouze, pokud pracuje v daném projektu.

Tohle vymezení zároveň napovídá, jakou oblast instrukcí ve kterém souboru pokrýt.

**Globální, v domovském adresáři** (`~/.claude/CLAUDE.md`) — platí pro každé
sezení, ať jsem v jakékoli složce nebo projektu. Patří sem jen to, co je pravda pořád. U mě například:

- kdo jsem a jak se mnou mluvit — jazyk, tykání, tón, kreativita („*Rád brainstormuju, nahazuj mi často různé nápady a nešetři popisem*“)
- podrobnější informace o mém počítači — hardware, PowerShell, WSL2, můj domácí server
- že si má informace automaticky a bez ptaní hledat na webu a **nevymýšlet si**, „*znalosti modelu jsou zastaralé a na většinu dotazů potřebuju aktuální z webu*“ (tohle je dobré AI připomenout)
- kam co na disku patří
- co se nikdy nesmí: mazat a přepisovat bez potvrzení, cokoli veřejně postovat, vybrané „nedotknutelné“ složky
- poučení z chyb a jak jim do budoucna předcházet — pravidelné zapisování toho, co má pro příště udělat jinak a lépe, automaticky a bez vyzvání (tohle je důležité)

**Projektová, ve složce projektu** — všechno ostatní, co se specificky týká daného projektu, na kterém AI pracuje.
Cesty, zvyklosti, stavy, rozhodnutí, důvody. Nic z toho nemá co dělat v globálním souboru, protože v ostatních projektech to platit nebude.

Společně s množstvím informací a instrukcí bude soubor nutně bobtnat, proto se v pozdějších fázích používá ideálně jako **rozcestník** na ostatní soubory v dokumentaci. Stále by měl ale obsahovat obecný popis projektu a nedotknutelná pravidla.

Konkrétní projekt z mého počítače, záměrně netechnický:

## Soubor o fotoaparátu

První pořádný fotoaparát po letech focení na iPhone. Do `CLAUDE.md` v projektu
`foto` jsem napsal instrukce, které nemají s kódem nic společného:

> **Jsem naprostý začátečník.** Neznám žánrovou terminologii ani zkratky.
>
> **Vysvětluj pojmy.** Když použiješ jakýkoli odborný pojem nebo zkratku, VŽDY
> ho hned vysvětli jednoduše. Nepředpokládej, že něco znám.
>
> **Oprav mě přímo.** Když se v něčem pletu, řekni to. Nesnaž se mi dát
> za pravdu, když ji nemám.
>
> **Žádné „záleží na tom“.** Když odpověď opravdu závisí na okolnostech, řekni
> na čem, a dej mi **rozhodovací pravidlo**, ne jen výčet možností.

Pod tím je seznam mojí výbavy do posledního detailu — tělo, objektiv, ohnisko,
od kolika centimetrů zaostří — a pak sekce **„Co už chápu“**. Je v ní, že expozici tvoří clona, čas a ISO, že ISO je
následek a ne tvůrčí volba a že se řídím pravidlem *použij nejdelší čas, při
kterém se nic nerozmaže*. Ne proto, aby to model věděl, ale proto, aby mi to přestal vysvětlovat.

A na konci povinný postup: **nejdřív manuál v repozitáři** — celých 452 stran
rozsekaných do markdownu, plus obrázek každé stránky, kdyby text nestačil —
**pak teprve web**. *Nikdy si nevymýšlej cestu v menu ani parametr.*

## Pravidlo bez jizvy je jen dekorace

Po zevrubné inspekci všech mých souborů s instrukcemi skoro každá věta, která něčemu zabránila,
vznikla až po tom, co se to stalo. Prvním chybám se obvykle nedá předejít. Na ty opravdu vážné slouží instrukce v domovském adresáři a pevné konfigurační limity příkazů, o těch ale tenhle článek není.

Zbytku se dá čelit jinak: AI agent by měl průběžně udržovat záznam o správných postupech i o chybách, do kterých projekt spadl. Obvykle to dělá sám od sebe, ale jako pojistku se hodí mít to explicitně uvedené v hlavním instruktážním souboru.

Tři příklady z `AGENTS.md` mého projektu Galerie:

> **Nikdy nerozhoduj podle popisku.** Jestli je obrázek čistá reprodukce, se
> pozná pohledem. Aukční texty, popisky pod obrázky a skromnost samotných
> autorů („jen studie“) neříkají nic spolehlivého.

> **Kontroluj roli, ne jen jméno.** Muzejní API vrací i díla, kde je autor
> **portrétovaný**, ne malíř. Bez filtru na roli tvůrce si pod svého autora
> zařadíš cizí obraz.

> **Prázdný výsledek není totéž co žádný.** Několik těch API vrací při omezení
> rychlosti prázdný seznam místo chyby. Zopakuj dotaz, než tomu uvěříš. Důvěra
> v jedinou prázdnou odpověď už jednou tiše vymazala celý katalog.

Ten poslední je z celé sbírky nejcennější, a ne kvůli tomu, co přikazuje, ale kvůli poslední větě. Bez ní je to obecná rada, s ní je to fakt o mém projektu.

## Urči si předem styl a tempo práce s AI

V úvodu projektu je dobré se s AI agentem nejdříve dohodnout na tom, jakým způsobem spolu budete spolupracovat. Agent ho klidně navrhne sám, ale je vhodné to nejdříve odsouhlasit a pak pevně zapsat, čímž se do budoucna předejde rozdílnému chování mezi jednotlivými sezeními. Z toho pak budou vycházet i pravomoci a úkoly, které AI bude mít.

Příklady z mých instrukcí:

> - Zálohovací skript commituj sám. **Push jen po výslovném odsouhlasení.**
> - U webu spravuj git kompletně sám — commit i push, bez ptaní. Nikde jinde.
> - Do mých původních repozitářů se nesahá. Veřejná kopie vzniká jako nový
>   repozitář, změna nikdy nejde zpátky do projektu, **i kdyby tam patřila**.
> - Na konci každého kroku ohlas, co jsi našel a co se chystáš udělat, čekej
>   na můj souhlas.
> - Nikdy nenabízej, že za mě někam něco napíšeš veřejně — Reddit, GitHub
>   issues, fóra. Svůj veřejný hlas si píšu sám.
> - Před čímkoli nevratným se ptej.

## Tvorba článků s AI

Obecně nedoporučuju nechat AI psát delší obsah, krom draftů či striktně technických popisů (README.md v projektech na GitHubu apod.), ale stále existuje pár způsobů, jak další psaný text alespoň částečně zbavit typických AI neduhů.

V instrukcích k webu to mám takhle:

> **Pryč s obraty, kterými text hodnotí sám sebe:** „being honest about
> this“, „a nebudu předstírat opak“, „stojí za to vědět, než na to obětuješ
> večer“. Říkej fakta, ne dojmy.
>
> Označování sama sebe za upřímný hlas je nejsilnější poznávací znak textu psaného AI —
> člověk, který informaci sdělí, o své upřímnosti obvykle nemluví.

Seznam slov, na který se text před vydáním projede: `honest`,
`pretend`, `worth knowing`, `to be fair`, `admittedly`, `frankly`.

## Rozděl instrukce podle toho, co smí opustit počítač

Tohle řešit nemusíš, dokud si projekt necháváš pro sebe. Jakmile ho ale chceš
vydat veřejně, narazíš: v instrukcích je adresa serveru, cesty k datům, jména
kontejnerů a rozhodnutí, která nikomu cizímu nic neřeknou.

U Galerie jsem to rozsekal na tři soubory podle jediného kritéria — **smí to
ven?**

- `AGENTS.md` je o projektu: jak funguje, co se nesmí rozbít, jak přidat
  další zdroj. Jde ven beze změny.
- `docs/ops.md` je o tomhle stroji: server, nasazení, moje kurátorská
  rozhodnutí. Ven nejde nikdy.
- `CLAUDE.md` zbyl jako rozcestník na ty dva.

Kontrola, jestli to sedí, je pak jednoduchá. Ve veřejné kopii je proti
soukromé verzi rozdíl jednoho řádku, a je to název kontejneru.

Tohle není bezpečnostní opatření, ale organizační.
Klíče a hesla v instrukcích nemají co dělat tak jako tak, patří do `.env`
mimo repozitář, a před zveřejněním se na projekt pouští strojový sken.

## Co instrukce neumí

**Napsané pravidlo není dodržené pravidlo.**

V instrukcích stálo, že AI pushuje obsah do vzdáleného repozitáře až po odsouhlasení. Model to porušil — vzal si zmocnění platné pro jeden repozitář a přenesl ho na jiný. Soubor instrukcí riziko snižuje, ale neeliminuje ho.

Když potřebuješ jistotu, instrukce nestačí a musíš sáhnout po technických zábranách, které se obejít nedají. U každého agenta vypadají jinak, princip je ale stejný: konfiguračním souborem se dá omezit, jaké příkazy smí vůbec spustit. A pak je tu odsouhlasení každé akce zvlášť, které bývá ve výchozím nastavení zapnuté.

**Instrukce zastarávají rychleji než kód.**

U dlouhodobého projektu se neudržuje jen jeho obsah, ale i soubor, který ho popisuje. Na konci každého pracovního sezení je dobré nechat AI agenta kromě zapsání aktuálního stavu udělat i review instrukcí. Mělo by odhalit, zda si novější příkazy neprotiřečí se staršími a zda některé části dokumentace neobsahují zastaralé informace.

Jednou za čas je pak dobré požádat AI o kompletní analýzu a revizi. Ta předejde nejen duplicitám, ale i velkému množství věcí, které se už nemusí pravidelně načítat, protože nejsou potřeba. Zbytečně totiž plní kontext každé konverzace, čímž plýtvají tokeny a můžou přebíjet důležitější instrukce v rámci kontextového okna.

## Poučení

U naprosté většiny projektů, ať už těch velkých korporátních, nebo zcela malých soukromých (viz „Soubor o fotoaparátu“), je žádoucí, aby se AI agent choval co nejvíce deterministicky a předvídatelně. Toho dosáhneme správným udržováním instrukcí. Samotné psaní ale není nutné dělat ručně — formulaci i průběžnou údržbu zvládne agent lépe a rychleji. Je dobré věnovat nějaký čas (který se v dlouhodobém horizontu mnohonásobně vrátí) na předběžnou definici toho, jakým způsobem bude spolupráce s AI probíhat, ať tě nic nepřekvapí.
