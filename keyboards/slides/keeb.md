# Claviers Mécaniques & Ergonomie

![Keyboard](/resources/keyboards.jpeg) <!-- .element class=".stretch" -->

&copy; 2019 Brice Figureau

---

# Une (brêve) histoire

--

## Premières machines à écrire

<figure>
![hansen ball](resources/hansenball.jpg) <!-- .element width="50%" -->
<figcaption>Hansen ball - 1870</figcaption>
</figure>

note: beaucoup d'invention début 19e, mais pas encore de commercialisation

--

## Industrialisation des machines à écrire

<figure>
![remington 1](resources/sholesglidden.png) <!-- .element width="30%" -->
<figcaption>Sholes & Glidden - Remington 1 - 1875</figcaption>
</figure>

note: première machine commerciale 1864, premier succès la Sholes & Glidden en 1875 (premiere avec un clavier QWERTY)
invention du SHIFT, puis DOUBLE SHIFT (3 caractères par touches)

--

## Machines électriques

<figure>
![selectric I](resources/selectric1.jpg) <!-- .element width="50%" -->
<figcaption>IBM Selectric I - 1961</figcaption>
</figure>

note: première machine commerciale IBM Model 01 en 1935, puis le succès de la selectric, machine à boule, vendue jusque dans les années 80.

--

## Le teletype

<figure>
![teletype](resources/teletype.jpg) <!-- .element width="35%" -->
<figcaption>Teletype ASR 33 - By AlisonW [<a href="https://creativecommons.org/licenses/by-sa/3.0">CC BY-SA 3.0</a>]</figcaption>
</figure>

note: teletype utilisé en telegraphie (morse), puis adapté aux ordinateurs (Bell MULTICS dans les 60s), soit en direct soit avec cartes perforées

--

## Le terminal video

<figure>
![VT52](resources/vt52.jpg) <!-- .element width="50%" -->
<figcaption>DEC VT52 - By <a href="//commons.wikimedia.org/wiki/User:ClickRick" title="User:ClickRick">ClickRick</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=6693682">Link</a></figcaption>
</figure>

note: Datapoint 3300, puis DEC VT52 et enfin le fameux VT100

--

## Le micro-ordinateur

<figure>
![c64](resources/c64.jpg) <!-- .element width="50%" -->
<figcaption>Commodore 64 - 1982, By <a href="//commons.wikimedia.org/wiki/User:Evan-Amos" title="User:Evan-Amos">Evan-Amos</a> - <span class="int-own-work" lang="en">Own work</span>, Public Domain, <a href="https://commons.wikimedia.org/w/index.php?curid=17414881">Link</a></figcaption>
</figure>

note: fin des 70s et 80s, révolution du micro-ordinateur

--

## Le clavier moderne

<figure>
![ibm model m](resources/ibm-m.png) <!-- .element width="65%" -->
<figcaption>IBM Model M - 1986, By <a href="//commons.wikimedia.org/w/index.php?title=User:Raymangold22&amp;action=edit&amp;redlink=1" class="new" title="User:Raymangold22">Raymangold22</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="http://creativecommons.org/publicdomain/zero/1.0/deed.en" title="Creative Commons Zero, Public Domain Dedication">CC0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=37410391">Link</a></figcaption>
</figure>

note: fin des 70s et 80s, révolution du micro-ordinateur

---

# Qu'est-ce qu'un clavier, finalement ?

--

## A l'intérieur d'un clavier

* matrice de switchs
* plaque
* boitier
* controleur
* touches
* (leste)

--

### Enter the matrix

* circuit imprimé connectant les switchs en lignes et colonnes
* les switchs sont soudés dessus

--

### Matrix scanning

![matrix](resources/matrix.png) <!-- .element width="75%" -->

--

### Anti-ghosting

![anti-ghosting](resources/anti-ghosting-matrix.png) <!-- .element width="65%" -->

--

## La plaque

* les switchs sont clipsés dessus
* apporte de la rigidité (ou souplesse :)
* inox, aluminium mais aussi PC, fibre de carbonne

<figure>
![plate](resources/plate.jpeg) <!-- .element width="45%" -->
<figcaption>&copy;&nbsp;Gon</figcaption>
</figure>

--

## Le controlleur

* maintenant: microcontrolleur (comme les arduino)
* firmware dédié (proprietaire ou Open Source: QMK, TMK)

![controller](resources/controller.jpg) <!-- .element width="65%" -->

--

## Le boitier

