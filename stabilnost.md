U ovoj skripti obrađeno je **Poglavlje 13: Stabilnost sustava** (autori: Ivan Lorencin, Nikola Anđelić, Zlatan Car).

Nastavljamo u istom stilu – bez suhoparnih formula na prvu, već kroz razumljive fizikalne analogije i slikovite primjere iz života.

---

## 1. Ključni koncepcijski temelji: Što je uopće stabilnost?

### A. Tri stanja stabilnosti (Fizikalna intuitivna slika)

Najlakši način za shvatiti stabilnost je zamišljanje **kuglice na različitim terenima** (Slika 13.1 iz skripte):

1. **Stabilan sustav (Kuglica u udubljenju / zdjeli):**
* *Slika:* Ako pogurneš kuglicu u zdjeli, ona će se malo zaljuljati, ali će se zbog otpora zraka i trenja **vratiti na dno (početni položaj)**.


* *Praksa:* Auto naleti na rupu, malo skrene, ali se sam izravna na cestu.


2. **Granično stabilan sustav (Kuglica na ravnoj podlozi):**
* *Slika:* Ako pogurneš kuglicu na ravnom stolu, ona će se pomaknuti i **ostati na novoj poziciji ili se nastaviti kotrljati neprekidno** bez ubrzavanja ili vraćanja.


* *Praksa:* Zvučnik koji neprekidno pišti na istoj glasnoći ili njihalo u satu bez trenja koje se beskonačno ljulja.




3. **Nestabilan sustav (Kuglica na vrhu brda):**
* *Slika:* Ako kuglicu na vrhu brda dotakneš samo prstom, ona se **nikada ne vraća**, nego ubrzava i pada sve brže prema dolje.


* *Praksa:* Mikrofon prinesen zvučniku (mikrofon hvata zvuk, zvučnik ga pojačava, mikrofon opet hvata... dok ne nastane nepodnošljiva mikrofonija i uništi se oprema).



---

### B. Stabilnost preko Polova u $s$-ravnini ($\sigma - j\omega$)

Polovi ($s_p$) iz nazivnika prijenosne funkcije ($D(s) = 0$) direktno diktiraju stabilnost:

$$\text{Pol } s_p = \sigma + j\omega$$

* **Realni dio ($\sigma$):** Određuje **raste li ili pada** signal kroz vrijeme (eksponecijalni dio $e^{\sigma t}$).
* **Imaginarni dio ($j\omega$):** Određuje **oscilacije/ljuljanje** (sinus i kosinus $\sin(\omega t)$).

```
         Imaginarna os (jω)
                ^
  STABILNO      |     NESTABILNO
  PODRUČJE      |      PODRUČJE
  (Lijeva       |      (Desna
  poluravnina)  |     poluravnina)
                |
       X        |        X         <-- Nesmetano raste ili oscilira do beskonačnosti!
 (Odziv zamire) |  (Odziv eksplodira)
----------------+-----------------> Realna os (σ)
                |
                |
    GRANIČNO STABILNO (Na samoj osi jω)
    (Stalne neprekidne oscilacije)
```[cite: 23, 24, 25]

#### Pravila polova u sekundi:
* **Svi polovi imaju $\text{Re}(s_p) < 0$ (Lijeva poluravnina):** Sustav je **STABILAN**[cite: 23]. Svaki poremećaj izumire s vremenom[cite: 24].
* **Barem jedan pol ima $\text{Re}(s_p) > 0$ (Desna poluravnina):** Sustav je **NESTABILAN**[cite: 23, 25]. Čak i najmanji šum uzrokuje da izlaz ode u beskonačnost (eksplodira/pukne)[cite: 25].
* **Polovi leže točno na imaginarnoj osi ($\text{Re}(s_p) = 0$):** Sustav je **GRANIČNO STABILAN**[cite: 23, 24]. Odziv trajno oscilira stalnom amplitudom[cite: 24].

---

### C. Zašto nam treba Hurwitzov postupak?

Pronalaženje korijena (polova) za kvadratnu jednadžbu $s^2 + bs + c = 0$ je lako. Ali što kada imamo sustav 3., 4. ili 5. reda ($s^4 + 12s^3 - 5s^2 - 336s - 320 = 0$)[cite: 28]?
Nijedan inženjer ne želi ručno tražiti kompleksne korijene polinoma 4. reda!

**Hurwitzov kriterij** je trik: omogućuje nam da izračunavanjem par jednostavnih determinanti iz koeficijenata nazivnika saznamo **jesu li svi polovi u lijevoj poluravnini**, bez da ikada izračunamo točne vrijednosti samih polova[cite: 26]!

---

## 2. Kako radi Hurwitzov postupak? (Algoritam)

Pretpostavimo da je nazivnik prijenosne funkcije:
$$D(s) = b_n s^n + b_{n-1} s^{n-1} + \dots + b_1 s + b_0$$
[cite: 26]

### KORAK 1: Nužan uvjet (Brza provjera šmekom)
Prije nego raspisuješ matrice, pogledaj koeficijente $b_0, b_1, b_2, \dots, b_n$[cite: 26]:
1. **Svi koeficijenti moraju postojati** (nijedan ne smije biti 0)[cite: 26].
2. **Svi koeficijenti moraju imati ISTI predznak** (svi pozitivni)[cite: 26].
> ⚠️ **Ako je bilo koji koeficijent negativan ili nula $\implies$ Sustav je ODMAH NESTABILAN[cite: 26, 28]! (Prekidaš računanje)**.

