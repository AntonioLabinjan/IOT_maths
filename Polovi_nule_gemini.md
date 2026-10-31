## 1. Ključni koncepti i značenje (Čemu to služi?)

### A. Prijenosna funkcija $G(s)$

* **Što je:** Matematički model koji u s-domeni (Laplaceovoj domeni) opisuje omjer izlaznog i ulaznog signala sustava uz nulte početne uvjete:



$$G(s) = \frac{Y(s)}{X(s)} \implies Y(s) = G(s) \cdot X(s)$$





* **Zašto nam treba:** U vremenskoj domeni ponašanje sustava opisuje se diferencijalnim jednadžbama (što je matematički složeno za računanje). Prelaskom u Laplaceovu $s$-domenu, diferencijalne jednadžbe postaju obične algebarske jednadžbe (množenje i dijeljenje).

### B. Karakteristični pobudni signali i odzivi $y(t)$

Odziv sustava je ponašanje izlaza u vremenskoj domeni $y(t) = \mathcal{L}^{-1}\{G(s)X(s)\}$ kada na ulaz dovedemo neki pobudni signal $X(s)$.

1. **Jedinična stepenica / skokovni signal ($S(t) \xrightarrow{\mathcal{L}} \frac{1}{s}$):**
* *Značenje:* Trenutačni preklop iz stanja 0 u stanje 1 (npr. paljenje sklopke).


* *Odziv:* **Prijelazna funkcija**. Služi za promatranje kako sustav prelazi iz jednog stacionarnog stanja u drugo.




2. **Jedinični impuls / Diracova delta funkcija ($\delta(t) \xrightarrow{\mathcal{L}} 1$):**
* *Značenje:* Kratkotrajan, izuzetno jak udar (npr. udarac čekićem ili strujni udar).


* *Odziv:* **Težinska funkcija** ($y(t) = \mathcal{L}^{-1}\{G(s)\}$). Opisuje dinamički "otisak prsta" samog sustava.




3. **Nagibna funkcija / Rampa ($r(t) = t \cdot S(t) \xrightarrow{\mathcal{L}} \frac{1}{s^2}$):**
* *Značenje:* Linearno rastući ulaz (npr. postepeno dodavanje gasa ili praćenje vozila koje se giba stalnom brzinom).





### C. Polovi i nule sustava

Zapisivanjem prijenosne funkcije u obliku razlomka polinoma $G(s) = \frac{N(s)}{D(s)}$:

* **Nule ($z_i$):** Rješenja jednadžbe brojnika $N(s) = 0$. To su vrijednosti $s$ za koje je prijenosna funkcija jednaka 0 ($\lim_{s \to z_i} G(s) = 0$). Oni utječu na amplitudu i oblik prijelaznih pojava.


* **Polovi ($p_i$):** Rješenja jednadžbe nazivnika $D(s) = 0$. To su vrijednosti $s$ za koje prijenosna funkcija ide u beskonačnost ($\lim_{s \to p_i} G(s) = \infty$).


* **Zašto su polovi ključni:** Polovi **izravno određuju stabilnost i brzinu sustava**:
* Ako su svi polovi u **lijevoj poluravnini** ($\text{Re}(p_i) < 0$), sustav je **stabilan**.


* Kompleksni polovi ($s = -\sigma \pm j\omega$) uzrokuju **oscilatorno ponašanje**.





### D. Parametri skokovnog odziva sustava 2. reda

Sustav drugog reda standardno se zapisuje kao:


