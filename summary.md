# Master skripta: Laplace, prijenosne funkcije, stabilnost
---

## 0. Cijela priča u 30 sekundi (idiot level)

Sustav je crna kutija: ulaz → **G(s)** → izlaz.

- Diferencijalne jednadžbe u vremenu (t) su teške za rješavati.
- **Laplace** je "prevoditelj": diferencijalnu jednadžbu pretvara u običnu algebru (množenje, dijeljenje, razlomci).
- Riješiš algebru u s-svijetu, pa prevedeš natrag u t-svijet (inverzna transformacija).
- **Polovi** (nultočke nazivnika) odlučuju kako se sustav ponaša i je li stabilan.
- **Hurwitz** je trik za provjeru stabilnosti bez računanja polova.

Analogija: Laplace je kao logaritam. Množenje je teško, pa ga pretvoriš u zbrajanje, zbrojiš i vratiš natrag.

**Tok rada na ispitu:**
1. Pobuda → Laplace (tablica).
2. Y(s) = G(s)·X(s).
3. Rastav na parcijalne razlomke.
4. Inverz (tablica) → y(t).

---

## 1. Laplaceova transformacija (poglavlje 8)

### 1.1 Definicija
F(s) = ∫₀^∞ e^(−st) f(t) dt

Ne računaš je integralom, nego iz **tablice**.

### 1.2 Pobudne funkcije
| Naziv | Oznaka | Laplace |
|---|---|---|
| Step (stepenica) | S(t) = 0 za t<0, 1 za t≥0 | 1/s |
| Dirac (impuls) | δ(t) | 1 |
| Rampa | r(t) = t·S(t) | 1/s² |

### 1.3 Tablica koju moraš znati
| f(t)·S(t) | F(s) |
|---|---|
| 1 | 1/s |
| tⁿ | n!/sⁿ⁺¹ |
| e^(−at) | 1/(s+a) |
| sin(bt) | b/(s²+b²) |
| cos(bt) | s/(s²+b²) |
| e^(−at) sin(bt) | b/((s+a)²+b²) |
| e^(−at) cos(bt) | (s+a)/((s+a)²+b²) |
| t·e^(−at) | 1/(s+a)² |

**Pamćenje:** sin ima b u brojniku, cos ima s. Faktor e^(−at) samo **pomiče s u s+a**.

### 1.4 Pravila
- **Linearnost:** L{af+bg} = aF+bG.
- **Derivacija:** L{f′} = sF − f(0); L{f″} = s²F − s·f(0) − f′(0).
- **Početna vrijednost:** f(0) = lim(s→∞) sF(s).
- **Konačna vrijednost:** f(∞) = lim(s→0) sF(s). Vrijedi samo ako je sustav stabilan.

### 1.5 Primjer A: direktna transformacija
y(t) = 3e^(−2t) + 5 sin(4t)
→ Y(s) = 3/(s+2) + 20/(s²+16)

(Faktor 5 ostaje ispred, sin(4t) daje 4/(s²+16), pa 5·4 = 20.)

### 1.6 Primjer B: diferencijalna jednadžba
6y″ + 48y′ + 192y = S(t), s y(0)=0 i y′(0)=0.

Pošto su početni uvjeti nula, svaki y′ postaje "·s", a y″ postaje "·s²":

Y(s)·(6s² + 48s + 192) = 1/s → **Y(s) = 1/(s(6s²+48s+192))**

### 1.7 Primjer C: inverzna transformacija (rastav na parcijalne razlomke)

**Recept:**
1. Nazivnik faktoriziraj.
2. Za svaki linearni faktor stavi A/(s−p). Za kvadratni faktor sa složenim korijenima stavi (Bs+C)/(kvadrat).
3. Pomnoži s nazivnikom i izjednači koeficijente uz iste potencije s.
4. Kvadrat dovedi u oblik (s+a)²+b² nadopunom do potpunog kvadrata.
5. Očitaj iz tablice.

**Primjer 1:** Y = 1/(s(s+2)) = A/s + B/(s+2)
1 = A(s+2) + Bs → A=½, B=−½
→ **y(t) = ½(1 − e^(−2t))·S(t)**

