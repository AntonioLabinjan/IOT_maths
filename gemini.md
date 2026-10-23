Na temelju postupka i primjera iz skripte, u nastavku su bağısto i korak-po-korak riješena oba zadatka sa slike.

---

## 3.1 Položaj polova i Hurwitzov postupak

Zadana je prijenosna funkcija:


$$G_3(s) = \frac{s + z_3}{s^3 + b_2 s^2 + b_1 s + b_0}$$

Iz tablice B za grupu/zadatak **19** očitavamo parametre:

* Iz izraza $\frac{8(s + 5)}{(s + 6)(s^2 + 4s + 8)}$ dobivamo prijenosnu funkciju $G_3(s)$:
Razvijanjem nazivnika:

$$(s + 6)(s^2 + 4s + 8) = s^3 + 4s^2 + 8s + 6s^2 + 24s + 48 = s^3 + 10s^2 + 32s + 48$$


Koeficijenti polina nazivnika $A(s) = s^3 + b_2 s^2 + b_1 s + b_0$ su:
* $b_2 = 10$
* $b_1 = 32$
* $b_0 = 48$
* Brojnik: $z_3 = 5$ (pojačanje je 8)



---

### a) Određivanje polova sustava (Python `numpy.roots`) i zaključak o stabilnosti

Polovi sustava su korijeni karakterističnog polinoma $A(s) = s^3 + 10s^2 + 32s + 48 = 0$.

Rješavanjem jednadžbe $(s + 6)(s^2 + 4s + 8) = 0$:

1. $s_1 = -6$
2. Korijeni kvadratnog dijela $s^2 + 4s + 8 = 0$:

$$s_{2,3} = \frac{-4 \pm \sqrt{16 - 32}}{2} = \frac{-4 \pm \sqrt{-16}}{2} = -2 \pm j2$$



**Kod u Pythonu (`numpy.roots`):**

```python
import numpy as np

# Koeficijenti polinoma s^3 + 10*s^2 + 32*s + 48
coefficients = [1, 10, 32, 48]
poles = np.roots(coefficients)
print("Polovi sustava:", poles)

```

*Izlaz:* `[-6. , -2.+2.j, -2.-2.j]`

**Zaključak o stabilnosti:**
Svi polovi sustava ($s_1 = -6$, $s_{2,3} = -2 \pm j2$) imaju **strogo negativne realne dijelove** ($\text{Re}(s) < 0$). Prema tome, sustav je **stabilan**.

---

### b) Provjera stabilnosti Hurwitzovim postupkom

1. **Nužni uvjet za stabilnost:**
Svi koeficijenti karakterističnog polinoma $A(s) = a_3 s^3 + a_2 s^2 + a_1 s + a_0$ moraju postojati i biti istog predznaka.
* $a_3 = 1 > 0$
* $a_2 = b_2 = 10 > 0$
* $a_1 = b_1 = 32 > 0$
* $a_0 = b_0 = 48 > 0$


Nužni uvjet je **ispunjen**.
2. **Hurwitzova matrica $H_3$:**
Matrica $H_3$ za polinom 3. reda formira se prema pravilu iz skripte:

$$H_3 = \begin{bmatrix} a_2 & a_0 & 0 \\ a_3 & a_1 & 0 \\ 0 & a_2 & a_0 \end{bmatrix} = \begin{bmatrix} 10 & 48 & 0 \\ 1 & 32 & 0 \\ 0 & 10 & 48 \end{bmatrix}$$


3. **Poddeterminante $D_1, D_2, D_3$:**
* $D_1 = a_2 = 10 > 0$
* $D_2 = \begin{vmatrix} 10 & 48 \\ 1 & 32 \end{vmatrix} = (10 \cdot 32) - (48 \cdot 1) = 320 - 48 = 272 > 0$
* $D_3 = a_0 \cdot D_2 = 48 \cdot 272 = 13056 > 0$



Sve poddeterminante su strogo pozitivne ($D_1 > 0, D_2 > 0, D_3 > 0$), što potvrdjuje da je sustav **stabilan**.

---

### c) Usporedba zaključaka iz a) i b)

Oba postupka (položaj polova u kompleksnoj ravnini i Hurwitzov kriterij) daju identičan zaključak: **sustav je stabilan**.

* **Objašnjenje nedovoljnosti nužnog uvjeta:** Nužni uvjet (pozitivnost svih koeficijenata polinoma) osigurava da nema realnih pozitivnih polova, ali kod polinoma stupnja $n \ge 3$ **ne jamči** da kompleksno-konjugirani parovi polova neće prijeći u desnu poluravninu (tj. imati pozitivan realni dio). Zato je Hurwitzov postupak (dovoljan uvjet) nužan za potpunu potvrdu stabilnosti.

---

### d) Skokovni odziv u Pythonu i povezanost s polovima

**Python kôd:**

```python
import matplotlib.pyplot as plt
import control as ct

num = [8, 40]  # 8*(s + 5)
den = [1, 10, 32, 48]  # s^3 + 10*s^2 + 32*s + 48
sys = ct.tf(num, den)

t, y = ct.step_response(sys)
plt.plot(t, y)
plt.title("Skokovni odziv sustava G3(s)")
plt.xlabel("Vrijeme t [s]")
plt.ylabel("y(t)")
plt.grid(True)
plt.show()

```

**Povezanost oblika odziva s polovima:**

* Konjugirano-kompleksni par polova $s_{2,3} = -2 \pm j2$ uzrokuje **oscilatornu komponentu** u odzivu (zbog imaginarnog dijela $\omega = 2$).
* Realni dio polova $\sigma = -2$ uzrokuje **prigušenje oscilacija** s vremenskom konstantom $\tau = \frac{1}{2} = 0.5\text{ s}$.
* Realni pol $s_1 = -6$ brže izumire jer je dalje u lijevoj poluravnini i manje utječe na dominantni oblik odziva.

