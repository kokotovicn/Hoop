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

### Analiza ritma

Za analizo ritma bo sistem uporabljal tempo-map usklajevanje in napredne metode zaznavanja udarcev (onsetov). Glavne komponente načrta so:

1. **Detekcija onsetov z metodo SuperFlux**  
   Sistem bo izračunal log-frekvenčni spektrogram ter nato uporabil SuperFlux ODF (nadgrajena verzija Spectral Flux algoritma), ki temelji na maksimalnem filtru preko frekvenčnih sosedov in pozitivnih spektralnih razlikah med okvirji. Tak pristop sledi spektralnim trajektorijam in učinkovito zatre lažne onsete, ki nastanejo zaradi vibrata, pri tem pa ostane primeren za uporabo v realnem času.

2. **Usklajevanje z znanim tempo mapom**  
   Če ima vaja vnaprej določen tempo, bo sistem izračunal idealne čase udarcev ter primerjal zaznane onsete z referenčnim ritmičnim omrežjem. Tako se lahko natančno oceni:
   - ali uporabnik ritmično sledi tempu,
   - ali prihaja do sistematičnih odstopanj (prehitevanje, zamujanje),
   - ali se tempo uporabnika postopoma spreminja (ritmični drift).

3. **Analiza subdivizij (osmin, šestnajstink, triol)**  
   Za vsak zaznan onset se izračuna relativni položaj znotraj udarca (t. i. beat-phase). Sistem nato primerja porazdelitev onsetov z različnimi ritmičnimi mrežami (npr. {0, 0.5} za osmine, {0, 0.25, 0.5, 0.75} za šestnajstinke, {0, 1/3, 2/3} za triolne subdivizije). Izbere se tista struktura, ki najbolje pojasni uporabnikov vzorec.

4. **Merjenje ritmične natančnosti in konsistentnosti**  
   Sistem bo izračunal:
   - povprečno časovno odstopanje od idealnega ritma,
   - odstotek pravilno izvedenih udarcev,
   - odstopanja znotraj posamezne fraze ali takta.

5. **Vizualni in tekstovni povratni odziv**  
   Uporabniku se prikaže:
   - graf ritmičnih odstopanj,
   - označeni pravilni in napačni udarci,
   - priporočila za izboljšave.

Analiza ritma tako omogoča natančno oceno uporabnikovega ritmičnega občutka, podpira adaptivne lekcije in pomaga pri ustvarjalnem delu, kjer je pravilno časovno umeščanje ključnega pomena.

### Analiza višine tona


Za analizo višine tona bo sistem uporabil kognitivno voden večglasni model, zasnovan po principih Li et al. (2022), vendar optimiziran za hitro in natančno uporabo v kratkih posnetkih.


#### 1. Spektralna predobdelava (CQT)
Najprej se zvočni signal pretvori v logaritemski frekvenčni prostor z uporabo Constant‑Q Transform (CQT). Takšna pretvorba omogoča glasbeno poravnavo binov z dejanskimi toni, kar izboljša nadaljnjo analizo.

#### 2. Harmonične predloge in instrumentno-specifični modeli
Uporabnik na začetku izbere svoj inštrument, kar sistemu omogoča uporabo vnaprej definiranih harmoničnih predlog za posamezne note. 

#### 3. NNLS (Non‑Negative Least Squares)
Spekter posnetka \(S\) se nato razstavi na aktivacije posameznih predlog z uporabo NNLS. Metoda poišče nabor pozitivnih uteži, ki najbolje pojasnijo trenutni spekter. Tako dobimo seznam aktivnih tonov in njihovo relativno moč.

#### 4. Harmonična in časovna stabilizacija
Za odpravo lažnih detekcij se uporabijo:
- preverjanje prisotnosti harmonskih komponent (fundamental + multiplikatorji),
- združevanje aktivacij skozi čas (temporal grouping),
- odstranjevanje kratkih ali naključnih izbruhov.

Pristop združuje elemente glasbene percepcije (kontinuiteta, harmonični kontekst).

