# RTT vs. Speed-of-Light — Analysis

Itamar Dekel
4/13/2026
Boston, MA (42.3584, -71.0598)

## Question 1 — Which city has the highest inefficiency ratio?

Across my runs, Sendai had the highest inefficiency ratio, ranging from 17.61 to 20.38. The theoretical minimum from Boston is ~104.9 ms, yet measured medians were consistently around 1,850–2,150 ms.
Two things explain this. First, the target is tohoku.ac.jp, a university server with no CDN, no caching, and slow response times compared to Google. Second, looking at submarinecablemap.com, Sendai is not a major cable landing point. Japan's main cable stations are concentrated around Tokyo and Osaka, so a packet going to Sendai lands there first, then travels inland over domestic network to reach the university. That extra hop, combined with slow server processing, drives the ratio sky high.
The pattern holds across all university targets: London (IC) scored ~9.10 and Canberra ~13.07, versus 5.75 and 1.85 for the Google versions of the same cities.


## Question 2 — Which city is closest to the theoretical minimum?

Sydney was the closest, with ratios of 1.78, 1.85, and 2.12 across runs. The speed-of-light minimum is ~162.4 ms and measured times were 288–345 ms, very close for a 16,240 km trip.
Two reasons. First, when the distance is this large, the travel time through the cable dominates everything else. Fixed costs like handshakes and DNS lookups become a tiny fraction of the total, so the ratio shrinks naturally. Second, according to submarinecablemap.com, trans-Pacific connectivity uses modern cables such as Southern Cross NEXT, Hawaiki, and the AJC cable system, which provide direct high-capacity routes between the US and Australia. Google's backbone also helps keep routing efficient across the long haul.

## Question 3 — Why does Africa route through Europe, and what would need to change?

The cables themselves go to Europe. According to submarinecablemap.com, major West African cables like ACE, SAT-3/WASC, and MainOne all connect West Africa to European landing points in Portugal, France, and the UK rather than directly to the Americas. So a packet from Boston to Lagos has to cross the Atlantic to Europe first, then travel back south to Nigeria, adding thousands of unnecessary kilometers.
My Lagos ratios of 2.57–3.58 are surprisingly low, probably because Google routes google.com.ng through a nearby edge server in West Africa rather than sending traffic the full Europe path, making performance look better than typical routing would suggest.
To fix this: direct cables between West Africa and the US are needed. New systems like Equiano (Google) and parts of 2Africa are steps toward this, reducing reliance on Europe. More internet exchange points inside Africa would keep regional traffic local instead of sending it abroad. And expanding data centers on the continent would mean packets do not need to leave Africa for common services even before major new cables are built
