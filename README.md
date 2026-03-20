# GigShield

## Inspiration
India has millions of gig workers delivering groceries for platforms like Zepto and Blinkit. A gig worker is someone who works on a per-task, per-delivery, or per-ride basis. They are not full-time employees. They get paid per job completed. They work with no fixed salary and no safety net. Studies show gig workers lose **20 to 30 percent** of their monthly earnings due to external disruptions like heavy rain, extreme heat, AQI spikes, and sudden zone shutdowns — all completely outside their control. Nobody compensates them for this lost time.

What made this personal was a real quote from a delivery partner: *"If the delivery is delayed, I get a pay cut."* When it rains, customers are charged a surge fee but riders get almost nothing extra. Then customers give low ratings because of weather-caused delays, which reduces the rider's future order allocation and cuts their incentives. The rider suffers from every angle — and none of it is their fault.

The challenge that drove us was this — if you charge a full-time rider who earns more and a part-time rider who earns less the same premium, it would not be AI-powered or fair. Our AI had to understand the difference between a part-time student delivering food and a full-time father as the sole breadwinner — and treat them differently. That is what inspired GigShield.

## What it does
**GigShield** is an AI-powered parametric income insurance platform for Q-commerce delivery riders working with Zepto and Blinkit. The rider pays a small weekly premium based on their earnings. When an external disruption is detected in their zone — heavy rain, extreme heat, severe AQI, a dark store shutdown, or a platform outage — GigShield automatically triggers a payout. **No forms, no calls, no waiting.**

### Our Persona — Q-Commerce Riders (Zepto / Blinkit)
We chose Q-commerce riders specifically because they work in very small delivery zones of 2 to 3 kilometers around a dark store. They do 10-minute sprint deliveries, so their entire earning potential depends on completing many orders quickly. When their zone floods or shuts down, they cannot shift to another area like a cab driver can. They are a mix of full-time workers supporting families and part-time workers like students — each with very different income levels and risk profiles. They are uniquely vulnerable.

## Coverage — Income Loss Only
GigShield covers only the income lost due to external disruptions. Here is exactly how each scenario is handled:

| Scenario | What GigShield does | Why |
| :--- | :--- | :--- |
| **Worker cancels order because of rain** | Payout triggered | The extreme rain parameter was met. The AI assumes they cannot work. |
| **Worker delivers late because of rain** | Payout triggered | Even if they deliver, they are earning less per hour because they are slower. We are insuring their time. |
| **Worker sits at home not logged in** | No payout | If they were not online on their work app, they did not lose income. |

### What if the rider works through the rain?
This is the core of GigShield. Even if the rider delivers the order but it takes much longer because of a flood, they are still losing money — because they could have done many more orders in that same time. GigShield pays for the reduced earning capacity during the disruption period, not just for orders that were cancelled.

### Rain — A Real and Important Scenario
When heavy rain hits, customers are charged a surge fee by the platform. Riders receive very little extra for braving the rain. Then customers give low ratings because of weather-caused delays. Those low ratings reduce the rider's future order allocation and cut their incentives. GigShield steps in to cover the income lost during those hours.

### What GigShield strictly does NOT cover
- ❌ Vehicle repairs — no flat tires, engine damage, or accident repairs
- ❌ Medical and health bills — no hospital bills, medicines, or doctor visits
- ❌ Life and accident cover — no payouts for injuries or death
- ❌ Stolen or damaged assets — no cover for phones, bags, or equipment
- ❌ Personal choice absences — if a rider stays home because they are tired with no active disruption in their zone, no payout is issued

## Parametric Triggers
GigShield covers five external disruptions, all detected automatically via APIs. **No rider action is required.**

### How the trigger works — three steps:
1.  **The Threshold** — a rule is set, for example rain above a certain level per hour or AQI above a certain level.
2.  **The Validation** — the AI checks the Weather API plus the rider's GPS location.
3.  **The Payout** — if the rule is met and the rider is confirmed to be in that area, the money is sent instantly.

