---
title: Queuing Models
draft: false
date: 2025-09-21
ObsidianUIMode: preview
tags:
- OptimisationTechniques
---

**The most important information required to solve a waiting line problem is the nature and probability distribution of arrivals and service pattern.**

1. *Queue Length*: Number of person in system at anytime.
2. *Waiting Time*: Probablity distribution of waiting time of customers. It depends on following factors.
	1. Number of units already in systems.
	2. Number of service stations.
	3. Schedule in which units are selected for service.
	4. Nature and magnitude of service being given.
3. *Average idle time*: Average time for which system is ideal. One customer arrive, as he is being serviced, more arrive, system will keep servicing all customers until no customers are left.
4. *System Discipline*: The order in which customer are served; FCFS, LIFO, SIRO, Priority based.

## States of System
### Steady State: 
when rate of arrival < rate of service but both are constant. *A steady state system is also independent of time.* Probability of finding a particular length of queue is same!

>[!info] We always reach steady state
>A system will reach steady state at  t → ∞ if currently rate of arrival is > rate of service

### Transient State:
In this state, the operation characteristic of system are dependent on time.

### Explosive state:
Here arrival rate >> service rate. Theoretically, queue length will increase with time and can also tend to ∞.

---

## Designation of Queue

M / M / 1 : N / FCFS
A / B / S : ( d / f )

A: Arrival pattern of units.

B: The probability distribution of service time of individual actually being served.

S: Number of service channels.

d: Capacity of system.

f: The system discipline.

so M / M / 1: N / FCFS means:
Markovian (Poisson Distirbution) / Markovian / 1 service channels : fininte capacity / First come first serve

---
## Notations:

| Notations   | Meanings                                                                                                                                                       |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **X**       | Inter arrival time between two successive customers                                                                                                            |
| **Y**       | The service time required by any customer                                                                                                                      |
| **w**       | The waiting time for any customer before it is taken into service                                                                                              |
| **v**       | Time spent by the customer in the system                                                                                                                       |
| **n**       | Number of customers                                                                                                                                            |
| **Pn (t)**  | Probability that 'n' customers arrive in the system in time 't'                                                                                                |
| **Φn (t)**  | Probability that 'n' units are served in time 't'                                                                                                              |
| **U (T)**   | Probability distribution of inter arrival time P (t ≤ T).                                                                                                      |
| **V (T)**   | Probability distribution of servicing time P (t ≤ T).                                                                                                          |
| **F (N)**   | Probability distribution of queue length at any time P (N ≤ n)                                                                                                 |
| **En**      | Some state of the system at a time when there are 'n' units in the system                                                                                      |
| **λn**      | Average number of customers arriving per unit of time, when there are already ëní units in<br>the system.                                                      |
| **λ**       | Average number of customers arriving per unit of time.                                                                                                         |
| **µn**      | Average number of customers being served per unit of time when there are already ëní units<br>in the system.                                                   |
| **µ**       | Average number of customers being served per unit of time.                                                                                                     |
| **1 / λ**   | Inter arrival time between two arrivals.                                                                                                                       |
| **1 / µ**   | Service time between two units or customers.                                                                                                                   |
| **ρ = λ/µ** | System utility or traffic intensity. **ρ = 3 / 8, it means<br>to say that out of 8 hours the system is used for 3 hours and (8 ñ 3 = 5) 5 hours the is idle.** |

---

## Formula of  M/M/1: ∞/FCFS

### Formulae used:
1. Average number of arrivals per unit of time = λ
2. Average number of units served per unit of time = µ
3. Traffic intensity or utility ratio $$ρ=λ/µ$$ $$condition : µ > λ $$
4. Probability that the system is empty $$P_0 = (1 - ρ )$$
5. Probability that there are 'n' units in the system $$P_n =  ρ^n P_o$$
6. Average number of units in the system

	$$ E (n) = ρ/(1-ρ)\; or = λ/(λ−µ) = L_q + λ/µ$$

