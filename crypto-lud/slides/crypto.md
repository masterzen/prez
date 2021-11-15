# La cryptographie moderne

&copy; 2021 Brice Figureau

---

## L'histoire d'Alice et Bob

---

## Chiffrement symmétrique

--

## Protocole

<figure>
![Symmetric key protocol](resources/symmetric-key-protocol.svg) <!-- .element width="100%" class="plain" -->
<figcaption>Symmetric key protocol</figcaption>
</figure>

--

## Différents types d'algorithmes

* flux
* block

---

### Chiffrement par flot

* la clé produit un flot infini d'octets (basés sur un générateur pseudo-aléatoire cryptographique)
* opération XOR bit à bit (ou toute autre opération bijective) avec les caractères du texte
* algorithmes fréquemment utilisés
  * RC4
  * A5
  * E0

--

#### RC4 à la loupe

<figure>
![RC4](resources/RC4.svg) <!-- .element width="100%" class="plain" -->
<figcaption>RC4</figcaption>
</figure>

--

#### RC4 à la loupe

```
i := 0
j := 0
while GeneratingOutput:
    i := (i + 1) mod 256
    j := (j + S[i]) mod 256
    swap values of S[i] and S[j]
    K := S[(S[i] + S[j]) mod 256]
    output K
endwhile
```

<figure>
![RC4 PRGA](resources/RC4-s-table.svg) <!-- .element width="60%" class="plain" -->
<figcaption>RC4 S-table</figcaption>
</figure>

---

### Chiffrement par bloc

* découpage du message en blocs de 8 ou 16 octet
* clé de même taille que le bloc
* chiffrement par bloc
* algorithmes les plus connus:
  * 3DES
  * Blowfish/Twofish
  * AES

--

### AES à la loupe

* blocs de 128, 192 ou 256 bits
* conçu pour résister

--

### AES - étage d'entrée

Le message clair est placé dans une matrice 4x4 (128 bits):

|  |  |  |  |
|--|--|--|--|
| P0 | P1 | P2 | P3 |
| P4 | P5 | P6 | P7 |
| P8 | P9 | P10 | P11 |
| P12 | P13 | P14 | P15 |

appelé 'État'

--

### AES - un tour

L'algorithme fait subir les transformations suivantes à chaque tour (répété 9, 11, ou 13 fois)

1. substitution par octet (`SubBytes`)
2. décalage par ligne (`ShiftRows`)
3. mélange par colonne (`MixColumns`)
4. XOR avec la clé du tour (`AddRoundKey`)
5. on recommence au 1. :)

--

### AES - 1. Substitution

 Application d'une S-box (non linéaire)

<figure>
![AES SubBytes](resources/AES-SubBytes.svg) <!-- .element width="70%" class="plain" -->
<figcaption>AES SubBytes</figcaption>
</figure>

Note: non linéaire, S-box: table de lookup précalculée

--

### AES - 2. Décalage lignes


<figure>
![AES ShiftRows](resources/AES-ShiftRows.svg) <!-- .element width="70%" class="plain" -->
<figcaption>AES ShiftRows</figcaption>
</figure>

Note: permet d'éviter que les colonnes soient chiffrées indépendemment transformant l'algo en 4 chiffrements plus faibles. Grace à ce décalage, les colonnes de sorties contiennent des informations de toutes les colonnes d'entrées.

--

### AES - 3. Mélange colonnes

<figure>
![AES MixColumns](resources/AES-MixColumns.svg) <!-- .element width="50%" class="plain" -->
<figcaption>AES MixColumns</figcaption>
</figure>

`$\begin{bmatrix}
b_{0,j} \\ b_{1,j} \\ b_{2,j} \\ b_{3,j}
\end{bmatrix} = \begin{bmatrix}
2 & 3 & 1 & 1 \\
1 & 2 & 3 & 1 \\
1 & 1 & 2 & 3 \\
3 & 1 & 1 & 2
\end{bmatrix} \begin{bmatrix}
a_{0,j} \\ a_{1,j} \\ a_{2,j} \\ a_{3,j}
\end{bmatrix}
\qquad 0 \le j \le 3$`

Note: équivalent à des calculs polynomiaux dans le corps de Galois fini 2^8

--

### AES - 4. Clé de tour

A chaque tour un sous-clé (taille du bloc) est dérivée de la clé principale par l'algorithm `KeyScheduler`

<figure>
![AES AddRoundKey](resources/AES-AddRoundKey.svg) <!-- .element width="50%" class="plain" -->
<figcaption>AES AddRoundKey</figcaption>
</figure>

--

### Mode opératoire des algorithme à bloc

* Padding: ajout d'octets morts pour compléter le dernier bloc (par ex des octets nuls)
* Initialization Vector: clé additionnelle
* enchainement de blocs: ECB, CBC, etc

--

#### ECB (Electronic codebook)

L'opération la plus simple, chaque bloc de texte est chiffré indépendemment des suivants.

* un même block source, donnera le même bloc chiffré
* laisse apparaitre des motifs dans les données chiffrées
* ne surtout pas utiliser

--

#### CBC (Cipher block chaining)

<figure>
![CBC](resources/CBC.svg) <!-- .element width="80%" class="plain" -->
<figcaption>CBC</figcaption>
</figure>

--

#### OFB (Output Feedback)

<figure>
![OFB](resources/OFB.svg) <!-- .element width="80%" class="plain" -->
<figcaption>OFB</figcaption>
</figure>

--

#### CTR (Counter Mode)

<figure>
![CTR](resources/CTR.svg) <!-- .element width="80%" class="plain" -->
<figcaption>CTR</figcaption>
</figure>

---

## Chiffrement asymmétrique

--

### Protocole