* Plastique (ABS)
* Kustoms et haut de gamme: aluminium usiné
* leste optionnel (laiton): améliore le son et la stabilité

--

## Switchs

Fonctionne comme un interrupteur électrique, mais c'est un petit peu plus que ça...

--

### Buckling Spring

* l'ancestre

<figure>
![Buckling spring](resources/buckling-spring.gif) <!-- .element width="30%" -->
<figcaption>By <a href="//commons.wikimedia.org/w/index.php?title=User:Shaddim&amp;action=edit&amp;redlink=1" class="new" title="User:Shaddim">Shaddim</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=30568410">Link</a></figcaption>
</figure>

--

### Membrane

<figure>
![membrane](resources/membrane.jpg) <!-- .element width="50%" -->
<figcaption>By <a href="https://en.wikipedia.org/wiki/User:Asiir" class="extiw" title="en:User:Asiir">Asiir</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/2.5" title="Creative Commons Attribution-Share Alike 2.5">CC BY-SA 2.5</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=68089609">Link</a></figcaption>
</figure>

--

### Electro capacitive

la Rolls des switchs tactiles

<figure>
![topre](resources/topre.png)
<figcaption>&copy;&nbsp;Topre</figcaption>
</figure>

--

### Cherry MX & Clones

* 3 types
  * Linéaires
  * Tactiles
  * Clicky
* ressorts de differentes forces (couleur), niveaux de déclenchement
* environ 100+ switchs différents sur le marché

--

### Cherry MX & Clones

<figure>
![MX Switchs](/resources/switches.gif)
<figcaption>&copy;&nbsp;<a href="https://steelseries.com/blog/gaming-keyboard-mechanical-switches-44">SteelSeries</a></figcaption>
</figure>

--

### Cherry MX & Clones

* moding
* frankenswitches: Invyrr Holy Panda
* lubrification (son, confort)

<figure>
![holy panda](resources/holypanda.jpg)
<figcaption>&copy;&nbsp;<a href="https://massdrop.com">Massdrop</a></figcaption>
</figure>

--

### Alps

* plus fabriqués mais très recherchés
* se salissent vite
* utilisé dans les Apple Extended Keyboards (80s-90s)

<figure>
![Alps](resources/alps.jpg) <!-- .element width="50%" -->
<figcaption><a title="Daniel beardsmore [CC0], via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Alps_SKCM_Orange_--_fully_disassembled.jpg">Daniel beardsmore [CC0]</a></figcaption>
</figure>

--

## Keysets

--

### Materiaux

* ABS (durable, mais deviennent brillant, peuvent jaunir)
* PBT (extra durable)

--

### Lettrage

* laser etching
* pad printing
* dyesub
* double-shot injection

note: dyesub heats the surface and colour melts into the plastic to tint it, it's not printing

--

### Profils

![profiles](resources/profile.jpg)

--

### Fabricants

* GMK (ex Cherry, historique)
* SP (SA, DSA profile)
* ePBT (clones de Cherry, Chinois)
* beaucoup de petites usines Chinoises

--

### Des exemples

![e1](resources/example1.png) <!-- .element width="30%" -->
![e2](resources/example2.png) <!-- .element width="30%" -->
![e3](resources/example2.jpg) <!-- .element width="26%" -->
![e4](resources/example4.jpg) <!-- .element width="30%" -->
![e5](resources/example5.jpg) <!-- .element width="30%" -->

---

# Artisans

![a1](resources/artisan1.jpg) <!-- .element width="49%" -->
![a2](resources/artisan2.jpg) <!-- .element width="48%" -->

---

# Des claviers variés!

--

## 100%

<figure>
![100%](resources/100.jpg) <!-- .element width="80%" -->
<figcaption>By <a href="//commons.wikimedia.org/wiki/User:Nosachevd" title="User:Nosachevd">Dmitry Nosachev</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/4.0" title="Creative Commons Attribution-Share Alike 4.0">CC BY-SA 4.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=67361545">Link</a></figcaption>
</figure>

--

## TKL

<figure>
![TKL](resources/tkl.jpg) <!-- .element width="90%" -->
<figcaption>&copy;&nbsp;u/b7ad<figcaption>
</figure>

note: OTD 365.2

--

## 1800

<figure>
![1800](resources/1800.jpg) <!-- .element width="80%" -->
<figcaption>&copy;&nbsp;u/diiiP</figcaption>
</figure>

note: TX CP

--

## 75%

<figure>
![75%](resources/75.jpg) <!-- .element width="65%" -->
<figcaption>&copy;&nbsp;Exclusive Designs</figcaption>
</figure>