### Trigger Categories:
-   **Environmental Triggers**:
    -   **Heavy Rain and Floods**: Detected via OpenWeatherMap API. The most common trigger. If a zone is waterlogged, deliveries stop.
    -   **Extreme Heat**: Triggers when temperature crosses dangerous outdoor working levels. The AI triggers a payout so the rider can rest during the hottest hours without losing the day's earnings.
    -   **Severe AQI**: Detected via AQICN API. In cities like Delhi, if the AQI crosses the Severe category, it becomes a health hazard to be outside. GigShield covers the income lost during Red Alert hours, adjusted for the local 30-day baseline.
-   **Social and Civic Triggers**:
    -   **Zone Shutdown and Curfews**: Detected via mock civic alert API. Covers unplanned curfews, local strikes and bandhs, and dark store closures by authorities.
    -   **Dark Store Closure**: Detected when the rider's assigned pickup point is flagged as closed by authorities.
-   **Technical Trigger**:
    -   **Platform Outage**: Detected when the delivery platform API shows downtime above a minimum threshold during the rider's active hours. Since this is an external disruption out of their control, GigShield triggers a payout for those hours.

## Weekly Premium Model
**Why weekly?** Q-commerce riders are paid weekly by their platforms. Structuring the premium on a weekly cycle means it feels natural and affordable — it comes out of the same week's earnings it protects. Every Monday the rider pays their premium. Every Sunday GigShield settles the weekly payout.

### The Percentage Rule — How the premium is decided:
Instead of a fixed amount, GigShield charges roughly **2 to 3 percent** of what the rider usually earns in a week. This is called **Sachet Insurance** — it feels affordable to everyone because it is always proportional to what they earn.

-   **Worker A** (Full-timer): Pays a percentage of their higher weekly earnings on Monday and receive higher protection.
-   **Worker B** (Part-timer): Pays a percentage of their lower weekly earnings on Monday and receive proportional coverage.

> **Higher earners → pay more → get more protection**
> **Lower earners → pay less → get less protection**

### The Hourly Replacement Rule — How the payout is decided:
GigShield replaces the rider's actual time value. The AI calculates their **Average Hourly Rate** from their past 4 weeks of data. During a disruption, the payout is the disrupted hours multiplied by that hourly rate, adjusted for severity.

#### Tiered Payout Scale based on disruption severity:
-   **Light disruption**: 20% of their hourly rate
-   **Moderate disruption**: 50% of their hourly rate
-   **Severe disruption**: 80% of their hourly rate
-   **Red Alert and Flood**: 100% of their hourly rate

**Weekly Payout Cap**: Every policy has a maximum payout per week. If a rider pays a lower premium, the most they can receive back in a week is capped proportionally. This protects the business while still giving the rider a meaningful safety net.

**Adaptive Thresholds**: The AI looks at the 30-day local average for weather and AQI. A disruption is only triggered when conditions cross significantly above that baseline. For example, if the average AQI in Delhi is already 300, GigShield only pays if it hits the Extreme level. This prevents paying for routine bad weather and ensures payouts are reserved for genuine extreme events.

## Hybrid Payout System
1.  **Instant Advance**: An instant advance hits the rider's UPI within minutes of the trigger firing.
2.  **Weekly Settlement**: Every Sunday the AI calculates total hours lost across all disruptions that week, multiplies by the rider's Average Hourly Rate, applies the severity percentage, deducts advances already paid, and settles the remaining balance. The rider sees a weekly summary showing exactly what happened, how many hours were disrupted, and what they received.

## The Onboarding — How the AI builds the plan
-   **Step 1: Data Sync** — the rider connects their platform account or uploads a screenshot of their earnings.
-   **Step 2: AI Analysis** — the AI reads the numbers and calculates their average hourly rate.
-   **Step 3: Custom Plan** — the AI generates a personalized shield showing exactly what they pay this week and what their hourly income protection rate is.

## Distress Protection Feature
When the AI detects a disruption, it immediately notifies the rider that their income loss is being calculated and a payout is on the way. The rider does not panic. They do not rush dangerous deliveries through flooded roads trying to protect their earnings — because GigShield already has them covered.

