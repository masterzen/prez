# Introduction à la théorie des files d'attente

&copy; 2021, 2022 Brice Figureau

---

## Définition

> La théorie des file d'attentes s'attache à modéliser mathématiquement l'expérience la moins plaisante de la vie: l'attente !

--

## Loi de Murphy (appliquée aux queues)

* loi: _si tu changes de file, celle que tu quittes avancera plus vite que celle dans laquelle tu es_.
* corrolaire 1: _ta file d'attente est toujours la plus lente_
* corrolaire 2: _quelque soit la file d'attente que tu rejoins, même la plus courte, ton temps d'attente sera toujours le plus long_

---

## Le monde est rempli de files d'attente

--

### Dans la vie de tous les jours

* la salle de bain le matin
* les bouchons
* banque, la poste, les caisses de magasin
* restaurants
* et même au travail (attente de documents, collaboration, travail en cours, etc)
...

--

### ainsi que dans les systèmes informatiques

* RAM / CPU / disques durs
* routers / switchs
* kernels / logiciel
...

--

### Il y a des files partout !

> Le temps d'attente est du temps perdu (quelque système que ce soit), essayons de le minimiser !

---

## La théorie des files d'attente

Branche de la recherche faisant partie des mathématiques appliquées ayant pour but de modéliser le comportement des files d'attente.

--

## Mais...

Nous ne parlerons pas:

* de psychologie
* de mécanique des fluides
* de dynamique des foules
* du balking, jockeying et du renoncement

note: balking: ne pas entrer dans une file car elle semble trop longue, jockeying changer de file pour tenter d'optimiser, renoncement quand le temps d'attente est trop long (modèle beaucoup plus compliqués)

---

### Un peu d'histoire

<figure>
![Agner Krarup Erlang](resources/Erlang.jpg) <!-- .element width="30%" class="plain" -->
<figcaption>Agner Krarup Erlang (1878-1929)</figcaption>
</figure>

--

### Le système téléphonique à l'époque

<figure>
![Opératrices suedoises](resources/operatrice-SE.jpg) <!-- .element width="40%" class="plain" -->
![commutateur](resources/operatrice-2.jpg) <!-- .element width="40%" class="plain" -->
</figure>

--

### Le "réseau" téléphonique

<figure>
![Appel longue distance](resources/interco.svg) <!-- .element width="70%" class="plain" -->
<figcaption>Appel longue distance</figcaption>
</figure>

--

### Problème

> Combien de lignes d'interconnexion et combien d'opérateurs faut-il sachant le nombre d'abonnés, la fréquence des appels et leur durées moyennes ?

Note: article de 1909 "The theory of probabilities and telephone conversations" et plus tard les formules de "perte" d'appel qui furent utilisées partout dans le monde. Certains ingénieurs allant jusqu'à apprendre le danois pour comprendre les articles d'Erlang

--

### L'oeuvre

Erlang a découvert que les files d'attente du système téléphonique obéissent à des processus stochastiques (et notamment aux processus de "naissance et de mort" théorisés par Markov) et pu ainsi créer 2 formules.

Note: il y a une formule Erlang-A découverte par Conny Palm (suedois) en 1946 et qui prend en compte les abandons

--

### Erlang-B

Donne la probabilité d'un appel perdu pour un groupe de lignes ou opérateur donné:
`
$$
P_b = B(E,m) = \frac{\frac{E^m}{m!}} { \sum_{i=0}^m \frac{E^i}{i!}} \\
$$
`

avec:

* `$P_b$` probabilité d'appel perdu
* `$E = {\lambda}h$` charge appliquée
* `$m$` nombre de resources parallèles (lignes, opérateurs, etc)

--

### Erlang-C

Donne la probabilité qu'un client entrant devra attendre avant de pouvoir obtenir le service:

`
$$
P_w = {{\frac{E^m}{m!} \frac{m}{m - E}} \over \left ( \sum\limits_{i=0}^{m-1} \frac{E^i}{i!} \right ) + \frac{E^m}{m!} \frac{m}{m - E}}
$$
`

avec:

* `$E$` le traffic total
* `$m$` le nombre de serveurs (resources parallèles)
* `$P_w$` probabilité qu'un client ait à attendre

--

### Erlang

En 1948, le CCITT assigna le nom d'Erlang (symbole `E`) à l'unité de charge d'une ligne téléphonique. Par ex, une ligne seule peut accueillir 60 min de conversation par heure, soit 1 Erlang.

---

## Pourquoi étudier les files d'attente ?

Pour pouvoir répondre à ces questions:

