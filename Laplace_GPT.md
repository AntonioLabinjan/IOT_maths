# Laplaceova transformacija — univerzalni šalabahter

> **Glavna ideja:** Laplaceova transformacija omogućuje nam da problem koji se mijenja kroz vrijeme prebacimo u matematički prostor u kojem je puno jednostavniji za rješavanje.

---

## 1. Što je Laplaceova transformacija?

Laplaceova transformacija matematička je operacija koja funkciju vremena $f(t)$ pretvara u funkciju kompleksne varijable $F(s)$.

Definicija jednostrane Laplaceove transformacije:

$$
\boxed{F(s)=\int_0^\infty f(t)e^{-st}\,dt}
$$

Oznake:

- $t$ — vrijeme.
- $f(t)$ — izvorna funkcija, odnosno signal u vremenu.
- $s$ — kompleksna varijabla.
- $F(s)$ — Laplaceova transformacija funkcije $f(t)$.
- $e^{-st}$ — eksponencijalna težinska funkcija.

Pišemo:

$$
\mathcal{L}\{f(t)\}=F(s)
$$

A inverzna transformacija vraća nas natrag:

$$
\mathcal{L}^{-1}\{F(s)\}=f(t)
$$

### Intuitivno objašnjenje

Zamisli da promatraš brzinu nekog motora kroz vrijeme.

Umjesto da cijelo vrijeme analiziraš kako se brzina mijenja, Laplaceova transformacija omogućuje ti da tu vremensku funkciju prikažeš na drugi način, u kojem su mnogi matematički problemi jednostavniji.

Najvažnija prednost:

$$
\boxed{
\text{Diferencijalne jednadžbe}
\longrightarrow
\text{Algebarske jednadžbe}
}
$$

To je cijela poanta.

---

## 2. Što je varijabla $s$?

Varijabla $s$ kompleksna je varijabla:

$$
\boxed{s=\sigma+j\omega}
$$

Gdje su:

- $\sigma$ — realni dio, povezan s eksponencijalnim rastom ili opadanjem.
- $\omega$ — imaginarni dio, povezan s oscilacijama.
- $j$ — imaginarna jedinica, $j^2=-1$.

Budući da je:

$$
e^{-st}=e^{-(\sigma+j\omega)t}
$$

možemo zapisati:

$$
e^{-st}=e^{-\sigma t}e^{-j\omega t}
$$

Dakle, transformacija istovremeno uzima u obzir:

1. Eksponencijalno ponašanje signala.
2. Njegovu oscilatornu komponentu.

Ne moraš odmah znati kompleksnu analizu da bi razumio Laplaceovu transformaciju. Za početak je dovoljno znati da je $s$ matematički alat koji nam omogućuje analiziranje različitih vremenskih ponašanja.

---

## 3. Zašto nam je Laplaceova transformacija korisna?

U stvarnom svijetu gotovo sve što se mijenja može se promatrati kao sustav koji evoluira kroz vrijeme.

Primjeri:

| Područje | Primjena |
|---|---|
| Elektrotehnika | Analiza napona i struje u električnim krugovima |
| Robotika | Modeliranje kretanja i upravljanja motorima |
| Automatika | Analiza stabilnosti i odziva sustava |
| Mehanika | Vibracije, opruge, prigušenje |
| Obrada signala | Analiza i projektiranje filtara |
| Elektronika | RC, RL i RLC krugovi |

### Primjer: električni motor

Kada uključiš motor, njegova brzina ne skoči odmah na maksimalnu vrijednost.

Brzina se postupno povećava.

To ponašanje može se opisati diferencijalnom jednadžbom:

$$
m\frac{dv(t)}{dt}+bv(t)=F(t)
$$

Gdje su:

- $m$ — masa ili ekvivalentna tromost sustava.
- $b$ — koeficijent otpora/prigušenja.
- $v(t)$ — brzina.
- $F(t)$ — vanjska sila.