### KORAK 2: Dovoljan uvjet (Hurwitzove poddeterminante)
Slakže se matrica i provjeravaju poddeterminante $D_1, D_2, D_3 \dots$[cite: 26]:
* $D_1 = b_1 > 0$[cite: 26]
* $D_2 = \begin{vmatrix} b_1 & b_0 \\ b_3 & b_2 \end{vmatrix} = b_1 b_2 - b_3 b_0 > 0$[cite: 26, 27]
* $D_3 = \begin{vmatrix} b_1 & b_0 & 0 \\ b_3 & b_2 & b_1 \\ b_5 & b_4 & b_3 \end{vmatrix} > 0$[cite: 26]

Ako su **sve determinante pozitivne ($D_i > 0$)**, sustav je **STABILAN**[cite: 26].

---

## 3. Detaljno riješeni primjeri iz skripte

---

### ZADATAK 1: Provjera preko položaja polova (P7.2.2)
**Zadana prijenosna funkcija:**
$$G(s) = \frac{s+2}{(s-5)(s+1)(s+8)^2}$$
[cite: 26]

**Zadatak:** Odredi stabilnost sustava[cite: 26].

#### Postupak:
1. Nule nazivnika (polovi) su izravno vidljive jer je nazivnik već rastavljen na faktore[cite: 26]:
   * $(s-5) = 0 \implies \mathbf{s_{p1} = +5}$[cite: 26]
   * $(s+1) = 0 \implies \mathbf{s_{p2} = -1}$[cite: 26]
   * $(s+8)^2 = 0 \implies \mathbf{s_{p3,4} = -8}$ (dvostruki pol)[cite: 20, 26]
2. Zaključak o stabilnosti:
   Pol $s_{p1} = +5$ ima pozitivan realni dio ($\text{Re} > 0$)[cite: 25, 26]. Nalazi se u desnoj poluravnini[cite: 23].
   $$\mathbf{Sustav\ je\ NESTABILAN.}$$
[cite: 23, 28]

---

### ZADATAK 2: Isti zadatak preko Hurwitzovog postupka (P7.3.2)
**Zadatak:** Provjeri stabilnost funkcije $G(s) = \frac{s+2}{(s-5)(s+1)(s+8)^2}$ koristeći Hurwitzov postupak[cite: 27].

#### Postupak:
1. Moramo pomnožiti zagrade u nazivniku da dobijemo polinom[cite: 27]:
   $$D(s) = (s-5)(s+1)(s^2 + 16s + 64)$$
[cite: 27]
   $$D(s) = (s-5)(s^3 + 17s^2 + 80s + 64)$$
[cite: 28]
   $$D(s) = s^4 + 12s^3 - 5s^2 - 336s - 320$$
[cite: 28]

2. Primjena KORAKA 1 (Nužan uvjet)[cite: 26]:
   Koeficijenti polinoma nazivnika su:
   $$b_4 = 1, \quad b_3 = 12, \quad b_2 = -5, \quad b_1 = -336, \quad b_0 = -320$$
[cite: 28]
   Spazimo negativne predznake ($-5, -336, -320$)[cite: 28]!
   Budući da svi koeficijenti nemaju isti predznak, **nužan uvjet nije ispunjen**[cite: 26, 28].

3. **Zaključak:** $\mathbf{Sustav\ je\ NESTABILAN}$[cite: 28]. (Uopće ne moramo računati matrice[cite: 26, 28]).

---

### ZADATAK 3: Određivanje kritičnog pojačanja $K$ za stabilnost (P7.3.4)
Ovo je **tipičan ispitni zadatak**! Imamo sustav u povratnoj vezi gdje je $K$ pojačanje regulatora koje sami podešavamo (npr. koliko jako motor reagira na skretanje)[cite: 30].

**Zadak:** Za sustav s nazivnikom zatvorenog kruga:
$$D(s) = s^3 + 13s^2 + 140s + (800 + 400K)$$
[cite: 31]
Odredi raspon pojačanja $K$ za koji je sustav stabilan[cite: 30].

#### Postupak:
1. **Očitamo koeficijente polinoma nazivnika[cite: 31]:**
   * $b_3 = 1$[cite: 31]
   * $b_2 = 13$[cite: 31]
   * $b_1 = 140$[cite: 31]
   * $b_0 = 800 + 400K$[cite: 31]

2. **Nužan uvjet (Svi koeficijenti moraju biti $> 0$)[cite: 26, 31]:**
   Jedini koeficijent koji ovisi o $K$ je $b_0$[cite: 31].
   $$800 + 400K > 0 \implies 400K > -800 \implies \mathbf{K > -2}$$
[cite: 31]

3. **Dovoljan uvjet — Hurwitzova determinanta $D_2 > 0$[cite: 26, 31]:**
   $$D_2 = b_1 b_2 - b_3 b_0 > 0$$
[cite: 26, 31]
   Uvrstimo naše koeficijente[cite: 31]:
   $$140 \cdot 13 - 1 \cdot (800 + 400K) > 0$$
[cite: 31]
   $$1820 - 800 - 400K > 0$$
[cite: 31]
   $$1020 - 400K > 0$$
   $$1020 > 400K \implies K < \frac{1020}{400} \implies \mathbf{K < 2.55}$$
[cite: 32]

4. **Konačni zaključak (Presjek uvjeta)[cite: 32]:**
   Sustav će biti stabilan ako se pojačanje $K$ nalazi u rasponu[cite: 32]:
   $$\mathbf{K \in \langle -2, \; 2.55 \rangle}$$
[cite: 32]

* **Što se događa ako stavimo $K = 5$ (izvan raspona)?** Sustav poddivlja i oscilacije neprekidno rastu dok ne unište komponente (prikazano žutom linijom na Slici 13.12 iz skripte)[cite: 25, 32]!
* **Što se događa za $K = 1$ (unutar raspona)?** Odziv se lijepo umiri na stabilnu vrijednost (plava linija)[cite: 24, 32].

```
