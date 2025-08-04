# 🚀 Project Pitch Deck

## Project Title:

**Optimized Hybrid Satellite Internet Model for Low-Latency Rural Connectivity**

---

## 📈 Problem Statement

* Over 2.7 billion people lack reliable internet access, primarily in rural areas.
* Starlink provides LEO satellite coverage, but 1 terminal per household is costly and inefficient.
* Rural schools, hospitals, and villages often lack power, structured networking, or tech support.

---

## 🛍️ Target Users

* Rural Schools and Students
* Village Health Clinics
* NGOs and Disaster Response Units
* Local Governments in Developing Regions

---

## 🌐 Our Solution

> A **hybrid internet system** using a **single Starlink terminal** as backhaul, connected to a **local mesh distribution system** powered by outdoor Wi-Fi routers, solar backups, and optional edge caching.

---

## 🔌 Key Features

* **Starlink Gateway Node** for satellite uplink
* **Mesh Wi-Fi Distribution** using PoE-enabled routers
* **Local Edge Caching** to save bandwidth and reduce latency
* **Solar/Battery Power Support** for off-grid setups
* **Dashboard Monitoring Panel** for administrators

---

## 🌍 Deployment Flow

```
[Starlink Terminal] → [Mesh Gateway Router] → [Outdoor Mesh Nodes] → [User Devices]
```

---

## ⚡ Impact Metrics

| Metric         | Traditional Starlink         | Hybrid Model                  |
| -------------- | ---------------------------- | ----------------------------- |
| Cost per user  | \$599 hardware + \$120/month | \$25/user (shared terminal)   |
| Latency (avg)  | 40-60ms                      | 10-20ms locally + 40ms uplink |
| Power required | 100% AC grid                 | Hybrid (solar-ready)          |
| Uptime         | Limited in weather           | Resilient w/ edge failover    |

---

## 🚀 Competitive Advantage

* Utilizes existing Starlink hardware
* Scalable to 50-100 users per node
* Works in off-grid regions
* Compatible with government & NGO missions
* Highly cost-effective in the long term

---

## 💡 Strategic Opportunities

* Collaborate with governments on digital inclusion
* Partner with Starlink for community packages
* Integrate with school/hospital development programs
* Position as emergency connectivity solution (disaster recovery)

---

## 📊 Roadmap

| Phase   | Timeline   | Milestone                            |
| ------- | ---------- | ------------------------------------ |
| Phase 1 | 1 month    | Prototype in rural school            |
| Phase 2 | 2-3 months | Pilot in 2 villages & 1 clinic       |
| Phase 3 | 6 months   | Government & NGO partnership rollout |

---

## 💼 Team Requirements

* Networking Engineer
* Power Systems Advisor (solar/PoE)
* Rural Deployment Technician
* Frontend Dev (admin panel UI)
* Project Lead / NGO Liaison

---

## 💰 Funding & Support Needed

* \$3,000 for pilot deployment (routers, solar kits, edge device)
* Starlink hardware support (via partnership)
* Local logistics & training materials

---

## ✅ Final Slide: Why This Matters

> "We're not just delivering internet. We're delivering education, healthcare, and opportunity — with one satellite dish at a time."



### List of Possible Questions and Solutions

#### General Understanding and Context
1. **Question**: What is the main challenge Starlink faces in rural areas that your project addresses?
   - **Solution**: The main challenge is high latency, often 40–100 milliseconds in rural areas like Bangladesh, due to limited ground infrastructure and environmental factors like monsoons. Our project targets reducing this to under 25 milliseconds using a hybrid system with satellites, CDNs, and optimized ground stations.

2. **Question**: Why did you choose a hybrid approach instead of relying solely on satellites?
   - **Solution**: A hybrid approach combines LEO satellites’ low propagation latency (~7.33 ms) with terrestrial CDNs and ground stations to cache content and minimize terrestrial routing delays. This balances cost and performance, especially for rural areas with diverse needs like streaming and gaming.

3. **Question**: How does your project differ from Starlink’s current implementation?
   - **Solution**: Our project enhances Starlink by integrating CDNs at ground stations to serve cached content and prioritizing ground station density for all traffic types, aiming for consistent sub-25 ms latency, compared to Starlink’s current 25–60 ms global average.

#### Stakeholder and Requirement Analysis
4. **Question**: How did you identify the needs of rural users in your stakeholder analysis?
   - **Solution**: We considered rural users like farmers and students in areas like Bangladesh, who need low-latency internet for streaming, gaming, and communication. This was derived from understanding their daily reliance on real-time applications, informed by typical rural connectivity demands.

5. **Question**: What are the key needs of Starlink as a stakeholder, and how do they align with your design?
   - **Solution**: Starlink aims to grow its subscriber base and reduce churn. Our design supports this by offering a cost-effective, scalable hybrid system with low latency (< 25 ms), attracting more rural users and improving retention through reliable service.

6. **Question**: How do regulatory constraints impact your requirements?
   - **Solution**: Regulatory bodies like the BTRC in Bangladesh require licensing and spectrum compliance. This shapes our requirements by necessitating secure, localized infrastructure and ensuring the system adheres to national telecom policies, affecting ground station placement.