#### 5. Prepoznavanje akordov in večglasja
Ker NNLS vrne več aktivnih tonov, lahko sistem prepozna večglasne strukture: intervale, akorde ali razširjene harmonije. Te informacije se nato uporabijo pri ocenjevanju nalog v učnem delu in pri podpori kreativnemu delu (npr. harmonizacija posnetka).

#### 6. Izračun intonacijske natančnosti
Sistem za vsak detektirani ton izmeri:
- odstopanje od idealne frekvence (v centih),
- stabilnost tona skozi čas,
- vpliv vibrata ali glisanda na oceno.

Uporabniku se prikaže graf in besedilni povzetek, ki omogočata razumevanje, ali je bil ton čist, nizek ali previsok.

#### Razlike glede na originalno metodo Li et al. (2022)

Pristop, opisan v tem diplomskem projektu, je neposredno navdihnjen z metodologijo Li et al. (2022), vendar ni popolna implementacija njihovega modela. Spodaj so navedene ključne razlike:

1. **Uporaba NNLS namesto SI‑PLCA**  
   Li et al. uporabljajo *Shift‑Invariant Probabilistic Latent Component Analysis (SI‑PLCA)* kot glavno metodo za razcep CQT-spektrograma na latentne komponente.  
   V tem projektu je namesto iterativne probabilistične dekompozicije uporabljen determinističen postopek *Non‑Negative Least Squares (NNLS)*, ki temelji na vnaprej definiranih harmoničnih predlogah. Gre za metodološko poenostavitev, ki bistveno zmanjša računsko zahtevnost, vendar ohranja koncept harmonične strukture.

2. **Vnaprej definirane harmonične predloge**  
   V članku Li et al. so harmonične razporeditve implicitno naučene preko SI‑PLCA in vodene z dodatnimi utežmi, ki izhajajo iz glasbene kognicije.  
   Tukaj so predloge za vsako noto izračunane *vnaprej*, ločeno za vsak inštrument, kar omogoča hitrejše procesiranje in boljšo kontrolo nad modelom, vendar pomeni, da se predloge ne učijo iz podatkov.

3. **Instrument izbira kot vhodni podatek**  
   Avtorji originalnega članka ne predvidevajo, da uporabnik sam izbere inštrument.  
   V tem projektu to predstavlja pomemben del zasnove: izbrani inštrument določa njegovo harmonično predlogo (decay zakon, število harmonskih komponent, inharmoničnost). Zasnova tako namerno vključuje uporabnikovo vedenje, ki ni prisotno v originalni metodi.

4. **Dodatna analiza intonacijske natančnosti**  
   Li et al. se osredotočajo na zaznavo večglasnih višin in evalvacijo znotraj multi‑pitch metrik (npr. F1, precision/recall).  
   V tem projektu pa sistem za vsako noto izračuna odstopanje v centih, stabilnost tona in vpliv vibrata, kar v članku ni obravnavano in predstavlja razširitev modela glede na potrebe učnega okolja.

Te razlike jasno razmejujejo originalno metodo od njene adaptacije v tem diplomskem projektu ter omogočajo, da je implementacija hkrati teoretično utemeljena in praktično izvedljiva.

### Raziskovalni del

V raziskovalnem delu se bo analiziralo:

- kako gamifikacija vpliva na motivacijo uporabnikov in spodbujanje kreativnosti,
- kako uporabniki prehajajo iz učnega v kreativni del sistema,
- ali uporabniki imajo večjo željo za ustvarjanjem kot po lekcijah in urah v glasbeni šoli.

Pri tem bodo uporabljeni vprašalniki za učitelje in študente ter analiza podatkov o uporabi sistema.

### Pričakovani rezultati

Projekt bo pokazal, v kolikšni meri lahko računalniško okolje nadomesti ali dopolni glasbeno izobraževanje. Poseben doprinos je integracija analitičnih in ustvarjalnih procesov v eno okolje, ki podpira tako učenje osnov kot tudi svobodno eksperimentiranje z zvokom.
