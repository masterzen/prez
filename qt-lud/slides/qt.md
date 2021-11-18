# Introduction à la théorie des files d'attente

&copy; 2021 Brice Figureau

---

## Définition

> La théorie des file d'attentes s'attache à modéliser mathématiquement l'expérience la moins plaisante de la vie: l'attente !

--

## Loi de Murphy (appliquée aux files d'attente)

* si tu changes de file, celle que tu quittes avancera plus vite que celle dans laquelle tu es.
* corrolaire: ta file d'attente est toujours la plus lente
* corrolaire 2: quelque soit la file d'attente que tu rejoins, même la plus courte, ton temps d'attente sera toujours le plus long

---

## Le monde est rempli de files d'attente

--

### Dans la vie de tous les jours

* la salle de bain le matin
* les bouchons
* banque, la poste
* restaurants
* et même au travail (attente de documents, collaboration, travail en cours, etc)
...

--

### ainsi que dans les systèmes informatiques

* RAM / CPU
* routers
* kernels
* software
...

--

### Il y a des files partout !

> Le temps d'attente est du temps perdu (quelque système que ce soit), essayons de le minimiser !

---

## La théorie des files d'attente

Branche de recherche faisant partie des mathématiques appliquées (et un peu de l'automatique) ayant pour but de modéliser le comportement des files d'attente.

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

> Combien de lignes d'interconnexion et combien d'opérateurs faut-il sachant le nombre d'abonnés, la fréquence des appels et leur durés moyennes ?

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

La théorie des files d'attente est basée sur l'étude des probabilités, un discipline compliquée et rarement intuitive. 

Notre intuition humaine est avant tout _linéaire_: si le trafic double, le reste doublera pensons-nous ?

Que nenni, les systèmes à base de files sont avant tout _non-linéaires_.

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
* M/D/3 -> temps de services constant time, 3 servers
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

* si `$λ$` fréquence moyenne d'arrivées
* et `$µ$`: vitesse moyenne de service (client/unité de temps)
* alors `$\rho = {\lambda}/{\mu} $` correspond à la charge:
  * `$ \rho < 1 $` -> file d'attente finie
  * `$ \rho > 1 $` -> file d'attente infinie !

---

## M/M/1

* le modèle le plus simple, 1 file, 1 serveur
* arrivées: distribution de Poisson (bon modèle des phénomènes aléatoire naturels, mais suppose un grand échantillon et pas d'interdépendance entre les clietns)
* service: distribution Exponentielle (le pendant de Poisson pour les distribution continues)

--

## M/M/1 à la loupe

Temps d'attente moyen dans la file:
`
$$ W = \frac{\rho S}{1 - \rho} $$
`
Temps moyen passé dans le système:
`
$$ R = W + S = \frac{S}{1 - \rho} = \frac{1}{\mu - \lambda} $$
`
Nombre de clients dans la file:
`
$$ L = \lambda W = \frac{\rho^2}{1 - \rho} $$
`
Nombre moyen de clients:

$$ Q = \lambda R = \frac{\rho}{1 - \rho} $$

--

## M/M/1 au microscope

Probabilité d'avoir une file vide:

`
$$ P_0 = 1 - \frac{\lambda}{\mu} $$
`

Probabilité d'avoir `$n$` clients

`
$$ P_n = \rho^n P_0 $$
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

C'est le modèle file unique, plusieurs guichets, et requiert la formule Erlang-C:

`
$$ C(c,\rho) = \frac{1}{1 + (1 - \rho)(\frac{c!}{(c \rho)^c})(\sum_{k=0}^{c-1} \frac{(c \rho)^k}{k!})} $$
`

\\(c \rho\\) = traffic intensity mesured in Erlangs

Nombre moyen de clients dans le système:

`
$$ L = \frac{\rho}{1 - \rho} C(c,\rho) + c \rho $$
`

note: C equation requires iterative computations - can't be computed in Excel 
it's also not intuitive (can't derive any information if c increases/decreases)
Erlang is a measure of load (number of call active at a moment in a telephone system)

--

## M/M/c

We need approximations !

Hirotaka Sakasegawa 1977 approximation

$$ L\_q \approx \frac{\rho \sqrt{2(c + 1)}}{1 - \rho} $$

note:
increase rho -> increase in q time
increase c -> decrease of q time 

--

## M/M/c

Gunther's approximation:

$$ L\_q \approx \rho c (\frac{1}{1 - \rho^c} - 1) $$


--

## M/M/c

|servers | utilization  | Erlang C  | Sakasegawa | Gunther   |
|--------|------------- |-----------|------------|-----------|
|    1   |     0.500    | 0.500000  |  0.500000  | 0.500000  |
|    2   |     0.500    | 0.333333  | 0.333333   | 0.366151  |
|    2   |     0.999    | 997.50175 |  997.50175 | 997.552285|
|    8   |     0.500    | 0.059044  |  0.015686  | 0.105650  |
|    8   |     0.999    | 995.760755|  994.509747| 995.764233|
|   64   |     0.999    | 989.334082|  966.873556| 988.657359|

--

## Utilization per \# of servers

![Utilization per # server](utilization-servers.png)

note:
different server count=1, 2, 16
this has an impact -> more concurrency can use system at higher utilization

---

## Combined or Separate ?

Airport checking with 2xM/M/1 or an M/M/2 with 240 passengers/hour with a service time of 15s per passenger:

| Metric       | Combined | Separate |
|------------- |----------|----------|
| Utilization  |   50%    |   50%    |
| Avg Q Length |   0.33   |   0.5    |
| Avg W        |   20s    |   30s    |

--

## Combined or Separate ?

4 times more passengers, adding 4 servers

| Metric       | Combined | Separate |
|------------- |----------|----------|
| Utilization  |   50%    |   50%    |
| Avg Q Length |   0.06   |   0.5    |
| Avg W        |   15.24s |   30s    |