**Primjer 2 (složeni korijeni):** Y = 25/(s(s²+16s+80))
- Rastav: A = 25/80 = 5/16, B = −5/16, C = −5.
- Nadopuna: s²+16s+80 = (s+8)²+4²
- Rezultat: **y(t) = (5/16)·[1 − e^(−8t)cos(4t) − 2e^(−8t)sin(4t)]·S(t)**
- Provjera: y(0) = 5/16·(1−1) = 0, što je ispravno.

**Trik za brzu provjeru:** y(0) iz teorema o početnoj vrijednosti i y(∞) iz teorema o konačnoj vrijednosti moraju se poklapati s tvojim rješenjem.

---

## 2. Prijenosne funkcije i odzivi (poglavlje 9)

### 2.1 Definicija
G(s) = Y(s)/X(s), dakle **Y(s) = G(s)·X(s)**.

Odziv: y(t) = L⁻¹{G(s)·X(s)}.

**Primjer (obrnuti zadatak):** ulaz je step, izlaz y(t)=e^(−20t).
- X = 1/s, Y = 1/(s+20)
- G = Y/X = **s/(s+20)**

(Skripta ovdje griješi, vidi točku 5.)

### 2.2 Tri standardna odziva
| Pobuda | Y(s) | Naziv odziva |
|---|---|---|
| Step | G(s)/s | skokovni (prijelazna funkcija) |
| Dirac | G(s)·1 | impulsni (težinska funkcija) |
| Rampa | G(s)/s² | nagibni |

**Primjer za G = 1/(s+1):**
- Skokovni: 1/(s(s+1)) = 1/s − 1/(s+1) → **1 − e^(−t)**
- Impulsni: **e^(−t)**
- Nagibni: 1/(s²(s+1)) = −1/s + 1/s² + 1/(s+1) → **−1 + t + e^(−t)**

Impuls je derivacija skoka, a rampa je integral skoka.

**Idiot level:** step je "uključio sam prekidač", impuls je "kratko lupnuo čekićem", rampa je "polako okrećem gas".

### 2.3 Sustav 2. reda: ključni dio za ispit
**G(s) = ωₙ² / (s² + 2ζωₙs + ωₙ²)**

- ωₙ = prirodna frekvencija
- ζ = faktor prigušenja

| ζ | Ponašanje |
|---|---|
| 0 | titra beskonačno (granično stabilan) |
| 0 < ζ < 1 | titra uz smirivanje (podkritično) |
| 1 | najbrži odziv bez prebačaja |
| > 1 | sporo, bez titraja |

**Formule:**
- Prebačaj: P.O. = 100·e^(−ζπ/√(1−ζ²)) %
- Vrijeme prvog maksimuma: **Tₚ = π/(ωₙ√(1−ζ²))**
- Vrijeme smirivanja: Tₛ = 4/(ζωₙ)

**Primjer:** G = 16/(s²+4s+16)
- ωₙ = √16 = 4
- 2ζωₙ = 4 → ζ = 4/8 = 0.5
- P.O. = 100·e^(−0.5π/√0.75) = 16.3 %
- Tₛ = 4/(0.5·4) = 2 s
- Tₚ = π/(4·0.866) = **0.91 s** (skripta daje 0.79, vidi točku 5)

**Idiot level:** ζ je "amortizer". Mali ζ znači auto bez amortizera, koji se ljulja. Veliki ζ znači auto s dobrim amortizerima.

### 2.4 Početna i konačna vrijednost
- y(0) = lim(s→∞) s·G(s)·X(s)
- y(∞) = lim(s→0) s·G(s)·X(s)
- Greška u ustaljenom stanju za step: **e_ss = 1 − y(∞)**

**Primjer:** G = (s+2)/(s²+8s+1), step ulaz.
y(∞) = lim s·G·(1/s) = G(0) = 2/1 = **2**. Pošto je 2 ≠ 1, sustav ne prati zadanu vrijednost: e_ss = 1 − 2 = −1.

**Primjer:** G = (5s+8)/(s³+4s²+25s+18)
y(∞) = G(0) = 8/18, pa e_ss = 1 − 8/18 = 10/18 ≈ **0.56**.

**Brzo pravilo:** za step ulaz je y(∞) = G(0), tj. uvrstiš s=0.

