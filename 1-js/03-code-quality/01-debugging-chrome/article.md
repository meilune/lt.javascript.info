# Klaidų taisymas naršyklėje Chrome

Prieš rašydami apie sudėtingesnius kodus, pakalbėkime apie klaidų ieškojimą ir taisymą (ang. debugging).

[Išrinktavimas](https://en.wikipedia.org/wiki/Debugging) yra toks procesas kai ieškome ir taisome klaidas skriptuose. Visos modernios naršyklės ir didžioji dalis kitų aplinkų palaiko klaidų taisymo (kitaip išriktavimo) įrankius -- tam tikra programuotojo įrankių vartotojo sąsaja (UI), kuri palengvina klaidų taisymą. Ji taip pat leidžia atsekti kodą žingsnis po žingsnio, kad pamatytume kas iš tikrųjų vyksta.

Mes tam naudosime Chrome, nes ši naršyklė turi užtektinai funkcijų, bet didžioji dalis naršyklių turi panašius procesus.

## Šaltinių panelis (ang. "Sources" panel)

Jūsų turima Chrome versija gali šiek tiek skirtis, bet ne tiek daug, kad nesuprastumėte kas kur yra.

- Atsidarykite Chrome [pavyzdinį puslapį](debugging/index.html).
- Įjunkite kūrėjo įrankius paspaudami `key:F12` (Mac: `key:Cmd+Opt+I`).
- Pasirinkite panelį `Sources`.

Štai ką turėtumėte pamatyti, jeigu tai darote pirmą kartą:

![](chrome-open-sources.svg)

Perjungimo mygtukas (ang. toggle button) <span class="devtools" style="background-position:-172px -98px"></span> atidaro kortelę su dokumentais.

Paspauskime ir pasirinkime `hello.js` detalaus vaizdo struktūroje. Štai kas turėtų pasirodyti:

![](chrome-tabs.svg)

Matome tris zonas:

1. **Resursų zona** (ang. Resources zone) pateikia HTML, JavaScript, CSS ir kitų dokumentų sąrašą, įskaitant ir prie puslapio pridėtus paveikslus. Chrome papildiniai (ang. extensions) taip pat gali čia pasirodyti.
2. **Šaltinio zona** (ang. Source zone) parodo šaltinio kodą.
3. **Informacinė ir kontrolės zona** (ang. Information and control zone) yra skirta klaidų taisymui, mes ją greitai tyrinėsime.

Dabar galite vėl paspausti tą patį perjungimo mygtuką <span class="devtools" style="background-position:-172px -122px"></span>, kad paslėptumėte resursų sąrašą ir duotumėte kodui šiek tiek vietos.

## Konsolė (ang. Console)

Jeigu paspausime `key:Esc`, tada apačioje atsidarys konsolė. Ten galime rašyti komandas ir paspaudę `key:Enter` jas įvykdyti.

Kai teiginys yra įvykdomas, jo rezultatai parodomi apačioje.

Pavyzdžiui, čia `1+2` rezultatas yra `3`, o `hello("išriktuotojau")` neduoda nieko, tad rezultatas yra `undefined`:

![](chrome-sources-console.svg)

## Lūžio taškai (ang. Breakpoints)

Ištirkime kas vyksta su kodu [pavyzdiniame puslapyje](debugging/index.html). Dokumente `hello.js`, paspauskite ant eilutės numeris `4`. Taip, būtent ant skaičiaus `4`, ne ant pačio kodo.

Sveikiname! Jūs ką tik nustatėte lūžio tašką. Prašau, taip pat paspauskite ant skaičiaus `8` eilutei.

Turėtų atrodyti taip, (mėlyna aprodo kur jums reikia paspausti):

![](chrome-sources-breakpoint.svg)

*Lūžio taškas* yra ta kodo vieta kur išriktavimas automatiškai stabtelės JavaScript įvykdymą.

Kol kodas yra pristabdytas, mes galėsime peržvelgti esamus kintamuosius, įvykdyti komandas konsolėje ir t.t. Kitaip sakant galėsime jį išriktuoti (taisyti klaidas).

Mes visada galėsime surasti lūžio taškus panelyje dešinėje. Tai yra naudinga kai turime skirtingus lūūžio taškus, skirtinguose dokumentuose. Tai mums leidžia:
- Greitai peršokti prie lūžio taško kode (paspaudami jį panelyje dešinėje).
- Laikinai atjungti lūžio tašką atžymint jo varnelę.
- Panaikinti lūžio tašką paspaudžiant dešinį pelės mygtuką ir pasirenkant pašalinti (ang. Remove).
- ...Ir taip toliau.

```smart header="Sąlyginiai lūžio taškai"
*Dešnio mygtuko paspaudimas* ant eilės skaičiaus leidžia sukurti *sąlyginį* lūžio tašką. Jis paleidžiamas tik tokiu atveju kai yra duota išraiška yra tiesa (ang truthy).

Tai labai naudinga kai mums reikia stabtelėti tik dėl tam tikro kintamojo vertės arba dėl tam tikrų funkcijos parametrų.
```

## Išriktuotojo komanda (ang. Debugger command)

Mes taip pat galime stabtelėti kodą naudodami `debugger` komandą jame, kaip ši:

```js
function hello(name) {
  let phrase = `Hello, ${name}!`;

*!*
  debugger;  // <-- išriktuotojas čia sustoja
*/!*

  say(phrase);
}
```

Tai yra labai naudinga kai mes esame kodo redaktoriuje ir nenorime pereiti prie naršyklės bei sukurti lūžio tašką per klaidų taisymo įrankius. 


## Sustokite ir apsižvelgykite

Mūsų pavyzdyje, `hello()` iškviečiamas paleidžiant puslapį, tad lengviausias būdas aktyvuoti išriktuotoja (kai mes pasirinkome lūžio taškus) yra perkraunant puslapį. Tad paspauskime mygtuką `key:F5` (Windows, Linux) arba `key:Cmd+R` (Mac).

Kai lūžio taškai yra nustatyti, įvykdymas stabteli prie ketvirtos eilės:

![](chrome-sources-debugger-pause.svg)

Prašau, atidarykite informacinius išsiskleidžiančius meniu dešinėje (pažymėtus rodyklėmis). Jie leis jums ištirti esamo kodo padėtį:

1. **`Watch` (stebėjimas) -- parodo esamas vertes bet kokioms išraiškoms.**

    Jūs galite paspausti `+` ir įvesti išraišką. Išriktuotojas parodys jos vertę bet kuriuo momentu, automatiškai perskaičiuodamas įvykdymo proceso metu.

2. **`Call Stack` (iškvietimo eiliškumas) -- parodo matrioškinių šaukinių grandinę (ang. nested calls chain).**

    Esamu momentu išriktuotojas yra `hello()` šaukinio  viduje, iškviesto skripto `index.html` pagalba (viduje nėra jokios funkcijos, tad jis vadinamas "anoniminiu").

    Jeigu paspausite ant iškvietimo eilės (pvz. "anonymous"), išriktuotojas peršoks prie atitinkamo kodo ir tada visi jo kintamieji gali būti ištirti. 
3. **`Scope` (apimtis) -- esami kintamieji.**

    `Local` (vietiniai) parodo vietinių funkcijų kintamuosius. Jūs taip pat galite pamatyti jų vertes paryškintas šaltinyje. 

    `Global` (globalūs) turi globalius kintamuosius (iš bet kurios funkcijos).

    Taip pat yra raktažodis `this`, kurio dar nesimokinome, bet greitu laiku tai padarysime.

## Sekant įvykdymą

Dabar laikas *sekti* skriptą.

Tam yra mygtukai dešinio panelio viršuje. Panaudokime juos.
<!-- https://github.com/ChromeDevTools/devtools-frontend/blob/master/front_end/Images/src/largeIcons.svg -->
<span class="devtools" style="background-position:-146px -168px"></span> -- "Resume" (tęsti): tęskite įvykdymą, mygtukas `key:F8`.
: Vykdymas tęsiamas. Jeigu nėra papildomų lūžio taškų, tad vykdymas tiesiog vyksta toliau ir išriktuotojas netenka kontrolės.

    Štai ką galime pamatyti paspausdami ant jo:

    ![](chrome-sources-debugger-trace-1.svg)

    Įvykdymas tęsiamas, pasiekiamas kitas lūžio taškas viduje `say()` ir ten pristabdomas. Pažiūrėkite į "Call Stack" dešinėje. Jis pasipildė dar vienu šaukiniu. Dabar mes esame `say()` viduje.

<span class="devtools" style="background-position:-200px -190px"></span> -- "Step" (žingsniuoti): paleiskite sekančią komandą, mygtukas `key:F9`.
: Paleiskite sekantį teiginį. Jeigu jį paspausime dabar, bus parodytas įspėjimas `alert`.

    Spaudžiant jį vėl ir vėl pažingsniui pereisime visus skripto teiginius.

<span class="devtools" style="background-position:-62px -192px"></span> -- "Step over" (peržengti): paleiskite komandą, bet *neikite į funkciją*, mygtukas `key:F10`.
: Panašu į prieš tai buvusią "Žingsnio" komandą, bet elgiasi kitaip, jeigu sekantis teiginys yra funkcijos išvkietimas. Tai yra: ne iš anksto sutvertas kaip `alert`, bet mūsų pačių funkcija.

    Komanda "Step" prasideda ir stabteli prie pirmos eilės vykdymo, tuo tarpu "Step over" įvykdo matrioškines funkcijas slapta, praleidžiant vidines funkcijas.

    Vykdymas tada automatiškai sustabdomas po tos funkcijos.

    Tai yra gerai, jeigu mums nėra įdomu kas vyksta funkcijos šaukinio viduje.

<span class="devtools" style="background-position:-4px -194px"></span> -- "Step into" (įžengti), mygtukas `key:F11`.
: Šis panašus į "Step", bet elgiasi kitaip kai yra šaukiama asinchroninė funkcija. Jeigu dar tik pradeda mokintis JavaScript, tad nekreipkitė dėmesio į skirtumą, nes mes dar nenaudojome asinchroninių šaukinių.

    Ateičiai žinokite, kad "Step" komanda ignoruoja async veiksmus, tokius kaip `setTimeout` (suplanuotas funkcijos šaukimas), kuris įvykdomas vėliau. "Step into" eina į kodo vidų, laukdami jeigu reikia. Žiūrėkite daugiau [DevTools manual](https://developers.google.com/web/updates/2018/01/devtools#async).

<span class="devtools" style="background-position:-32px -194px"></span> -- "Step out" (išeiti): tęsti vykdymą iki esamos funkcijos pabaigos, mygtukas `key:Shift+F11`.
: Tęsti vykdymą ir sustoti pačioje paskutinėje esamos funkcijos eilėje. Tai yra naudinga kai atsitiktinai patekome į matrioškinį šaukimą naudodami <span class="devtools" style="background-position:-200px -190px"></span>, bet mūsų jis nedomina ir mes norime atsidurti jo pabaigoje kaip galima greičiau.

<span class="devtools" style="background-position:-61px -74px"></span> -- įjungti/išjungti (ang. enable/disable) visus lūžio taškus.
: Šis mygtukas vykdymo neišjugina. Tik masiškai išjungia/įjungia visus lūžio taškus.

<span class="devtools" style="background-position:-90px -146px"></span> -- įjungti/išjungti automatinius stabtelėjimus esant klaidai.
: Kai įjungtas, išriktuotojo įrankiai yra atviti, skripto klaida automatiškai stabteli vykdymą. Tada galima analizuoti kintamuosius ir rasti kas įvyko ne taip. Tad jeigu mūsų skriptas miršta su klaida, mes galime ją išriktuoti. Įjunkite šį pasirinkima ir paleiskite puslapį iš naujo, kad pamatytumėte kur jūsų kodas miršta ir kas tuo metu vyksta.

```smart header="Continue to here"
Right click on a line of code opens the context menu with a great option called "Continue to here".

That's handy when we want to move multiple steps forward to the line, but we're too lazy to set a breakpoint.
```

## Logging

To output something to console from our code, there's `console.log` function.

For instance, this outputs values from `0` to `4` to console:

```js run
// open console to see
for (let i = 0; i < 5; i++) {
  console.log("value,", i);
}
```

Regular users don't see that output, it is in the console. To see it, either open the Console panel of developer tools or press `key:Esc` while in another panel: that opens the console at the bottom.

If we have enough logging in our code, then we can see what's going on from the records, without the debugger.

## Summary

As we can see, there are three main ways to pause a script:
1. A breakpoint.
2. The `debugger` statements.
3. An error (if dev tools are open and the button <span class="devtools" style="background-position:-90px -146px"></span> is "on").

When paused, we can debug - examine variables and trace the code to see where the execution goes wrong.

There are many more options in developer tools than covered here. The full manual is at <https://developers.google.com/web/tools/chrome-devtools>.

The information from this chapter is enough to begin debugging, but later, especially if you do a lot of browser stuff, please go there and look through more advanced capabilities of developer tools.

Oh, and also you can click at various places of dev tools and just see what's showing up. That's probably the fastest route to learn dev tools. Don't forget about the right click and context menus!