**Hidden Impact — Ratings**: When a customer gives a low rating because of a weather-caused delay, the rider gets fewer future orders and their incentives reduce. GigShield's Distress Protection notifies the rider the moment a disruption is detected, so they stay calm, ride safely, and do not make desperate decisions that could hurt their rating further.

## How we built it

### Tech Stack
-   **Mobile App**: Kotlin, Android Studio
-   **Backend AI Engine**: Python, FastAPI
-   **Insurer Web Dashboard**: Next.js
-   **Database**: Supabase (PostgreSQL)
-   **Weather Data**: OpenWeatherMap API
-   **Air Quality Data**: AQICN API
-   **Zone and Traffic Data**: Mock APIs
-   **Payout Processing**: Razorpay test mode (UPI simulation)

### AI and ML Integration
-   **Dynamic Premium Calculation**: Every week the AI recalculates the rider's premium based on their updated earnings data, their delivery zone's historical risk score, and the upcoming week's weather forecast. The premium reflects actual current risk and changes weekly.
-   **Average Hourly Rate Engine**: The AI builds an earnings profile from the rider's past 4 weeks, understanding the difference between full-time and part-time workers to provide proportional coverage.
-   **Adaptive Threshold Engine**: Monitors the 30-day rolling average of weather and AQI per city zone to ensure payouts are triggered only by genuine extreme events.

### Fraud Detection — Multi-Layer AI
1.  **Layer 1 — GPS Validation**: Checks if the rider's GPS shows movement toward a work zone before the disruption hit.
2.  **Layer 2 — Historical Work Pattern**: Compares current activity against the rider's typical schedule from the past 4 weeks.
3.  **Layer 3 — Platform Activity Check**: Checks if the rider was online and accepting orders before the disruption started.
4.  **Layer 4 — Sensor Fusion**: Uses Accelerometer, Gyroscope, and Barometer data to detect if someone is faking movement.
5.  **Layer 5 — Network-Based Verification**: Uses IP address, Wi-Fi, and cellular tower data via Google's Geolocation API.
6.  **Layer 6 — Device Integrity Check**: Detects mock location apps and rooted or jailbroken devices.
7.  **Layer 7 — Physical Proof (High Risk)**: Requires a timestamped photo or scanning a location QR/NFC code for suspicious claims.
8.  **Layer 8 — AI Behavioral Tracking**: Analyzes speed, route consistency, stop times, and frequency of claims to detect sophisticated spoofing rings.

## Challenges we ran into
-   Building adaptive thresholds that adjust per city and season.
-   Designing strict but fair fraud detection.
-   Developing the hourly replacement payout model for various income levels.
-   Structuring a financially sustainable payout model for the insurer.
-   Catching subtle fraud (e.g., riders online with no intent to work).
-   Integrating multiple live data sources into a real-time decision engine.

## Accomplishments that we're proud of
-   Built a truly personalized insurance model.
-   Designed an eight-layer fraud detection system beyond just GPS.
-   Created the Distress Protection feature for psychological safety.
-   Structured the financial model around the gig worker's actual earning cycle.
-   Built adaptive thresholds that understand local weather baselines.

## What we learned
-   Parametric insurance is fundamentally about the trigger, not the claim.
-   Gig workers are not a single persona; coverage models must be diverse.
-   Fraud in income insurance is subtle and often involves inflated loss or wrong timing.
-   Adaptive thresholds are critical for fairness across different cities.
-   The hidden damage of weather on a rider's future earning potential (ratings) is a major pain point.

## What's next for GigShield
-   Expanding to food delivery riders on Zomato and Swiggy.
-   Partnering directly with Zepto and Blinkit for real-time earnings data sync.
-   Adding a rider reputation protection feature (disruption certificates for platforms).
-   Building predictive risk alerts to help riders plan their shifts.
-   Launching a micro-investment feature for unused weekly coverage.
-   Expanding adaptive thresholds to more Indian cities.
