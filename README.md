# GigaGuard: Automated Income Protection for Food Delivery Partners

## Inspiration
India’s platform-based delivery partners (working for platforms like Zomato and Swiggy) are the backbone of our fast-paced digital economy. However, they are highly vulnerable to external disruptions. When heavy monsoon rains flood the streets or extreme summer heatwaves strike, these workers are forced to halt deliveries, causing them to lose 20-30% of their monthly earnings. Currently, they bear this full financial loss with absolutely no safety net. We were inspired to build a system that finally offers them automated, hassle-free protection for the hours they can't work.

## What it does
GigaGuard is an AI-enabled parametric insurance platform built specifically for food delivery gig workers. It strictly safeguards against **loss of income** caused by environmental or social disruptions.

Crucially, it is structured entirely around a **weekly pricing model**, perfectly matching the typical payout cycle of a gig worker. If a disruption hits, the platform uses real-time triggers to instantly process payouts for the lost wages—no manual claims, no lengthy paperwork. We strictly excluded coverage for health, life, accidents, or vehicle repairs, focusing 100% on keeping their weekly income stable.

## How we built it
We architected the platform using a mobile-first approach to optimize onboarding for the delivery persona. Local development and early model testing were orchestrated on macOS environments before pushing to the cloud. Our core engine relies on three main pillars:

* **AI-Powered Risk Assessment:** We implemented predictive risk modeling to calculate dynamic weekly premiums. 
_Technical note:_ Our dynamic weekly premium ($P_{weekly}$) is calculated using a base rate adjusted by AI-derived local risk coefficients:
$$P_{weekly} = P_{base} \times (1 + \alpha_{weather} + \beta_{zone})$$

* **Intelligent Fraud Detection:** To ensure platform integrity, we integrated anomaly detection for claims. To validate location and activity, we explored advanced computer vision techniques, specifically assessing the viability of lightweight YOLO models to process visual proof of zone closures or severe weather conditions at the edge, preventing duplicate or spoofed claims.

* **Parametric Automation:** We hooked into external APIs to create real-time trigger monitoring. When an API confirms a severe rainstorm in a worker's active zone, it triggers an automatic claim initiation.

**Deployment Architecture:**
* **Frontend:** React Native via Expo.
* **Serverless Backend:** AWS Lambda, Amazon API Gateway, running Python and FastAPI.
* **Automation:** Amazon EventBridge for scheduled cron jobs to check external APIs.
* **Database:** Amazon RDS for PostgreSQL.

## Challenges we ran into
One of the biggest challenges was shifting our mindset away from traditional insurance. Ensuring the financial model was structured on a **Weekly basis** required rethinking how premiums are calculated. Additionally, building a robust fraud detection mechanism that accurately validates a worker's activity without relying on intrusive tracking took significant effort. Ensuring the UI felt seamless for a user constantly on the move was a major design hurdle.

## Accomplishments that we're proud of
We are incredibly proud of our dynamic pricing model, which uses machine learning to adjust the weekly premium based on hyper-local risk factors. We also successfully built a simulated instant payout system that demonstrates how a worker receives their lost wages seamlessly via mock payment gateways.

## What we learned
We learned a massive amount about the gig economy's financial realities. We realized that traditional yearly insurance policies are completely incompatible with workers who operate week-to-week. We also learned how to effectively implement parametric triggers—moving from "assessing damage" to "verifying an event"—which completely changes the speed at which help can be delivered.

## What's next for GigaGuard
Currently, we simulate our payouts and platform APIs. Next, we want to integrate real-world payment systems to finalize the instant payout loop. We also plan to expand our intelligent dashboard for insurers to include deeper predictive analytics on the next week's likely weather disruptions, optimizing their loss ratios.
