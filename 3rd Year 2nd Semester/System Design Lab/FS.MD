

# Latency Calculation with and without CDN


---

## Assumptions

* **LEO Satellite Propagation Delay**: 7.33 ms round-trip (550 km altitude, calculated using speed of light).
* **Terrestrial Routing Delay (Without CDN)**: 10–20 ms (average 15 ms) for 500–1,000 km fiber routing.
* **CDN Latency Reduction**: 5–10 ms (average 7.5 ms) from a local Point of Presence (PoP).
* **Handover Delay**: 2–5 ms (average 3.5 ms) due to satellite switches.
* **Weather Impact**: 10–15 ms (average 12.5 ms), mitigated to 1.25 ms with resilient hardware.

---

## Latency Without CDN

The total latency without CDN includes satellite propagation, terrestrial routing, handover delays, and weather impacts.




$$
T_{\text{total without CDN}} = T_{\text{satellite}} + T_{\text{terrestrial}} + T_{\text{handover}} + T_{\text{weather}}
$$

---



### Satellite Propagation Delay (T<sub>satellite</sub>)

$$
T_{\text{satellite}} = \frac{2 \cdot d}{c}
= \frac{2 \cdot 550 \times 10^3}{3 \times 10^8} \approx 7.33 \, \text{ms}
$$

### Terrestrial Routing Delay (T<sub>terrestrial</sub>)

$$
T_{\text{terrestrial}} = \frac{2 \cdot d_{\text{fiber}}}{v} \cdot k
$$

Where:

* $d_{\text{fiber}} = 500–1000 \, \text{km} = 5 \times 10^5 – 1 \times 10^6 \, \text{m}$
* $v = 2 \times 10^8 \, \text{m/s}$
* $k = 2$ (routing overhead)

Results:

* Min: $10 \, \text{ms}$
* Max: $20 \, \text{ms}$
* **Average**: $15 \, \text{ms}$

### Handover Delay (T<sub>handover</sub>)

$$
T_{\text{handover}} = 3.5 \, \text{ms}
$$

### Weather Impact (T<sub>weather</sub>)

$$
T_{\text{weather}} = 12.5 \, \text{ms}
$$

### Total Latency Without CDN

$$
T_{\text{total without CDN}} = 7.33 + 15 + 3.5 + 12.5 = \boxed{38.33 \, \text{ms}}
$$

---

## Latency With CDN

In this case, most terrestrial routing is replaced with local PoP access via CDN.


$$
T_{\text{total with CDN}} = T_{\text{satellite}} + T_{\text{CDN}} + T_{\text{handover}} + T_{\text{weather (mitigated)}}
$$




### Satellite Propagation Delay (T<sub>satellite</sub>)

$$
T_{\text{satellite}} = 7.33 \, \text{ms}
$$

### CDN Delay (T<sub>CDN</sub>)

$$
T_{\text{CDN}} = \frac{2 \cdot d_{\text{PoP}}}{v}
$$

Where:

* $d_{\text{PoP}} = 50–100 \, \text{km} = 5 \times 10^4 – 1 \times 10^5 \, \text{m}$
* $v = 2 \times 10^8 \, \text{m/s}$

Results:

* Raw delay: 0.5–1 ms
* With caching/processing: **5–10 ms**, **average: 7.5 ms**

### Handover Delay (T<sub>handover</sub>)

$$
T_{\text{handover}} = 3.5 \, \text{ms}
$$

### Weather Impact (T<sub>weather (mitigated)</sub>)

$$
T_{\text{weather (mitigated)}} = 12.5 \cdot 0.1 = \boxed{1.25 \, \text{ms}}
$$

### Total Latency With CDN

$$
T_{\text{total with CDN}} = 7.33 + 7.5 + 3.5 + 1.25 = \boxed{19.58 \, \text{ms}}
$$

---

## Latency Difference

$$
\Delta T = 38.33 \, \text{ms} - 19.58 \, \text{ms} = \boxed{18.75 \, \text{ms}}
$$

---

