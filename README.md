# RavenTrek Nasdara Bunker Decoder

**Dekodér rádiové morseovky z DayZ pro mapu Nasdara.** Přepiš vysílání nebo načti nahrávku a zjisti souřadnice bunkru i čtyřmístný PIN, pokud ho vysílání obsahuje.

Aplikace funguje přímo v prohlížeči, v jediném HTML souboru. Bez instalace, účtu a vlastního serveru. Rozhraní je v angličtině.

![RavenTrek Nasdara Bunker Decoder](thumbnail-bunker-decoder.png)

## Co aplikace umí

- **Ruční přepis morseovky** pomocí teček a čárek nebo dvou vlastních znaků. Jejich význam umí rozpoznat automaticky.
- **Dekódování zvuku** z načteného souboru, mikrofonu nebo zvuku počítače podle možností prohlížeče a zařízení.
- **Rozpoznání souřadnic i souřadnic s PINem** a hledání začátku zprávy při připojení uprostřed vysílání.
- **Sledování opakující se smyčky** s proměnlivým počtem bunkrů. Další průchody pomáhají doplnit chybějící údaje a potvrdit číslice.
- **Porovnání s 23 známými bunkry**, jejich zobrazení na vložené mapě Nasdary a odkazy na iZurvive.
- **Pomoc s chybami v přepisu** a barevné rozlišení číslic, souřadnic, PINů a jednotlivých bunkrů.
- **Kontrolu nahrávky** s přehráváním od 0,5× do 2×, grafem tónů, značkou začátku a ručními opravami rozpoznaných pípnutí.
- **Trénink poslechu** s generovaným vysíláním, nastavitelnou rychlostí, šumem a vyhodnocením odpovědi.
- **Kopírování výsledků**, export zvuku do MP3 a volitelné uchování dat v prohlížeči.
- **Dotyková tlačítka** pro zadávání na telefonu.

## Rychlé spuštění

1. Stáhni soubor [`decoder_v3.html`](decoder_v3.html) z repozitáře. Ulož samotný HTML soubor, nikoli stránku s náhledem kódu na GitHubu.
2. Otevři ho ve webovém prohlížeči.
3. Klikni na **Load example signal**, pokud si chceš aplikaci nejdřív vyzkoušet.
4. Pak zadej vlastní signál nebo otevři panel **Recording** a načti herní nahrávku přes **Load audio file**.

Pro ruční přepis a práci se souborem není potřeba nic sestavovat ani instalovat. Živé nahrávání vyžaduje oprávnění a podporu prohlížeče; pokud ho prohlížeč při lokálním otevření nenabízí, použij nahraný soubor nebo aplikaci otevři přes HTTPS či localhost.

## Ruční přepis vysílání

Do pole **Received signal** zapisuj krátké pípnutí jako tečku `.` a dlouhé jako čárku `-`. Každou číslici tvoří pět symbolů; přehled číslic najdeš přímo v aplikaci.

- Mezera mezi číslicemi usnadní čtení a pomůže dekodéru s rozdělením signálu.
- Lomítkem můžeš oddělit části souřadnic a PIN.
- Při dlouhé pauze mezi bunkry stiskni **Enter** a pokračuj na novém řádku.
- Můžeš používat i dvě vlastní klávesy, například `x` a `o`. Aplikace zkusí obě přiřazení k tečce a čárce; tlačítkem **Swap dot ↔ dash** lze přiřazení změnit ručně.
- Na telefonu použij **Dot**, **Dash** a **Back**.

**Decoded view** pod vstupem ukazuje, jak aplikace signál čte. Číslice, u kterých musela přepis opravit, označuje vlnovkou. **Tidy into rows** uspořádá přepis podle bunkrů a **Copy results** zkopíruje nalezené výsledky.

### Příklad

Tento ukázkový přepis obsahuje souřadnice `028 100` a ilustrativní PIN `1234`:

```text
----- ..--- ---.. / .---- ----- ----- / .---- ..--- ...-- ....-
```

PIN v příkladu slouží pouze k předvedení formátu.

## Dekódování ze zvuku

### Načtení nahrávky

1. V panelu **Recording** klikni na **Load audio file**.
2. Vyber nahrávku rádiového vysílání.
3. Nech zapnuté **Decode bunkers from the recording**, aby se výsledky počítaly z rozpoznaného zvuku.
4. Zkontroluj přepis v části **Heard in the recording** a nalezené bunkry na mapě.

Výběr souboru umožňuje například MP3, WAV, M4A, OGG, WebM a MP4. Skutečná podpora závisí na kodecích prohlížeče.

### Živé nahrávání

V nabídce **Record from** vyber mikrofon, jiný zvukový vstup nebo dostupnou možnost **Computer sound (share a screen, window or tab)**. Potom klikni na **Record** a povol přístup ke zvolenému zdroji.

Při sdílení obrazovky či karty zapni také sdílení zvuku v dialogu prohlížeče. Zachycení zvuku počítače závisí na systému a prohlížeči; alternativou je zvukový vstup typu Stereo Mix nebo virtuální zvukový kabel. Mikrofon musí slyšet vysílání z reproduktoru. Nahrávání ukončíš tlačítkem **Stop**.

