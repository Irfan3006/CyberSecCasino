# CyberSec Casino - PRNG JUDOL Simulator

**🔗 Live Demo: [https://cyberseccasino.netlify.app/](https://cyberseccasino.netlify.app/)**

**IMPORTANT: This project was created exclusively for internal research, experimentation, and personal educational purposes.**

This project is a simulation of Pseudo-Random Number Generator (PRNG) systems commonly used in software development, specifically focusing on probability systems in gacha games and online slot machines (iGaming).

Through this application, I experiment with, audit, and deconstruct the logic behind artificial luck. The ultimate goal is to verify and audit common algorithms from a Cyber Security perspective to understand how they can be exploited or manipulated.

## Learning Objectives
1. **PRNG Analysis**: Studying how standard math random functions and built-in language PRNG engines operate under the hood.
2. **LCG Exploitation**: Investigating the vulnerabilities of the Linear Congruential Generator (LCG), a deterministic generator that can be 100% predicted if the initial seed and mathematical constants are known.
3. **Predetermined Outcome Systems**: Understanding advanced probability manipulation using a Closed Deck System (fixed outcome quota), where probabilities are not purely random but predetermined to ensure the house edge is mathematically absolute.
4. **Execution Security**: Experimenting with the impact of seed manipulation and package modification on lottery simulations for understanding real-world attack vectors and mitigations.

## Technical Explanations of Algorithms

### 1. Standard Math.random()
The default pseudorandom number generator provided by JavaScript engines (such as V8's implementation of xorshift128+). While it is heavily optimized for performance, it is **not cryptographically secure**. Although harder to crack than older algorithms, determined attackers analyzing enough sequential outputs can potentially reconstruct the internal state and predict future values.

### 2. Linear Congruential Generator (LCG)
One of the oldest and simplest PRNG algorithms. It generates sequences based on the following mathematical formula:
`X_(n+1) = (a * X_n + c) mod m`
Where `X` is the sequence of random values, `m` is the modulus, `a` is the multiplier, and `c` is the increment.
**Vulnerability**: LCG is highly insecure for cryptographic or high-stakes random generation. If an attacker discovers the seed (X_0) and the constants (a, c, m), the entire future and past sequence of numbers can be calculated instantly.

### 3. Custom Card Gacha (CCG) / Closed Deck System
Often referred to technically as a "House Mode" or predetermined pool. This algorithm abandons continuous random generation in favor of a shuffled array of fixed outcomes (e.g., 2 Jackpots, 8 Big Wins, 20 Mid Wins, 70 Loses out of 100 spins). 
**Mechanism**: The outcomes are populated into an array and perfectly randomized using the **Fisher-Yates Shuffle** algorithm. The system then simply pops items from this array one by one.
**Reality Check**: This ensures the platform's return-to-player (RTP) matches exactly with the intended mathematics every X spins. From a user's perspective, the spinning reels are merely a cosmetic illusion over a predetermined result array.

## Simulation Modules

### 1. Gacha PRNG Module (gacha.html)
A lottery/gacha pull simulation wrapped in a Cybersecurity theme.
* Allows instant switching between standard Math.random() and deterministic LCG.
* Features Deck Manipulation where the outcome composition of every 100 pulls is fixed and decided by the operator.
* Includes a transparent audit log to verify the exact PRNG floats and the resulting pulls.

### 2. Slot Exploit Module (slot.html)
A slot machine terminal simulation complete with a visual representation of spinning reels.
* Simulates auto-spins and tracks the durability of user balance against the configured house edge.
* Demonstrates how the predetermined system overrides visual mechanics, proving that what the user sees on the spinning reels is entirely disjointed from the pre-calculated payout logic.

## Tech Stack
* **HTML5**: UI Structure.
* **JavaScript (ES6+)**: Core simulation engine, PRNG algorithms, deck creation logic, and recursive animation handling.
* **Tailwind CSS v3**: Modern interface styling utilizing Glassmorphism and Dark/Light Theme support.
* **Canvas Confetti**: Visual validation for win states executed via canvas rendering.

## Disclaimer & Code of Ethics
* This project is **not** functional real-money gaming or gambling software.
* The simulation is built strictly to study security engineering, reverse-engineering, and vulnerabilities in pseudo-random number algorithms.
* The author **takes no responsibility** for any misuse of the algorithms or concepts demonstrated in this repository for illegal activities or the development of actual gambling platforms.

---
*Created by Irfan as a personal cyber security research lab.*
