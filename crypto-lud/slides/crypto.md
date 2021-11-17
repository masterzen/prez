# La cryptographie moderne

&copy; 2021 Brice Figureau

---

## Alice, Bob et Eve

<figure>
![Alice](resources/alice.png) <!-- .element width="20%" class="plain"-->
![Bob](resources/bob.png) <!-- .element width="20%"  class="plain"-->
![Eve](resources/eve.png) <!-- .element width="20%" class="plain" -->
</figure>


---

## Chiffrement symmétrique

--

## Protocole

<figure>
![Symmetric key protocol](resources/symmetric-key-protocol.svg) <!-- .element width="75%" class="plain" -->
<figcaption>Symmetric key protocol</figcaption>
</figure>

--

## Différents types d'algorithmes

* par flot
* par block

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

* découpage du message en blocs de 8 ou 16 octets
* clé de même taille que le bloc
* chiffrement par bloc
* algorithmes les plus connus:
  * 3DES
  * Blowfish/Twofish
  * AES

--

### AES à la loupe

* blocs de 128, 192 ou 256 bits
* conçu pour résister à de nombreuses attaques
* standard du NIST
* facilement implémentable en hardware
* rapide en soft
* utilisé partout

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

A chaque tour une sous-clé (taille du bloc) est dérivée de la clé principale par l'algorithm `KeyScheduler`

<figure>
![AES AddRoundKey](resources/AES-AddRoundKey.svg) <!-- .element width="50%" class="plain" -->
<figcaption>AES AddRoundKey</figcaption>
</figure>

--

### Mode opératoire des algorithmes à bloc

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

<style type="text/css">
  .reveal p {
    text-align: left;
  }
  .reveal ul {
    display: block;
  }
  .reveal ol {
    display: block;
  }
</style>

Concept inventé par Whitfield Diffie & Martin Hellman en 1976, et largement utilisé de nos jours dans toutes les communications numériques, les paiement par carte, etc (PKI)

--

### Protocole: une histoire de cadenas

<figure>
![Cadenas](resources/lock-sending.svg) <!-- .element width="80%" class="plain" -->
<figcaption>Protocole du cadenas</figcaption>
</figure>


note: Pour simplifier, cela revient par exemple pour Bob à envoyer un cadenas ouvert à Alice et à garder la clé. Alice peut mettre un message dans une boite et la fermer avec le cadenas, seul Bob peut l'ouvrir.
Un attaquant recevant le cadenas ouvert, ou interceptant la boite ne pourra l'ouvrir, car seul Bob possède la clé.

--

### Protocole

<figure>
![Public Key](resources/asymmetric-key-message.svg) <!-- .element width="80%" class="plain" -->
<figcaption>Chiffrement à clé publiques</figcaption>
</figure>


--


### Les algorithmes

* seuls RSA et les algorithmes à courbe elliptiques sont actuellement sûrs
* ces algorithmes sont lents
* ils sont tous basés sur une opération mathématique réputée "complexe" (incassable en temps raisonnable en force brute)

Note: RSA >= 2048bits

--

#### RSA

* du nom de ses créateurs: Ron Rivest, Adi Shamir, Leonard Adleman.
* basé sur la difficulté à factoriser un très grand nombre
* et sur les calculs en groupe de Galois fermé (mod n)

--

#### RSA: création des clés

