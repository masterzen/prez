# Queueing Theory



Brice Figureau - Asmodee Digital - 2017

---

## Definition

--

## Definition

> Queueing theory is the mathematical study of waiting lines.

--

## History

Agner Krarup Erlang designed models to describe the Copenhagen telephone exchange in 1909.

---

# There are queues everywhere !

--

## in life
* toilets in the morning
* traffic jam
* banks, post office
* restaurant
* even at work!
...

note: for instance at work: work in progress is a queue that
you want to minimize

--

## or in computer systems
* RAM / CPU
* routers
* kernels
* software
...

--

Queueing happens everywhere.

Waiting time is lost time.

---

## Why would you want to study that ?

* systems get congested under load
* waiting time increases
* queueing theory allows understanding relationships between congestion and delay

---

## Models

Queueing theory proposes models based on some assumptions, if your system verifies those assumptions you can predict the queues behaviors. 

It allows to simulate behaviors by changing the queue model.

---

## Little's Theorem

$$N = \lambda T$$

* N is the average number of customers or events in the queuing system
* λ is the average customer or event arrival rate
* T is the average service time for the customer or event processing time

note: restaurant: double the number of customer arriving, you get double of customers in the restaurant
same if you double the service time.

---

# What's in a queue ?

--

## Queueing discipline

aka how do you serve the clients

* FIFO
* LIFO
* Priority
* Loop

note: we're focusing only on FIFO

--

## Arrival distribution

* random arrival over long periods
* customers arrival independent of other
* count the arrival per time slot
* distribution: histogram of arrival frequency
* this is the Probability Mass Function

--

## Arrival distribution (supermarket)

* count number of arrivals per 5 min slots
* count number of occurences we had for 0, 1, 2... customers
* relative frequency: 
$$ A_n / Total $$

note: 
count arrival of customers per 5 min slots
count the number of times it happened for 0 cust, 1 cust, ...
compute relative frequency

--

## Arrival distribution (supermarket)

| Arrivals | number | relative freq |
|----------|--------|---------------|
|    0     |  255   |    47%        |
|    1     |  190   |    35%        |
|    2     |   72   |    13%        |
|    3     |   19   |     4%        |
|    4     |    3   |     1%        |
|  total   |  539   |   100%        |

--

## Arrival distribution (supermarket)

$$ \lambda = 0x47\% + 1x35\% + 2x13\% + 3x4\% + 4x1\% = 0.74768 $$

This forms a _Poisson distribution_ (like most random phenomenon)

$$P(x) = \frac{\lambda_x e^{-\lambda}}{x!} , x=0,1,2...$$

$$P(0) = \frac{1 e^{-0.75}}{1} = e^{-0.75} = 0.47$$ 
$$P(0) = \frac{0.75 e^{-0.75}}{1} = 0.75 e^{-0.75} = 0.35$$ 
...

note: This also is called a Markovian distribution

--

## Service time distribution

Same kind of analysis (except we measure the time spent to serve a client) as the Arrival distribution, if random an Exponential distribution applies.

---

## Kendall Classification

* suggested by David Georges Kendall in 1957
* simplest form: a/b/c

with

* a: probability distribution of arrival
* b: probability distribution of service time
* c: number of servers

--

## Kendall Classification

* M: Poisson distribution (arrival) or Exponential (service time)
* E: Erlang distribution
* D: Constant distribution
* G: General distribution (with known mean/variance)

--

## Kendall

* M/M/1 -> Poisson, Exponential 1 server
* M/M/2 -> 2 servers
* M/D/3 -> constant service time, 3 servers

note:
complex form adds 2 parameters total capacity and total population
assumed infinite in simplest form


---

## Infinite Queues ?

* λ: arrival rate (client/unit of time)
* µ: processing rate (client/unit of time)
* λ / µ < 1 -> finite queue
* λ / µ > 1 -> need an inifinite: bad!

---

## M/M/1

* most used model
* Poisson: 
  * assumes large number of clients
  * impact of one client small on the system
  * indepence of clients

--

## M/M/1 the gory details