**Početna vrijednost:** ako je stupanj nazivnika veći od stupnja brojnika za 2 ili više, y(0) za step je 0. Za G=(2s+1)/(s³+…) imamo y(0)=0.

### 2.5 Polovi i nule
- **Nule** = korijeni brojnika → G = 0.
- **Polovi** = korijeni nazivnika → G → ∞.

Za kvadrat as²+bs+c vrijedi s = (−b ± √(b²−4ac))/2a.
- Ako je D = b²−4ac > 0, polovi su realni.
- Ako je D < 0, polovi su konjugirano-kompleksni par −σ ± jω.

**Primjer 1:** G = (s+1)/(s²+s+1)
- Nula: s = −1
- Polovi: D = 1−4 = −3 → s = −0.5 ± 0.87j

**Primjer 2:** G = (s+2)/((s+1)(s²+3s+1))
- Nula: −2
- Pol: −1
- Iz s²+3s+1: D = 9−4 = 5 > 0 → **realni** polovi (−3±√5)/2 = −0.38 i −2.62

**Primjer 3:** G = (s²+4s+10)/((s+8)(6s²+12s+59))
- Nule: s = −2 ± j√6 = −2 ± 2.45j
- Polovi: −8 i (−12 ± √(144−1416))/12 = −1 ± 2.97j

**Veza polova i odziva:**
- Realni pol −a daje e^(−at).
- Par −σ ± jω daje e^(−σt)·sin/cos(ωt).

---

## 3. Stabilnost (poglavlje 13)

### 3.1 Definicija
Stabilan sustav se nakon poremećaja vraća u ravnotežu (kuglica u dolini). Granično stabilan sustav je kuglica na ravnoj podlozi. Nestabilan sustav je kuglica na brdu.

### 3.2 Metoda polova
| Položaj polova | Sustav |
|---|---|
| Svi Re{p} < 0 (lijeva poluravnina) | **stabilan** |
| Neki Re{p} = 0 (na osi jω), nijedan desno | **granično stabilan** (oscilira) |
| Barem jedan Re{p} > 0 | **nestabilan** (raste do ∞) |

Stabilnost ovisi **samo o polovima**, nule nisu bitne.

**Primjer 1:** G = (s+2)/(s²+2s+4). Polovi: s = −1 ± j√3. Re = −1 < 0 → **stabilan**.
**Primjer 2:** G = (s+2)/((s−5)(s+1)(s+8)²). Polovi: 5, −1, −8, −8. Pol 5 je pozitivan → **nestabilan**.

### 3.3 Hurwitzov (Routh–Hurwitz) kriterij
Nazivnik: bₙsⁿ + … + b₁s + b₀.

**Korak 1 (nužan uvjet):** svi koeficijenti moraju biti istog predznaka i različiti od nule. Ako ne, nestabilan je odmah.
Primjer: s⁴+12s³−5s²−336s−320 ima negativne koeficijente → **nestabilan**.

**Korak 2 (dovoljan uvjet):** sve Hurwitzove poddeterminante moraju biti > 0.

**Praktična pravila po redu:**
- **2. red** (b₂s²+b₁s+b₀): dovoljno je da su svi koeficijenti > 0.
- **3. red** (b₃s³+b₂s²+b₁s+b₀): svi koeficijenti > 0 **i** **b₂·b₁ > b₃·b₀**.
- 4. i viši redovi: stvarna Hurwitzova matrica (determinante D₁…Dₙ).

### 3.4 Najčešći ispitni zadatak: "za koje K je sustav stabilan"

**Recept:**
1. Napiši zatvoreni krug: G_z = K·G / (1 + K·G).
2. Skrati nazivnike → karakteristični polinom.
3. Primijeni uvjete (koeficijenti > 0 + Hurwitz).
4. Presjek svih uvjeta.

**Primjer 1 (2. red):** blok K·(s+2)/((s+7)(2s+5)) s jediničnom povratnom vezom.
- Nazivnik: (s+7)(2s+5) + K(s+2) = 2s² + (19+K)s + (35+2K)
- Uvjeti: 19+K > 0 → K > −19; 35+2K > 0 → K > −17.5
- Presjek: **K > −17.5**