Laplaceova transformacija omogućuje nam da tu jednadžbu riješimo algebarski, analiziramo odziv i utvrdimo kako se sustav ponaša.

---

## 4. Najvažniji parovi Laplaceovih transformacija

Ovo su osnovne funkcije koje se najčešće pojavljuju.

| Funkcija $f(t)$ | Transformacija $F(s)$ |
|---|---|
| $1$ | $\frac{1}{s}$ |
| $t$ | $\frac{1}{s^2}$ |
| $t^2$ | $\frac{2}{s^3}$ |
| $t^n$ | $\frac{n!}{s^{n+1}}$ |
| $e^{at}$ | $\frac{1}{s-a}$ |
| $\sin(\omega t)$ | $\frac{\omega}{s^2+\omega^2}$ |
| $\cos(\omega t)$ | $\frac{s}{s^2+\omega^2}$ |
| $\sinh(at)$ | $\frac{a}{s^2-a^2}$ |
| $\cosh(at)$ | $\frac{s}{s^2-a^2}$ |

Posebno zapamti:

$$
\boxed{\mathcal{L}\{1\}=\frac{1}{s}}
$$

$$
\boxed{\mathcal{L}\{t\}=\frac{1}{s^2}}
$$

$$
\boxed{\mathcal{L}\{e^{at}\}=\frac{1}{s-a}}
$$

$$
\boxed{
\mathcal{L}\{\sin(\omega t)\}
=\frac{\omega}{s^2+\omega^2}
}
$$

$$
\boxed{
\mathcal{L}\{\cos(\omega t)\}
=\frac{s}{s^2+\omega^2}
}
$$

---

## 5. Najvažnija svojstva

### 5.1. Linearnost

Transformacija zbroja jednaka je zbroju transformacija.

$$
\boxed{
\mathcal{L}\{af(t)+bg(t)\}
=aF(s)+bG(s)
}
$$

Primjer:

$$
\mathcal{L}\{3t+2\}
=3\mathcal{L}\{t\}+2\mathcal{L}\{1\}
$$

$$
=\boxed{\frac{3}{s^2}+\frac{2}{s}}
$$

**Praktična posljedica:** funkciju možeš rastaviti na jednostavnije dijelove i transformirati svaki zasebno.

### 5.2. Transformacija derivacije

Ovo je najvažnije svojstvo za rješavanje diferencijalnih jednadžbi.

Prva derivacija:

$$
\boxed{\mathcal{L}\{f'(t)\}=sF(s)-f(0)}
$$

Druga derivacija:

$$
\boxed{
\mathcal{L}\{f''(t)\}
=s^2F(s)-sf(0)-f'(0)
}
$$

Treća derivacija:

$$
\boxed{
\mathcal{L}\{f'''(t)\}
=s^3F(s)-s^2f(0)-sf'(0)-f''(0)
}
$$

Općenito:

$$
\mathcal{L}\{f^{(n)}(t)\}
=s^nF(s)-s^{n-1}f(0)-\cdots-f^{(n-1)}(0)
$$

**Zašto je ovo toliko bitno?**

U vremenskoj domeni deriviranje može biti komplicirano.

U Laplaceovoj domeni derivacija postaje množenje s $s$, uz korekciju za početne uvjete.

To je razlog zašto diferencijalne jednadžbe postaju algebarske.

### 5.3. Množenje eksponencijalnom funkcijom

$$
\boxed{
\mathcal{L}\{e^{at}f(t)\}=F(s-a)
}
$$

Primjer:

$$
\mathcal{L}\{e^{3t}\sin(2t)\}
=
\frac{2}{(s-3)^2+4}
$$

### 5.4. Pomak u vremenu

Za Heavisideovu funkciju $u(t-a)$:

$$
\boxed{
\mathcal{L}\{u(t-a)f(t-a)\}
=e^{-as}F(s)
}
$$

Ovo je korisno za modeliranje funkcija koje se aktiviraju tek nakon određenog vremena.

---

## 6. Posebne funkcije

### 6.1. Heavisideova funkcija

Heavisideova funkcija opisuje naglo uključivanje signala.

$$
u(t-a)=
\begin{cases}
0,&t<a\\
1,&t\geq a
\end{cases}
$$

Primjer: uključivanje grijača nakon 5 sekundi.

$$
f(t)=u(t-5)
$$

Transformacija:

$$
\boxed{
\mathcal{L}\{u(t-a)\}=\frac{e^{-as}}{s}
}
$$

Za naš primjer:

$$
F(s)=\frac{e^{-5s}}{s}
$$

### 6.2. Diracova delta funkcija

Diracova delta predstavlja idealizirani impuls.

$$
\delta(t-a)
$$

Intuitivno: signal koji djeluje u jednom trenutku, s konačnom ukupnom površinom.

$$
\boxed{\mathcal{L}\{\delta(t-a)\}=e^{-as}}
$$

Posebno:

$$
\mathcal{L}\{\delta(t)\}=1
$$

Primjena: modeliranje kratkog udara, impulsa ili idealiziranog ulaza u sustav.

### 6.3. Ramp funkcija

Ramp funkcija predstavlja linearno rastući signal.

$$
r(t)=tu(t)
$$

Transformacija:

$$
\boxed{\mathcal{L}\{tu(t)\}=\frac{1}{s^2}}
$$

Primjer: zadana brzina koja se linearno povećava tijekom vremena.

---

## 7. Inverzna Laplaceova transformacija

Ponekad imamo izraz $F(s)$, a želimo vratiti izvornu funkciju $f(t)$.

Tada koristimo inverznu transformaciju:

$$
\boxed{f(t)=\mathcal{L}^{-1}\{F(s)\}}
$$

Najčešće se koristi tablica transformacija i rastavljanje na parcijalne razlomke.

### Primjer 1

$$
F(s)=\frac{5}{s(s+2)}
$$

Rastavljamo:

$$
\frac{5}{s(s+2)}
=\frac{A}{s}+\frac{B}{s+2}
$$

Množenjem sa $s(s+2)$:

$$
5=A(s+2)+Bs
$$

Za $s=0$:

$$
5=2A\Rightarrow A=\frac52
$$

Za $s=-2$:

$$
5=-2B\Rightarrow B=-\frac52
$$

Dakle:

$$
F(s)=\frac{5}{2s}-\frac{5}{2(s+2)}
$$

Vraćamo pomoću tablice:

$$
\boxed{
f(t)=\frac52-\frac52e^{-2t}
}
$$

### Primjer 2 — kvadratni nazivnik

$$
F(s)=\frac{3s+7}{s^2+4s+13}
$$

Dovršimo kvadrat:

$$
s^2+4s+13=(s+2)^2+9
$$

Prilagodimo brojnik:

$$
3s+7=3(s+2)+1
$$

Zato:

$$
F(s)=
\frac{3(s+2)}{(s+2)^2+9}
+
\frac{1}{(s+2)^2+9}
$$

Koristimo pomaknute transformacije sinusa i kosinusa:

$$
\boxed{
f(t)=3e^{-2t}\cos(3t)
+\frac13e^{-2t}\sin(3t)
}
$$

---

## 8. Kako riješiti diferencijalnu jednadžbu pomoću Laplacea?

Ovo je praktični postupak koji možeš primijeniti na velik broj problema.

**Korak 1 — Zapiši diferencijalnu jednadžbu.**

Primjer:

$$
2v'(t)+4v(t)=10
$$

Uz početni uvjet:

$$
v(0)=0
$$

**Korak 2 — Primijeni Laplaceovu transformaciju.**

$$
2\mathcal{L}\{v'(t)\}
+4\mathcal{L}\{v(t)\}
=\mathcal{L}\{10\}
$$

**Korak 3 — Uvrsti svojstva.**

$$
2(sV(s)-v(0))+4V(s)=\frac{10}{s}
$$

Budući da je $v(0)=0$:

$$
2sV(s)+4V(s)=\frac{10}{s}
$$

**Korak 4 — Izoliraj $V(s)$.**

$$
V(s)(2s+4)=\frac{10}{s}
$$

$$
\boxed{V(s)=\frac{5}{s(s+2)}}
$$

**Korak 5 — Rastavi na parcijalne razlomke.**

$$
V(s)=\frac{5}{2s}-\frac{5}{2(s+2)}
$$

**Korak 6 — Primijeni inverznu transformaciju.**

$$
\boxed{v(t)=2.5(1-e^{-2t})}
$$

### Što nam rezultat govori?

- U početku je brzina 0.
- Brzina postupno raste.
- S vremenom se približava vrijednosti 2.5.
- Ne raste beskonačno, nego se stabilizira.

Fizikalno objašnjenje: sustav ubrzava dok se vanjska sila ne izjednači s otporom.

---

## 9. Prijenosna funkcija (Transfer Function)

Jedan od najvažnijih koncepata u automatici i teoriji sustava.

Prijenosna funkcija opisuje odnos između ulaza i izlaza sustava u Laplaceovoj domeni.

Za sustav s nultim početnim uvjetima:

$$
\boxed{G(s)=\frac{Y(s)}{U(s)}}
$$

Gdje su:

- $U(s)$ — ulaz sustava.
- $Y(s)$ — izlaz sustava.
- $G(s)$ — prijenosna funkcija.

Primjer:

$$
G(s)=\frac{5}{s+2}
$$

Ona opisuje kako sustav reagira na različite ulazne signale.

### Polovi i nule

Ako imamo:

$$
G(s)=\frac{(s+1)(s+3)}
{(s+2)(s+5)}
$$

- Nule su vrijednosti $s$ koje poništavaju brojnik.
- Polovi su vrijednosti $s$ koje poništavaju nazivnik.

Nule:

$$
s=-1,\quad s=-3
$$

Polovi:

$$
s=-2,\quad s=-5
$$

### Zašto su polovi važni?

Polovi nam govore puno o ponašanju sustava.

Za jednostavne sustave s polovima:

- Negativni realni polovi: eksponencijalno opadanje.
- Pozitivni realni polovi: eksponencijalni rast.
- Kompleksni polovi: oscilatorno ponašanje, uz rast ili opadanje ovisno o realnom dijelu.

Za standardne kontinuirane linearne vremenski nepromjenjive sustave, stabilnost zahtijeva da svi polovi budu u lijevoj poluravnini kompleksne $s$-ravnine.

---

## 10. Početni i završni teorem

Ovi teoremi omogućuju određivanje vrijednosti funkcije bez računanja cijele inverzne transformacije.

### Početni teorem

$$
\boxed{f(0^+)=\lim_{s\to\infty}sF(s)}
$$

Omogućuje određivanje početne vrijednosti funkcije, uz uvjete primjenjivosti teorema.

### Završni teorem

$$
\boxed{f(\infty)=\lim_{s\to0}sF(s)}
$$

Omogućuje određivanje konačne vrijednosti funkcije, ako ona postoji i ako su zadovoljeni uvjeti teorema.

Važno: završni teorem ne smiješ koristiti naslijepo. Ako sustav oscilira bez smirivanja ili raste bez granice, konačna vrijednost ne postoji.

---

## 11. Laplace vs. Fourier

Obje transformacije omogućuju analizu signala na način koji nije izravno vezan uz vremenski prikaz.

| Laplaceova | Fourierova |
|---|---|
| Koristi kompleksnu varijablu $s=\sigma+j\omega$ | Koristi frekvencijsku varijablu $\omega$ |
| Uključuje eksponencijalno opadanje/rast i oscilacije | Analizira frekvencijske komponente |
| Posebno korisna za diferencijalne jednadžbe i prijelazne pojave | Posebno korisna za frekvencijsku analizu signala |
| Može analizirati i nestabilna ponašanja u odgovarajućoj domeni definicije | Za klasičnu Fourierovu transformaciju potrebni su odgovarajući uvjeti integrabilnosti |

Možeš razmišljati o Fourierovoj transformaciji kao o posebnom slučaju Laplaceove transformacije kada je realni dio $s$ jednak nuli, pod uvjetom da transformacija na toj osi postoji.

---

## 12. Brzi pregled formula

| Operacija | Formula |
|---|---|
| Definicija | $\int_0^\infty f(t)e^{-st}dt$ |
| Inverzna transformacija | $\mathcal{L}^{-1}\{F(s)\}=f(t)$ |
| Konstanta | $1\rightarrow 1/s$ |
| Potencija | $t^n\rightarrow n!/s^{n+1}$ |
| Eksponencijalna | $e^{at}\rightarrow 1/(s-a)$ |
| Sinus | $\sin(\omega t)\rightarrow \omega/(s^2+\omega^2)$ |
| Kosinus | $\cos(\omega t)\rightarrow s/(s^2+\omega^2)$ |
| Prva derivacija | $f'\rightarrow sF-f(0)$ |
| Druga derivacija | $f''\rightarrow s^2F-sf(0)-f'(0)$ |
| Vremenski pomak | $u(t-a)f(t-a)\rightarrow e^{-as}F(s)$ |
| Impuls | $\delta(t-a)\rightarrow e^{-as}$ |
| Eksponencijalni pomak | $e^{at}f(t)\rightarrow F(s-a)$ |

---

## 13. Najčešće pogreške i zamke

1. **Zaboravljanje početnih uvjeta.**  
   Kod transformacije derivacije moraš uključiti vrijednosti funkcije u $t=0$.

2. **Miješanje $s-a$ i $s+a$.**  
   Za $e^{at}$ dobivamo $1/(s-a)$, ne $1/(s+a)$.

3. **Pogrešno rastavljanje na parcijalne razlomke.**  
   Nakon rastavljanja provjeri rezultat vraćanjem na zajednički nazivnik.

4. **Zaboravljanje dovršavanja kvadrata.**  
   Izraz poput $s^2+4s+13$ često treba pretvoriti u $(s+2)^2+9$.

5. **Miješanje vremenske i Laplaceove domene.**  
   $f(t)$ i $F(s)$ nisu ista funkcija i ne smiju se tretirati kao ista stvar.

6. **Nekritičko korištenje završnog teorema.**  
   Mora postojati konačna završna vrijednost i moraju biti zadovoljeni uvjeti teorema.

7. **Zaboravljanje pomaka u eksponentu.**  
   Ako vidiš $F(s-a)$, razmišljaj o množenju s $e^{at}$ u vremenskoj domeni.

---

## 14. Kako razmišljati kada dobiješ novi problem?

Postavi si sljedeća pitanja:

1. Imam li funkciju vremena ili diferencijalnu jednadžbu?
2. Želim li transformirati funkciju ili vratiti funkciju iz $F(s)$?
3. Koji poznati par transformacija mogu prepoznati?
4. Ako imam derivacije, koje početne uvjete moram uključiti?
5. Ako imam razlomak, mogu li ga rastaviti na jednostavnije dijelove?
6. Ako imam kvadratni nazivnik, trebam li dovršiti kvadrat?
7. Što mi dobiveni rezultat govori o ponašanju stvarnog sustava?

**Najvažnija stvar koju trebaš razumjeti:**

Laplaceova transformacija nije samo matematički trik za rješavanje zadataka. Ona je način na koji inženjeri analiziraju dinamičke sustave — kako reagiraju na ulaz, koliko brzo se stabiliziraju, osciliraju li i jesu li stabilni.
