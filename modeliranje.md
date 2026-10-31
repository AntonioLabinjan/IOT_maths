Kada inženjer želi napraviti tempomat za auto, aktivni ovjes ili autonomni dno-dron, ne može odmah spajati žice i dijelove "napamet". Prvo mora na papiru napraviti **matematički model** tog sustava.

---

## 1. Ključni koncepti i intuitivno objašnjenje

U nastavku je objašnjeno kako se stvarni mehanički i električni sustavi prevode u matematiku kroz **preslikavanje analogija**.

---

### A. Mehanički vs. Električni sustavi (Velika Analogija)

Iako mehanički i električni sustavi naizgled nemaju veze jedan s drugim, fizikalni zakoni koji ih opisuju identični su!

| Funkcija u sustavu | Mehanički sustav (Translacijski) | Električni sustav | Matematički opis u $s$-domeni ($Z(s)$) |
| --- | --- | --- | --- |
| **Spremanje energije (Inercija/Magnetsko polje)** | Masa $m$ [kg]

 | Induktivitet / Zavojnica $L$ [H]

 | $Z_m(s) = m \cdot s^2$ ili $Z_L(s) = L \cdot s$

 |
| **Gubitak/Trošenje energije (Prigušenje/Toplina)** | Amortizer $b$ [kg/s]

 | Otpornik $R$ [$\Omega$]

 | $Z_b(s) = b \cdot s$ ili $Z_R(s) = R$

 |
| **Spremanje potencijalne energije (Elastičnost/Naboje)** | Opruga $k$ ili $C$ [kg/s²]

 | Kondenzator $C$ [F]

 | $Z_k(s) = k$ ili $Z_C(s) = \frac{1}{C \cdot s}$

 |
| **Pobuda / Pritisak** | Sila $F(t)$ [N]

 | Napon $U(t)$ [V]

 | $F(s)$ ili $U(s)$

 |
| **Odziv / Odgovor** | Pomak $x(t)$ [m]

 | Struja $I(t)$ [A] ili Napon $U_2(s)$

 | $X(s)$ ili $I(s)$ / $U_2(s)$

 |

---

### B. Elementi s koncentriranim parametrima (Slika 10.1)

Niti jedan auto u stvarnosti nema "idealnu točkastu masu" ili "savršenu oprugu". Cijela šasija je elastična, guma se savija, a ulje u amortizeru mijenja gustoću. No, da bismo izračunali jednadžbe, vršimo **pojednostavljenje (koncentriranje parametara)**:

* Četvrtina mase auta prikazuje se kao jedna masa $m_2$.


* Ovjes (opruga + amortizer) prikazuju se kao idealni koeficijenti $k_2$ i $b$.


* Elastičnost gume prikazuje se kao opruga $k_1$.


* Neravnina na cesti (rupa ili ležeći policajac) prikazuje se kao ulazni signal $u(t)$.



---

### C. Temeljni zakoni za postavljanje jednadžbi