$$G(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$



* $\omega_n$ – Vlastita (prirodna) frekvencija oscilacija.


* $\zeta$ (zeta) – Faktor prigušenja:


* $\zeta > 1$: Aperiodski (preprigušen) odziv, nema oscilacija.
* $0 < \zeta < 1$: Podprigušen odziv – sustav oscilira prije smirivanja.


* $\zeta = 0$: Neoslabljene neprekidne oscilacije.


* Procijenjeni parametri:


1. **Postotak nadvišenja ($P.O.$):** Koliko izlaz "prebaci" konačnu vrijednost:



$$P.O. = 100 \cdot e^{-\frac{\zeta \pi}{\sqrt{1-\zeta^2}}} \quad [\%]$$





2. **Vrijeme prvog maksimuma ($T_p$):** Vrijeme potrebno da odziv dosegne najveću vrijednost:



$$T_p = \frac{\pi}{\omega_n}$$





3. **Vrijeme smirivanja ($T_s$):** Vrijeme nakon kojeg se izlaz trajno zadržava unutar uskog pojasa (obično $\pm 2\%$ ili $\pm 5\%$) oko konačne vrijednosti:



$$T_s = \frac{4}{\zeta \omega_n}$$








### E. Teoremi o graničnim vrijednostima (Početna i konačna vrijednost)

* **Početna vrijednost odziva $y(0)$:** Vrijednost signala u trenutku $t=0^+$:



$$y(0) = \lim_{s \to \infty} s \cdot Y(s) = \lim_{s \to \infty} s \cdot G(s) X(s)$$





* **Ustaljeno stanje $y(\infty)$:** Konačna vrijednost signala u stacionarnom stanju ($t \to \infty$):



$$y(\infty) = \lim_{s \to 0} s \cdot Y(s) = \lim_{s \to 0} s \cdot G(s) X(s)$$





* **Greška u ustaljenom stanju ($e_{ss}$):** Razlika između referentnog ulaza (jedinične stepenice $1$) i ostvarenog izlaza u ustaljenom stanju:



$$e_{ss} = 1 - y(\infty)$$






---

## 2. Riješeni primjeri iz skripte (Korak-po-korak)

### Primjer 1: Određivanje prijenosne funkcije iz zadanog odziva (P3.1.1)



**Zadatak:** Na ulaz sustava doveden je $x(t) = S(t)$. Izlaz je $y(t) = e^{-20t}$. Nađi $G(s)$.

1. Laplace ulaza: $X(s) = \mathcal{L}\{S(t)\} = \frac{1}{s}$.


2. Laplace izlaza: $Y(s) = \mathcal{L}\{e^{-20t}\} = \frac{1}{s+20}$ (u skripti je greška u tipkanju gdje piše $s+10$ u međukoraku).


3. Prijenosna funkcija:

$$G(s) = \frac{Y(s)}{X(s)} = \frac{\frac{1}{s+20}}{\frac{1}{s}} = \frac{s}{s+20}$$






---

### Primjer 2: Skokovni odziv sustava 1. reda (P3.2.1)



**Zadatak:** Odredi skokovni odziv za $G(s) = \frac{1}{s+1}$.

1. Odziv u $s$-domeni: $Y(s) = G(s) \cdot \frac{1}{s} = \frac{1}{s(s+1)}$.


2. Rastav na parcijalne razlomke:



$$\frac{1}{s(s+1)} = \frac{A}{s} + \frac{B}{s+1} \implies 1 = A(s+1) + Bs$$





* Za $s = 0 \implies A = 1$


* Za $s = -1 \implies 1 = B(-1) \implies B = -1$




3. Inverzna Laplaceova transformacija:



$$y(t) = \mathcal{L}^{-1}\left\{\frac{1}{s} - \frac{1}{s+1}\right\} = (1 - e^{-t})S(t)$$






---

### Primjer 3: Impulsni odziv (P3.2.3)



**Zadatak:** Odredi impulsni odziv za $G(s) = \frac{1}{s+1}$. 1. Za impulsni ulaz$XOva skripta detaljno obrađuje **prijenosne funkcije, odzive sustava te polove i nule** u sklopu teorije automatskog upravljanja.

---

## 1. Ključni koncepti i što pojedine stvari predstavljaju

### Prijenosna funkcija $G(s)$

* **Što je:** Matematički model sustava u Laplaceovoj (kompleksnoj) domeni koji opisuje odnos između ulaznog (pobude $X(s)$) i izlaznog signala (odziva $Y(s)$) uz pretpostavku nultih početnih uvjeta.


* **Matematički zapis:**

$$G(s) = \frac{Y(s)}{X(s)} = \frac{\mathcal{L}\{y(t)\}}{\mathcal{L}\{x(t)\}} \quad \Rightarrow \quad Y(s) = X(s) \cdot G(s)$$





* **Zašto nam treba:** U vremenskoj domeni odnos ulaza i izlaza opisuju diferencijalne jednadžbe, što otežava proračun. Laplaceovom transformacijom te jednadžbe prelaze u algebarske (množenje i dijeljenje), što drastično olakšava analizu i sintezu sustava.

---

### Odzivi sustava $y(t)$

Odziv predstavlja vremensko ponašanje izlaza sustava $y(t)$ kada na njegov ulaz dovedemo neki standardni ispitni signal. Izračunava se primjenom **inverzne Laplaceove transformacije**:


$$y(t) = \mathcal{L}^{-1}\{Y(s)\} = \mathcal{L}^{-1}\{G(s) \cdot X(s)\}$$



Karakteristične pobude su:

1. **Jedinična stepenica / skok ($S(t)$ ili $u(t)$):** Modelira naglu promjenu radnog stanja (npr. paljenje sklopke).


* Pobuda u $s$-domeni: $X(s) = \frac{1}{s}$


* Skokovni odziv (prijelazna funkcija): $y(t) = \mathcal{L}^{-1}\left\{\frac{G(s)}{s}\right\}$




2. **Jedinični impuls / Diracova funkcija ($\delta(t)$):** Modelira kratkotrajni, udarni poremećaj.


* Pobuda u $s$-domeni: $X(s) = 1$


* Impulsni odziv (težinska funkcija): $y(t) = \mathcal{L}^{-1}\{G(s)\}$




3. **Nagibna funkcija / Rampa ($r(t) = t \cdot S(t)$):** Modelira linearni porast ulaza.


* Pobuda u $s$-domeni: $X(s) = \frac{1}{s^2}$


* Nagibni odziv: $y(t) = \mathcal{L}^{-1}\left\{\frac{G(s)}{s^2}\right\}$





---

### Parametri skokovnog odziva sustava 2. reda

Generalni oblik sustava drugog reda je:


$$G(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$



* $\omega_n$ – Vlastita (prirodna) frekvencija oscilacija.


* $\zeta$ (zeta) – Faktor prigušenja.



Karakteristični parametri odziva su:

* **Nadvišenje prvog maksimuma ($P.O.$):** Postotak za koji odziv pređe konačnu (ustaljenu) vrijednost.



$$P.O. = 100 \cdot e^{-\frac{\zeta \pi}{\sqrt{1-\zeta^2}}} [\%]$$





* **Vrijeme prvog maksimuma ($T_p$):** Vrijeme potrebno da odziv dosegne prvu vršnu vrijednost.



$$T_p = \frac{\pi}{\omega_n}$$





* **Vrijeme smirivanja ($T_s$):** Vrijeme nakon kojeg izlaz ostaje unutar uskog pojasa (obično $\pm 2\%$ ili $\pm 5\%$) oko ustaljene vrijednosti.



$$T_s \approx \frac{4}{\zeta \omega_n}$$






---

### Granične vrijednosti odziva

* **Početna vrijednost $y(0)$:** Vrijednost odziva u trenutku $t = 0$.



$$y(0) = \lim_{s \to \infty} s \cdot G(s) X(s)$$





* **Ustaljeno stanje $y(\infty)$:** Vrijednost odziva kad prođe prijelazna pojava ($t \to \infty$).



$$y(\infty) = \lim_{s \to 0} s \cdot G(s) X(s)$$





* **Greška u ustaljenom stanju ($e_{ss}$):** Razlika između željenog ulaza i stvarni izlaza za $t \to \infty$. Za jedinčni skok:



$$e_{ss} = 1 - y(\infty)$$






---

### Polovi i nule sustava

Zapisivanjem prijenosne funkcije u obliku omjera polinoma $G(s) = \frac{N(s)}{D(s)}$:

* **Nule ($s_{z}$):** Korijeni brojnika, tj. $N(s) = 0$. Vrijednosti $s$ za koje je $G(s) = 0$.


* **Polovi ($s_{p}$):** Korijeni nazivnika, tj. $D(s) = 0$. Vrijednosti $s$ za koje $G(s) \to \infty$.


* **Zašto su važni:** Polovi **izravno određuju stabilnost i dinamiku sustava** (brzinu odziva, prisutnost oscilacija). Ako svi polovi leže u lijevoj poluravnini kompleksne $s$-ravnine ($\text{Re}(s_p) < 0$), sustav je stabilan. Polovi i nule prikazuju se u $s$-ravnini gdje su nule označene kružićima ($\circ$), a polovi križićima ($\times$).



---

## 2. Detailjno riješeni primjeri iz skripte

### Primjer 1: Određivanje prijenosne funkcije iz poznatog izlaza (P3.1.1)

* **Zadatak:** Na ulaz je doveden $x(t) = S(t)$, a izlaz je $y(t) = e^{-20t}$.


* **Rješenje:**
1. Ulaz u $s$-domeni: $X(s) = \mathcal{L}\{S(t)\} = \frac{1}{s}$.


2. Izlaz u $s$-domeni: $Y(s) = \mathcal{L}\{e^{-20t}\} = \frac{1}{s+20}$ (u skripti je greška u tipkanju u rješenju s $s+10$, ali postupak prati par za $e^{-at}$).


3. Iz definicije $G(s) = \frac{Y(s)}{X(s)}$:



$$G(s) = \frac{\frac{1}{s+20}}{\frac{1}{s}} = \frac{s}{s+20}$$








---

### Primjer 2: Skokovni odziv sustava 1. reda (P3.2.1)

* **Zadatak:** Izračunaj skokovni odziv za $G(s) = \frac{1}{s+1}$.


* **Rješenje:**
1. $Y(s) = G(s) \cdot \frac{1}{s} = \frac{1}{s(s+1)}$


2. Rastav na parcijalne razlomke:



$$\frac{1}{s(s+1)} = \frac{A}{s} + \frac{B}{s+1} \quad \Rightarrow \quad 1 = A(s+1) + Bs = (A+B)s + A$$





* Uz $s^0$: $A = 1$


* Uz $s^1$: $A + B = 0 \Rightarrow B = -1$




3. Inverzna Laplaceova transformacija:



$$y(t) = \mathcal{L}^{-1}\left\{\frac{1}{s} - \frac{1}{s+1}\right\} = (1 - e^{-t})S(t)$$








---

### Primjer 3: Izračun parametara skokovnog odziva (P3.2.5)

* **Zadatak:** Za $G(s) = \frac{16}{s^2 + 4s + 16}$ odredi parametre $P.O.$, $T_p$ i $T_s$.


* **Rješenje:**
1. Usporedba s općim oblikom $G(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$:


* $\omega_n^2 = 16 \Rightarrow \omega_n = 4\text{ rad/s}$


* $2\zeta\omega_n = 4 \Rightarrow 2\zeta(4) = 4 \Rightarrow \zeta = 0.5$




2. Vrijeme prvog maksimuma:



$$T_p = \frac{\pi}{\omega_n} = \frac{\pi}{4} \approx 0.795\text{ s}$$





3. Postotak nadvišenja:



$$P.O. = 100 \cdot e^{-\frac{0.5\pi}{\sqrt{1-0.5^2}}} = 100 \cdot e^{-\frac{0.5\pi}{\sqrt{0.75}}} \approx 16.3\%$$





4. Vrijeme smirivanja:



$$T_s = \frac{4}{\zeta \omega_n} = \frac{4}{0.5 \cdot 4} = 2\text{ s}$$








---

### Primjer 4: Početna vrijednost i greška u ustaljenom stanju

* **Početna vrijednost (P3.2.4):**
Za $G(s) = \frac{2s+1}{s^3+4s^2+2s+1}$ uz pobudu $X(s) = \frac{1}{s}$:



$$y(0) = \lim_{s \to \infty} s \cdot \frac{2s+1}{s(s^3+4s^2+2s+1)} = \lim_{s \to \infty} \frac{2s+1}{s^3+4s^2+2s+1} = 0$$





* **Odziv u ustaljenom stanju i greška (P3.2.6):**
Za $G(s) = \frac{5s+8}{s^3+4s^2+25s+18}$:



$$y(\infty) = \lim_{s \to 0} s \cdot \frac{5s+8}{s^3+4s^2+25s+18} \cdot \frac{1}{s} = \frac{8}{18}$$





$$e_{ss} = 1 - y(\infty) = 1 - \frac{8}{18} = \frac{10}{18} \approx 0.56$$






---

### Primjer 5: Određivanje polova i nula (P3.3.1)

* **Zadatak:** $G(s) = \frac{s+1}{s^2+s+1}$


* **Rješenje:**
1. **Nule:** Brojnik $= 0 \Rightarrow s+1 = 0 \Rightarrow s_z = -1$


2. **Polovi:** Nazivnik $= 0 \Rightarrow s^2+s+1 = 0$


$$s_{p1,2} = \frac{-1 \pm \sqrt{1^2 - 4 \cdot 1 \cdot 1}}{2} = \frac{-1 \pm \sqrt{-3}}{2} = -0.5 \pm 0.866j$$





3. Prikaz u $s$-ravnini: Nula je na realnoj osi u $(-1, 0)$, a polovi su konjugirano-kompleksni par u $(-0.5, \pm 0.87j)$.


Ovo je tema u kojoj apstraktne matematičke formule (poput $s$-domene i Laplacea) često djeluju nepovezano sa stvarnim svijetom. Zaboravimo nakratko teške jednadžbe i objasnimo sve preko opipljivih sustava iz svakodnevnog života – poput **automobila, sustava za grijanje ili tempomata**.

---

## 1. Što je što? (Povezivanje s realnim svijetom)

### A. Prijenosna funkcija $G(s)$ — "Crna kutija" ili DNK sustava

* **Što predstavlja:** Matematički "recept" koji nam govori kako se neki sustav ponaša.
* **Analagija:** zamisli da pritisneš papučicu gasa u automobilu do pola (to je **ulaz $X(s)$**). Auto ne poleti odmah do $100\text{ km/h}$, nego postepeno ubrzava dok ne postigne stacionarnu brzinu (to je **izlaz $Y(s)$**). Prijenosna funkcija $G(s)$ je zapravo opis same fizike auta – mase, otpora zraka i motora – koja određuje *koliko brzo* i *na koji način* auto reagira na taj pritisak gasa.


* **Zašto $s$-domena?** U realnom vremenu ($t$) morali bismo rješavati teške diferencijalne jednadžbe. Pretvaranjem u Laplaceovu $s$-domenu, računanje se svodi na najobičnije množenje i dijeljenje razlomaka.



---

### B. Karakteristični ulazi i odzivi — "Ispitivanje sustava"

Da bismo saznali kakav je neki sustav, na ulaz mu dovodimo tri tipična signala:

1. **Skokovni odziv (Jedinična stepenica / Step):**
* **Što je:** Trenutačni preklop ulaza s $0$ na $1$.


* **Primjer:** Naglo stisneš sklopku za grijanje u sobi ili postaviš tempomat u autu sa $0$ na $100\text{ km/h}$.
* **Zašto nam treba:** Da vidimo koliko brzo sustav prelazi iz starog u novo stanje i prebacuje li zadanu vrijednost.




2. **Impulsni odziv (Diracov impuls):**
* **Što je:** Izuzetno jak, trenutačni udarac (traje 0 sekundi).


* **Primjer:** Udarac čekićem po konstrukciji ili nagli nalet vjetra na dron u zraku.
* **Zašto nam treba:** Govori nam o "prirodnoj dinamici" sustava – kako se sam od sebe primiri nakon šoka.




3. **Nagibni odziv (Rampa):**
* **Što je:** Linearno i konstantno rastući ulaz.


* **Primjer:** Lagano i ravnomjerno dodavanje gasa pri vožnji uzbrdo.
* **Zašto nam treba:** Služi za provjeru koliko dobro sustav prati metu koja se stalno giba.





---

### C. Polovi i Nule — "Upravljačke poluge sustava"

Kada prijenosnu funkciju napišemo kao razlomak dvoju polinoma $G(s) = \frac{N(s)}{D(s)}$:

* **Polovi ($D(s) = 0$):** Rješenja nazivnika.


* **Analagija:** Polovi su **srce i priroda sustava**. Oni određuju hoće li auto oscilirati (ljuljati se), hoće li brzo ubrzati te hoće li sustav biti **stabilan ili skrenuti u kaos**.
* Ako je pol u **negativnom dijelu** (npr. $s = -2$), odziv se smiruje (stabilan sustav). Ako je u **pozitivnom dijelu** (npr. $s = +2$), odziv neprekidno raste do uništenja (nestabilan sustav).


* **Nule ($N(s) = 0$):** Rješenja brojnika.


* **Analagija:** Nule djeluju kao "fino podešavanje". One mijenjaju visinu oscilacija i amplitudu odziva, ali ne mogu promijeniti temeljnu stabilnost sustava.





---

### D. Parametri skokovnog odziva (Odziv sustava drugog reda)

Kada zadas naredbu tempomatu na $100\text{ km/h}$, auto neće trenutačno skočiti na tu brzinu. Reakcija izgleda ovako:

```
 Brzina [km/h]
   ^
120|             /---\  <-- Nadvišenje (P.O.) - prebacio je zadanu brzinu!
100|------------/-----\------------------ <-- Zadani ulaz (100 km/h)
   |           /       \_______/~~~~~~~  <-- Smirivanje oko 100 km/h
 0 +-----------------------------------> Vrijeme [s]
              |               |
             Tp               Ts

```

* **$\zeta$ (Faktor prigušenja):** Otpor sustava oscilacijama. Ako je prigušenje malo ($\zeta < 1$), auto će "prebaciti" $100\text{ km/h}$, malo oscilirati gore-dolje pa se smiriti.


* **$P.O.$ (Postotak nadvišenja):** Koliko je posto izlaz otišao *iznad* željene vrijednosti. (Npr. umjesto $100\text{ km/h}$ dosegne $116\text{ km/h}$, pa je $P.O. = 16\%$).


* **$T_p$ (Vrijeme maksimuma):** Trenutak u kojem se dogodilo to najveće nadvišenje.


* **$T_s$ (Vrijeme smirivanja):** Trenutak nakon kojeg se vožnja konačno umiri i drži zadanu brzinu.



---

## 2. Detaljno riješeni praktični primjeri

Pogledajmo kako izračunati ove parametre korak po korak na zadacima iz skripte.

---

### ZADATAK 1: Analiza auta/tempomata (Parametri odziva - P3.2.5)

**Zadana je prijenosna funkcija:**


$$G(s) = \frac{16}{s^2 + 4s + 16}$$



**Pitanje:** Kakvo će biti ponašanje odziva? Izračunaj nadvišenje $P.O.$, vrijeme maksimuma $T_p$ i vrijeme smirivanja $T_s$.

#### Postupak i objašnjenje:

1. Usporedba s općim matematičkim modelom 2. reda:
Opći oblik glasi: $G(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$.


2. Izvlačenje fizičkih parametara:


* Pogledamo član bez $s$ u nazivniku: $\omega_n^2 = 16 \implies \mathbf{\omega_n = 4\text{ rad/s}}$ (prirodna frekvencija).


* Pogledamo član uz $s$: $2\zeta\omega_n = 4$.
Uvrstimo $\omega_n = 4$:



$$2 \cdot \zeta \cdot 4 = 4 \implies 8\zeta = 4 \implies \mathbf{\zeta = 0.5}$$



(Budući da je $\zeta = 0.5 < 1$, sustav je podprigušen i imat će oscilacije).




3. Izračun karakteristika ponašanja odziva:


* **Vrijeme prvog skoka/maksimuma ($T_p$):**

$$T_p = \frac{\pi}{\omega_n} = \frac{3.14159}{4} \approx \mathbf{0.79\text{ s}}$$



(Auto će prvi vrhunac brzine dosegnuti za 0.79 sekundi).


* **Postotak nadvišenja ($P.O.$):**

$$P.O. = 100 \cdot e^{-\frac{\zeta \pi}{\sqrt{1-\zeta^2}}} = 100 \cdot e^{-\frac{0.5 \cdot 3.14159}{\sqrt{1 - 0.5^2}}} = 100 \cdot e^{-\frac{1.5708}{\sqrt{0.75}}} = 100 \cdot e^{-1.8138} \approx \mathbf{16.3\%}$$



(Sustav će prebaciti zadanu vrijednost za $16.3\%$).


* **Vrijeme smirivanja ($T_s$):**

$$T_s = \frac{4}{\zeta \cdot \omega_n} = \frac{4}{0.5 \cdot 4} = \mathbf{2\text{ s}}$$



(Nakon 2 sekunde, sve oscilacije prestaju i sustav vozi stabilno).





---

### ZADATAK 2: Pronalaženje polova i nula te stabilnosti (P3.3.1)

**Zadana je prijenosna funkcija:**


$$G(s) = \frac{s + 1}{s^2 + s + 1}$$



**Pitanje:** Gdje leže nule i polovi te kako ih skicirati?

#### Postupak i objašnjenje:

1. Traženje Nula ($N(s) = 0$):
Izjednačimo brojnik s nulom:



$$s_z + 1 = 0 \implies \mathbf{s_z = -1}$$



(Imamo jednu nulu na realnoj osi u točki $-1$).


2. Traženje Polova ($D(s) = 0$):
Izjednačimo nazivnik s nulom:



$$s_p^2 + s_p + 1 = 0$$



Rješavamo običnu kvadratnu jednadžbu $s_{p1,2} = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$:



$$s_{p1,2} = \frac{-1 \pm \sqrt{1^2 - 4 \cdot 1 \cdot 1}}{2 \cdot 1} = \frac{-1 \pm \sqrt{-3}}{2} = \mathbf{-0.5 \pm 0.87j}$$





3. **Što nam ovo govori i kako se crta?**
* Polovi su u obliku $s = -\sigma \pm j\omega$, gdje je realni dio $\sigma = -0.5$, a imaginarni $\omega = 0.87$.


* Zbog negativnog realnog dijela ($-0.5$), polovi leže na **lijevoj strani** kompleksne ravnine — što nam govori da je sustav **siguran i stabilan**.


* Imaginarni dio ($0.87j$) uzrokuje da odziv ima prigušene oscilacije.





```
 Imaginarna os (jw)
        ^
   0.87 |      X  <-- Pol (sp1 = -0.5 + 0.87j)
        |
--------O------|-----> Realna os (σ)
       -1     -0.5
        |
  -0.87 |      X  <-- Pol (sp2 = -0.5 - 0.87j)
        |
  Nula (sz = -1)
```[cite: 17]

---

### ZADATAK 3: Koliko sustav griješi u radu? (P3.2.6)
**Zadana je prijenosna funkcija:**
$$G(s) = \frac{5s + 8}{s^3 + 4s^2 + 25s + 18}$$
[cite: 14]

**Pitanje:** Ako mu damo naredbu veličine 1 (jedinični skok), kolika će biti greška kada se sustav potpuno umiri ($t \to \infty$)[cite: 14]?

#### Postupak i objašnjenje:
1. **Izračun izlaza u ustaljenom stanju $y(\infty)$[cite: 13]:**
   Prema teoremu o konačnoj vrijednosti, kada se vrijeme smiri ($t \to \infty$), kompleksna frekvencija postaje $s = 0$[cite: 13, 14]:
   $$y(\infty) = \lim_{s \to 0} s \cdot G(s) \cdot \frac{1}{s} = \lim_{s \to 0} G(s)$$
[cite: 14, 15]
   Uvrstimo $s = 0$ izravno u prijenosnu funkciju[cite: 15]:
   $$y(\infty) = \frac{5(0) + 8}{0^3 + 4(0)^2 + 25(0) + 18} = \frac{8}{18} \approx \mathbf{0.44}$$
[cite: 15]

2. **Izračun greške $e_{ss}$[cite: 14]:**
   Tražili smo izlaz visine $1$, a sustav se umirio tek na $0.44$[cite: 14, 15]. Greška iznosi[cite: 14]:
   $$e_{ss} = 1 - y(\infty) = 1 - 0.44 = \mathbf{0.56} \quad \text{(ili } 56\% \text{)}$$
[cite: 14, 15]
   *(Ovo nam govori da je sustav bez dodatnog regulatora prilično neprecizan jer ostvaruje tek manje od polovice traženog izlaza).*

```