### Kontrola a opravy

Pokud se tón rozpoznal chybně, klikni na něj v grafu a vyber **Dot**, **Dash** nebo **Ignore**. **Reset** vrátí původní rozpoznání daného tónu a **Undo all corrections** odstraní všechny ruční opravy.

Pomocí **Mark start at playhead** nastavíš začátek úseku pro analýzu. Při obtížném poslechu zpomal přehrávání. Přepis můžeš přes **Copy into signal field** přenést do ručního vstupu; pro dekódování jeho upravené podoby vypni **Decode bunkers from the recording**.

## Jak číst výsledky

Aplikace rozlišuje dva formáty záznamu:

```text
XXX YYY         souřadnice bunkru bez PINu
XXX YYY PPPP    souřadnice bunkru a čtyřmístný PIN
```

`XXX` označuje sloupec souřadnicové sítě a `YYY` řádek počítaný od horního okraje mapy. Prvních šest číslic aplikace porovnává s uloženými souřadnicemi bunkrů. PIN čte z vysílání; samotná znalost polohy bunkru ho nedoplní. Pokud vysílání PIN neobsahuje, zobrazí **not broadcast**.

Stavy **Guessing**, **Likely** a **Locked** vyjadřují odhad jistoty dekódování. U nejasných výsledků zkontroluj přepis nebo počkej na další opakování. Označení **Locked** není zárukou správného PINu.

Kliknutím na bunkr v mapě zobrazíš jeho souřadnice, typ, popis polohy a odkaz **Open on iZurvive**.

## Trénink poslechu

Rozbal **Listening practice** a vyber tři číslice, jeden bunkr nebo celou smyčku. Nastav rychlost a úroveň šumu, případně přidej čtyřmístný PIN nebo blikání kontrolky při pípnutí.

Klikni na **Start**, zapisuj slyšený signál a pak použij **Check my answer** nebo **Show the answer**. Trénink používá generované tóny a rytmus odvozený z herního vysílání. Tvůj původní přepis se na dobu tréninku odloží a po jeho ukončení se vrátí.

## Offline provoz a ukládání dat

Dekódování, analýza zvuku i převod do MP3 probíhají místně v prohlížeči. **Mapa, písma a MP3 kodér jsou vložené přímo v HTML**, takže samotná aplikace funguje offline. Otevření iZurvive potřebuje internet. Aplikace zadaný signál ani nahrávky neodesílá na server.

Volba **Keep my data after I close the page** je ve výchozím stavu zapnutá:

| Nastavení | Zadaný signál a nastavení | Nahrávka |
| --- | --- | --- |
| Zapnuto | Ukládají se v tomto prohlížeči. | Ukládá se místně včetně značky začátku a ručních oprav; při dalším otevření se obnoví. |
| Vypnuto | Zůstávají pro tuto kartu, včetně obnovení stránky. | Zůstává jen v paměti; obnovení stránky nebo zavření karty ji zahodí. |

**Clear signal** vymaže přepis, **Delete recording** odstraní nahrávku a **Delete all saved data** slouží k vymazání přepisu i uloženého zvuku. Exportované soubory zůstávají samostatně na disku.

Úložiště prohlížeče není záloha. Data může odstranit jeho nastavení, soukromý režim nebo nedostatek místa; důležité nahrávky exportuj. Mikrofon zaznamenává také okolní zvuky, které slyší.

## Omezení

- Dekodér je zaměřený na číslice v rádiovém vysílání bunkrů na Nasdaře. Nejde o obecný překladač textové morseovky.
- Zvukový detektor je naladěný na herní tón přibližně **988 Hz**. Šum, jiné zvuky, příliš slabý signál nebo odlišné vysílání mohou ovlivnit výsledek.
- Opravy a doplňování jsou odhady. Pro přesnější výsledek zachyť delší úsek a další opakování vysílání.
- Seznam 23 bunkrů je součástí aplikace. Změny mapy nebo úpravy konkrétního serveru mohou vyžadovat jeho aktualizaci.
- Dostupnost nahrávání, sdílení systémového zvuku, formátů a ukládání závisí na prohlížeči a zařízení.
- Velké soubory a dlouhé nahrávky mohou výrazně zatížit paměť zařízení.
- Pokud se převod do MP3 nezdaří, export uloží původní zvukový formát.

## Technologie

HTML, CSS a JavaScript bez sestavování. Pro zvuk aplikace používá Web Audio API, MediaRecorder a Web Worker; graf vykresluje přes Canvas, značky na mapě přes SVG. Místní data ukládá pomocí localStorage, sessionStorage a IndexedDB. Součástí HTML je MP3 kodér **lamejs 1.2.1**.

## Hlášení chyb

Do GitHub Issues přidej popis problému, postup jeho vyvolání, prohlížeč a zařízení. U chyb dekódování pomůže přepis signálu nebo krátký zvukový vzorek s očekávaným výsledkem.