7. **Question**: Can you explain the difference between functional and non-functional requirements in your project?
   - **Solution**: Functional requirements define what the system does—e.g., transmitting data with < 25 ms latency and caching content at CDNs. Non-functional requirements specify how it performs—e.g., 99.9% uptime and scalability for 1,000+ users—ensuring reliability and efficiency.

#### Technical Details and Design Choices
8. **Question**: Why is a latency of under 25 milliseconds your target, and is it achievable?
   - **Solution**: A < 25 ms target supports real-time applications like gaming, aligning with user needs. It’s achievable with LEO satellites (~7.33 ms propagation) plus optimized ground stations and CDNs, as seen in U.S. data reaching 25.7 ms, with further improvements possible.

9. **Question**: How does the CDN placement at ground stations reduce latency?
   - **Solution**: CDNs at ground stations cache content like videos, serving it directly and avoiding long terrestrial routes (e.g., saving 20–50 ms). This can reduce latency to 17–25 ms for cached data, complementing satellite efficiency.

10. **Question**: What role do inter-satellite laser links play in your design?
    - **Solution**: ISLLs enable direct satellite-to-satellite data transfer, reducing reliance on ground stations for long distances. This can cut latency by up to 50% on international routes, enhancing performance in rural areas with sparse infrastructure.

11. **Question**: How do you handle dynamic content that CDNs can’t cache?
    - **Solution**: For dynamic content like gaming or video calls, we rely on increased ground station density to minimize terrestrial routing latency to 25–35 ms, ensuring consistent performance across all use cases.

12. **Question**: What are the technical limits you considered in your requirements?
    - **Solution**: We accounted for the minimum 7.33 ms propagation time for 550 km LEO satellites and CDN limitations to cacheable content. These set a baseline, with additional delays from weather or routing addressed through optimization.

#### Feasibility and Constraints
13. **Question**: Is your proposed system feasible given rural infrastructure limitations?
    - **Solution**: Yes, by leveraging existing Starlink satellites and placing CDNs at feasible PoPs, we can work within limited fiber connectivity. Ground station expansion, though costly, is viable with phased deployment based on demand.

14. **Question**: How do you address the high cost of ground stations in your design?
    - **Solution**: We prioritize CDNs ($50K–$100K per site) for initial cost-effectiveness, supplementing with selective ground station growth ($1–2M) where user density justifies it, balancing short-term savings with long-term scalability.

15. **Question**: How will monsoons in rural areas like Bangladesh affect your system?
    - **Solution**: Monsoons can increase latency by 10–20 ms due to signal degradation. Our design includes 99.9% uptime requirements and weather-resilient hardware, with CDNs mitigating some impact by serving cached content locally.

16. **Question**: What trade-offs did you consider between CDNs and ground stations?
    - **Solution**: CDNs are cheaper and effective for cached content (17–25 ms latency) but limited to specific use cases. Ground stations, though costlier, reduce latency for all traffic (25–35 ms) and improve reliability, making them essential for comprehensive rural coverage.

#### Data Flow and Visualization
17. **Question**: Can you walk us through the data flow diagram and explain each step?
    - **Solution**: Sure! Data starts at the user device, goes to the Starlink dish, then to a satellite. From there, it can use an optional ISLL to the internet or reach a ground station. The ground station’s PoP with a CDN serves cached content, reducing latency to 17–25 ms, while dynamic content routes through the internet.

18. **Question**: Why did you place the CDN at the ground station rather than elsewhere?
    - **Solution**: Placing the CDN at the ground station leverages existing high-speed fiber connections and proximity to satellites, minimizing terrestrial delays to 5–10 ms and enabling 17–25 ms latency for cached content, which is optimal for rural efficiency.

19. **Question**: How does your data flow handle peak traffic loads?
    - **Solution**: The hybrid system uses CDNs to offload cached content during peaks, while additional ground stations and ISLLs distribute dynamic traffic. This ensures latency stays below 25 ms for cached data and 35 ms for dynamic, meeting scalability goals.

#### Presentation and Next Steps
20. **Question**: What’s the next step after this requirement analysis?
    - **Solution**: The next SDLC phase is system design, where we’ll detail CDN and ground station integration, followed by prototyping and testing in rural environments to validate the < 25 ms latency target.

21. **Question**: How will you measure the success of your system?
    - **Solution**: Success will be measured by achieving median latency < 25 ms, a 70%+ CDN cache hit ratio, and 99.9% uptime during testing in rural areas, aligning with our non-functional requirements.

22. **Question**: Can you justify the rural focus of your project?
    - **Solution**: Rural areas like Bangladesh lack reliable internet, with high latency hindering growth. Our system addresses this gap, improving connectivity for education, business, and communication, making it a critical use case.

### Preparation Tips
- **Practice Answers**: Rehearse these responses aloud, keeping them concise (1–2 minutes each) to fit your 5–7 minute slot starting at 09:53 AM +06 today.
- **Anticipate Follow-Ups**: Be ready for deeper questions (e.g., “How will you test latency?”—answer with real-world trials using Starlink’s data collection methods).
- **Visual Support**: Refer to your slides (e.g., Slide 9 for data flow) to reinforce answers visually.
- **Confidence**: If unsure, acknowledge it (e.g., “I’ll research that further”) and pivot to a related point you know.

This list covers a broad range of questions your teacher might ask, from theoretical to practical, ensuring you’re well-prepared for your presentation. Good luck at 09:53 AM +06 on July 30, 2025! Let me know if you need help refining any answers!