7. Average number of units in the waiting line:

	$$E_L = \rho^2/(1-ρ )\ = \lambda^2 /\mu(\mu-\lambda)$$

8. Average waiting length (mean time in the system) = E (L / L > 0)
	$$= 1/(\mu - \lambda)\ = 1/(1-\rho)\ = \ E(w) + 1/\mu = L/\lambda$$

9. Average length of waiting line with the condition that it is always greater than zero

	$$= V(n)\ = \ \rho/(1-\rho)^2\ = \lambda/(\mu - \lambda)^2$$

	$$= L_q/\lambda \ = \ \lambda/\mu(\mu - \lambda)$$

10. Average time an arrival spends in the system 

	$$E (v) = 1/\mu(1-\rho) = 1/(\mu - \lambda)$$

11. P (w > 0) = System is busy = ρ
12. Idle time  =  (1− ρ)
13. Probability distibution of waiting time  
$$
	P (w) dw =\mu\rho(1-\rho)e^{-\mu w (1-\rho)}
$$
14. Probability that a consumer has to wait on arrival = (P (w > 0) = ρ
15. Probability that a new arrival stays in the system 
$$
	P (v) dv =\mu(1-\rho)e^{-\mu w (1-\rho)}dv
$$
---
## Finite Queue: M/M/1 : N/FCFS

Various equation for this model are:

Probability of 0 customers in system


$$ P_0 = \ (1-\rho) / (1 - \rho^{N+1})$$

$$ where\ \rho=\lambda/\mu\ and\ \lambda/\mu > 1\ is\ allowed$$

Probability of N customers in System


$$P_n = (1-\rho)\rho^n/(1-\rho^{N+1})$$

$$ P_n = P_0*\rho^n$$

$$for\ all\ n=0,1,2 ...N$$

Average customers in system:

$$L_s = \rho[1-(1+N)\rho^N+N\rho^{N+1}]/(1-\rho)(1-\rho^{N+1})$$

this simplifies to:

$$ L_s=p_0*\sum_{n=0}^Nn*\rho^n$$

$$ L_s=\sum_{n=0}^Nn*P^n$$

Similarily,  Average queue length:

$$ L_q=\sum_{n=0}^N(n-1)*P^n$$
Simplifying, we get,

$$L_q = L_s - \lambda/\mu $$

>[!note] Pay Attention to Problem
>Customer in System = 1 + Length of queue


Waiting time in system:

$$W_s = L_s/\lambda'$$

$$where\ \lambda'=\lambda(1-P_N)$$

Waiting time in queue:

$$ W_q = W_s/\lambda'$$

---

# Operating Characteristics of a Queuing System

The performance of any queuing system can be studied by evaluating certain operating characteristics. These characteristics provide a mathematical and statistical basis to measure how effectively the system is working, whether the resources are being utilized properly, and how much delay or congestion customers experience. Below is a detailed explanation of the key operating characteristics and how they are used to evaluate system performance.

---

### 1. **Arrival Rate (λ)**

The arrival rate represents the average number of customers arriving into the system per unit of time. It is usually modeled as a Poisson process in many real-life situations, where arrivals are random and independent. For example, if 20 customers arrive every hour, then λ = 20/hour.

- **Performance use:** The arrival rate indicates the demand placed on the system. If the system is receiving customers at a higher rate than it can handle, it will experience congestion and longer waiting times. It helps in identifying if system resources need to be increased.
---

### 2. **Service Rate (μ)**

The service rate is the average number of customers a server can serve per unit of time. Like arrivals, service is often modeled as an exponential distribution. For instance, μ = 25/hour means a single server can handle 25 customers in an hour.

- **Performance use:** The service rate reflects the capacity of the system to process requests. Comparing service rate with arrival rate helps determine whether the system is underloaded, balanced, or overloaded.

---

### 3. **Traffic Intensity (ρ)**

Traffic intensity is defined as the ratio of the average arrival rate to the service rate. For a single-server system:

ρ=λμρ = \frac{λ}{μ}ρ=μλ​

For a system with _c_ servers:

ρ=λcμρ = \frac{λ}{cμ}ρ=cμλ​

- **Performance use:** This parameter tells us the proportion of time that servers are busy. If ρ < 1, the system is stable; if ρ ≥ 1, the system cannot handle the load and queues will grow indefinitely. This measure is critical to ensure a balance between efficiency (high utilization) and customer satisfaction (low waiting).
---

### 4. **Average Number of Customers in the System (L)**

This represents the expected number of customers present in the system, including those waiting in the queue and those being served.

- **Performance use:** A high value of _L_ shows congestion and inefficiency, while a moderate value indicates smooth operation. Managers use this measure to know how many customers the system can handle at a time.
---

### 5. **Average Number of Customers in the Queue (Lq)**

This is the expected number of customers waiting in the queue before service starts.

- **Performance use:** _Lq_ reflects the size of the waiting line. If _Lq_ becomes large, customers may feel dissatisfied or leave the system (balking or reneging). It is a direct indicator of delay severity.
---

### 6. **Average Waiting Time in the System (W)**

This measures the average time a customer spends in the system, including both waiting time and service time.

W=LλW = \frac{L}{λ}W=λL​

- **Performance use:** _W_ is important because it tells how long, on average, a customer has to commit to the system. This value influences service satisfaction and is often compared with service-level goals.
---

### 7. **Average Waiting Time in the Queue (Wq)**

This refers to the average time a customer spends only in the waiting line, before service begins.

$$Wq=\frac {L_q}λ$$​

- **Performance use:** _Wq_ helps to measure the customer delay directly. If waiting time is too high, it indicates insufficient service capacity or poor system design.

---

### 8. **Probability of Zero Customers in the System (P0)**

This is the probability that there are no customers in the system, meaning the server is idle.

- **Performance use:** _P0_ reflects idle time and helps in evaluating underutilization of resources. A very high P0 means wasted resources, while a very low P0 may mean servers are always busy, creating long queues.
---

### 9. **Probability of n Customers in the System (Pn)**

This is the probability that exactly _n_ customers are in the system at a given time.

- **Performance use:** These probabilities are used for capacity planning, resource allocation, and risk analysis. For example, in a call center, Pn helps determine how often a certain number of calls are in progress.
---

### 10. **Effective Arrival Rate and Blocking Probability**

In finite queue systems or systems with limited capacity, not all arriving customers can be admitted. The effective arrival rate considers only those who actually enter the system, while blocking probability gives the chance that an arrival is denied service due to lack of space.

- **Performance use:** In telecommunications, networks, and manufacturing, these parameters are critical for ensuring that the system design does not lose too many customers due to capacity limits.
---

### **How These Characteristics Evaluate System Performance**

1. **Efficiency of Resources:** Traffic intensity (ρ) and P0 help determine if resources are overutilized or underutilized. Balanced utilization ensures cost-effectiveness.
    
2. **Customer Satisfaction:** W, Wq, L, and Lq directly measure the customer’s waiting experience. Shorter waiting times mean higher satisfaction.
    
3. **System Stability:** The relationship between λ and μ (via ρ) helps determine whether the system can handle long-term demand without becoming unstable.
    
4. **Capacity Planning:** L, Lq, and Pn provide inputs for decisions on how many servers, counters, or machines are required to maintain desired performance levels.
    
5. **Cost vs. Performance Trade-off:** Reducing waiting times often requires adding servers, which increases cost. These characteristics provide quantitative measures to balance cost and service quality.
    
6. **Bottleneck Identification:** High Lq or Wq values highlight system bottlenecks, guiding where improvements should be made.
---

**Conclusion:**  
The operating characteristics of a queuing system—arrival rate, service rate, traffic intensity, average numbers and waiting times, and system probabilities—are essential tools for analyzing performance. They allow engineers and managers to evaluate system stability, resource utilization, customer satisfaction, and cost-effectiveness. By carefully monitoring and optimizing these measures, a queuing system can be designed or adjusted to achieve the best possible balance between efficiency and service quality.