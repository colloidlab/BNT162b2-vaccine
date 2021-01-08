---
title: "Reverzni inženiring izvorne kode cepiva BioNTech/Pfizer proti SARS-CoV-2"
date: 2020-12-25T20:12:20+01:00
draft: false
images:
 - bnt162b2.png
---
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@powerdns_bert">
<meta name="twitter:creator" content="@powerdns_bert">
<meta name="twitter:title" content="Reverse Engineering the source code of the BioNTech/Pfizer SARS-CoV-2 Vaccine">
<meta name="twitter:description" content="Welcome! In this post, we'll be taking a character-by-character look at the source code of the BioNTech/Pfizer SARS-CoV-2 mRNA vaccine.">
<meta name="twitter:image" content="https://berthub.eu/articles/bnt162b2.png">

**Translations**: [ελληνικά](https://berthub.eu/articles/posts/greek-reverse-engineering-source-code-of-the-biontech-pfizer-vaccine/)
/ [عربى](https://docs.google.com/document/d/17IEvUBHZnx-Yf-sPoGzih_pAr4eemBmXUplOd0WtWk4/edit)
/ [中文](https://mp.weixin.qq.com/s/b0Mw8uKLYuXHJ5Bj3t2Dwg)
/ [粵文](https://medium.com/@it9gamelog/reverse-engineering-biontech-pfizer-bnt162b2-2ce758508fb4)
/ [bahasa Indonesia](https://berthub.eu/articles/posts/merekayasa-balik-kode-sumber-vaksin-sars-cov-2-biontech-pfizer/)
/ [Català](https://www.webscatalunya.com/blog-disseny-web/programacio/enginyeria-inversa-del-codi-font-de-la-vacuna-de-biontech-pfizer-per-la-sars-cov-2/)
/ [Deutsch](https://berthub.eu/articles/posts/german-reverse-engineering-source-code-of-the-biontech-pfizer-vaccine/)
/ [Español](https://berthub.eu/articles/posts/ingenieria_inversa_del_codigo_fuente_de_la_vacuna_de_biontech_pfizer_para_el_sars-cov-2/)
/ [Français](https://renaudguerin.net/posts/explorons-le-code-source-du-vaccin-biontech-pfizer-sars-cov-2/)
/ [עִברִית](https://github.com/chilik/Hebrew-ReversingSARS-CoV-2mRNAVaccine/blob/main/%D7%94%D7%A0%D7%93%D7%A1%D7%94%20%D7%9C%D7%90%D7%97%D7%95%D7%A8%20%D7%A9%D7%9C%20%D7%A7%D7%95%D7%93%20%D7%94%D7%9E%D7%A7%D7%95%D7%A8%20%D7%A9%D7%9C%20%D7%94%D7%97%D7%99%D7%A1%D7%95%D7%9F%20BioNTech%20-%20Pfizer%20SARS-CoV-2.pdf)
/ [עִברִית2](https://madaduhcom.wpcomstaging.com/2020/12/28/mrna_vaccine_programming_language/)
/ [Hrvatski](https://docs.google.com/document/d/1BODRitAvGuDYGZCHU5LY-AkNhs9_1cVDubdRvz-cSPY/edit)
/ [Italiano](https://berthub.eu/articles/posts/italian-reverse-engineering-source-code-of-the-biontech-pfizer-vaccine/)
/ [Nederlands](https://berthub.eu/articles/posts/dutch-reverse-engineering-source-code-of-the-biontech-pfizer-vaccine/)
/ [日本語](https://note.com/yubais/n/n349ab986da42)
/ [日本語 2](https://msakai.github.io/bnt162b2/reverse-engineering-source-code-of-the-biontech-pfizer-vaccine.ja/)
/ [नेपाली](https://onedrive.live.com/view.aspx?resid=9C571BA15BC4287D!15298&ithint=file%2cdocx&authkey=!ALATa2b8xetI7lQ)
/ [Polskie](https://randomseed.pl/rna/reverse-engineering-kodu-zrodlowego-szczepionki-biontech-pfizer-covid-sars-cov-2/)
/ [русский](https://localcrew.ru/reversepfizer) 
/ [Português](https://docs.google.com/document/d/1pDo40DXcpXjzqAUfhFfup50-IQ2Qct-mhLnmRpjFZWM/edit)
/ [Română](https://www.astarostech.com/read/sarscov2-ro/vaccine-mrna.html)
/ [Slovensky](https://dennikn.sk/blog/2205850/ako-funguje-zdrojovy-kod-vakciny-sars-cov-2/) 
/ [Slovenščina](https://berthub.eu/articles/posts/slovene-reverse-engineering-source-code-of-the-biontech-pfizer-vaccine/) 
/ [український](https://texty.org.ua/articles/102631/rekonstrukciya-vyhidnoho-kodu-vakcyny-biontechpfizer-sars-cov-2/)
/ [Markdown for translating](https://raw.githubusercontent.com/berthubert/bnt162b2/master/reverse-engineering-source-code-of-the-biontech-pfizer-vaccine.md)

Pozdravljeni! V tem članku bomo črko po črko pregledali izvorno kodo cepiva
BioNTech/Pfizer SARS-CoV-2 mRNA.

> *Želim se zahvaliti vsem, ki so si vzeli čas in pregledali ta članek in
> preverili pravilnost ter izboljšali berljivost. Za vse napake sem kriv sam, če
> kakšno najdete, jo prosim sporočite na bert@hubertnet.nl ali
> [@PowerDNS_Bert](https://twitter.com/PowerDNS_Bert)*

Cepivo je tekočina, ki jo injiciramo v roko, kako lahko torej govorimo o
njegovi izvorni?

To je dobro vprašanje. Da si lahko bolje predstavljamo o čem govorimo, začnimo
z delčkom izvorne kode cepiva BioNTech/Pfizer, zananega tudi kot
[BNT162b2](https://en.wikipedia.org/wiki/Tozinameran) ali Tozinameran [also known as
Comirnaty](https://twitter.com/PowerDNS_Bert/status/1342109138965422083).

<center>
{{< figure src="/articles/bnt162b2.png" caption="Privih 500 črk v BNT162b2 mRNK. Source: [World Health Organization](https://mednet-communities.net/inn/db/media/docs/11889.doc)">}}
</center>

Digitalna koda je bistvo BNT162b2 mRNK cepiva. Sestavljena je iz 4284 znakov,
kar pomeni da je lahko stlačimo v malo več kot 10 tvitov. Na začetku postopka
priprave cepiva, nekdo pošlje to kodo na DNK tiskalnik (da DNK tiskalnik!), ki
spremeni digitalne bite na disku v prave DNK molekule.

<center>
{{< figure src="/articles/bioxp-3200.jpg" caption="A [Codex DNA](https://codexdna.com/products/bioxp-system/) BioXp 3200 DNA printer" >}}
</center>

Iz tega tiskalnika pridobimo majhne količine DNK, ki skozi veliko bioloških
in kemijskih procesov spremenijo v RNK (več o RNK kasneje), ki konča v steklenički s
cepivom. 30 miligramska doza vsebuje 30 miligramov molekul RNK. Poleg tega,
je mRNK zapakirana v pametno lipidno membrano, ki jo dostavi v naše celice.

RNK je verzija DNK, ki ustreza 'delovnemu spominu'. DNK je biološka oblika
'flash' računalniškega spomina. DNK je zelo stabilna, ima veliko redundance
in je izredno zanesljiva. Podobno kot v računalništvu, se koda ne izvaja direktno
iz flash spomina (DNK), ampak se najprej skopira na hitrejši, bolj vsestranski, a
krhkejši sistem.

V računalništvu je to RAM, v biologiji pa RNK. Podobnost je osupljiva. V nasprotju
s flash spominom, so podatki v RAM-u zelo neobstojni, če ne skrbimo za njih. mRNK
Pfizer/BioNTech cepivo moramo shranjevati v zamrzovalnikih iz istega razloga.

Vsaka črka v molekuli RNK tehta pribljžno 0.53&middot;10⁻²¹ gramov, kar pomeni da
je v vsaki 30 mikogramski dozi cepiva 6&middot;10¹⁶ RNK črk. To je približno 25
petabajtov, kar ustreza 2000 milijard kopijam 4284 znakov, ki sestavljajo izvorno 
kodo cepiva. Dejanskih podatkov je v cepivu zgolj malo več kot en kilobajt.
Celoten virus [SARS-CoV-2](https://www.ncbi.nlm.nih.gov/projects/sviewer/?id=NC_045512&tracks=[key:sequence_track,name:Sequence,display_name:Sequence,id:STD649220238,annots:Sequence,ShowLabel:false,ColorGaps:false,shown:true,order:1][key:gene_model_track,name:Genes,display_name:Genes,id:STD3194982005,annots:Unnamed,Options:ShowAllButGenes,CDSProductFeats:true,NtRuler:true,AaRuler:true,HighlightMode:2,ShowLabel:true,shown:true,order:9]&v=1:29903&c=null&select=null&slim=0) vsebuje 7.5 kilobajtov podatkov.

Kratek uvod
------------------------------
DNK je digitalna koda. Za razliko od računalnikov, kjer uporabljamo 0 in 1, 
življenje uporablja A, C, G in U/T (nukleotide oziroma baze). 

V računalnikih shranjujemo 0 in 1 v obliki naboja, električnega toka, magnetnega
dipola, napetosti, modulacije signala, ali kot spremembe v reflektivnosti.
Torej, 0 in 1 nista neka abstraktna koncepta, ampak živita v obliki elektronov
in drugih fizičnih oblikah.

V naravi so A, C, G in U/T baze shranjene v verigah, ki sestavljajo DNK (ali RNK)
molekule.

V računalništvu, 8 bitov predstavlja en bajt, ki je tipična podatkovna enota.

Narava združuje 3 nukleotide v en kodon, to je tipična enota v biologiji. Kodon
vsebuje 6 bitov informacije (2 bita na en DNK znak, 3 znaki = 6 bitov. Kar
omogoča 2⁶ = 64 različnih kodonov.)

Vse to izgleda do sedaj zelo digitalno. Če ste v dvomih, poglejte
[WHO document](https://mednet-communities.net/inn/db/media/docs/11889.doc) in se
preglejte digitalno kodo z lastnimi očmi.

> *Nadaljno branje je na voljo
> [tukaj](https://berthub.eu/articles/posts/what-is-life/) - tale povezava ('What
> is life') vam bo v pomoč pri razumevenju nadaljnega besedila. V obliki videa
> jo najdete [tukaj](https://berthub.eu/dna).*


Torej, kaj pravzaprav ta izvorna koda naredi?
-------------------------------
Ideja cepiva je, da nauči imunski sistem, kako se obvarovati pred patogenom, tako
da oseba ne zboli. Navadno to storimo z vbrizganjem oslabljenega
virusa. Z dodatkom 'adjuvanta' poženemo imunski sistem v akcijo. Oslabitev virusa
ponavadi zahteva na milijone
[jajc](https://en.wikipedia.org/wiki/Attenuated_vaccine) (ali insektov). Pri tem
postopku je potrebno tudi veliko sreče in zahteva precej časa. Včasih lahko
uporabimo tudi drug (nesoroden) virus za vzpodbuditev imunskega sistema.

Cepivo na osnovi mRNK doseže enak cilj ('natrenira naš imunski sistem'), ampak
z lasersko natančnostjo.

Cepivo vsebuje genetski material, ki vsebuje načrt za slavni 'spike' protein
virusa SARS-CoV-2. S pomočjo premetenih kemijskih trikov, cepivo vnese ta
genetski material v nekatere naše celice.

Te celice potem začnejo proizvajati SARS-CoV-2 'spike' protein, kar požene
naš imunski sistem v akcijo. Produkcija spike proteinov in (pomebno) znaki,
da je nekaj prevzelo nadzor nad našimi celicami, sprožijo močan imunski
odziv na 'spike' protein IN njegov proces proizvodnje.

In to nas pripelje do 95% učinkovitega cepiva.

Izvorna koda!
----------------
[Začnimo na začetku, kar je zelo dobro mesto za začetek](https://youtu.be/jp0opnxQ4rY?t=8).
WHO-jev dokument vsebuje tole pomebno sliko:

<center>
{{< figure src="/articles/vaccine-toc.png"  >}}
</center>

To je na nek način kazalo. Začnimo s 'cap', k je naslikan kot majhna kapa.

Podobno kot na računalniku, ne morete preprosto vstaviti 'opcode' v datoteko
in jo zagnati, tudi biološki operacijski sistem potrebuje 'header-je',
'linker-je' in konvencije klicanja ukazov.

Koda cepiva se začne z nukleotidoma:

```
GA
```

To lahko primerjamo z [DOS in Windows izvršnimi datotekami, ki se začnejo z MZ](https://en.wikipedia.org/wiki/DOS_MZ_executable), ali UNIX skriptami, ki se
začnejo z [`#!`](https://en.wikipedia.org/wiki/Shebang_(Unix)).

V obeh primerih, na računalniku in v celici, se ti dve prvi črki ne izvedeta
(zaženeta), vendar če ju ni, potem se tudi nadaljnja koda ne izvede.

Kapa mRNK molekule ima [več funkcij](https://en.wikipedia.org/wiki/Five-prime_cap#Function).
Na primer, ta kapa označuje, da naša koda prihaja iz jedra celice. V našem
primeru to ni res, ker koda prihaja iz cepiva, vendar na ta način prelisičimo
celico. Kapa daje legitimnost naši kodi, kar jo zaščiti pred uničenjem.

Prva dva nukleotida `GA` sta kemijsko malce drugačna od preostale RNK.
V tem smislu `GA` omogoči zunajpasovno signalizacijo.


5' nekodirajoča regija (5' UTR)
------------------------------------
RNK molekule se lahko berejo zgolj v eno smer. Del kjer se branje začne
se imenuje 5' ali 'five-prime'. Branje se konča na 3' mestu ('three-prime').

Življenje je osnovano na proteinih (in molekulah narejenih s pomočjo proteinov).
Recept za te proteine je shranjen v RNK. Prepis RNK v proteine se imenuje
translacija.

Spodaj je prikazana 5' nekodirajoča regija ('UTR'), ta del ni del proteina:

```
GAAΨAAACΨAGΨAΨΨCΨΨCΨGGΨCCCCACAGACΨCAGAGAGAACCCGCCACC
```

Tu nas čaka prvo presenečenje. Normalna RNK vsebuje baze A, C, G in U. U ustreza
'T' v DNK. Ampak zgoraj vidimo Ψ, zakaj?

To je eden od premetenih delov cepiva. Naše telo uporablja zelo dober
antivirusni sistem. Naše celice so zelo pozorne na tuje RNK molekule in jih
poskušajo uničiti preden se te uspejo prepisati v proteine

To je problematično za naše cepivo, ki se mora izmakniti temu obrambnemu
sistemu. Raziskovalci so z dolgoletnim eksperimentiranjem ugotovili, da
menjava U v RNK z nekoliko spremenjeno molekulo, pretenta naš imunski sistem.

V BioNTech/Pfizer cepivu je tako vsak U zamenjan z 1-metil-3'-pseudouridilil-om,
ki ga označujemo s Ψ. Resnično premetena ideja se skriva v tem, da čeprav ta
zamenjava pomiri imunski sistem, celica še vedno prebere ta del kot U.

Tudi v računalništvu poznamo ta trik - včasih je mogoče
poslati rahlo spremenjeno različico sporočila, ki zmede požarni zid in
varnostne rešitve, vendar ga strežniki še vedno sprejmejo - kar lahko omogoči
vdor v strežnik.

Sedaj pobiramo sadove fundamentalnih raziskav opravljenih v preteklosti.
[Raziskovalci](https://twitter.com/PennMedicine/status/1341766354232365059),
ki so odkrili ta trik s Ψ, so se najprej morali boriti za financiranje njihovega
[dela](https://www.statnews.com/2020/11/10/the-story-of-mrna-how-a-once-dismissed-idea-became-a-leading-technology-in-the-covid-vaccine-race/) in kasneje za objavo v znanstvenih člankih. Sedaj smo jim vsi
lahko hvaležni in prepričan sem, da jih čakajo
[Nobelove nagrade](https://twitter.com/PowerDNS_Bert/status/1329861047168225281).

> Veliko ljudi zanima, ali lahko tudi pravi virus uporabi to Ψ tehniko in
> prelisiči naš imunski sistem?  Na kratko, to je zelo malo verjetno. Narava
> nima mehanizmov, da sintetizira 1-metil-3'-pseudouridilil nukleotide. 
> Virusi uporabljajo mehanizme celic za njihovo razmnoževanje in ta opcija v
> celicah enostavno ne obstaja.  mRNK iz cepiva se hitro razgradi v človeškem
> telesu, in ni možnosti, da bi se Ψ-modificirana RNK začela podvojevati.
> Za več informacij preberite "[No, Really, mRNA Vaccines Are Not Going To Affect Your
> DNA](https://www.deplatformdisease.com/blog/no-really-mrna-vaccines-are-not-going-to-affect-your-dna)"

Dobro, pojdimo nazaj na 5' nekodirajočo regijo. Kakšno funkcijo ima zaporedje
teh 51 črk? Kot večina stvari v naravi, ima tudi to zaporedje več funkcij.

Naše celice *prevajajo* RNK v proteine z posebnim molekulskim ustrojem -
ribosom-om. Ribosom deluje kot 3D tiskalnik za proteine, ki sprejme navodila
v obliki RNK in sintetizira zaporedje aminokislin. To zaporedje se nato zvije
v protein.

<center>
<video controls width="90%" loop>
<source src="/articles/protein-short.mp4" type="video/mp4">
</video>
<br/>
Source: [Wikipedia user Bensaccount](https://commons.wikimedia.org/wiki/File:Protein_translation.gif)
</center>

Ta proces je prikazan zgoraj. Črn trak spodaj je RNK. Trak, ki nastaja v zelenem
delu je nastajajoč protein. Stvari, ki prihajajo in odhajajo iz ribosoma so
aminokisline z nastavki, slednji omogočajo prileganje v RNK. Ribosom se mora
pripeti na RNK, da jo lahko začne brati. Lahko si predstavljate, da ribosom
ne more začeti branja kar nekje na sredini RNK. 5' UTR tako predstavlja mesto,
kjer se branje začne ('landing zone').

Poleg tega, UTR vsebuje tudi meta-podatke: kdaj naj se prepis zgodi? In koliko
naj se prepiše? Za cepivo so uporabili UTR, ki naroči ribosomu naj s
prepisovanjem začne takoj. Ta UTR je osnovan na osnovi [gena za alfa globin](https://www.tandfonline.com/doi/full/10.1080/15476286.2018.1450054). Znano je, da ta gen
robustno proizvede veliko proteinov. V zadnjih letih, so znanstveniki dodatno
optimizirali ta UTR (kot je opisano v WHO dokumentu), tako da uporabljen UTR
ne ustreza čisto alfa globinovemu, ampak izboljšani različici.

Signalni peptid glikoproteina S
---------------------------------
Cilj cepiva je vzpodbuditi celico, da začne proizvajati kopije 'spike' proteina
virusa SARS-CoV-2. Do sedaj smo v izvorni kodi srečali predvsem metapodatke.
Sedaj pa gremo proti dejanski kodi za virusni protein.

Prebiti se moramo še skozi zadnji sloj metapodatkov. Ko ribosom (iz zgornje
animacije) zgradi protein, mora ta protein dobiti navodila, kam oditi. Ta
navodila so zapisana v zaporedju za signalni peptid glikoproteina S (razširjena
vodilna sekvenca).

Na začetku proteina je neke vrste etiketa za naslov, kamor mora ta protein oditi.
V našem primeru signalni peptid pravi, da mora protein oditi iz celice skozi
endoplazemski retikulum.

Signalni peptid je precej kratek, vendar ko pogledamo zaporedje, ki ga kodira,
opazimo razlike med virusno RNK in RNK v cepivu:

(Za lažjo primerjavo sem zamenjal modificiran Ψ nazaj v navadni RNK U)

```
           3   3   3   3   3   3   3   3   3   3   3   3   3   3   3   3
Virus:   AUG UUU GUU UUU CUU GUU UUA UUG CCA CUA GUC UCU AGU CAG UGU GUU
Cepivo:  AUG UUC GUG UUC CUG GUG CUG CUG CCU CUG GUG UCC AGC CAG UGU GUU
               !   !   !   !   ! ! ! !     !   !   !   !   !            
```

Kaj se torej dogaja? Ni naključje, da sem zapisal RNK zaporedje v skupkih
treh črk. Tri črke namreč predstavljajo kodon. Vsak kodon predstavlja kodo
za eno aminokislino. Signalni peptid v cepivu je sestavljen iz *natančno*
enakih aminokislin kot v virusu samem.

Zakaj potem obstajajo razlike v RNK?

Obstaja 4³=64 različnih kodonov, ker imamo 4 različne črke in tri črke
predstavljajo en kodon. Ampak v naravi imamo zgolj 20 različnih aminokislin.
To pomeni, da več različnih kodonov predstavlja enako aminokislino.

Življenje uporablja praktično univerzalno tabelo za pretvorbo RNK kodonov v
aminokisline:


<center>
{{< figure src="/articles/rna-codon-table.png" caption="[Tabela z RNK kodoni](https://en.wikipedia.org/wiki/DNA_and_RNA_codon_tables) (Wikipedia)" >}}
</center>

V tej tabeli lahko opazimo, da so vse spremembe v cepivu *sinonimi* (UUU -> UUC).
RNK v cepivu je drugačna, ampak aminokislinsko zaporedje, ki ga RNK kodira je
enako kot v virusu.

Če pogledamo podrobneje, opazimo, da je večina sprememb v tretji črki kodona,
označeni s '3' zgoraj. Iz zgornje tabele je razvidno, da je črka na mestu '3'
ponavadi nepomembna za večino aminokislin.

Če te spremembe v RNK vodijo do sinonimov, zakaj so potem sploh prisotne?
Podroben pregled zaporedja nam razkrije, da vse spremembe, *razen ene*, pomenijo
več C-jev kot G-jev v mutanti.

Vendar zakaj bi to storili? Kot opisano zgoraj, je naš imunski sistem zelo
pozoren na 'eksogeno' RNK, ki prihaja od zunaj. Da se bi izognili odkritju, smo
'U' že zamenjali s Ψ.

Izkaže se, da telo RNK z [večjo vsebnostjo](https://www.nature.com/articles/nrd.2017.243)
G-jev in C-jev z [večjo učinkovitostjo](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1463026/) 
pretvori v proteine.

V cepivu so tako, na mestih kjer je to mogoče, zamenjali ostale črke z G-ji
in C-ji.


> Zame je zanimivo to, da v *enem* primeru te zamenjave niso naredili. Specifično
> v primeru CCA -> CCU. Če kdo slučajno pozna razlog za to, naj mi ga prosim
> sporoči! Zavedam, se da so nekateri kodoni bolj običajni v človeškem genomu
> kot nekateri drugi, ampak
>[prebral sem tudi](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1006024),
> da to ne vpliva preveč na hitrost translacije.

Spike protein
------------------------
Naslednji 3777 črk v RNK cepiva je podobno optimiziranih z dodatkom veliko C-jev
in G-jev. Ker tu ni prostora, ne bom zapisal celotnega zaporedja, ampak se bomo
osredotočili zgolj na en izjemno poseben del. To je del zaradi katerega cepivo
deluje in nam bo omogočil vrnitev življenja v normalo:

```
                  *   *
          L   D   K   V   E   A   E   V   Q   I   D   R   L   I   T   G
Virus:   CUU GAC AAA GUU GAG GCU GAA GUG CAA AUU GAU AGG UUG AUC ACA GGC
Cepivo:  CUG GAC CCU CCU GAG GCC GAG GUG CAG AUC GAC AGA CUG AUC ACA GGC
          L   D   P   P   E   A   E   V   Q   I   D   R   L   I   T   G
           !     !!! !!        !   !       !   !   !   ! !              
```

Tu lahko opazimo običajne *sinonimne* RNK spremembe. Na primer, v prvem kodonu
vidimo, da je bil CUU zamenjan v CUG. To doda en G v zaporedje cepiva, ki
pomaga povečati proizvodnjo proteinov. Vendar oba kodona CCU in CUG kodirata
isto aminokislino 'L' ali leucin, tako, da ne pride do spremembe aminokislinskega
zaporedja.

Če pogledamo celoten spike protein v cepivu, so vse spremembe sinonimne ... razen
dveh. Ti dve posebni spremembi vidimo v prikazanem delu.

Tretji in četrti kodon zgoraj predstavljata ti spremembi. Aminokislini K in V
sta zamenjani s P ali prolinom. Za 'K' smo potrebovali tri spremembe ('!!!'),
za 'V' pa zgolj dve ('!!').

**Izkaže se, da ti dve spremembi močno povečata učinkovitost cepiva**.

Zakaj? Virusni delec SARS-CoV-2 ima na površini veliko spike proteinov:

<center>
{{< figure src="/articles/sars-em.jpg" caption="[SARS virusni delec](https://en.wikipedia.org/wiki/Severe_acute_respiratory_syndrome_coronavirus) (Wikipedia)" >}}
</center>

Spike-i (roglji, bodice) so pritrjene na 'telo' virusa ('virusna kapsida').
Problem je v tem, da imamo v našem cepivu zgolj spike in ne celotnega virusa.

Nespremenjeni spike, se brez pritrditve na kapsido ne zvije v pravo obliko.
Če bi takšno cepivo injicirali v naše telo, bi razvili imunost za nepravo
obliko spike proteina.

Ker je takšna struktura spike proteina preveč različna od tiste, ki je pritrjena
na virus, cepivo v tem primeru ne bi delovalo dobro.

Kaj lahko storimo? V letu [2017](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5584442/)
so znanstveniki opazili, da če vnesejo dvojno prolinsko substitucijo v SARS-CoV-1
in MERS spike protein, se ta zvije v pravo konformacijo, takšno, ki je prisotna
v virusu samem. To deluje, ker je prolin zelo rigidna aminokislina in deluje kot
nekakšna opornica, ki stabilizira protein v strukturo, ki jo potrebujemo za
dober imunski odziv.

[Raziskovalci](https://twitter.com/goodwish916), ki so
[odkrili](https://twitter.com/KizzyPhD) to zamenjavo, bi morali hoditi na okoli
in si deliti petke. Iz njih bi morala sijati ogromna količina ponosa. [In vse to bi bilo zelo zasluženo](https://twitter.com/McLellan_Lab/status/1291077489566142464). 

> Nova novica! Kontaktirali so me iz [McLellan-ovega
> laboratorija](https://twitter.com/McLellan_Lab/status/1291077489566142464), 
> to je ena izmed skupin, ki je odkrila prolinsko zamenjavo.
> Povedali so mi, da je deljenje petk zaenkrat prestavljeno zaradi pandemije
> in da so veseli, da so njihovi rezultati pripomogli razvoju cepiva.
> Poudarili so tudi, da so k odkritju prispevale druge skupine in raziskovalci.

Konec proteina, naslednji koraki
----------------------------------
Tudi na koncu izvorne kode spike proteina najdemo nekaj sprememb:

```
          V   L   K   G   V   K   L   H   Y   T   s             
Virus:   GUG CUC AAA GGA GUC AAA UUA CAU UAC ACA UAA
Cepivo:  GUG CUG AAG GGC GUG AAA CUG CAC UAC ACA UGA UGA 
          V   L   K   G   V   K   L   H   Y   T   s   s          
               !   !   !   !     ! !   !          ! 
```

Na koncu proteina najdemo 'stop' kodon, tukaj je označen z malim 's'. To je
oznaka, da je protein tukaj konča. Originalni virus uporablja stop kodon UAA,
v cepivu pa najdemo dva UGA stop kodona, verjetno za vsak slučaj.

3' nekodirajoča regija
--------------------------
Na podoben način kot ribosom potrebuje 5' regijo za začetek, na koncu potrebuje
3' regijo, da ve kje končati.

Veliko bi lahko napisal o 3' UTR regiji, ampak bom na tem mestu samo
[citiral Wikipedijo](https://en.wikipedia.org/wiki/Three_prime_untranslated_region): 
"3' nekodirajoča regija igra ključno vlogo v izražanju genov. Izražanje kontrolira
preko vpliva na lokalizacijo, stabilnost in učinkovitost translacije mRNK ...
**Kljub našemu trenutnemu razumevanju 3' UTR, je še vedno veliko neznanega**".

Vemo, da nekatere 3' UTR regije zelo uspešno pospešujejo izražanje proteinov.
Kot je zapisano v dokumentu WHO, je bila 3' UTR regija, ki je uporabljena v
cepivu BioNTech/Pfizer, izbrana iz "amino-terminalnga ojačevalec razcepa (AES)
mRNK in mitohondrijsko kodirano 12S ribosomsko RNK, ki daje RNK stabilnost
in omogoča visoko izražanje proteinov". Kar lahko k temo dodam je samo, bravo!

<center>
{{< figure src="/articles/vaccine.jpg" >}}
</center>


Konec vsegAAAAAAAAAAAAAAAAAAAAAA
----------------------------------------
Konec mRNK je poliadeniliran. Ali povedano bolj enostavno, mRNK se koča z
veliko zaporednih AAAAAAAAAAAAAAAAAAA. Celo mRNK je dovolj leta 2020!

mRNK molekula je lahko uporabljena večkrat, vendar z vsako uporabo izgubi nekaj
A-jev na koncu. Ko A-jev na koncu zmanjka, mRNK izgubi funkcionalnost. Tako, da
'poli-A' rep predstavlja zaščito pred razgradnjo.

Raziskave so pokazale, da je optimalno število A-jev na koncu mRNK cepiva nekje
okoli 120.

Cepivo BNT162b2 se konča z:

```
                                     ****** ****
UAGCAAAAAA AAAAAAAAAA AAAAAAAAAA AAAAGCAUAU GACUAAAAAA AAAAAAAAAA 
AAAAAAAAAA AAAAAAAAAA AAAAAAAAAA AAAAAAAAAA AAAAAAAAAA AAAA
```

To je 30 A-jev, potem nukleotidni linker (GCAUAUGACU), ki mu sledi še 70 A-jev.

Sumim, da gre tukaj za dodatno optimizacijo, ki izboljša izražanje proteina.

Povzetek
-----------
Spoznali smo mRNK zaporedje cepiva BNT162b2 in naučili smo se, čemu so
posamezni deli zaporedja namenjeni: 

 * Kapa 'cap' zagotovi, da RNK izgleda kot normalna mRNK molekula
 * Optimizirana 5' nekodirajoča regija (UTR) poskrbi za boljšo sintezo proteina
 * Optimizirano zaporedje za signalni peptid, ki določa kam bo protein šel
 (100% kopija originalnega virusa)
 * Optimizirano zaporedje za spike protein, z dvema 'prolinskima'
 zamenjavama, ki poskrbita, da ima protein pravo obliko
 * Optimizirana 3' nekodirajoča regija (UTR) poskrbi za boljše izražanje proteina
 * Nekoliko skrivnostni poly-A rep z nepojasnjenim 'linker-jem' je pomemben za
  stabilnost mRNK

Optimizacija kodonov doda tudi precej G in C v mRNK zaporedje. Uporaba Ψ
(1-metil-3'-pseudouridilil) namesto U pretenta imunski sistem, da ta ne
uniči mRNK. mRNK tako nauči naš imunski sistem, da se lahko uspešno
bori proti pravemu virusu.

Nadaljnje branje/viri
-----------------------
V letu 2017 sem imel dvourno predstavitev o DNK, ki jo lahko pogledate
[tukaj](https://berthub.eu/dna). Tako kot ta članek, je tudi predstavitev
namenjena računalničarjem.

Od leta 2001 upravljam spletno stran
[DNK za programerje](https://berthub.eu/amazing-dna).

Všeč vam bo mogoče tudi ta
[uvod v naš neverjeten imunski sistem](https://berthub.eu/articles/posts/immune-system/).

Tudi na mojem [blogu](https://berthub.eu/articles) lahko najdete veliko 
informacij o DNK, SARS-CoV-2 in COVID-u.