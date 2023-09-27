---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.15.2
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Especificaciones de sistemas de control en el dominio de la frecuencia

## Sensibilidad y sensibilidad complementaria

Sea el sistema de control de la {ref}`espec_frec_fig1`. Su función de transferencia de lazo es $L=GK$ y las relaciones de lazo cerrado son:

$$
e=S (r-d Gd)
u=S K (r-d)
y=Gd S d+T r
$$

```{figure} espec_frec_fig1.png
---
height: 150px
alt : sistema realimentado donde K(s) es el compensador G(s) es la planta y G_d(s) es la TF de la perturbación
name: espec_frec_fig1
align : center
---
Sistema realimentado genérico
```

Las dos funciones de transferencia más importantes son:
La sensibilidad $S$: Es la función de transferencia entre la entrada de referencia $r$ y el error $e$ (en ausencia de perturbaciones). También es la función de transferencia entre la perturbación $d$ y la salida $y$ con $G_d=1$ cuando la referencia $r$ es cero.

$$
S=\frac{1}{1+L}
$$

La sensibilidad complementaria T: Es la función de transferencia entre la referencia $r$ y la salida $y$ (en ausencia de perturbaciones).

$$
T=\frac{L}{1+L}
$$

se cumple que: $S+T=1, \Rightarrow  T=1-S$

* Las referencias, perturbaciones y ruidos que afectan a un sistema de control tienen una frecuencia característica, que no suele ser fácil representar o modelar.
* La capacidad de rechazar perturbaciones o de seguir referencias puede especificarse mejor en el dominio frecuencial que en el plano-s.

## Control perfecto

El error de un sistema de control, definido como $e=r-y$ es

$$
e=r-y=Sr-G_dSd+T\eta
$$

Control perfecto significa que el error $e \approx 0$, para que esto suceda, es necesario que $S\approx 0$ para que los términos $Sr\approx 0$ y $G_dSd\approx 0$ y $T \approx 0$ para que $T\eta \approx 0$, esto es posible solamente para distintas frecuencias, ya que $S+T=1$. Por lo tanto, si las referencias $r$ y perturbaciones $d$ se encuentran en la zona de frecuencias donde $S \approx 0$ y el ruido $\eta$ en la zona de frecuencias donde $T\approx 0$, es posible logra control perfecto.

## Características de lazo cerrado

La sensibilidades $S$ y $T$ especifican la capacidad de seguimiento de referencias o de atenuación de perturbaciones y ruidos de un sistema de control.

Características sobre $S$:

* _Ancho de Banda_ ($\omega_b^S$): Establece la banda de frecuencias donde las perturbaciones $d$ no se atenúan, ($\omega_b^S, \infty$).
* _Pico de resonancia_ ($M_p^S$): Es la máxima amplificación de ganancia.
* _Frecuencia de pico_ ($\omega_p^S$): Es la frecuencia a la que ocurre el pico resonante.

Características sobre $T$:

* _Ancho de Banda_ ($\omega_b^T$): Establece la banda de frecuencias donde las referencias $r$ que pueden ser seguidas, ($0,\omega_b^T$).
* _Pico de resonancia_ ($M_p^T$): Es la máxima amplificación de ganancia.
* _Frecuencia de pico_ ($\omega_p^T$): Es la frecuencia a la que ocurre el pico resonante.

```{figure} espec_frec_fig2.png
---
height: 150px
alt : Módulo de la funciones de sensibilidad S y T
name: espec_frec_fig2
align : center
---
Módulo del Bode de $S$ y $T$
```

## Características de lazo abierto

Las principales características que se obtienen de la función de transferencia a lazo abierto $L$ son:

* _Margen de ganancia_ $MG$ la ganancia cuando la fase vale -180°.
* _Margen de fase_ $MF$ la fase sobre los -180° para la frecuencia $\omega_c$.
* _Frecuencia de corte_ $\omega_c$ es la frecuencia en la cual $|L(j\omega)|= 1$  o $0dB$.

La pendiente de $|L|$ en el entorno de la frecuencia de corte $\omega_c$ no debe ser muy elevada para que los margenes de estabilidad sean razonables.

```{figure} espec_frec_fig3.png
---
height: 150px
alt : Margenes de fase y de ganancia en el diagrama de Bode de la función de lazo L
name: espec_frec_fig3
align : center
---
Margenes de fase y ganancia de sistema
```

## Objetivos de un sistema de control

Sea el sistema de control de la figura {ref}`espec_frec_fig1`. Las relaciones entre todas las variables importantes del sistema son:

$$
y=Tr+G_dSd-T\eta+SGl
$$
$$
e=Sr-G_dSd+T\eta-SGl
$$
$$
u=SKr-G_dSKd-SK\eta-Sl
$$

siendo $T=\frac{L}{1+L}$, la sensibilidad complementaria. Además $L$ es estrictamente propia, es decir $\lim_{\omega\rightarrow \infty}|L(j\omega)|=0$ por lo que  $\lim_{\omega\rightarrow \infty}|S(j\omega)|=1$ y $\lim_{\omega\rightarrow \infty}|T(j\omega)|=0$.