1. **Za Mehaničke sustave (D'Alembertov princip / II. Newtonov zakon):**
Suma svih vanjskih i unutarnjih (inercijalnih, elastičnih, prigušnih) sila na neko tijelo mora biti jednaka nuli:



$$\sum F = 0 \implies F_{\text{vanjska}} - F_m - F_b - F_k = 0$$





2. **Za Električne sustave (Kirchhoffovi zakoni):**
* **Za struje (KZS):** Suma struja koje ulaze u čvor jednaka je sumi struja koje izlaze.


* **Za napone (KZN):** Suma svih padova napona u zatvorenoj petlji jednaka je sumi izvora napona.



$$U_1(t) = U_R(t) + U_L(t) + U_C(t)$$








---

## 2. Detaljno riješeni primjeri iz skripte (Korak-po-korak)

---

### ZADATAK 1: Translacijski mehanički sustav (Primjer P4.1)

**Zadatak:** Zadan je masa-opruga-prigušivač sustav (Slika na stranici 222 skripte). Nađi prijenosnu funkciju $G(s) = \frac{X(s)}{F(s)}$ za zadane parametre: $m = 10\text{ kg}$, $b = 5\text{ kg/s}$, $k = 7\text{ kg/s}^2$.

#### Postupak i objašnjenje:

1. **Postavljanje diferencijalne jednadžbe u vremenskoj domeni ($t$):**
Suma svih sila na masu $m$ jednaka je nuli:



$$f(t) - F_m - F_b - F_k = 0$$



Znajući da je $F_m = m \cdot x''(t)$, $F_b = b \cdot x'(t)$ i $F_k = k \cdot x(t)$:



$$m \cdot x''(t) + b \cdot x'(t) + k \cdot x(t) = f(t)$$





2. Prebacivanje u Laplaceovu $s$-domenu (prema pravilu deriviranja $\mathcal{L}\{x'\} = sX(s)$, $\mathcal{L}\{x''\} = s^2X(s)$):



$$m \cdot s^2 X(s) + b \cdot s X(s) + k \cdot X(s) = F(s)$$





3. Izlučivanje $X(s)$ i oblikovanje prijenosne funkcije $G(s) = \frac{X(s)}{F(s)}$:



$$X(s) \left( m s^2 + b s + k \right) = F(s)$$


$$G(s) = \frac{X(s)}{F(s)} = \frac{1}{m s^2 + b s + k}$$





4. Uvrštavanje zadanih brojčanih vrijednosti ($m=10, b=5, k=7$):



$$G(s) = \frac{1}{10s^2 + 5s + 7}$$






---

### ZADATAK 2: Električni RLC krug (Primjer P4.4.1)

**Zadatak:** Zadan je serijski RLC strujni krug s izlazom na kondenzatoru $U_2(t) = U_C(t)$ (Slika na stranici 229 skripte). Odredi prijenosnu funkciju $G(s) = \frac{U_2(s)}{U_1(s)}$ za $R = 1\,\Omega$, $L = 1\text{ H}$, $C = 2\text{ F}$.

#### Postupak i objašnjenje:

1. Jednadžba po Kirchhoffovom zakonu za napone (KZN):
Ukupni ulazni napon $U_1(s)$ dijeli se na padove napona na otporniku, zavojnici i kondenzatoru:



$$U_1(s) = U_R(s) + U_L(s) + U_C(s)$$





2. Izražavanje napona preko impedancija i struje $I_1(s)$ u $s$-domeni:


* $U_R(s) = R \cdot I_1(s)$


* $U_L(s) = L \cdot s \cdot I_1(s)$


* $U_C(s) = \frac{1}{C \cdot s} \cdot I_1(s)$




Zbroj napona iznosi:

$$U_1(s) = \left( R + L s + \frac{1}{C s} \right) \cdot I_1(s)$$





3. Definiranje izlaznog napona $U_2(s)$U ovom dijelu gradiva iz poglavlja **"10. Matematičko modeliranje sustava"** (autori: Ivan Lorencin, Nikola Anđelić, Zlatan Car) prelazi se s čiste matematike na **fiziku realnih sustava**.



Cilj je naučiti kako stvarne fizikalne komponente (opruge, amortizere, mase, otpornike, zavojnice) prevesti u jednadžbe i postaviti prijenosnu funkciju $G(s)$.

---

## 1. Što je modeliranje i zašto nam treba?

U inženjerstvu se stvarni kompleksni sustavi (poput auta na cesti) pojednostavljuju modelom s **koncentriranim parametrima**.

* **Primjer s početka skripte (Ovjes automobila - Slika 10.1):** Četvrtina auta modelira se kao masa $m_2$, ovjes kao opruga krutosti $k_2$ i amortizer $b$, guma kao masa $m_1$ i opruga $k_1$, a neravnine na cesti su ulazni signal $u(t)$.



---

## 2. Mehanički sustavi (Translacija i Rotacija)

U mehaničkim sustavima imamo 3 osnovna elementa:

| Element | Translacija (Ravnocrtno) | Rotacija (Vrtnja) | Značenje u praksi |
| --- | --- | --- | --- |
| **Masa / Inercija** | Masa $m$

 | Moment inercije $J$

 | Opire se promjeni brzine (akceleraciji).

 |
| **Krutost (Opruga)** | Koeficijent $C$ ili $k$

 | Torzijska krutost $C$ ili $k$

 | Opire se promjeni položaja/pomaka ($\Delta x$ ili $\Delta \theta$).

 |
| **Prigušenje (Amortizer)** | Koeficijent $B$ ili $b$

 | Koeficijent prigušenja $B$ ili $b$

 | Opire se brzini ($\Delta x'$ ili $\Delta \theta'$) i troši energiju.

 |

### Osnovna fizikalna pravila za postavljanje jednadžbi:

1. **Masa (Sila inercije):** $F_{in} = m \cdot x''$ (odnosno $ms^2 X(s)$ u Laplaceovoj domeni).


2. **Prigušivač (Amortizer):** $F_p = b \cdot x'$ (odnosno $bs X(s)$ u Laplaceovoj domeni).


3. **Opruga:** $F_o = k \cdot x$ (odnosno $k X(s)$ u Laplaceovoj domeni).



Ako se opruga ili amortizer nalaze između dva pokretna čvora (npr. čvor 1 s pomakom $x_1$ i čvor 2 s pomakom $x_2$), sila ovisi o **razlici pomaka ili brzina**:


$$F = k(x_1 - x_2) \quad \text{ili} \quad F = b(x_1' - x_2')$$



---

## 3. Električni sustavi i analogija s mehaničkima

U električnim sustavima primjenjuju se **Ohmov zakon** te **Kirchhoffovi zakoni za struje (KZS)** i **napone (KZN)**.

Ključ je prevesti komponente u njihove **impedancije $Z(s)$** u $s$-domeni:

1. **Otpornik ($R$):** $Z_R(s) = R$ *(Analogon prigušivaču $b$)*


2. **Zavojnica / Induktivitet ($L$):** $Z_L(s) = L \cdot s$ *(Analogon masi $m$)*


3. **Kondenzator / Kapacitet ($C$):** $Z_C(s) = \frac{1}{C \cdot s}$ *(Analogon opruzi $k$)*



Pad napona na bilo kojoj impedanciji računa se kao:


$$U(s) = I(s) \cdot Z(s)$$



---

## 4. Detaljno riješeni primjeri iz skripte

---

### PRIMJER 1: Mehanički sustav s masom, oprugom i amortizerom (P4.1)

**Slika sa str. 222 (Slika 10.12/P4.1):** Na masu $m$ odozgo djeluje vanjska sila $f(t)$. Ispod mase su paralelno spojeni amortizer $b$ i opruga $k$ učvršćeni za podlogu.

**Zadani parametri:**

* $m = 10 \text{ kg}$


* $b = 5 \text{ kg/s}$


* $k = 7 \text{ kg/s}^2$



**Traži se:** Prijenosna funkcija $G(s) = \frac{X(s)}{F(s)}$.

#### Postupak korak po korak:

1. **Ravnoteža sila na masu $m$ (II. Newtonov zakon):**
Suma svih sila koje se opiru plus vanjska sila jednaka je 0:



$$F_m + F_b + F_k = f(t)$$





$$m x''(t) + b x'(t) + k x(t) = f(t)$$





2. **Prelazak u Laplaceovu $s$-domenu:**
Derivacije zamjenjujemo sa $s$ ($x' \to sX(s)$, $x'' \to s^2 X(s)$):



$$m s^2 X(s) + b s X(s) + k X(s) = F(s)$$





3. **Izlučivanje $X(s)$:**

$$(m s^2 + b s + k) X(s) = F(s)$$





4. **Prijenosna funkcija $G(s) = \frac{\text{Izlaz}}{\text{Ulaz}} = \frac{X(s)}{F(s)}$:**

$$G(s) = \frac{1}{m s^2 + b s + k}$$





5. **Uvrštavanje brojeva:**

$$G(s) = \frac{1}{10s^2 + 5s + 7}$$






---

### PRIMJER 2: Električni RLC krug (P4.4.1)

**Slika sa str. 229:** Krug s izvorom napona $U_1$, serijski spojenim otpornikom $R$ i zavojnicom $L$, te paralelno spojenim kondenzatorom $C$ na kojem se mjeri izlazni napon $U_2$.

**Zadani parametri:** $R = 1$, $L = 1$, $C = 2$.

**Traži se:** Prijenosna funkcija $G(s) = \frac{U_2(s)}{U_1(s)}$.

#### Postupak korak po korak:

1. Napišemo impedancije elemenata u $s$-domeni:


* $Z_R = R$


* $Z_L = L \cdot s$


* $Z_C = \frac{1}{C \cdot s}$




2. Napon na ulazu $U_1(s)$ (KZN za cijelu petlju):
Ukupna impedancija petlje je zbroj svih serijskih impedancija:



$$Z_{\text{ukupno}} = Z_R + Z_L + Z_C = R + L s + \frac{1}{C s}$$



Struja u krugu je:



$$I_1(s) = \frac{U_1(s)}{Z_{\text{ukupno}}} = \frac{U_1(s)}{R + L s + \frac{1}{C s}}$$





3. **Napon na izlazu $U_2(s)$:**
Izlazni napon $U_2(s)$ mjeri se točno na kondenzatoru $C$:



$$U_2(s) = I_1(s) \cdot Z_C = I_1(s) \cdot \frac{1}{C s}$$





4. **Omjer izlaza i ulaza $G(s)$:**

$$G(s) = \frac{U_2(s)}{U_1(s)} = \frac{\frac{1}{C s}}{R + L s + \frac{1}{C s}}$$


Množenjem brojnika i nazivnika s $C s$ dobivamo standardni oblik:

$$G(s) = \frac{1}{L C s^2 + R C s + 1}$$


5. Uvrštavanje zadanih vrijednosti ($R=1, L=1, C=2$):



$$G(s) = \frac{1}{(1 \cdot 2)s^2 + (1 \cdot 2)s + 1} = \mathbf{\frac{1}{2s^2 + 2s + 1}}$$



Ako imaš bilo kakvih dodatnih pitanja oko pripreme za ispit, sretno s učenjem!