## Real-Life Comparison (18.75 ms Difference)

* **Human Reaction Time**: 7.5–9.4% of 200–250 ms; improves response in games like *PUBG Mobile*.
* **Video Streaming**: Saves \~1.1 s over a 10-min YouTube video (0.625–1.875% of 1–3 s buffering).
* **Real-Time Communication**:

  * From 38.33 ms (slight echo)
  * To 19.58 ms (crisp Zoom calls)
  * Enhances remote learning in rural areas.

---


Slide 1: Title Slide
Feasibility Study: Optimized Hybrid Satellite Internet System

Presented by: [Your Name]
Course: System Design Lab
Date: August 1, 2025
Objective: Assess viability using Traffic Light Approach

Explanation: Introduces the feasibility study with the traffic light method.

Slide 2: Project Recap and Traffic Light Context
Recap and Context

Project Goal: < 25 ms latency with hybrid system (satellites, CDNs, ground stations).
Traffic Light Approach:
Green: Low risk.
Yellow: Moderate risk, needs monitoring.
Red: High risk, requires action.


Focus: Rural connectivity (e.g., Bangladesh).

Explanation: Recaps the project and introduces the traffic light evaluation method.

Slide 3: Technical Feasibility
Technical Feasibility

Status: Green
Details:
LEO satellites: ~7.33 ms propagation (proven).
CDNs at PoPs: Feasible with existing tech.
ISLLs: Operational in newer satellites.


Risks:
Yellow: Limited rural fiber, weather impacts (monsoons).


Mitigation: Weather-resilient hardware, phased fiber upgrades.

Explanation: Assesses technical viability, using green for core tech and yellow for rural challenges.

Slide 4: Economic Feasibility
Economic Feasibility

Status: Yellow
Details:
CDN: $50K–$100K per site (low cost).
Ground Stations: $1–2M per site (high cost).
ROI: Long-term gains with subscriber growth.


Risks:
Yellow: High initial investment for ground stations.


Mitigation: Phased deployment, prioritize CDNs initially.

Explanation: Marks economic feasibility as yellow due to costs, with mitigation strategies.

Slide 5: Operational Feasibility
Operational Feasibility

Status: Yellow
Details:
User adoption: Benefits (gaming, streaming) drive interest.
Maintenance: Requires local support in rural areas.


Risks:
Yellow: Training needs, sparse support infrastructure.


Mitigation: Community education, ISP partnerships.

Explanation: Indicates moderate risk due to operational challenges in rural settings.

Slide 6: Legal Feasibility
Legal Feasibility

Status: Green
Details:
BTRC licensing achievable.
Encryption meets privacy laws.


Risks:
None significant.


Mitigation: Ongoing regulatory liaison.

Explanation: Confirms legal feasibility with low risk, given compliance measures.

Slide 7: Schedule Feasibility
Schedule Feasibility

Status: Green
Details:
Timeline: 12 months (design 2–3, prototyping 4–6, testing 3–4).
Based on SpaceX’s rapid deployment.


Risks:
Yellow: Ground station delays possible.


Mitigation: Prioritize CDN rollout, stagger station builds.

Explanation: Sets a green baseline with a yellow caution for delays.

Slide 8: Feasibility Conclusion and Next Steps
Conclusion and Next Steps

Overall Status: Green (with yellow areas manageable).
Recommendations:
Phase 1: CDN deployment (low cost, quick impact).
Phase 2: Ground station expansion.


Next SDLC Phase: System design and prototyping.
Traffic Light Summary:
Technical: Green/Yellow
Economic: Yellow
Operational: Yellow
Legal: Green
Schedule: Green/Yellow



Explanation: Summarizes the traffic light assessment and outlines the next steps.

Slide 9: References
References

SpaceX Starlink Updates, July 2025.
Ookla Speedtest Reports, Q3 2023–Q1 2024.
Bangladesh Telecommunication Regulatory Commission Guidelines.
Starlink Availability Map: starlink.com/map

Explanation: Credits sources for credibility.