Las relaciones anteriores quedan completamente determinadas por las seis funciones de transferencias de sensibilidad: $S$, $T$,$G_dS$, $SG$, $SK$ y  $G_dSK$, que deben diseñarse para atenuar el efecto de las señales exógenas $r$, $l$, $d$ y $\eta$ sobre el lazo de control.

Los objetivos de control son:

1. Las sensibilidades $S$, $T$,$G_dS$, $SG$, $SK$ y  $G_dSK$ deben ser estables. (estabilidad interna)
1. Para conseguir seguimiento asintótico perfecto (es decir $y=r$), en ausencia de perturbaciones, ante escalones en la referencia $r$, $|T(j\omega)|= 1$ para bajas frecuencias es decir $L(j\omega)$ debe ser grande.
1. Ademas el efecto de las perturbaciones $l$, $d$ y $\eta$ sobre el lazo de control debe ser pequeño, para ello:

* $|S|$ debe ser pequeño en la banda de frecuencias de las perturbaciones $d$, para no deteriorar la señal de salida $y$. Es decir $|L|$ debe ser grande para dicha zona de frecuencias.
* Para no deteriorar el error de seguimiento $r-y$, $S$ debe ser pequeño en las banda de frecuencias de $r$ y $d$, $|T|$ debe ser pequeño para las frecuencias características del ruido $\eta$ y $|SG|$ debe ser pequeño en la banda de frecuencias de la perturbación $l$.
* Finalmente, para que el esfuerzo de control $u$ sea moderado, $|SK|$ debe ser moderado en aquellas frecuencias donde $|T|>1$. En caso contrario podrían saturarse los actuadores que generan $u$.

## Especificaciones sobre las sensibilidades

Los objetivos de control parecen ser contradictorios, ya que al ser $S+T=1$, si la sensibilidad $S$ debe ser pequeña $|S|<<1$, es decir $|L|>>1$, entonces $|T|=\frac{L}{1+L}$ no puede ser también pequeña $|T|<<1$, esto genera una relación de compromiso para $|L|$.

* La solución de la paradoja está en que las frecuencias características de cada señal exógena son diferentes (en el mejor de los casos).
* Las señales de referencia $r$ y las perturbaciones $l$ y $d$ son típicamente de baja frecuencia , $\omega \leq \omega_1$.
* las señales de ruido en los sensores $\eta$ son de alta frecuencia, $\omega \geq \omega_2$.

Por tanto: $|S|<<1$ en una banda de frecuencias $(0, \omega_1]$ y $|T|<<1$ en una banda de frecuencias $[\omega_2,\infty)$, con $\omega_1<\omega_2$.

La atenuación se especifica utilizando las cantidades $M_a$ y $M_b$.

$$
|S|<M_b<<1 \text{ para }\omega \leq \omega_1\text{, } |T|<M_a<<1 \text{ para } \omega \geq \omega_2  
$$

Las frecuencias $\omega_1$ y $\omega_2$, y los factores de atenuación $M_a$ y $M_b$ dependen de cada problema especifico.

## Especificaciones sobre la función de transferencia a lazo abierto $L(s)$

Las especificaciones sobre $|S|$ y $|T|$ pueden ponerse en función de $|L|$ teniendo en cuenta que:

$$
\text{Siendo } S=\frac{1}{1+L} \text{, } |S|<<1   \Rightarrow |L|>>1 \text{ y } |S|\approx \frac{1}{|L|}
$$

$$
\text{Siendo } T=\frac{L}{1+L} \text{, } |T|<<1   \Rightarrow |L|<<1 \text{ y } |T|\approx |L|
$$

En baja frecuencia (Zona B): Atenuación de perturbaciones de proceso.

$$
\omega \leq \omega_1 \text{ : } |S(j\omega)|<-M_b \Rightarrow |L(j\omega)|>M_b
$$

En alta frecuencia (Zona A): Atenuación ruido en los sensores.

$$
\omega \geq \omega_2 \text{ : } |T(j\omega)|<-M_a \Rightarrow |L(j\omega)|<-M_a
$$

En media frecuencia (Zona C): Se busca buena estabilidad relativa.

$$
\omega_1 < \omega_c \approx \omega_b^T<\omega_2 \text{, con } |L(j\omega_c)|=1(=0dB)
$$

En términos de los márgenes de estabilidad es necesario margen de fase $MF>50°$, margen de ganancia $MG>12dB$ y margen de sensibilidad o radio de estabilidad $RS\geq 0.5$, por lo que, $máx|S(j\omega)|<1/RS=2$.

La pendiente de $|L(j\omega)|$ en las proximidades de la frecuencia de corte no debe ser superior a $-20dB/dec$ para conseguir estabilidad relativa.

## Diseño de controladores en el dominio frecuencial