given λ and µ (1/S)

Utilization (% of use)
$$ \rho = \frac{\lambda}{\mu} $$

note: I'm won't do any demonstration but all those formulas can be demonstrated
with probabilities (see Erlang)

--

## M/M/1 the gory details

$$R = S + W = S + QS = S + (\lambda R)S $$
$$  = S + R (\lambda S) = 

--

## M/M/1 the gory details

Average time in waiting line:
$$ W_q = \frac{\lambda}{\lambda(\mu - \lambda)} $$

Average time in system:
$$ W = \frac{1}{\mu - \lambda} $$

--

## M/M/1 the gory details

Average number of customers in waiting line:
$$ L_q = \lambda W_q = \frac{\lambda^2}{\mu - \lambda} $$

Average number of customers in system:
$$ L = \lambda W = \frac{\rho}{1 - \rho} $$

--

## M/M/1 the gory details

Probability of no customers:

$$ P_0 = 1 - \frac{\lambda}{\mu} $$

Probability of a \# *n* of customers

$$ P_n = \rho^n P_0 $$

--

## M/M/1 conclusion

waiting time proportional to 

$$ \frac{\rho}{1 - \rho}$$

![Beware!](rho.png)

note: at high utilization, waiting times become
 asymptotical

---

## M/M/c

Much more complex, based on Erlanc C formula


Probability that a customer has to enter a queue
$$ C(c,\rho) = \frac{1}{1 + (1 - \rho)(\frac{c!}{(c \rho)^c})(\sum_{k=0}^{c-1} \frac{(c \rho)^k}{k!})} $$

\(c \rho\) = traffic intensity mesured in Erlangs

Average number of customers in system:
$$ L = \frac{\rho}{1 - \rho} C(c,\rho) + c \rho $$

note: C equation requires iterative computations - can't be computed in Excel 
it's also not intuitive (can't derive any information if c increases/decreases)

--

## M/M/c

We need approximations !

Hirotaka Sakasegawa 1977 approx for M/G/c

$$ L\_q \approx \frac{\rho \sqrt{2(M + 1)}}{1 - \rho} \times \frac{ CV\_{IAT}^2 CV\_{ST}^2 }{2} $$

for M/M/c, the second terms becomes 1 !

--

## M/M/c

Gunther's approximation:

$$ L\_q \approx \rho \c (\frac{1}{1 - \rho^c} - 1)


--

## M/M/c

|servers | utilization  | Erlang C  | Sakasegawa | Gunther   |
|--------|------------- |-----------|------------|-----------|
|    1   |     0.500    | 0.500000  |  0.500000  | 0.500000  |
|    2   |     0.500    | 0.333333  | 0.333333   | 0.366151  |
|    2   |     0.999    | 997.50175 |  997.50175 | 997.552285|
|    4   |     0.500    | 0.173913  |  0.133333  | 0.223403  |
|    4   |     0.999    | 996.784391|  996.503749| 996.841140|
|    8   |     0.500    | 0.059044  |  0.015686  | 0.105650  |
|    8   |     0.999    | 995.760755|  994.509747| 995.764233|


---

## Combined or Separate ?

Airport checking with 2xM/M/1 or an M/M/2 with 240 passengers/hour with a service time of 15s per passenger:

| Metric       | Combined | Separate |
|------------- |----------|----------|
| Utilization  |   50%    |   50%    |
| Avg Q Length |   0.33   |   0.5    |
| Avg W        |   20s    |   30s    |


---

References:

https://en.wikipedia.org/wiki/M/M/c_queue
http://people.revoledu.com/kardi/tutorial/Queuing/Queuing-What-Is.html
http://irh.inf.unideb.hu/~jsztrik/education/16/SOR_Main_Angol.pdf
https://github.com/VividCortex/approx-queueing-theory
https://speakerdeck.com/drqz/m-a-new-view-of-an-old-queue
https://www.slideshare.net/vividcortex/quantifying-scalability-with-the-usl
https://github.com/VividCortex/approx-queueing-theory/blob/master/sakasegawa-1977.pdf




