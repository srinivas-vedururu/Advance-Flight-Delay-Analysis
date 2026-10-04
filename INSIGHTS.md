# 📊 Flight Delay Analysis: Complete Empirical Insights & Strategic Briefing

> **Dataset:** 336,776 commercial flights departing NYC (EWR, JFK, LGA) in 2013  
> **Source Notebook:** [`flight_delay_analysis_pro.ipynb`](flight_delay_analysis_pro.ipynb)  
> **Interactive Report:** [`flight_delay_intelligence_report.html`](flight_delay_intelligence_report.html)  

---

## 📑 Table of Contents
1. [Executive Summary & Core Takeaways](#1-executive-summary--core-takeaways)
2. [Distribution Mechanics: The Mean vs. Median Paradox](#2-distribution-mechanics-the-mean-vs-median-paradox)
3. [Diurnal Rhythm: The Afternoon "Snowball" Delay Cascade](#3-diurnal-rhythm-the-afternoon-snowball-delay-cascade)
4. [Weekly Operational Cadence: Peak Congestion Windows](#4-weekly-operational-cadence-peak-congestion-windows)
5. [Seasonality & Weather Disruptors](#5-seasonality--weather-disruptors)
6. [Airport Hub Benchmarking: EWR vs. JFK vs. LGA](#6-airport-hub-benchmarking-ewr-vs-jfk-vs-lga)
7. [Airline Reliability & Performance Scorecards](#7-airline-reliability--performance-scorecards)
8. [Corridor & Route Dynamics: Best and Worst City Pairs](#8-corridor--route-dynamics-best-and-worst-city-pairs)
9. [Delay Carryover & In-Flight Recovery Physics](#9-delay-carryover--in-flight-recovery-physics)
10. [Statistical Hypothesis Testing Proof Table](#10-statistical-hypothesis-testing-proof-table)
11. [Actionable Recommendations: Airlines, Airports, & Passengers](#11-actionable-recommendations-airlines-airports--passengers)

---

## 1. Executive Summary & Core Takeaways

Across 336,776 flight movements in 2013, the NYC metropolitan airspace operated under severe capacity and scheduling strain:

* **21.0%** of all flights departed with **FAA-defined delays** (> 15 minutes).
* **28.4%** experienced minor-to-extreme departure delays (> 0 minutes).
* **2.45%** (8,255 flights) were completely cancelled.
* **The "Snowball Effect" is the primary operational driver:** Flights scheduled between 05:00 and 07:00 exhibit a delay probability of just **6.0% - 8.1%** with an average delay of **~1.5 minutes**. By 19:00 - 21:00, the delay probability surges **5.9× to 35.8%**, and average departure delay skyrockets **16× to 24.8 minutes**.
* **Departure delays are irreversible:** The correlation between departure delay and arrival delay is **$r = 0.937$** ($p < 10^{-300}$). Airlines recover less than **6.3%** of lost departure time while airborne.
* **Hub infrastructure matters significantly:** Newark Liberty (**EWR**) is the most delay-prone NYC hub (mean delay: **15.1 min**, delay rate: **24.0%**), while LaGuardia (**LGA**) demonstrates superior operational velocity (mean delay: **10.3 min**, delay rate: **18.3%**).

---

## 2. Distribution Mechanics: The Mean vs. Median Paradox

A foundational finding of this EDA is the **severe right-skewness** of departure delay data:

| Metric | Empirical Value | Operational Interpretation |
| :--- | :---: | :--- |
| **Median Delay** | **`-2.0 min`** | Over **50% of all flights push back early** or exactly on-time. |
| **Mean Delay** | **`+12.6 min`** | Skewed upward by an extreme, heavy right tail. |
| **Standard Deviation**| **`40.2 min`** | High variance indicates low schedule predictability. |
| **Skewness Coefficient**| **`4.84`** | Strong positive skew; extreme outlier-dominated. |
| **90th Percentile** | **`+49.0 min`** | The top 10% worst flights suffer delays near 1 hour. |
| **99th Percentile** | **`+191.0 min`**| 1 in 100 flights experiences a delay exceeding 3.2 hours. |
| **Maximum Recorded Delay** | **`1,301 min`** | Extreme 21.7-hour overnight aircraft turnaround hold. |

> 💡 **Recruiter Takeaway:** Reporting only mean delay severely misleads business stakeholders. Because the median is `-2.0 minutes`, the typical flight departs slightly ahead of schedule. Delays are an **asymmetric risk** driven by tail-risk operational bottlenecks rather than systemic baseline sluggishness.

---

## 3. Diurnal Rhythm: The Afternoon "Snowball" Delay Cascade

Analyzing departure performance across each hour of the operating day reveals a relentless compound propagation mechanism:

| Departure Hour | Scheduled Flights | Mean Departure Delay | FAA Delay Rate (>15m) | Risk Profile |
| :---: | :---: | :---: | :---: | :--- |
| **05:00** | 1,953 | **0.7 min** | **5.9%** | 🟢 Minimal Risk (Clean slate) |
| **06:00** | 25,951 | **1.6 min** | **7.4%** | 🟢 Optimal Morning Window |
| **07:00** | 22,821 | **1.9 min** | **8.1%** | 🟢 Low Congestion |
| **08:00** | 27,242 | **4.1 min** | **11.0%** | 🟡 Morning Push begins |
| **12:00** | 20,387 | **11.5 min** | **18.9%** | 🟡 Midday Buffer Erosion |
| **15:00** | 21,701 | **17.9 min** | **26.1%** | 🟠 Compound Delays Form |
| **17:00** | 24,426 | **21.1 min** | **29.6%** | 🔴 Evening Gridlock |
| **19:00** | 21,441 | **24.8 min** | **33.4%** | 🔴 Peak Delay Intensity |
| **20:00** | 16,739 | **24.3 min** | **34.5%** | 🔴 Severe Cascade |
| **21:00** | 10,933 | **24.2 min** | **35.8%** | 🔴 Maximum Delay Probability |

### Why Does This Happen?
Commercial aircraft operate 4 to 6 legs (flight turns) daily. In the morning, aircraft start rested at gates with full crew duty clocks and empty taxiways. When an early-afternoon leg experiences a 25-minute ground turnaround delay, the buffer vanishes. By evening, crew duty timeout thresholds, gate contention, and congested TRACON airspace multiply minor delays into hours of system lag.

---

## 4. Weekly Operational Cadence: Peak Congestion Windows

Evaluating flight performance across all 7 days reveals distinct business vs. leisure travel patterns:

| Day of Week | Total Flights | Mean Dep Delay | Delay Rate (>15m) | Operational Environment |
| :--- | :---: | :---: | :---: | :--- |
| **Monday** | 50,690 | 14.8 min | 22.4% | Heavy business outbound traffic |
| **Tuesday** | 50,422 | 10.6 min | 19.6% | Smooth midweek operations |
| **Wednesday** | 50,060 | 11.8 min | 19.8% | Stable airspace throughput |
| **Thursday** | 50,219 | **16.1 min** | **24.3%** | ⚠️ **Worst operational day** (Business returns) |
| **Friday** | 50,308 | 14.7 min | 23.4% | ⚠️ Peak holiday/leisure departure surge |
| **Saturday** | 38,720 | **7.7 min** | **16.3%** | 🏆 **Best operational day** (-52% delay duration) |
| **Sunday** | 46,357 | 11.6 min | 20.1% | Inbound leisure arrivals |

* **The Thursday/Friday Pinch Point:** Thursday afternoon/evening represents the single worst recurring 6-hour window in NYC aviation.
* **The Saturday Relief:** Flight volumes drop by **~23%**, allowing runways to operate below saturated capacity and cutting average delay nearly in half.

---

## 5. Seasonality & Weather Disruptors

Monthly analysis demonstrates that flight delays are strongly bi-modal, driven by distinct weather regimes:

| Month | Volume | Mean Dep Delay | Delay Rate | Primary Vector |
| :--- | :---: | :---: | :---: | :--- |
| **January** | 27,004 | 10.0 min | 18.2% | Winter storms / De-icing holds |
| **February** | 24,951 | 10.8 min | 19.2% | Cold weather ground ops |
| **March** | 28,834 | 13.2 min | 21.6% | Spring transition winds |
| **April** | 28,330 | 13.9 min | 22.0% | Heavy rain fronts |
| **May** | 28,796 | 13.0 min | 22.4% | Elevated flight traffic |
| **June** | 28,243 | **20.8 min** | **27.8%** | ⛈️ Severe summer convective thunderstorms |
| **July** | 29,425 | **21.7 min** | **28.6%** | ⛈️ **Worst month** (Peak thunderstorms + passenger volume) |
| **August** | 29,327 | 12.6 min | 21.7% | Summer tail demand |
| **September** | 27,574 | 6.7 min | **13.7%** | 🌤️ **Best month** (Clear weather, off-peak volume) |
| **October** | 28,889 | 6.2 min | 14.8% | 🌤️ Ideal flying weather |
| **November** | 27,268 | **5.4 min** | 14.4% | 🌤️ Lowest average delay of entire year |
| **December** | 28,135 | 16.6 min | 26.7% | ❄️ Holiday surge + Northeast winter weather |

### Analytical Insights:
* **Summer Convective Storms are Far Worse than Snow:** July delays (**21.7 min**) are more than **2×** worse than January delays (**10.0 min**). Convective thunderstorms shut down FAA arrival gates and ground-stop entire East Coast corridors.
* **The Autumn Window (Sep–Nov):** Represents the golden quarter for aviation reliability.

---

## 6. Airport Hub Benchmarking: EWR vs. JFK vs. LGA

Comparing the three major Port Authority gateways reveals striking operational differences:

| Hub Airport | Total Flights | Mean Dep Delay | Median Dep Delay | Delay Rate (>15m) | Cancellation Rate |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Newark Liberty (EWR)** | 120,835 (35.9%) | **15.1 min** | -1.0 min | **24.0%** | 2.68% |
| **JFK International (JFK)**| 111,279 (33.0%) | **12.1 min** | -1.0 min | **20.4%** | **1.67%** |
| **LaGuardia (LGA)** | 104,662 (31.1%) | **10.3 min** | **-3.0 min** | **18.3%** | 3.01% |

### Key Takeaways:
1. **EWR is the Congestion Bottleneck:** Suffers the highest mean delay and delay rate, largely due to single-runway dependency during crosswinds and saturated departure fixes into the Midwest.
2. **LGA Outperforms on Punctuality:** With strict perimeter rules limiting flights past 1,500 miles, LGA handles high-frequency regional shuttles with rapid gate turns.
3. **JFK Prioritizes Long-Haul Integrity:** Lowest cancellation rate (1.67%) because international wide-body flights have massive turnaround buffers and cancellation costs are prohibitive.

---

## 7. Airline Reliability & Performance Scorecards

Aggregating all 16 carriers reveals massive performance disparity:

| Carrier | Flights | Mean Dep Delay | Delay Rate (>15m) | Composite Reliability Tier |
| :--- | :---: | :---: | :---: | :--- |
| **US Airways (`US`)** | 20,536 | **3.8 min** | 11.8% | 🥇 **Tier 1 (Exceptional)** |
| **Hawaiian Airlines (`HA`)** | 342 | **4.9 min** | **7.0%** | 🥇 **Tier 1 (Flawless)** |
| **Alaska Airlines (`AS`)** | 714 | **5.8 min** | 13.2% | 🥇 **Tier 1 (High Reliability)** |
| **American Airlines (`AA`)** | 32,729 | **8.6 min** | 15.6% | 🥈 **Tier 2 (Strong Network)** |
| **Delta Air Lines (`DL`)** | 48,110 | **9.3 min** | 16.2% | 🥈 **Tier 2 (Operational Leader)** |
| **Envoy Air (`MQ`)** | 26,397 | 10.6 min | 20.2% | 🥉 **Tier 3 (Average Regional)** |
| **United Airlines (`UA`)** | 58,665 | 12.1 min | 20.8% | 🥉 **Tier 3 (Hub Saturated at EWR)** |
| **JetBlue Airways (`B6`)** | 54,635 | 13.0 min | 22.6% | 🥉 **Tier 3 (Northeast Heavy)** |
| **Endeavor Air (`9E`)** | 18,460 | 16.7 min | 24.2% | ⚠️ **Tier 4 (Struggling Regional)** |
| **Southwest Airlines (`WN`)**| 12,275 | 17.7 min | 26.5% | ⚠️ **Tier 4 (Tight Turnaround Lag)** |
| **ExpressJet (`EV`)** | 54,173 | **20.0 min** | **28.9%** | 🛑 **Tier 5 (Severe Delay Risk)** |
| **Frontier Airlines (`F9`)** | 685 | **20.2 min** | **28.0%** | 🛑 **Tier 5 (Severe Delay Risk)** |

---

## 8. Corridor & Route Dynamics: Best and Worst City Pairs

Filtering for high-frequency routes (minimum 1,000 annual flights):

### 🏆 Top 5 Most Punctual Corridors
| Rank | Route | Volume | Mean Dep Delay | Delay Rate (>15m) | Primary Driver |
| :---: | :--- | :---: | :---: | :---: | :--- |
| **1** | **`LGA -> BOS`** | 4,283 | **`-0.5 min`** | **8.6%** | High-priority hourly executive shuttle |
| **2** | **`LGA -> DCA`** | 4,716 | **`5.0 min`** | 14.1% | Protected Capitol shuttle corridor |
| **3** | **`LGA -> DFW`** | 4,858 | **`5.8 min`** | 13.0% | Major mainline AA fortress hub |
| **4** | **`EWR -> RSW`** | 1,437 | **`5.9 min`** | 14.1% | Point-to-point Florida leisure |
| **5** | **`LGA -> MIA`** | 5,781 | **`7.4 min`** | 14.4% | Dedicated mainline slots |

### ⚠️ Top 5 Most Delay-Prone Corridors
| Rank | Route | Volume | Mean Dep Delay | Delay Rate (>15m) | Primary Driver |
| :---: | :--- | :---: | :---: | :---: | :--- |
| **1** | **`EWR -> RIC`** (Richmond) | 1,667 | **`26.5 min`** | **35.3%** | Lower-priority regional feeder |
| **2** | **`EWR -> MKE`** (Milwaukee) | 1,094 | **`23.6 min`** | **32.8%** | Regional jet airspace ground holds |
| **3** | **`EWR -> MCI`** (Kansas City)| 1,356 | **`21.7 min`** | **31.5%** | Midwest storm convergence |
| **4** | **`JFK -> ORD`** (Chicago) | 2,326 | **`21.6 min`** | **28.9%** | Compounding ORD ground delay programs |
| **5** | **`JFK -> MSP`** (Minneapolis)| 1,095 | **`21.3 min`** | **28.9%** | Severe winter & connecting holds |

> 📌 **Takeaway:** Regional feeder flights (`EWR -> RIC`, `EWR -> MKE`) are systematically sacrificed by ATC Ground Delay Programs to protect transcontinental and international wide-body slots.

---

## 9. Delay Carryover & In-Flight Recovery Physics

One of the most powerful findings in the notebook centers on in-flight delay recovery:

```
Regression Equation:   Arrival_Delay = 1.018 * Departure_Delay - 5.76 min
Pearson Correlation:   r = 0.9372  (p < 1e-300)
R-Squared:             R² = 0.878  (Departure delay explains 87.8% of arrival delay)
```

### Empirical Physics of Delays:
* **The "Make Up Time In the Air" Myth:** Pilots can only burn extra fuel to increase Mach numbers by small increments. On average, scheduled padding recovers just **~5.8 minutes** over an entire flight.
* If a flight departs **60 minutes late**, it will arrive on average **55.3 minutes late**.
* **Distance to Air Time Fidelity:** Pearson correlation between scheduled distance and actual flight duration is **$r = 0.9904$** ($R^2 = 0.981$), proving that once airborne, flight times are extraordinarily deterministic.

---

## 10. Statistical Hypothesis Testing Proof Table

| Hypothesis Test | Null Hypothesis ($H_0$) | Statistical Test | Test Statistic | p-Value | Formal Verdict |
| :--- | :--- | :--- | :---: | :---: | :---: |
| **1. Airport Homogeneity** | Delays are identically distributed across EWR, JFK, LGA | **Kruskal-Wallis H-Test** | $H = 1,234.8$ | **$< 10^{-250}$** | ❌ **REJECT $H_0$** (Significant difference) |
| **2. Weekday vs Weekend** | Weekday delays equal weekend delays | **Mann-Whitney U-Test** | $U = 1.28 \times 10^{10}$ | **$< 10^{-45}$** | ❌ **REJECT $H_0$** (Significant difference) |
| **3. Seasonal Disparity** | Delay distribution is equal across 4 seasons | **Kruskal-Wallis H-Test** | $H = 3,418.2$ | **$< 10^{-300}$** | ❌ **REJECT $H_0$** (Significant difference) |
| **4. In-Flight Predictability**| Distance has no linear correlation with air time | **Pearson Correlation** | $r = 0.9904$ | **$< 10^{-300}$** | ❌ **REJECT $H_0$** (Strong positive relationship) |

---

## 11. Actionable Recommendations: Airlines, Airports, & Passengers

### 🛫 For Airline Network Planners & Dispatch Operations
1. **Dynamic Turnaround Buffering:** Insert an additional **15–20 minutes** of scheduled ground buffer into aircraft turnarounds scheduled between **15:00 and 19:00** to break the cascading delay chain.
2. **De-Prioritize Peak Regional Slots:** Swap high-frequency regional jet departures out of EWR during the 17:00–19:00 peak into larger mainline aircraft with lower frequencies.
3. **Transparent Checkout Badges:** Display historical on-time probability badges during customer ticket purchase.

### 🏢 For Airport Authorities (PANYNJ & FAA)
1. **EWR Flow Management:** Prioritize taxiway throughput improvements and runway de-confliction procedures at Newark.
2. **Convective Weather Early-Reroute Protocols:** Implement proactive early reroutes around Pennsylvania/Ohio airspace during June/July convective storm alerts.

### 🧳 For Corporate Travel Managers & Passengers
1. **The 07:00 Rule:** Book flights departing before **08:00 AM** to achieve an **>92%** probability of on-time departure.
2. **Airport Selection Strategy:** Choose **LGA** over EWR for domestic east-coast travel to shave an average of **4.8 minutes** off departure delay risk.
3. **Avoid Thursday/Friday Evenings:** If flying late in the day, opt for Tuesday, Wednesday, or Saturday departures.
