# Povzetek

## Interaktivno glasbeno učno okolje

### Uvod

Projekt raziskuje razvoj interaktivnega glasbenega učnega okolja, ki združuje elemente formalnega učenja in kreativnega ustvarjanja. Glavni cilj je omogočiti uporabniku (študentu glasbe ali začetniku), da skozi strukturirane lekcije in praktične naloge postopno razvija razumevanje ritma, intonacije, harmonije in improvizacije. Sistem temelji na principih sprotnega povratnega odziva, gamifikacije in avtomatske analize glasbenih vnosov. Kreativno ustvarjanje se pri uporabniku spodbuje tako, da mu sistem ponuja možnosti dodajanja novih inštrumentov (katerih mogoče še vedno ne zna igrati), beatov ali načinov oblikovanja zvoka za lastne glasbene ideje.

### Cilji in namen sistema

Osnovni namen je raziskati, kako lahko računalniško podprto okolje spodbuja samostojno učenje glasbene teorije brez prisotnosti učitelja in hkrati spodbuja kreativnost pri posamezniku. Ideja je, da se študentu poda možnost ustvarjanja brez kakršnegakoli nadzora in (če je to možno) narediti prostor, kjer naučene koncepte lahko uporablja za svoje ideje, ne da bi pri tem postal svoj lastni samonadzor (Foucault).

### Struktura sistema

Sistem je zasnovan kot dvodelna aplikacija:

1. **Učni del** – nabor kuriranih lekcij z jasno strukturiranimi cilji, vajami in avtomatskim ocenjevanjem. Naloge vključujejo preverjanje intonacije, ritma in osnovne harmonizacije.
2. **Kreativni del** – odprto okolje za eksperimentiranje, kjer lahko uporabnik uporablja virtualne instrumente, looper, metronom in harmonizacijske funkcije za ustvarjanje lastnih motivov in aranžmajev.

### Učni del

Pri kreiranju lekcij je pomembno naslednje:

- lekcije naj bodo primerne za vse ravni znanja - uporaba različnih nivojev težavnosti,
- lekcije so bazirane na detekciji tona in ritma,
- lekcije morajo imeti natančno definirane naloge in glasbene primere opravljenih nalog,
- naloge naj bodo grupirane; v posameznih skupinah uporabnik lahko izbira katere naloge bo opravljal; ko konča ali pribere dovolj točk lahko odpre novo skupino,
- naloge vsebujejo motivacijski mehanizem (točke).

### Kreativni del

Kreativni del naj bo vseboval več različnih funkcionalnosti. Glavna od teh bo looper, na kateri uporabnik lahko posname svojo idejo/motiv. Nato sistem analizira posneto in uporabniku ponuja možnost slojenja drugih inštrumentov, katere lahko 'kupuje' z uporabo točk pridobljenih pri opravljanju lekcij. Te inštrumente lahko nastavlja v druge, komplementarne (ali tudi ne, uporabniku mora biti na voljo čim večja kreativnost) harmonije in ritme tega motiva. Na voljo bo tudi možnost prirejanja beata tej ideji v obliki samplov iz različnih žanrov. Uporabnik bo na koncu lahko svojo posneto idejo izvozil kot audio fajl. Zaželjene so tudi funkcije oglaševalca, kvantizacije, pitch-correctiona in na koncu ponujanja nove glasbe uporabniku, ki je podobna temu, kar on kreira.

### Tehnološka zasnova

Implementacija bo raziskovala uporabo:

- **analize zvočnih signalov** (detekcija višine tona in ritma signala, ki se bo uporabljala tako pri lekcijah kot tudi v kreativnem delu),
- **samplerja**, ki se bo uporabljal za generiranje dodatnih inštrumentov,
- **grafičnega uporabniškega vmesnika** za intuitivno delo z instrumenti in lekcijami,
- **gamifikacijskih mehanizmov** za sledenje napredku in spodbujanje redne uporabe.

### Raziskovalni del

V raziskovalnem delu se bo analiziralo:

- kako gamifikacija vpliva na motivacijo uporabnikov in spodbujanje kreativnosti,
- kako uporabniki prehajajo iz učnega v kreativni del sistema,
- ali uporabniki imajo večjo željo za ustvarjanjem kot po lekcijah in urah v glasbeni šoli.

Pri tem bodo uporabljeni vprašalniki za učitelje in študente ter analiza podatkov o uporabi sistema.

### Pričakovani rezultati

Projekt bo pokazal, v kolikšni meri lahko računalniško okolje nadomesti ali dopolni glasbeno izobraževanje. Poseben doprinos je integracija analitičnih in ustvarjalnih procesov v eno okolje, ki podpira tako učenje osnov kot tudi svobodno eksperimentiranje z zvokom.