* quelle probabilité pour qu'une file se forme ?
* quelle taille va faire la file ?
* quelle attente vont subir les "clients" ?
* quel taux d'occupation les "serveurs" vont-ils supporter ?
* quelle capacité doit on mettre en oeuvre pour un niveau de demande donnée ?

--

## Modèles

La théorie des files d'attente propose des modèles basés sur des assomptions. Si le système vérifie ces assomptions, il est possible de prévoir les comportements des files d'attentes et les limites des systèmes.

--

## Modèles

Le problème est peu intuitif (cf Erlang-C) car basé sur des probabilités. 

Notre intuition humaine est _linéaire_: si le trafic double, le reste doublera pensons-nous ?

--

## Modèles

> Les systèmes à base de files d'attente sont avant tout **non-linéaires**.

--

## Anatomie

<figure>
![File d'attente](resources/queue.svg) <!-- .element width="50%" class="plain" -->
<figcaption>File d'attente</figcaption>
</figure>

--

## Anatomie: discipline ou modèle de service

Ou comment sont servis les clients:

* FIFO
* LIFO
* Par priorité
* en boucle
* ...

note: we're focusing only on FIFO

--

## Anatomie: population

Dans certains modèles, la population pouvant être servie est finie (file d'attente en boucle), au contraire des files d'attentes classiques (caisses de supermarchés, etc) ou la population est infinie

note: cas de machines industrielles devant être réparées dans une usine

--

## Anatomie: distribution des arrivées & des temps de services

* l'arrivée est-elle aléatoire ?
* les arrivées sont-elles indépendentes les unes des autres ?

---

## Classification de Kendall

* inventée par David Georges Kendall en 1957
* forme simple: `A/S/c`
* forme complète: `A/S/c/K/N/D`

où:

* A: processus d'arrivée
* S: distribution des temps de service
* c: nombre de "serveurs"
* K: taille maximale de la file
* N: taille de la population
* D: discipline

--

## Classification de Kendall: distributions

pour `A` et `S`:

* M: distribution de Poisson (arrivées) ou Exponentielle (temps de services)
* E: distribution d'Erlang
* D: distribution Constante
* G: distribution  Générique (de moyenne et variance connue)

--

## Classification de Kendall: exemples

* M/M/1 ou M/M/1/∞/∞/FIFO -> Poisson, Exponentielle 1 serveur
* M/M/2 -> 2 serveurs
* M/D/3 -> temps de services constant, 3 servers
* M/M/2/10/∞/FIFO -> Poisson/Exponentielle à taille de file fixe et 2 serveurs

---

## La loi de Little

`
$$
L = {\lambda}W
$$
`

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
avec:

* `$L$` moyenne du nombre de "clients" dans le système
* `$\lambda$` moyenne des intervalles d'arrivées des "clients"
* `$W$` moyenne des temps de service des "clients"

Cette loi ne dépends pas des processus d'arrivées ou de services, mais ne fonctionne que pour un système stable en fonctionnement.

note: formulée par Little en 1954 et démontrée en 1961. Ultra importante, et très intuitive: Au restaurant, on double le nombre de client arrivant, vous avez 2 fois plus de clients à servir. Si le temps de service double, avec le même vitesse d'arrivée le nombre de client double aussi.

--

## Quelques remarques en passant

* si `$λ$` vitesse moyenne des arrivées
* et `$µ$`: vitesse moyenne de service (client/unité de temps)
* alors `$\rho = {\lambda}/{\mu} $` correspond à la charge (utilisation):
  * `$ \rho < 1 $` -> file d'attente finie
  * `$ \rho > 1 $` -> file d'attente infinie !

---

## M/M/1

* le modèle le plus simple, 1 file, 1 serveur
* arrivées: distribution de Poisson 
* service: distribution Exponentielle 
note: poisson=(bon modèle des phénomènes aléatoire naturels, mais suppose un grand échantillon et pas d'interdépendance entre les clietns), exponentielle=(le pendant de Poisson pour les distribution continues)

--

## M/M/1 à la loupe

Taux d'occupation (mesure de la charge):

`
$$ \rho = \frac{\lambda}{\mu} $$
`

`$ 0 < \rho < 1$`

note: si lambda >> mu, problème, pas de stabilité.

--

## M/M/1 à la loupe

Processus de naissance & mort:

<figure>
![Naissance & Mort](resources/mm1-birth-death.svg) <!-- .element width="70%" class="plain" -->
<figcaption>Naissance & Mort</figcaption>
</figure>

* système ergodique: temps passé dans un état = probabilité d'être dans cet état
* il y a autant de passage d'un état n à un état n+1 que d'état n+1 à l'état n


note: utilisé pour l'analyse de population
1 naissance à la fois, 1 mort à la fois - représente les probabilités des états
systeme ergodique = proba d'etre dans tel état == temps dans cet état sur longue période
etat 0 -> pas de clietns
etat 1 -> 1 client servi
etat 2 -> 1 client servi 1 attend, etc
analogie de l'ascenseur
proba state 0 = % temps passé state 0
state 0 -> facile 1 - rho
probabilité état 0 ?
probabilité état X ?

--

## M/M/1 à la loupe II

* `$ \lambda P_0 = \mu P_1 $` et donc `$ P_1 = \frac{\lambda}{\mu}P_0 $`
* de même `$ P_n = \frac{\lambda}{\mu}P_{n-1} $`
* par extension: `$ P_n = (\frac{\lambda}{\mu})^{n}P_0 $`

`
$ 
\sum_{i=0}^{\infty} P_i = 1 => \sum_{i=0}^{\infty} (\frac{\lambda}{\mu})^{i}P_0 \\
comme \sum_{i=0}^{\infty} x^i = \frac{1}{1 - x} \\
alors \\
1 = \frac{1}{1 - \rho} P_0 => P_0 = 1 - \rho
$
`

--

## M/M/1 à la loupe III

* espérance mathématique du nombres de clients:

`$
L = \sum_{i=0}^{\infty} iP_i  = \sum_{i=0}^{\infty} i (\frac{\lambda}{\mu})^{i}P_0  = P_0 \sum_{i=0}^{\infty} i (\frac{\lambda}{\mu})^{i}   \\
et \sum_{i=0}^{\infty} ix^{(i-1)} = \frac{1}{(1 - x)^2} \\
donc \\
L = P_0 \sum_{i=0}^{\infty} i \rho^i  = (1 - \rho) \rho \sum_{i=0}^{\infty} i \rho^{i-1}  \\ 
= (1 -\rho) \rho \frac{1}{(1 - \rho)^2}  = \frac{(1-\rho) \rho}{(1 - \rho)^2}  = \frac{\rho}{1 - \rho} \\ 
L_q = L - (1 - P_0) = \frac{\rho^2}{1 - \rho}
$`

note: espérance: valeur moyenne pondérée d'une variable aléatoire

--

## M/M/1 exemple

Exemple: `$ \lambda = 2/m $` et `$ \mu = 3/m $`

Quel temps d'attente ?

`$
W = W_q + W_s = L_q \frac{1}{\mu} + \frac{1}{\mu} = \frac{\frac{2}{3}}{1 - \frac{2}{3}} \frac{1}{3} + \frac{1}{3} = 2(\frac{1}{3}) + \frac{1}{3} = 1 minute
$`

note: 2 clients arrivent par minutes, et 3 clients partent par minutes

--

## M/M/1 encore ?

Temps d'attente moyen dans la file:
`
$$ W_q = W - W_s = \frac{L}{\lambda} = \frac{W_s}{1 - \rho} = \frac{1}{\mu - \lambda} $$
`
Nombre de clients dans la file:
`
$$ L_q = \lambda W_q = \frac{\rho^2}{1 - \rho} $$
`

--

## M/M/1 conclusion

Le temps de résidence (normalisé) est proportionel à  

`
$$ \frac{1}{1 - \rho}$$
`

<figure>
![1/1-r](resources/rho.png) <!-- .element width="50%" class="plain" -->
<figcaption>Ça peut faire mal</figcaption>
</figure>

note: at high utilization, waiting times become
 asymptotical ! Clearly we need to keep the system
 under optimal utilization.

---

## M/M/c

Stable si `$ \lambda \le c\mu $`

Processus de naissance & mort:

<figure>
![Naissance & Mort](resources/mmc-birth-death.svg) <!-- .element width="70%" class="plain" -->
<figcaption>Naissance & Mort</figcaption>
</figure>

`$ \begin{cases}
          \lambda P_{n-1} = n \mu P_{n} & \mbox{si } n = 1,\ldots, c-1, c \\
          \lambda P_{n-1} = c \mu P_{n} & \mbox{si } n > c
  \end{cases} $`

note: C'est le modèle file unique plusieurs guichets, et requiert la formule Erlang-C:

--

## M/M/c II

donc avec `$ \rho = \lambda / \mu $`

`$ \begin{cases}
          P_n = \frac{\rho^n}{n!} P_0 & \mbox{si } n = 1,\ldots, c-1, c \\
          P_n = \frac{\rho^n}{c!c^{n-c}} P_0 & \mbox{si } n > c
  \end{cases} \\
  et \sum_{i=0}^{\infty} P_i = 1 \\
  donc \\
  P_0 = \frac{1}{(\sum_{n=0}^{c-1}{\frac{\rho^n}{n!}}) + \frac{\rho^c}{(c-1)!(c-\rho)}}
  $`

note: cela vous rappelle-t-il quelque chose?

--

## M/M/c III

Quelle est la probabilité lors d'une arrivée de trouver tous les serveurs occupés?

`
$$ C[c,\rho] = \sum_{n=c}^{\infty}P_n = 1 - \sum_{n=0}^{c-1} P_n = 1 - P_0 \sum_{n=0}^{c-1} \frac{\rho^n}{n!} \\
   = \frac{\frac{\rho^c c}{c!(c-\rho)}}{(\sum_{n=0}^{c-1}{\frac{\rho^n}{n!}}) + \frac{\rho^c c}{c!(c-\rho)}}
$$
`

note: comme par hasard c'est la formule Erlang-C. Par contre pas calculable directement, mais il existe de bonnes approximations (cf Hirotaka Sakasegawa en 1977, ou plus récemment Gunther)
ce n'est pas intuitif (on ne peut pas raisonner dessus en fonction augmentation lambda/mu)

--

## M/M/c IV

Nombre moyen de clients dans le système:

`
$$ L = \frac{\rho}{1 - \rho} C(c,\rho) + c \rho $$
`

Temps d'attente moyen:

`
$$ W = \frac{\lambda C(c,\rho)}{c\mu - \lambda} + \frac{1}{\mu} $$
`

---

## M/M/c comparaisons

<figure>
![Temps d'attente](resources/utilization-servers.png) <!-- .element width="50%" class="plain" -->
<figcaption>Temps d'attente en fonction de la charge pour c=1,2,16</figcaption>
</figure>

note: pour c=1, 2, 16, avec plus de serveurs concurrents on peut avoir plus de charge utilse

--

## 2 M/M/1 ou 1 M/M/2 ?

Comparons deux guichets d'aéroport 2xM/M/1 avec M/M/2 et 240 passagers/heure en supposant 15s par passager:

| Grandeur     | M/M/2    | 2xM/M/1  |
|------------- |----------|----------|
| Charge       |   50%    |   50%    |
| Lq           |   0.33   |   0.5    |
| W            |   20s    |   30s    |

--

## 4 M/M/1 ou 1 M/M/4 ?

Imaginons avoir 4 fois plus de passagers et 4 guichets

| Grandeur     | M/M/4    | 4xM/M/1  |
|------------- |----------|----------|
| Charge       |   50%    |   50%    |
| Lq           |   0.06   |   0.5    |
| W            |   15.24s |   30s    |


---

## Pour aller plus loin ?

* réseaux de files d'attente
* modèles non-markovien
* autres champs d'application

---

## Bibliographie

* Introduction to Queueing Theory - Robert Cooper
(cours en ligne EN: https://youtu.be/AsTuNP0N7DU)
* Probability, Statistics and Queueing Theory with Computer Science Application - Arnold Q. Allen
* Théorie des files d'attente - Bruno Baynat
* Théorie des files d'attente (cours en ligne https://youtu.be/MUgsCmbL9ls)

---

### Aurais-je menti ?

--

## Un (tout petit) peu de psychologie

* Richard C. Larson "The Psychology of Queuing and Social Justice", 1981
* David Maister "The Psychology of Waiting Lines", 1985

note: Larson, professeur au MIT, fondateur de la psychologie des files. A cause d'une attente injuste pour acheter un vélo dans un grand magasin ou des gens pouvaient retirer leur achats avant lui (non FIFO)

--

## Les 6 règles de David Maister

1. Le temps pendant lequel nous sommes inoccupés semble plus long que du temps ou on est occupé
2. Les gens veulent que cela démarre (temps d'attente de début de transaction)
3. Attendre un temps non connu est plus difficile qu'attendre un temps connu à l'avance
4. Les attentes inexpliquées sont plus difficiles que les attentes dont la cause est connue
5. Les attentes injustes sont plus difficiles que les attentes juste
6. L'anxiété augmente le temps d'attente perçu

note: 2. -> temps d'attente pour être assi au restaurant plus difficile que temps pour être servi, 5. -> lorsque FIFO non enforce

---

## Questions ?
