# Discussion on Welding Scheduling in Factory

---

## ⭐Case introduction - bicycle parts welding process

### 1. Research background

- **Welding process**
1. There are **four** different materials (**titanium, white iron, aluminum, iron**) for processing.
2. **Titanium, white iron** /**aluminum, and iron** share production capacity respectively (600 minutes of processing time each day).
3. The frame (divided into front and back), the front must be processed first and then the back.
4. Different parts have different welding times.
5. Assume that there are only two welding machines for operation, respectively **welding titanium, white iron** /**aluminum, and iron.**
6. Multiple parts **cannot** be welded on the same machine at the same time.

**Table 1-1 Frame welding time**

| material | Front  welding | back welding |
| --- | --- | --- |
| Titanium | 25 units/600 minutes | 25 units/600 minutes |
| White iron | 25 units/600 minutes | 25 units/600 minutes |
| Aluminum | 50 units/600 minutes | 50 units/600 minutes |
| iron | 20 units/600 minutes | 20 units/600 minutes |

**Table 1-2 Welding time of other parts**

| Component | Front  welding |
| --- | --- |
| Titanium front fork dropouts | 50 units/600 minutes |
| Iron front fork dropout | 100 pieces/600 minutes |
| Titanium crank | 30 groups/600 minutes |
| Titanium STEM | 50 pieces/600 minutes |

---

## Current status of production scheduling

This case factory currently uses manual scheduling to perform operations, and mostly uses the experience of senior masters as the production sequence evaluation.**There is no exact standard.**

---

### 2.. Research methods and framework

1. Scheduling theory research
2. **Production scheduling optimization and implementation**

📜step:

- Order data sorting Use python to read the original data and organize the raw data into a specific format.(**The following are assumptions)**

| serial | Type | amount | category | Machine  | Process Time |
| --- | --- | --- | --- | --- | --- |
| 1 | Aluminum frame-front | 265 | 4 | 1 | 12 |
| 2 | Aluminum frame-back | 265 | 5 | 1 | 12 |
| 3 | iron frame-front | 100 | 1 | 1 | 12 |
| 4 | iron frame-back | 100 | 2 | 1 | 12 |
| 5 | iron frame-front | 524 | 1 | 1 | 12 |
| 6 | iron frame-back | 524 | 2 | 1 | 12 |

- Use genetic algorithms to solve welding scheduling problems
    
    
- **Initial chromosomes**
    
     Initial chromosomes is **preset to 20**. Assuming that there are N orders, an array access will be generated, and the array is randomly arranged and combined from 0 to N. In the example above, there are 6 orders and it will be first Randomly generate 20 kinds of arrays composed of five digits from 0 to 5 .
    
- **Fitness function**
    
    **The goal is to minimize the delay time**, so compare the completion time of all orders with their latest delivery time. When the completion time of an order exceeds its latest delivery time, **the delay time is calculated and the delays of all orders are added up**.
    
- **Select parents to use binary competitive selection method**
    
    Each time, two kinds of parents are selected from the permutation and combination, and compared with the values obtained by bringing them into the fitness function, and the one with the smaller delay time is selected as The parent generation will eventually produce 20 permutations and combinations of five-digit numbers from 0 to 5.
    
- **Mating generates offspring**
    
    Use uniform mating to reproduce offspring. Use binary coding to generate a 6-bit random mask, and randomly select two arrangements from the parent generation to reproduce the offspring, so that the parent and mother generations retain their masks. is the number corresponding to the 1 part, and the mask is swapped to the number corresponding to the 0 part, so that the offspring retain randomness and variability.
    
- **Adjusting the infeasible solution**
    
    Because the welding frame has a sequence, it is necessary to adjust the correct order of the front and back and make the output result is a reasonable solution
    
- **Experimental Design**
    
    When the number of days in advance is set in different days in advance, what is the minimum delay time, and the minimum delay is just no delay
    

📏We also try to Build Flexsim model to help us in verification and simulation the project.

(The educational version is intended for study and research use!)

<img width="369" alt="flesxim" src="https://github.com/Linszuchi047/Discussion-on-Lathe-and-Welding-Scheduling-in-Factory/assets/140520487/cfde03ff-abea-456b-a377-a05f9e6a4de3">