1. générons aléatoirement deux nombres premiers très grands `p` et `q`
2. calculons: `$n = pq$`
3. choisissons aléatoirement un nombre `e` de telle sorte que `e` soit premier avec `$\phi(n) = (p - 1)(q - 1)$`
4. calculons `$\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} d = e^{-1}\Mod \phi(n)$`
5. `(d,n)` est la clé privée, et `(e,n)` la clé publique
6. on jette `p` et `q` qui ne servent plus (mais qui peuvent compromettre l'opération)

A noter que `n` doit être un grand nombre (par ex >= 2048 bits, soit un nombre d'environ 650 chiffres decimaux)

note: phi est l'indicatrice d'Euler

--

#### RSA: chiffrement & déchiffrement

1. découpage du message en blocs formant des nombres `$ < n $`
2. pour chiffrer chaque bloc: `$ \newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} c_i = m_i^e \Mod n $`
3. pour déchiffer: `$\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} m_i = c_i^d \Mod n$`

Pourquoi cela fonctionne:

`
$$
\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1}
\begin{align}
  & c_i^d \Mod n \\
  & = (m_i^e)^d \Mod{n} \\
  &  = m_i^{ed} \Mod{n} \\
  &  = m_i^{ee^{-1}} \Mod{n} \\
  &  = m_i \Mod{n}
   = m_i
\end{align}
$$
`

note: les calculs mod n ont des propriétés permettant d'être relativement rapides, pas besoin de faire des puissances de grand nombres, on peut réduire les puissances à un certain nombre de multiplications`

--

#### RSA: chiffrement I

1. avec `$p=241$` et `$q=223$` (premier aléatoires) `$n = pq = 53743$`
2. `e` ne doit avoir aucun facteur commun avec `$ \phi(n) = (p-1)(q -1) = 53280$`
3. choisissons `$ e = 2489 $` (dans la pratique c'est souvent 65537)
4. `$\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} d = 2489^{-1} \Mod 53280 = 21449 $`
5. on envoie `$(2489, 53743)$` à Alice on garde précieusement `$(21449,53743)$`

note: les calculs mod n ont des propriétés permettant d'être relativement rapides, pas besoin de faire des puissances de grand nombres, on peut réduire les puissances à un certain nombre de multiplications`

--

#### RSA: chiffrement II

Découpage du message: 'Hello Alice' en nombres `$< 53280$`:

| lettres | nombre | chiffrage |
|---------|-------:|----------:|
| He | `$72*256+101 = 18533$` | `$\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} 18533^{2489} \Mod 53743 = 4589 $`|
| ll | `$108*256+108 = 27756$` | `$\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} 27756^{2489} \Mod 53743 = 43255 $`|
| o  | `$111*256+32 = 28448$` | `$\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} 28448^{2489} \Mod 53743 = 38054 $`|
| Al | `$65*256 + 108= 16748$` | `$ \newcommand{\Mod}[1]{\ \mathrm{mod}\ #1}16748^{2489} \Mod 53743 = 42848 $`|
| ic | `$105*256+99 = 26979$` | `$\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} 26979^{2489} \Mod 53743 = 13350 $`|
| e | `$101$` | `$\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1} 101^{2489} \Mod 53743 = 42881 $`|

Message chiffré: `4589 43255 38054 42848 13350 42881` ou `11ed a8f7 94a6 a760 3426 a781` (hexadécimal)

--

#### RSA: déchiffrement

<style type="text/css">
  .reveal p {
    text-align: left;
  }
  .reveal ul {
    display: block;
  }
  .reveal ol {
    display: block;
  }
</style>

rappel: message en clair: 
`18533 27756 28448 16748 26979 101`

Message chiffré:
`4589 43255 38054 42848 13350 42881`

`
$$
\newcommand{\Mod}[1]{\ \mathrm{mod}\ #1}
4589^{21449} \Mod 53743 = 18533 \\
43255^{21449} \Mod 53743 = 27756 \\
38054^{21449} \Mod 53743 = 28448 \\
...
$$
`

---

## Fonction de hachage cryptographique

Algorithme qui transforme une source de taille arbitraire en un résultat de taille fixe depuis lequel il est pratiquement impossible de retrouver la source. Cela permet de calculer une empreinte numérique d'un message.

--

### Propriétés

* déterministe (un même message donnera toujours le même résultat)
* facile à calculer
* impossible de construire un message depuis un résultat donné
* impossible de trouver un autre message ayant la même résultat qu'un message donné
* impossible de trouver deux messages différents ayant la même valeur de hachage
* modifier un tant soit peu un message modifie considérablement la valeur de hachage

--

### Utilisations

* vérification d'intégrité de message
* vérification de mot de passe
* vérification de signatures
* identification de fichiers/données

note: pour signer on calcul le hachage du message puis calcul de la signature sur le hash.

--

### Exemples

* MD5 (n'est plus sécure)
* SHA-1 (bof bof aussi)
* SHA256

---

## Échange de clés

Comment échanger des clés entre Alice et Bob sans qu'Eve ne puisse récupérer celles-ci.

--

## Diffie Helmann




---

## La cryptographie et Internet

Le protocole derrière HTTPS appelé SSL/TLS utilise de 