**Primjer 2 (3. red):** K·400/((s+8)(s²+5s+100))
- (s+8)(s²+5s+100) = s³+13s²+140s+800
- Karakteristični polinom: **s³ + 13s² + 140s + (800+400K)**
- Uvjet 1: 800+400K > 0 → K > −2
- Uvjet 2: 13·140 > 800+400K → 1820−800 > 400K → K < 2.55
- Rezultat: **−2 < K < 2.55**

Ako je K prevelik (npr. 5), sustav je nestabilan: sve jače titra i raste.

**Idiot level:** pojačanje K je kao glasnoća mikrofona uz zvučnik. Premalo ništa ne čuješ, premnogo dobiješ zaglušujući "ŠTRIJA" (nestabilnost). Hurwitz ti kaže točno do koje glasnoće je sigurno.

---

## 4. Cheat sheet za ispit

1. **Pobuda:** step 1/s, impuls 1, rampa 1/s².
2. **Odziv:** Y = G·X, pa rastav na parcijalne razlomke i tablica.
3. **y(0):** lim(s→∞) sY. **y(∞):** lim(s→0) sY (za step y(∞) = G(0)).
4. **Polovi:** nazivnik = 0. **Nule:** brojnik = 0.
5. **Sustav 2. reda:** ωₙ² / (s²+2ζωₙs+ωₙ²), s formulama za P.O., Tₚ i Tₛ.
6. **Stabilnost:** Re{polovi} < 0.
7. **Hurwitz, 3. red:** svi koeficijenti > 0 i b₂b₁ > b₃b₀.
8. **Raspon K:** zatvoreni krug, karakteristični polinom, presjek uvjeta.

---

## 5. Greške u skripti na koje paziš

Autori su sami ostavili oznake "PAZI NA NUMERIRANJE", pa skripta nije dotjerana. Moje ispravke:

1. **P3.1.1:** y=e^(−20t), ali se dalje računa s 1/(s+10). Točno je Y=1/(s+20), pa **G = s/(s+20)**.
2. **Tₚ = π/ωₙ** (9.14) je pogrešno. Točno je π/(ωₙ√(1−ζ²)). Za ζ=0.5 to je 0.91 s, a ne 0.79 s. Slika 9.9 ima vrh oko 0.9 s.
3. **Derivacija (8.9, P2.3):** drugu derivaciju treba pisati s² Y − s·y(0) − y′(0), s minusima. U primjeru P2.3 su stavljeni plusevi, no to ne smeta jer su početni uvjeti nula.
4. **Tablica:** za cosh piše s²/(s²−b²), a treba **s/(s²−b²)**.
5. **P3.3.2 (drugi primjer):** s²+3s+1 ima D=5>0, pa su polovi realni, a ne kompleksni.
6. **P7.3.4:** piše "+400" umjesto "+400K" u nazivniku, a u D₂ piše "800−400K" umjesto "+". Moj račun gore je ispravan i daje isti rezultat (K<2.55).
7. **Hurwitz D₁:** skripta piše D₁=b₁, što bi za polinom 3. reda trebalo biti b₂. Rezultati zadataka ipak izlaze ispravno.
8. **Zadaci za vježbu:** neka rješenja izgledaju sumnjivo (npr. Z3.1 e_ss=0.92, a po formuli 1−G(0) = 1−1/96 ≈ 0.99; Z3.2 s polovima koji ne odgovaraju (s+12)²; Z2.3). **Ne uči rješenja napamet**, nego izračunaj sam prema receptima gore.

---

## 6. Vježba (provjeri se)

1. Pretvori u s-domenu: y(t) = 2t + 3e^(−5t).
2. Inverz od 1/(s(s+4)). *(Rješenje: ¼(1−e^(−4t)))*
3. Za G = 9/(s²+3s+9) odredi ζ, P.O. i Tₛ. *(ωₙ=3, ζ=0.5, P.O.≈16.3 %, Tₛ=4/(0.5·3)≈2.67 s)*
4. Je li s³+2s²+3s+10 stabilan? *(2·3=6 < 1·10=10 → nije)*
5. Za s³+4s²+5s+K nađi raspon K. *(K>0 i 4·5>K → 0<K<20)*
