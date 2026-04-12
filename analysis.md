# RTT vs. Speed-of-Light — Analysis

Itamar Dekel
4/11/2026
Boston, MA (42.3584, -71.0598)

## Question 1 — Which city has the highest inefficiency ratio?

Based on my measurements, London had the highest inefficiency ratio at approximately 3.26,3.30, 3.56 across multiple runs, despite being the closest city at only 5,264 km from Boston.
This is counterintuitive at first because London should appear to have the lowest inefficiency since it is geographically closest. However, the high ratio is explained by several factors:
HTTP and protocol overhead dominates short distances.
 At ~5,264 km, the theoretical minimum RTT is only ~52.6 ms. However, TCP handshakes, TLS negotiation, DNS resolution, and server processing time introduce fixed overhead that becomes disproportionately large at short distances. Since these costs are largely independent of distance, they inflate the inefficiency ratio more for nearby cities.
Submarine cable routing and physical infrastructure.
 According to submarinecablemap.com, the North Atlantic connection between Boston and London is supported by multiple major transatlantic submarine cable systems, including Hibernia Express, TAT-14, Apollo, and Transatlantic Express (TAE). While these cables provide high-capacity physical links across the Atlantic, real-world traffic still must traverse landing stations, terrestrial backbone networks, and multiple routing hops before reaching its destination.
CDN and routing decisions.
 Google's infrastructure may serve google.co.uk from regional edge locations or even non-UK data centers depending on load balancing, caching, and congestion conditions. As a result, traffic does not necessarily terminate in London itself, introducing additional latency unrelated to physical distance.
Overall, London’s high inefficiency ratio does not indicate poor infrastructure. Instead, it highlights a key limitation of the theoretical model: when distances are relatively small, fixed real-world overhead dominates the speed-of-light baseline, producing disproportionately high inefficiency ratios.


## Question 2 — Which city is closest to the theoretical minimum?

Sydney was closest to the theoretical minimum, with inefficiency ratios of 1.15, 1.03, 1.07, and 1.20 across runs, with one run being nearly ideal.

The theoretical minimum RTT from Boston to Sydney is about 162.4 ms, based on a great-circle distance of ~16,240 km. The measured median RTT ranged from 167.6–186.3 ms, which is very close to the physical limit given the long distance.

This result can be explained by several factors:

According to submarinecablemap.com, trans-Pacific connectivity uses modern submarine cables such as Southern Cross NEXT, Hawaiki, and the AJC cable system, which provide relatively direct high-capacity routes between the US and Australia.
Large distances reduce the impact of fixed overhead (DNS, TCP, TLS), since propagation delay dominates total RTT at this scale.
Google’s backbone and peering infrastructure help ensure efficient routing across long-haul paths, minimizing unnecessary detours.

Overall, Sydney is closest to the theoretical minimum because long-distance routes are dominated by physical propagation delay and benefit from well-optimized submarine cable infrastructure.

## Question 3 — Why does Africa route through Europe, and what would need to change?

Historically, African submarine cable infrastructure was built primarily to connect African countries to Europe rather than directly to other continents. As a result, a large portion of African internet traffic still routes through European hubs, even when this adds unnecessary distance and latency.

For Lagos specifically:

Major West African submarine cables such as ACE (Africa Coast to Europe), SAT-3/WASC, and MainOne primarily connect West Africa to Europe (e.g., Portugal, France, UK) rather than directly to the Americas.
As a result, traffic often follows a path like: Boston → US backbone → transatlantic cable → Europe → West African cable → Lagos.
There is limited direct submarine connectivity between West Africa and the US East Coast, so Europe acts as a default routing hub.

Why Lagos appears relatively efficient in my results:

Lagos showed a surprisingly low inefficiency ratio (~1.94–2.05). This is likely because my request was served by a nearby Google CDN edge location in or near West Africa, rather than traveling through the full Europe-based routing path. This reduces measured RTT and makes performance appear better than typical end-to-end internet routing would suggest.

What would need to change:

1.Direct transatlantic cables to West Africa.
New systems like Equiano (Google) and parts of 2Africa are steps toward improving direct connectivity between West Africa and global networks, reducing reliance on Europe.
2.Expanded intra-African connectivity.
More direct terrestrial and submarine links between African countries would reduce the need for traffic to leave the continent.
3.More Internet Exchange Points (IXPs).
Strengthening IXPs in cities like Lagos, Nairobi, and Johannesburg would keep regional traffic local instead of routing through Europe.
4.Greater CDN and data center distribution in Africa.
Expanding edge infrastructure would reduce latency for common services even before major cable expansion is complete.