note: E7-V1

--

## 65%

<figure>
![65%](resources/65.jpeg) <!-- .element width="75%" -->
<figcaption>&copy;&nbsp;Yutksi</figcaption>
</figure>

note: TGR 910

--

## 60%

<figure>
![60%](resources/60.jpeg) <!-- .element width="75%" -->
<figcaption>&copy;&nbsp;Rama Works</figcaption>
</figure>

note: M60

--

## 40%

<figure>
![40%](resources/40.jpeg) <!-- .element width="65%" -->
<figcaption>&copy;&nbsp;Pearl Boards</figcaption>
</figure>

note: pearl

--

## Ergonomiques

<figure>
![TGR Alice](resources/ergo1-alice.jpg) <!-- .element width="35%" -->
<figcaption>&copy;&nbsp;u/dantambok</figcaption>
</figure>
<figure>
![Ergodox](resources/ergodox.jpg) <!-- .element width="35%" -->
<figcaption>&copy;&nbsp;Brice Figureau</figcaption>
</figure>

---

# Layouts

--

## ANSI

![ANSI](resources/ansi.png)

--

## ISO: par pays

![ISO FR](resources/iso.png)

--

## JIS

![JIS](resources/jis.png)

---

## Dvorak & Colemak

![dvorak](resources/dvorak.png) <!-- .element width="75%" -->
![colemak](resources/colemak.png) <!-- .element width="75%" -->

note:
* qwerty is not optimal
* Dvorak is better for English
* Colemak is dvorak for code

--

## BéPO

![bepo](resources/bepo.png) <!-- .element width="100%" -->

note:
* couvre tous les caractères européen
* organisé par frequence Fr

--

## Echelonné vs ortholineaire

<figure>
![ortho](resources/ortho.jpg) <!-- .element width="75%" -->
<figcaption>&copy; u/f36nl</figcaption></figure>

note:
* staggered was necessary in typewriters to prevent jam
* electronic keyboards can have any form

---

# Comment taper ?

--

## Touch typing vs Hunt & Peck

* sans regarder les touches
* mémoire musculaire
* *tous* les doigts servent
* vitesse et précision accrue

--

## Apprendre le touch-typing

* démarrer lentement
* travailler sur la précision puis sur la vitesse
* 40/50 WPM en 2 semaines

https://www.typingclub.com/

http://touchtyping.guru/

https://thetypingcat.com/

https://www.typing.com/

--

## Les bons doigts

<figure>
![fingers](resources/touch-typing.svg)
<figcaption>By <a href="//commons.wikimedia.org/wiki/File:Touch_typing.png" title="File:Touch typing.png">Touch_typing.png</a>: Håvard Frøiland (software), <a href="https://en.wikipedia.org/wiki/User:Trav1085" class="extiw" title="en:User:Trav1085">Trav1085</a> (screenshot)derivative work: <a href="//commons.wikimedia.org/w/index.php?title=User:Gryn&amp;action=edit&amp;redlink=1" class="new" title="User:Gryn (page does not exist)">Gryn</a> (<a href="//commons.wikimedia.org/w/index.php?title=User_talk:Gryn&amp;action=edit&amp;redlink=1" class="new" title="User talk:Gryn (page does not exist)"><span class="signature-talk">talk</span></a>) - <a href="//commons.wikimedia.org/wiki/File:Touch_typing.png" title="File:Touch typing.png">Touch_typing.png</a>, <a href="http://www.gnu.org/licenses/gpl.html" title="GNU General Public License">GPL</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=6430936">Link</a></figcaption>
</figure>

---

# La communauté

--

## Forums

* Geekhack: https://geekhack.org/index.php
* Reddit: https://www.reddit.com/r/MechanicalKeyboards/ 
* Keebtalk: https://www.keebtalk.com/
* beaucoup de serveurs Discord (par région, fournisseur, etc)

--

## Group-Buy

* clavier kustoms/petites séries
* keysets
* artisans

--

## Mechmarket

Les productions de keyset, clavier custom ou artisan étant insuffisantes, le marché secondaire est très dynamique (reddit, discord).<!-- .element: style="text-align: left;"> -->

Beaucoup d'achat/revente et augmentation inconsidéré des prix<!-- .element: style="text-align: left;"> -->

note: some earlier Korean kustoms like the otd 365 are selling there for more +3k

---

# Travailler sur ordinateur

Danger pour votre santé !

---

## Fatigue oculaire (asthénopie)

