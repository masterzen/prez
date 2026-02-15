---
title: "Astrophotographie du ciel profond"
revealOptions:
  transition: "slide"
  slideNumber: true
  hash: true
  controls: true
  progress: true
---

<!--
Usage (exemples):
- reveal-md:
  reveal-md deck.md --watch --theme black --css style.css
  (MathJax activé par défaut sur reveal-md; sinon ajouter --mathjax)
- Quarto:
  quarto render deck.md (format revealjs)
- Reveal.js natif:
  inclure ce markdown via plugin markdown + plugin math
-->

# Astrophotographie du ciel profond

Brice Figureau

Lud'hiver 2026

---

## Nébuleuses

<img src="./img/ngc7000.jpg" class="r-stretch" />

---

## Galaxies

<img src="./img/ngc3628.jpg" class="r-stretch" />

---


## Amas

<img src="./img/ngc1866.jpg" class="r-stretch" />

---

# Coordonnées

Note:
Objectif: relier rotation terrestre → référentiels → choix de monture.
Garder en tête: RA/DEC = repère inertiel (étoiles), Alt/Az = repère local (observateur).

---

## Coordonnées équatoriales

* RA (ascension droite) : 0-24h (augmente vers l'est)
* DEC (déclinaison) : -90º -> +90º (pôles célestes)
* repère quasi fixe (hormis précession) - J2000/JNOW
* catalogue d'objets avec leurs coordonnées

<figure>
<img src="./img/equatorial-coord.png" height="50%" />
</figure>

Note:
Insister: RA/DEC ne dépend pas de l’heure ni du lieu (en première approximation).
C’est le repère “naturel” pour suivre le ciel sans rotation de champ sur une équatoriale.

---

## Alt/Az

* Alt : angle au-dessus de l’horizon (0° à 90°)
* Az : direction sur l’horizon (0°=Nord, 90°=Est…)
* Dépend de <b>l’heure</b> et de la <b>position</b> (latitude/longitude)</li>

<figure>
<img src="./img/alt-az.png" height="50%" />
</figure>

Note:
Dire clairement: même si la cible a un RA/DEC fixe, son Alt/Az varie continuellement.
Donc une monture Alt/Az doit bouger sur 2 axes en permanence.

---

## Problème Nº1

# La plupart des objets célestes sont petits (< 1º) et loin.

---

## Optiques

---

### Lunettes (réfracteurs)

* setup simple, étoiles propres, peu de maintenance  
* idéal débutant (focale modérée)  
* coût au diamètre, chromatisme si non APO
* accessoires : aplanisseur de champ, réducteur

<figure>
<img src="./img/refractor.png" width="1000" />
</figure>

---

### Newton

* excellent rapport diamètre/prix  
* souvent “rapide” (faible $f/D$)  
* collimation + sensibilité mécanique  
* coma : correcteur quasi obligatoire

<figure>
<img src="./img/newtown.png" width="1000"/>
</figure>

---

## Schmidt-Cassegrain / RC

* focale longue (galaxies / petits objets)  
* compacts  
* souvent $f/D$ élevé → plus exigeant  
* champ plus étroit, collimation délicate  

<figure>
<img src="./img/schmidt-cassegrain.png"  width="1000" />
</figure>

---

## Paramètres optiques clés

- **Diamètre** : collecte (capte plus de photons)
- **Focale** : champ & échelle
- **Rapport $f/D$** : vitesse “photographique”
- **Qualité de champ** : coma, courbure, vignettage

Échantillonnage (règle pratique) :

$$
\text{Échelle (arcsec/px)} = 206.265 \times \frac{p(\mu m)}{f(mm)}
$$


---

## Problème Nº2

# Ces objets émettent très peu de lumière.

---

## Poses longues

<figure>
<img src="./img/raw-no-stretch.png" width="50%"/>
<img src="./img/raw-histogram.png" width="20%"/>
</figure>

---

## Poses longues - 2

<figure>
<img src="./img/raw-stretched.png" width="60%"/>
</figure>

---

## Capteurs et caméras

---

## DSLR / hybrides vs caméras astro

* **appareil numérique classique**
  - polyvalents, accessibles (+)
  - bruit thermique, filtre IR (-)
  - traitements automatiques (-)

* **Caméras astro CMOS**
  - refroidissement, contrôle gain/offset (+)
  - meilleure sensibilité/full well (+)
  - mono vs couleur (OSC)

<figure>
<img src="./img/zwo-asi2600mm.webp" width="500"/>
</figure>

---

## Fonctionnement

<figure>
<img src="./img/pixel-adc.png" class="r-stretch"/>
</figure>

---

## Matrice de Bayer

<figure>
<img src="./img/bayer.png" class="r-stretch"/>
</figure>

---

## Gain/ISO

<figure>
<img src="./img/gain.png" class="r-stretch"/>
</figure>

---

## Paramètres capteur clés

- Taille pixel $p$ (résolution/échantillonnage)
- QE (quantum efficiency)
- Bruit de lecture $N_r$
- Full well capacity (saturation)
- Dynamique
- Gain / ISO

Notion :
$$
\text{Dynamique} \sim \frac{\text{Full Well}}{\text{Read Noise}}
$$

---

## Mono vs couleur (OSC)

- **OSC**
  - simplicité
  - matrice de Bayer

- **Mono**
  - flexibilité (LRGB, narrowband)
  - SNR par canal plus efficace
  - plus complexe (roue à filtres, temps, calibration)

---

## Problème Nº3

# La terre tourne sur elle même (vite)

---

## Montures

---

## Montures : types

- **Azimutale** : simple, mais rotation de champ (limite ciel profond)
- **Équatoriale** : standard ciel profond
  - manuelle / GoTo
  - entraînement courroie
  - harmonic drive (selon modèles)

<figure>
<img src="./img/equatorial-mount.webp" class="r-stretch"/>
</figure>

---

## Critères essentiels

- Capacité de charge **réelle** (viser 50–70% du max)
- Précision du suivi / erreur périodique
- Rigidité (trépied/colonne)
- Facilité de mise en station

---

## Problème Nº4

# Pollution lumineuse

---

## Bortle

<figure>
<img src="./img/bortle.jpg" class="r-stretch"/>
</figure>

---

## Mono & filtres "narrowband"

<figure>
<img src="./img/narrowband.webp" class="r-stretch"/>
</figure>

---

## Roue à filtre

<figure>
<img src="./img/filter-wheel.jpeg" width="50%"/>
</figure>

---

## Problème Nº5

# Le bruit

---

## Signal

### Nous voulons capturer le signal venu de l'objet.
### Et seulement son signal.

---

## Bruit

<figure>
<img src="./img/shot-noise.png" width="60%"/>
</figure>

---

## Sources de bruit

- Bruit de photon (shot noise)
- Fond de ciel : pollution lumineuse + Lune
- Bruit thermique / dark current
- Bruit de lecture (électronique)

---

## Sources de bruit

<figure>
<img src="./img/noise.png" class="r-stretch"/>
</figure>

---

## Bruit

* Variation aléatoire autour de la moyenne du signal
* modélisable avec une distribution de Poisson
* notre objectif: minimiser le bruit, favoriser le signal

---

## SNR

$$
\mathrm{SNR} \approx \frac{Signal_{object}}{\sqrt{Signal_{object} + Signal_{skyglow} + Signal_{thermal} + R^2}}
$$

- $Signal_{object}$ : signal de l’objet  
- $Signal_{skyglow}$ : fond de ciel  
- $Signal_{thermal}$ : bruit thermique/dark current  
- $R$ : bruit de lecture (read noise)  

---

## Augmenter l'intégration

* poses plus longues
* ou, augmenter le nombre de pose

$$
\mathrm{SNR} \approx \frac{N \cdot Signal_{object}}{\sqrt{ N \cdot \(Signal_{object} + Signal_{skyglow} + Signal_{thermal} + R^2\)}}
$$

---

<figure>
<img src="./img/ngc7000_noise.png" width="70%"/>
</figure>

---

## Bruit thermique

### refroidissement de la caméra

---

## Limiter le fond de ciel

### filtres narrowband et/ou site sombre

---

## Problème Nº6

# L'atmosphère

---

### Masse d'air

* Seeing (turbulences)
* Altitude de l'objet 
  * masses d'air traversées
  * diffusion

<figure>
<img src="./img/airmass.png" width="60%"/>
</figure>

---

## Problème Nº7

# Température et rosée

---

## Rosée & buée

* pare-buée
* résistance chauffante

<figure>
<img src="./img/dewheater.jpeg" width="30%"/>
</figure>


---

## Changements de température

* le point focal est très précis
* changements de température -> impact sur la netteté
* auto-focus et sonde de température

<figure>
<img src="./img/eaf-temp-probe.jpeg" width="30%"/>
</figure>

---

# Une séance type

0. **planification**
1. **installation**: on sort le matos, équilibre thermique
2. **mise au point**: bas les masques (de Bahtinov)
3. **mise en station** : collecte des photons  
4. **suivi et guidage** : on pointe vers la cible
5. **acquisition**: on prend les photos
6. **calibration**: on élimine le bruit
7. **post-traitement**: on fait une belle photo

---

## Planification

* trouver les bonnes cibles
  * visibles longtemps
  * bien au dessus de l'horizon
  * taille en accord avec notre focale/capteur
  * loin de la lune
* programmer à l'avance les séquences


<figure>
<img src="./img/planification-rosette.png" width="60%"/>
</figure>


---

## Installation

* Commencer avant la nuit
* Ciel dégagé
* Accès à l'éclectricité (ou batterie)

<figure>
<img src="./img/IMG_2603.jpeg" width="30%"/>
</figure>

---

## Mise au point

### Masque de Bahtinov

<figure>
<img src="./img/bahtinov.jpg" class="r-stretch"/>
<img src="./img/bahtinov-2.png" class="r-stretch"/>
</figure>

---

## Mise au point

### EAF

<figure>
<img src="./img/IMG_2319.jpeg" width="40%"/>
</figure>

---

## Mise en station

- Polariscope / alignement polaire assisté
- Méthodes logicielles (plate solving, drift align)
- Impact : étoiles rondes + guidage plus stable

<figure>
<img src="./img/polar-alignment-1.webp" class="r-stretch"/>
</figure>

---

## Suivi & guidage

* Suivi sidéral = mouvement quasi pur en <b>RA</b>
* Corrections en <b>DEC</b>
* Dithering: petites translations entre poses → réduit bruit structuré

<figure>
<img src="./img/IMG_3477.jpeg" width="40%"/>
</figure>

Note:
Expliquer le “shape” typique: RA oscille autour de 0 avec corrections, DEC presque plat si polar align OK.
Ajouter: backlash DEC rend les corrections alternées inefficaces → d’où l’intérêt d’éviter de “chasser” en DEC.

---

## Autoguidage

- permet des pauses plus longues
- Corrige :
  - erreurs périodiques
  - flexions / vent
  - micro-erreurs de mise en station

<figure>
<img src="./img/guide-scope.jpg" width="500"/>
<img src="./img/oag.jpg" width="500"/>
</figure>

---

## Acquisition

* Controllée par un ordinateur et un logiciel spécialisé
* séquencement des images, controle du focus et de la route à filtre

---

### Les 4 types d’images

- **Lights** : signal + bruit + défauts optiques/capteur
- **Darks** : bruit thermique + pixels chauds
- **Bias** : offset électronique / lecture
- **Flats** : vignettage + poussières + non-uniformités

Option : **dark-flats** (selon workflow capteur)

---

### Lights

* pose de 300s, filtre Ha, auto-stretched
* IC1805

<figure>
<img src="./img/Light_IC1805_300.0s_Bin1_2600MM_H_gain100_20240816-011041_0016.jpg" width="60%"/>
</figure>

---

### Darks

- Même :
  - temps de pose
  - gain/ISO
  - température
- Capture : bouchon, dans le noir
- Sert à modéliser :
  - courant d’obscurité
  - pixels chauds

---

### Bias

- Temps de pose minimal (ou très court)
- Même gain/ISO
- Sert à :
  - offset de lecture
  - composante fixe du signal électronique

---

### Flats

- Même train optique (focus, orientation, filtres)
- Sert à corriger
  - vignettage
  - poussières
  - défauts optiques

<figure>
<img src="./img/IMG_3163.jpeg" width="30%"/>
</figure>

---

### Flats

<figure>
<img src="./img/masterFlat-Ha_ngc7000.jpeg" width="60%"/>
</figure>

---

## Calibration

<figure>
<img src="./img/calibration.png" class="r-stretch"/>
</figure>

---

### Formule de calibration

$$
L_{\text{cal}} \approx \frac{L - D}{F}
$$

où :
- $L$ = light brut
- $D$ = master dark (incluant offset si applicable)
- $F$ = flat normalisé

---

# Stacking

<figure>
<img src="./img/stacking.png" class="r-stretch"/>
</figure>

---

## Pourquoi empiler ?

- Améliore le SNR statistiquement
- Permet le rejet d’artefacts :
  - satellites
  - avions
  - pixels chauds résiduels

---

## Registration/alignement

* repérage des étoiles dans la meileure light


<figure>
<img src="./img/regsitration-exp.png" class="r-stretch"/>
</figure>


---

## Rejet statistique

- Médiane : robuste mais moins optimal SNR
- Sigma-clipping : compromis courant
- Winsorized sigma / Linear fit clipping

<figure>
<img src="./img/plane_ic1805.jpg" width="50%"/>
</figure>

---

# Post-traitement (workflow)

---

# But : obtenir une image en couleur de haute qualité

---

## Les bases

* en phase linéaire:
  * Linear fit
  * enlèvement des étoiles
  * synthèse des couleurs (mono)
  * Elimination des gradients
  * Calibration des couleurs (osc/lrgb)
  * déconvolution
  * stretch
* en phase non-linéaire:
  * reduction du bruit
  * courbes de transformation
  * amélioration netteté & contraste
  * fusion des étoiles

---

## Synthèse des couleurs

<figure>
<img src="./img/sho.drawio.png" width="70%"/>
</figure>

---

## Stretch

* image “linéaire” (faible contraste).  
* application d'un étirement non-linéaire (courbes, arcsinh, histogram transform).

<figure>
<img src="./img/stretching.webp" width="70%"/>
</figure>


---

## OSC

<figure>
<img src="./img/osc-processing.png" width="70%"/>
</figure>

---

## Mono LRGB

<figure>
<img src="./img/lrgb-processing.png" width="70%"/>
</figure>

---

## Mono SHO

<figure>
<img src="./img/sho-processing.png" width="70%"/>
</figure>

---

# Quelques exemples

---

## Nébuleuse de la trompe d'éléphant (IC 1396)

<figure>
<img src="./img/ic1396-signature.jpg" width="30%"/>
</figure>

Note:
10h24 integration, fake RGB stars, SHO
2,400 années lumière

---

## Nébuleuse du coeur (IC 1805)

<figure>
<img src="./img/ic1805_signature.jpg" width="30%"/>
</figure>

Note:
14h15 integration, RGB stars, SHO
Nebuleuse du coeur, en dessous celle du poisson
7500 années lumières, constellation de Cassiopée
Découverte par William Herschel le 3 November 1787.

---

## Triplet du lion

<figure>
<img src="./img/LeoTriplet.jpg" width="60%"/>
</figure>

Note:
21h40, LRGB process
35 millions d'années-lumière dans la constellation du Lion. Cet amas regroupe les galaxies spirales M65, M66, et NGC 3628 , communément appelée "la galaxie du Hamburger".

---

## Nébuleuse du voile (NGC 6960)

<figure>
<img src="./img/NGC6960_signature.jpg" width="70%"/>
</figure>

Note:
14h, HOO, RGB stars
dentelles du Cygne[2], un rémanent de supernova. La supernova d'origine devait être une étoile 20 fois plus massive que le Soleil qui a explosé il y a entre 10 000 et 20 000 ans[3].

---

## Nébuleuse de l'Amérique du Nord et pélican (NGC 7000)

<figure>
<img src="./img/NGC7000_signature.jpg" width="70%"/>
</figure>

Note:
18h05
émission, constellation du Cygne
2590 années-lumière


---

## Quelques logiciels

- **planification**: Stellarium, SkyTools 4
- **acquisition**: NINA+PHD2, Asiair, Ekos/kstars
- **calibration & traitements**: Siril, PixInsight, Astro Pixel Processor
- **retouches finales**: Gimp, Photoshop

---

# Vous voulez vous lancer ?

---

## Attention !

* Une passion pour bidouilleur (beaucoup de paramètres)
* Lire/regarder des tuto
* Avoir un bon porte-monnaie peut aider
* Avoir du temps pour récupérer
* Habiter sous un ciel sombre et dégagé
* Ne pas sous-estimer la monture
* Commencer avec une petite focale (refracteur)
* Y aller progressivement
* Adhérer à un club ou association

---

## Litterature

* The Astrophotography Manual (3rd edition), Chris Woodhouse
* The Deep-Sky Imaging Primer (3rd edition), Charles Bracken
* Les secrets de l'Astrophoto (2ème edition), Thierry Legault