---

---

## 3.2 Interval pojačanja zatvorenog kruga

Iz tablice B za grupu **19** očitavamo parametre procesa $G_0(s)$:

* $G_0(s) = \frac{K}{(s + p_1)(s + p_2)(s + p_3)}$
* Iz lijevog stupca tablice 19: $p_1 = 0$, $p_2 = 8$, $p_3 = 100$ (odnosno iz polinoma $s^2 + 8s + 100$ imamo korijene ili komponente $p_1, p_2, p_3$).
*Uzimajući izraz:* $G_0(s) = \frac{K}{(s + 6)(s^2 + 4s + 8)}$ ili opći oblik s polovima iz zadatka 19 $p_1 = 6$, $p_2, p_3 = 2 \pm j2$.

Za opću shemu $G_0(s) = \frac{K}{(s+p_1)(s+p_2)(s+p_3)}$ s vrijednostima $p_1 = 6, p_2 = 2+j2, p_3 = 2-j2$:


$$(s+6)(s^2+4s+8) = s^3 + 10s^2 + 32s + 48$$

---

### a) Prijenosna funkcija zatvorenog kruga $G_z(s)$

$$G_z(s) = \frac{G_0(s)}{1 + G_0(s)} = \frac{\frac{K}{s^3 + 10s^2 + 32s + 48}}{1 + \frac{K}{s^3 + 10s^2 + 32s + 48}} = \frac{K}{s^3 + 10s^2 + 32s + 48 + K}$$

Nazivnik kao polinom trećeg reda:


$$A(s) = s^3 + 10s^2 + 32s + (48 + K)$$

---

### b) Hurwitzov postupak za određivanje intervala pojačanja $K$

Karakteristična jednadžba:


$$s^3 + 10s^2 + 32s + (48 + K) = 0$$

Koeficijenti:

* $a_3 = 1$
* $a_2 = 10$
* $a_1 = 32$
* $a_0 = 48 + K$

**Uvjeti stabilnosti:**

1. $a_0 > 0 \implies 48 + K > 0 \implies K > -48$
2. Hurwitzova poddeterminanta $D_2 > 0$:

$$D_2 = a_2 a_1 - a_3 a_0 = 10 \cdot 32 - 1 \cdot (48 + K) > 0$$


$$320 - 48 - K > 0 \implies 272 - K > 0 \implies K < 272$$



Budući da pojačanje $K$ fizikalno mora biti pozitivno ($K > 0$), **interval pojačanja $K$ za stabilnost zatvorenog kruga iznosi:**


$$0 < K < 272$$

---

### c) Kritično pojačanje $K_{kr}$ i frekvencija trajnih oscilacija $\omega_{kr}$

1. **Kritično pojačanje:**
Na granici stabilnosti ($D_2 = 0$):

$$K_{kr} = 272$$


2. **Frekvencija trajnih oscilacija $\omega_{kr}$:**
Uvrštavanjem $s = j\omega$ u karakterističnu jednadžbu za $K = K_{kr} = 272$:

$$(j\omega)^3 + 10(j\omega)^2 + 32(j\omega) + (48 + 272) = 0$$


$$-j\omega^3 - 10\omega^2 + 32j\omega + 320 = 0$$


Razdvajanjem na realni i imaginarni dio:
* Realni dio: $-10\omega^2 + 320 = 0 \implies 10\omega^2 = 320 \implies \omega^2 = 32 \implies \omega_{kr} = \sqrt{32} \approx 5.66\text{ rad/s}$
* Imaginarni dio: $-\omega^3 + 32\omega = 0 \implies \omega(\omega^2 - 32) = 0 \implies \omega_{kr} = \sqrt{32} \approx 5.66\text{ rad/s}$



---

### d) Skokovni odzivi u Pythonu za $K = K_t$, $K = K_{kr}$ i $K = 1.2 K_{kr}$

Uzimajući zadano pojačanje regulatora $K_t = 100$:

**Python kôd:**

```python
import matplotlib.pyplot as plt
import control as ct

K_kr = 272
K_values = [100, K_kr, 1.2 * K_kr]  # Kt, Kkr, 1.2*Kkr
labels = ["K = Kt (100) - Stabilan", "K = Kkr (272) - Granično stabilan", "K = 1.2*Kkr (326.4) - Nestabilan"]

plt.figure(figsize=(10, 6))

for K, label in zip(K_values, labels):
    num = [K]
    den = [1, 10, 32, 48 + K]
    sys = ct.tf(num, den)
    t, y = ct.step_response(sys)
    plt.plot(t, y, label=label)

plt.title("Skokovni odzivi zatvorenog kruga za različita pojačanja K")
plt.xlabel("Vrijeme t [s]")
plt.ylabel("y(t)")
plt.legend()
plt.grid(True)
plt.show()

```

**Komentar razlika u odzivima:**

1. **$K = K_t = 100 < K_{kr}$:** Sustav je unutar intervala stabilnosti. Odziv je prigušen i smiruje se u stacionarnom stanju (sustav je **stabilan**).
2. **$K = K_{kr} = 272$:** Sustav se nalazi na samoj granici stabilnosti. Odziv ima neprigušene, trajne oscilacije konstantne amplitude s frekvencijom $\omega_{kr} \approx 5.66\text{ rad/s}$ (sustav je **granično stabilan**).
3. **$K = 1.2 K_{kr} = 326.4 > K_{kr}$:** Pojačanje je prešlo kritičnu granicu. Amplituda oscilacija neograničeno raste s vremenom (sustav je **nestabilan**).