> La fatigue oculaire se manifeste par des symptômes non spécifiques tels que la fatigue, des douleurs dans ou autour des yeux, vision floue, des maux de tête et, occasionnellement, une vision double.

note: quality of light, artificial light, screen settings can help, watch out low quality LCD with PWM backlight, mate screen

--

## Fatigue oculaire

* crispation des muscles cillaires (modificateurs de la forme du cristallin)
* peut-être révélateur de troubles sous-jacents (myopie, astigmatisme, etc)
* soulager en restant dans le noir jusqu'au relachement des muscles

--

## Fatigue oculaire

* faire des pauses (regarder au loin par ex)
* attention aux réglages de l'écran (luminosité) et aux écrans basse qualité
* écran mat (attention aux portables avec écran réfléchissant)
* utiliser une source de lumière artificielle (lumière solaire inconstante)
* placer l'écran perpendiculairement aux fenêtres
* lampe de bureau en complément pour les papiers
* préférez le mode "light" au mode "dark" (moins de réflection, moins de fatigue entre document papier et écran)

---

## Troubles Musculo-squeletiques (TMS)

> Blessures des muscles, tendons, nerfs et squelette causées par des taches répétitives, des efforts soutenus, des vibrations, des compressions mécaniques ou par des positions anormales ou soutenues dans le temps.

https://fr.wikipedia.org/wiki/Trouble_musculosquelettique

--

## Troubles Musculo-squeletiques

<figure>
![RSI](resources/rsi.jpg) <!-- .element width="50%" -->
<figcaption>&copy;&nbsp;INRS</figcaption>
</figure>

--

## Troubles Musculo-squeletiques

* peuvent être renforcés par le stress
* affectent principalement: doigts, poignets, coudes, nuque, bas du dos
* Syndrome du Canal Carpien
* Tendinite, Tendinosynovite, Syndrome de Quiervain

note: Tendinosynovite = tendinite avec inflamation de la gaine du tendon, canal carpien = axe de passage tendon au milieu du poignet, quiervain: tendinosynovite du pouce

--

## Prendre la bonne position

<figure>
![right position](resources/workplace-ergo.png) <!-- .element width="55%" -->
</figure>

--

## Que faire si je suis atteind ?

note: stress is an aggravating factor

--

### Taper en position neutre

* poignets flottants
* attention au repose-poignets
* en dernier ressort porter des gants spéciaux

--

### Changer de clavier ou layout

* clavier mécanique FTW
* ergonomique (ergodox, kinesis, etc)
* layout BéPO, Dvorak, Colemak

note: ergonomic keyboards allow for a different hand placement with less constraints

--

### Changer de souris

<figure>
![vertical mouse](resources/logitech-vertical-mouse.jpg) <!-- .element width="55%" -->
<figcaption>&copy;&nbsp;Logitech</figcaption>
</figure>

--

### Essayer le trackball

<figure>
![trackball](resources/logitech-trackball.jpg)
<figcaption>&copy;&nbsp;Logitech</figcaption>
</figure>

--

### Ou le trackpad

<figure>
![trackpad](resources/apple-trackpad.jpeg) <!-- .element width="55%" -->
<figcaption>&copy;&nbsp;Apple</figcaption>
</figure>

--

### Faire des pause régulières

* La recommendation: 5 min toutes les heures, ou 15 min toutes les 2h
* regarder au loin toutes les 20 min
* Pomodoro
* rester devant son écran n'est pas une pause

note: during the break, walk a bit, go hydrate, stop starring at the screen

--

### Faire de l'exercice

note: unfortunately obesity is a risk factor

--

### Demander au CHSCT

...et lire les brochures de l'INRS

note: they are trained about this and can suggest workplace modifications

--

### Rencontrer la Médecine du Travail

En tant que salarié vous avez le droit de consulter la médecine du travail. L'entretien est confidentiel, et le médecin peut venir voir le poste de travail et demander à l'employeur des ajustements.

note: n'attendez pas!

--

## Quand c'est sérieux

* kiné
* infiltrations
* chirurgie

--

### Plus d'information

Les brochure de l'INRS:

http://www.inrs.fr/risques/travail-ecran/publications-outils-liens.html

La documentation INSERM:

https://intranet.inserm.fr/securite-et-prevention/sante-securite/Documents%20externes/3_PreventionRisques/7_TroublesMusculo/Inserm_DrhBCPR_TravailEcran_Guide.pdf

Travail Sécutitaire Quebec:

https://www.travailsecuritairenb.ca/docs/officefrdist.pdf

---

# Questions ?