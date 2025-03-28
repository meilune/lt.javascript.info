# JavaScript įvadas

Pažvelkime kuo ypatinga JavaScript kalba, ką mes galime su ja padaryti ir kokios kitos technologijos gali būti naudojamos kartu.

## Kas yra JavaScript?

Iš pat pradžių *JavaScript* buvo sukurta tam, kad *"padarytų tinklalapius gyvus"*.

Programos, parašytos šia kalba yra vadinamos *skriptais* (and. scripts). Jos gali būti parašytos tinklalapio HTML ir suveikti automatiškai, kuomet tinklalapis kraunamas.

Skriptai yra rašomi ir vykdomi paprastu (ang. "plain") tekstu. Jiems nereikia kompiliavimo fazės.

Šiuo aspektu JavaScript labai skiriasi nuo [Java](https://en.wikipedia.org/wiki/Java_(programming_language)).

```smart header="Iš kur kilo pavadinimas JavaScript?"
Iš pat pradžių JavaScript turėjo kitą pavadinimą: "LiveScript". Tačiau Java buvo itin populiari, todėl buvo nuspręsta pateikti naują kalbą kaip Java "jaunesnį brolį".

Tačiau ilgainiui JavaScript tapo nepriklausoma kalba, turinti atskirą specifikaciją, kuri vadinama [ECMAScript](http://en.wikipedia.org/wiki/ECMAScript). Šiuo metu JavaScript ir Java neturi nieko bendro. 
```

Dabar JavaScript gali būti vykdomas ne tik naršyklėje, bet taip pat ir serveryje arba praktiškai bet kokiame įrenginyje, kuris turi specialią programą, vadinamą JavaScript varikliu [(JavaScript engine)](https://en.wikipedia.org/wiki/JavaScript_engine).

Naršyklės turi savo vidinį variklį, kuris kartais vadinamas "JavaScript virtuali mašina"

Skirtingi varikliai turi skirtingus slapyvardžius (ang. "nicknames"). Pavyzdžiui:

- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) -- Chrome ir Opera.
- [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey) -- Firefox.
- Egzistuoja kiti slapyvardžiai, tokie kaip "Trident", "Chakra" skirtingoms IE versijom, "ChakraCore" Microsoft Edge naršklėje, "Nitro" ir "SquirellFish" Safari ir t.t.

Šias sąvokas verta atsiminti, nes jos naudojamos straipsniuose, skirtuose programuotojams. Mes taip pat jas naudosime. Pavyzdžiui, jeigu "feature X yra palaikoma V8", reiškias jinai ko gero veikia Chrome ir Opera naršklėse.

```smart header="Kaip veikia varikliai?"

Varikliai yra sudėtingi, bet pagrindai yra paprasti.

1. Variklis (vidinis, jei jis yra naršyklėje) skaito (ang. "parsing") skriptą.
2. Konvertuoja (dar kitaip - kompiliuoja) skriptą į mašininį kodą.
3. Įvykdomas mašininis kodas.

Varikliai optimizuoja kodą kiekviename žingsnyje. Jie netgi stebi sukompiliuotą skriptą, kuomet jis vykdomas, bei analizuoja duomenis, kurie jame naudojami, ir pagal tai taiko papildomas optimizacijas. Po viso šio procesio, skriptai yra vykdomi gan greitai.
```

## Ką gali JavaScript padaryti naršyklėje?

Modernus JavaScript yra "saugi" programavimo kalba. Ji neleidžia programuotojui pasiekti atminties arba CPU, nes iš pat pradžių ji buvo sukurta naršyklėms, kurioms to nereikia.

JavaScript galimybės stipriai priklauso nuo aplinkos, kurioje ji vykdomas. Pavyzdžiui, [Node.js](https://wikipedia.org/wiki/Node.js) palaiko funkcijas, kurios leidžia Javascript skaityti/rašyti failus, vykdyti kompiuterių tinklų užklausas ir pan.

Naršyklėje JavaScript gali daryti bet ką, tame tarpe tinklalapio manipuliacijas, sąveikas (ang. "interaction") su vartotojais ir web serveriu.

Pavyzdžiui, JavaScript naršyklėje gali:

- Pridėti naują HTML į tinklalapį, pakeisti jau esamą turinį, pakeisti stilius.
- Reaguoti į vartotojo veiksmus, pelės, klaviatūros paspaudimus.
- Siųsti užklausas į nuotolinius (ang. "remote") serverius, atsisiųsti ir įkelti (ang. "upload") failus ([AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)) ir [COMET](https://en.wikipedia.org/wiki/Comet_(programming)) technologijos).
- Gauti ir nustatyti slapukus (ang. "cookies"), užduoti klausimus vartotojo ir parodyti žinutes.
- Išsaugoti duomenis kliento pusėje (ang. "local storage").

## Ko NEGALI PADARYTI JavaScript naršyklėje?

JavaScript galimybės naryklėje yra ribojamos dėl vartotojų saugumo. Tikslas - neleisti tinklalapiams pasiekti privačius duomenis arba žaloti vartotojo duomenis.

Ribojimų pavyzdžiai:
- JavaScript tinklalapyje negali skaityti/rašyti failus esančius kietajame diske, juos kopijuoti arba vykdyti programas. JavaScript neturi tiesioginės prieigos prie operacinės sistemos funkcijų. 

	Modernios naršklės leidžia dirbti su failais, bet prieiga ribojama ir tai leidžiama tik jeigu vartotojas įvykdo kažką konkretaus. Pavyzdžiui, perkelia failą į naršyklę arba pažymi failą naudodamas `<input>` žymą.

Yra būdų komunikuoti su kamera/mikrofonu ir kitais įrenginiais, bet tai reikalauja išreikštinio vartotojo leidimo. Taigi, JavaScript tinklalapis negali suktai įjungti web kameros, stebėti aplinkos ir siųsti informaciją į [NSA](https://en.wikipedia.org/wiki/National_Security_Agency).
- Atskiros naršyklės kortelės (ang. "tabs") dažniausiai nežino viena apie kitą. Tačiau kartais viena kortelė naudoja JavaScript tam, kad atidarytų kitą kortelę, bet netgi tokiu atveju, JavaScript vienoje kortelėje negali pasiekti kitos, jeigu jie ateina iš skirtingų tinklalapių (skirtingas domenas, protokolas arba portas).
	Tai vadinama "Same Origin Policy". Tam, kad tai apeiti, *abudu tinklalapiai* turi sutikti apsikeisti duomenimis ir turėti specialų JavaScript kodą, kuris tai tvarkytų. Mes apie tai kalbėsime vienoje iš pamokų.
	Šis ribojimas yra, vėlgi, dėl vartotojų saugmo. Tinklapis `http://anysite.com`, kurį vartotojas atidarė, neturėtų pasiekti kitos naršklės kortelės su URL `http://gmail.com` ir vogti informaciją.
- JavaScript gali lengvai komunikuoti internetu su serveriu, iš kurio atėjo tinklalapis. Bet tinklalapio galimybės gauti duomenis iš kitų tinklapių/duomenų yra kiek sudėtingesnės. Nors ir įmanoma, tai reikalauja išreikštinio susitarimo (per HTTP antraštes) iš nuotolinio serverio pusės. Vėlgi, dėl saugumo priežasčių.

![](limitations.svg)

Šių ribojimų nėra, jeigu JavaScript vykdomas ne naršyklėje, bet, pavyzdžiui, serveryje. Šiuolaikinės naršyklės taip pat turi papildinius ir plėtinius(ang. "plugins/extensions"), kurie gali prašyti vartotojų leidimo.

## Kuo ypatinga JavaScript?

JavaScript turi bent *tris* nuostabius dalykus:

```compare
+ Pilna integracija su HTML/CSS
+ Paprastus dalykus padaryti yra nesudėtinga
+ Palaikoma visose populiariausiose naršyklėse
```
JavaScript yra vienintelė naršyklės technologija, kuri turi šiuos tris dalykus.

Štai kuo ypatinga JavaScript. Tai yra viena labiausiai išplitusių technologijų, kalbant apie naršyklės sąsajos (ang. "interface") kūrimą.

Tačiau su JavaScript galima rašyti serverines, mobilias programas (ang. "applications") ir pan.

## Alternatyvos

JavaScript sintaksė, be abejo, tinka ne visiem ir ne visada. Skirtingi žmonės nori skirtingų savybių.

Nieko nuostabaus, nes kiekvienas projektas yra skirtingas ir gali turėti labai skirtingų reikalavimų.

Dėl šių priežasčių atsirado daug kalbų, kurios yra konvertuojamos (dar kitaip - perrašomos, ang. "*transpiling*") į JavaScript ir tik tada vykdomos naršyklėje.

Modernūs įrankiai atlieka perrašymą labai greitai, tad programuotojai gali programuoti šiomis kalbomis nesigilindami į patį konvertavimo procesą.

Tokių kalbų pavyzdžiai:

- [CoffeeScript](http://coffeescript.org/) yra "syntactic sugar" JavaScript. Trumpesnė sintaksė, su kuria galima rašyti aiškesnį ir konkretesnį kodą. Tai dažniausiai patinka Ruby programuotojams.
- [TypeScript](http://www.typescriptlang.org/) pagrindinis tikslas yra įvesti statinį tipizavimą. Tai palengvina sudėtingų sistemų programavimą. Sukurtas Microsoft.
- [Flow](http://flow.org/) taip pat turi statinį tipizavimą, bet kiek kitokiu būdu. Sukurtas Facebook.
- [Dart](https://www.dartlang.org/) yra atskira kalba, kuri turi savo paties variklį, kuris veikia ne naršyklėse (pvz. mobiliose aplikacijose), bet taip pat gali būti transpiliuotas į Javascriptą. Sukurtas Google.

Yra ir daugiau pavyzdžių. Tačiau, netgi jeigu mes naudojame kažkurią iš transpiliuojamų kalbų, suprasti JavaScript yra ne mažiau svarbu.

## Santrauka

- JavaScript iš pat pradžių buvo sukurtas kaip kalba, veikianti naršyklėje, bet dabar turi ir daugiau aplinkų, kuriose gali būti vykdoma.
- Šią dieną JavaScript yra unikali tuo, kad tai labiausiai paplitusi kalba naršyklei, turinti pilną integraciją su HTML/CSS.
- Yra daug kalbų, kurios gali būti konvertuojamos į JavaScript ir turi papildomų funkcijų. Rekomenduojame į jas bent jau trumpai pažvelgti po to, kaip išmoksite JavaScript.
