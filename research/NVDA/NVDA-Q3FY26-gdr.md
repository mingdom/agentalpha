Institutional Equity Research: NVIDIA Corp (NVDA) – The Blackwell Transition and the Geopolitical Compute Arbitrage

Date: November 18, 2025
Subject: Fiscal Q3 2026 Earnings Preview, Strategic Architecture Analysis, and Sovereign AI Market Dynamics
Ticker: NASDAQ: NVDA
Rating: OVERWEIGHT
Price Target: Under Review due to volatility in Sovereign AI premiums

1. Executive Summary: The Structural Discontinuity of the AI Cycle

As NVIDIA Corporation approaches its Fiscal Q3 2026 earnings release on November 19, 2025, the semiconductor industry sits at a precarious yet transformative juncture. The prevailing market narrative is dominated by anxieties regarding the "law of large numbers" and the potential for a "capital expenditure air pocket" following two years of frenetic investment by hyperscalers. However, a rigorous forensic analysis of the supply chain, architectural shifts, and emerging geopolitical demand vectors suggests that the market is misinterpreting a structural discontinuity as a cyclical peak. The transition from the Hopper (H100/H200) architecture to the Blackwell (B200/GB200) platform represents not merely a performance upgrade, but a fundamental change in the unit of compute—from the individual chip to the rack-scale supercomputer. This shift fundamentally alters the revenue density, competitive moat, and total addressable market (TAM) for NVIDIA, effectively decoupling its fortunes from the immediate monetization struggles of consumer generative AI applications.
The consensus estimates for Q3 FY26 revenue oscillate between $54 billion and $57 billion 1, a figure that implies continued sequential growth despite the massive base established in FY25. While the "easy growth" characterizing the initial H100 shortage is concluding, a new phase of "hard growth" is emerging, driven by three distinct but accumulating factors: the necessary replacement cycle driven by power-efficiency arbitrage, the rise of "Sovereign AI" as a mechanism for nation-states to secure computational independence, and the intricate "gray market" routing of compute to restricted jurisdictions via regulatory arbitrage.
This report argues that the skepticism surrounding the immediate Return on Investment (ROI) for AI is valid but ultimately irrelevant to near-term hardware demand. The "Big Four" hyperscalers—Amazon, Microsoft, Meta, and Alphabet—are locked in a classic Prisoner's Dilemma where the cost of under-investing (existential obsolescence) vastly outweighs the cost of over-investing (capital depreciation). Furthermore, the "double monetization" dynamic unique to players like Amazon—where AI improves internal retail margins while simultaneously driving external AWS revenue—provides a capital buffer that pure-play skeptics fail to appreciate.2
The following analysis provides an exhaustive breakdown of the Blackwell technical ecosystem, the evolving geopolitical supply chain involving Indonesia and the UAE, and the granular financial mechanics of the Q3 FY26 print, projecting a complex but robust pathway through fiscal year 2027.

2. The Blackwell Architecture: Physics, Economics, and the Rack-Scale Pivot

To understand the durability of NVIDIA's revenue trajectory, one must dissect the product catalyzing the next wave of spending: the Blackwell B200 and the GB200 NVL72 system. The market frequently treats Blackwell as a linear extrapolation of the Hopper architecture. This is a category error. Blackwell represents a discontinuity in data center physics that enforces a "rip-and-replace" cycle faster than traditional server amortization schedules would typically dictate.

2.1 The "30x" Inference Claim vs. Silicon Reality

NVIDIA’s marketing literature prominently claims a "30x" performance increase for inference tasks compared to the H100.3 A technical audit of the MLPerf v5.1 benchmarks and architectural whitepapers reveals that this figure is not derived solely from raw transistor scaling, but from a radical shift in numerical precision standards. The B200 introduces native support for FP4 (4-bit floating point) precision, whereas the H100 peaked at FP8.3
In raw dense compute terms, the B200 delivers approximately 2.5x the TFLOPS of the H100 at equivalent precision (FP16/BF16).5 However, the shift to FP4 effectively doubles the memory bandwidth and capacity per parameter, allowing massive trillion-parameter models—which previously required multi-node H100 clusters—to run on smaller, more energy-efficient Blackwell footprints.4 This creates a deflationary force on the "cost per token," which paradoxically drives elasticity of demand. As the cost of inference collapses, the volume of tokens generated is expected to expand non-linearly, absorbing the increased supply.
Table 1: Architectural Discontinuity – Hopper vs. Blackwell

Feature
H100 (Hopper)
B200 (Blackwell)
GB200 NVL72 (Rack-Scale)
Strategic Implication
Process Node
TSMC 4N
TSMC 4NP (Two Reticle Limit)
N/A
Yield Risk: Dual-die design increases packaging complexity & CoWoS reliance.8
Memory Capacity
80GB HBM3
192GB HBM3e
13.5 TB HBM3e
Batch Scaling: 2.4x memory per chip allows larger batch sizes, improving throughput.3
Memory Bandwidth
3.35 TB/s
8.0 TB/s
576 TB/s (Aggregate)
Bottleneck Removal: Solves the "memory wall" for large language models.4
Precision Support
FP8, FP16
FP4, FP6, FP8
FP4
Efficiency: FP4 enables the "30x" claim by reducing data movement by 50% vs FP8.4
Interconnect
NVLink 4 (900 GB/s)
NVLink 5 (1.8 TB/s)
130 TB/s (Bi-sectional)
Coherence: Allows 72 GPUs to function as a single logic unit.4
Thermal Design (TDP)
700 W (Air)
1,000 W+ (Liquid Preferred)
~120 kW per Rack
Infrastructure Lock-in: Forces data centers to upgrade to liquid cooling.4


2.2 The Economics of the NVL72 Rack

The most profound shift in FY26/27 is the transition from selling components (GPUs) to selling systems (NVL72). In the Hopper generation, NVIDIA captured value primarily through the GPU and the HGX baseboard. With the GB200 NVL72, NVIDIA captures the value of the Compute (72 GPUs), the Host Processing (36 Grace CPUs), the Networking (NVLink Switches), and the Interconnect (Copper Backplane).4
Analysts estimate the price of a single H100 at approximately $30,000 to $40,000, while a full GB200 NVL72 rack is estimated to command between $3 million and $3.5 million.10 This 100x increase in unit transaction value fundamentally alters NVIDIA's revenue density. Even if unit volumes of racks are lower than individual GPU cards, the accretion to revenue is massive.
However, this introduces "binary" execution risks. The installation of an NVL72 system is not a "drop-in" upgrade. It requires liquid cooling infrastructure capable of handling densities exceeding 100kW per rack, a specification that few legacy data centers meet.4 This creates a bifurcation in the market: greenfield AI factories can deploy Blackwell immediately, while brownfield data centers face significant retrofit delays. This physical constraint—power density and cooling—is likely the true governor of Blackwell revenue recognition in the short term, rather than silicon supply.

2.3 TCO: The Inflationary Hedge

Despite the high initial capital outlay, the Total Cost of Ownership (TCO) argument for Blackwell is compelling for hyperscalers. Third-party benchmarks indicate that self-hosted B200 infrastructure can offer OpEx savings of 6x-30x compared to renting legacy H100 capacity in the cloud, driven by energy efficiency and throughput density.14
For training workloads, the B200 has demonstrated speeds up to 57% faster than the H100 on specific computer vision tasks.14 This efficiency gain essentially mandates a refresh cycle. Hyperscalers cannot afford to run H100 fleets if a competitor operating B200 fleets can produce intelligence at half the electrical cost. Thus, Blackwell demand is supported by an "efficiency floor" even if top-line AI revenue growth for the hyperscalers temporarily decelerates.

3. Hyperscale Capital Expenditure: The Prisoner's Dilemma and Double Monetization

The sustainability of NVIDIA’s $50 billion+ quarterly revenue run rate is inextricably linked to the capital expenditure plans of the "Big Four"—Amazon, Microsoft, Meta, and Alphabet. The analysis of their 2025 outlooks reveals a decoupling of capex from immediate revenue, driven by competitive paranoia and internal efficiency gains.

3.1 The $300 Billion Wall

Combined estimates suggest these four entities will spend over $300 billion in 2025, with the vast majority allocated to AI infrastructure.16 This spending is not uniform; it is characterized by distinct strategic imperatives for each player.
Amazon (AMZN): Amazon is projected to spend over $100 billion in capex in 2025, with CEO Andy Jassy explicitly stating that the "vast majority" is earmarked for AWS AI infrastructure.17 Unlike its peers, Amazon benefits from a "Double Monetization" dynamic. Investments in AI infrastructure drive external revenue via AWS, but they simultaneously drive internal margin expansion in the low-margin retail business through improved inventory forecasting, robotics optimization, and ad targeting.2 This internal utility effectively subsidizes the cost of the infrastructure, allowing Amazon to be more aggressive than peers who rely solely on external cloud revenue. Jassy has also noted that AWS is currently "supply constrained," implying that demand for AI chips exceeds their ability to deploy them.18
Microsoft (MSFT): CFO Amy Hood confirmed a record $30 billion spend in Q1 FY26 alone, with guidance for continued increases.19 Hood has emphasized that approximately half of this capex is for long-lived assets (land, building shells) which will support capacity for the next 15 years, while the other half is for servers (CPUs/GPUs).20 This distinction is crucial; it signals that Microsoft is building the physical shell capacity to house massive Blackwell clusters as soon as they are available.
Meta Platforms (META): CEO Mark Zuckerberg has outlined a $66 billion to $72 billion capex range for 2025.21 Meta is unique in that it does not have a public cloud business to amortize these costs. Instead, Zuckerberg views the development of "Meta Superintelligence" as an existential necessity to maintain engagement dominance in an era where AI-generated content may supersede user-generated content.22
Alphabet (GOOGL): Alphabet reported nearly $40 billion in capex for the first half of 2025.19 Ruth Porat, CFO, has reiterated that the risk of "under-investing is dramatically greater than the risk of over-investing".24 This commentary underscores the "Prisoner's Dilemma"—no firm can afford to blink first.

3.2 The Digestion Myth vs. Reality

A pervasive fear among investors is the "digestion" phase—a period where hyperscalers pause ordering to optimize existing capacity. While this is a historical pattern in semiconductor cycles, current utilization rates suggest otherwise. AWS CEO Andy Jassy’s comment that "people aren't showing up for 30,000 chips in a day" but rather that demand is fluid and massive suggests a backlog that insulates NVIDIA from a short-term pause.18 Furthermore, the shift to agentic AI (which requires significantly more inference compute per interaction than simple chatbots) creates a new layer of demand that legacy H100 clusters are ill-equipped to handle efficiently.25

4. Supply Chain Labyrinth: The HBM3e and CoWoS Bottlenecks

NVIDIA's ability to meet the consensus revenue targets relies heavily on the High Bandwidth Memory (HBM) and advanced packaging supply chains. The Blackwell architecture is performance-bound by HBM3e, and yield stability in this component is the primary variable for Q3/Q4 margin performance.

4.1 The SK Hynix vs. Samsung Dynamic

SK Hynix has established itself as the premier partner, holding a commanding 62% market share in HBM as of mid-2025.26 Their proprietary "Vertical Wire Fan-Out" (VFO) technology has allowed them to stack 16 layers of DRAM, a critical capability for the memory-dense Blackwell Ultra SKUs.27 They remain the supplier of choice for NVIDIA's highest-margin products.
However, the critical unlock for volume lies with Samsung. Reports indicate that Samsung has finally passed NVIDIA's 12-layer HBM3e qualification and is aggressively cutting prices to capture market share.26 While Samsung has struggled with yields compared to SK Hynix 29, their entry into the supply chain is a deflationary event for NVIDIA's Cost of Goods Sold (COGS). If Samsung can stabilize production, it provides NVIDIA with leverage to negotiate pricing with SK Hynix and Micron, potentially aiding gross margin recovery in late FY26.

4.2 The CoWoS Ceiling

While memory supply is loosening, Chip-on-Wafer-on-Substrate (CoWoS) capacity at TSMC remains the ultimate constraint. The Blackwell B200 utilizes a dual-reticle design, meaning it consumes twice the silicon area and significantly more complex packaging than the monolithic H100.8 This implies that even if HBM supply becomes abundant, unit volume growth is capped by TSMC’s packaging lines. This physical constraint acts as a floor for pricing; scarcity ensures that NVIDIA can maintain its premium pricing structure for the B200 and GB200 systems throughout FY26.

5. Geopolitical Arbitrage: The Mechanics of Sovereign AI

Perhaps the most underappreciated driver of NVIDIA's resilience is the rise of "Sovereign AI"—the drive by nations to own their own data and compute infrastructure. This trend not only opens new markets but has also birthed complex mechanisms to circumvent US export restrictions, particularly regarding China.

5.1 The Indonesia Loophole: Regulatory Arbitrage in Action

Investigative reports have uncovered a sophisticated "compute-as-a-service" arbitrage involving Indonesia. NVIDIA has reportedly sold substantial volumes of Blackwell GPUs to Indosat Ooredoo Hutchison, an Indonesian telecom provider.30 The deal was brokered by Aivres, a Silicon Valley-based server manufacturer. Crucially, Aivres is a subsidiary of a parent company that is one-third owned by Inspur, a Chinese tech giant currently on the US trade blacklist.32
The mechanism works as follows:
NVIDIA sells chips to the US-based subsidiary (Aivres), compliant with domestic laws.
Aivres integrates these into racks and ships them to Indosat in Indonesia.
Indosat leases the compute capacity to INF Tech, a Shanghai-based AI startup, effectively allowing Chinese entities to access Blackwell-class compute without the physical hardware entering China.30
This "Indonesian Backdoor" allows NVIDIA to effectively monetize Chinese demand while adhering to the letter of US export controls. It suggests that the "China revenue hole" (the drop from 25% of revenue to near-zero) is being backfilled by "Rest of World" revenue that is functionally funded by Chinese capital.

5.2 The UAE and G42: The Stargate Project

The Middle East represents another massive vector. The UAE’s G42 group, despite intense scrutiny, has partnered with Microsoft and NVIDIA to build the "Stargate" project—a massive AI infrastructure initiative.33 While initial chip exports were blocked, recent approvals indicate a thawing, with Microsoft acting as the guarantor of compliance.34 The sheer scale of capital available in the region (petrodollars converting to digital infrastructure) creates a price-insensitive buyer class that competes with Western hyperscalers, keeping ASPs elevated.

5.3 Japan’s Strategic Subsidies: AI-RAN

In Japan, the demand is state-sponsored and transparent. SoftBank, utilizing subsidies from the Ministry of Economy, Trade and Industry (METI), is deploying NVIDIA’s DGX B200 systems to build a sovereign AI grid.36 This initiative is linked to "AI-RAN" (Artificial Intelligence Radio Access Network), a convergence of 5G/6G telecom infrastructure and AI compute. By embedding AI compute directly into telecom base stations, SoftBank aims to create a distributed inference network that covers the entire archipelago. Additionally, RIKEN is integrating thousands of Blackwell GPUs into supercomputers for scientific research (drug discovery, climate modeling), further cementing NVIDIA's role as critical national infrastructure.37

6. Competitive Landscape: The Encroaching Moat

While NVIDIA retains dominance, the competitive vacuum is filling. The Q3 FY26 analysis must account for the rising competence of AMD and the looming threat of vertical silicon.

6.1 AMD’s Memory Play: MI325X and MI355X

AMD continues to execute on its roadmap, positioning the Instinct MI325X and the upcoming MI355X as memory-rich alternatives to Blackwell. The MI325X boasts 288GB of HBM3e, significantly higher than the standard B200’s 192GB.38 For memory-bound inference workloads (like serving Llama 3 405B), this extra capacity can offer TCO advantages. AMD claims the MI355X offers 40% better "tokens-per-dollar" performance compared to the H200.39
Furthermore, Oracle’s announcement that it will deploy a supercluster of 50,000 AMD MI450 GPUs in 2026 signals that major hyperscalers are actively cultivating a second source to keep NVIDIA’s pricing in check.40 However, NVIDIA’s defense remains the NVL72 rack. While AMD is developing its "Helios" rack standard 11, it lacks the mature, proprietary networking stack (NVLink 5) that allows 72 GPUs to function as a single domain. Until AMD can replicate the rack-scale coherence of the GB200, it will likely be relegated to "commodity" inference tiers rather than frontier model training.

6.2 The Hyperscale ASIC Threat

A more potent long-term threat comes from within. Amazon’s Trainium2 and Google’s TPU v6 are maturing rapidly. Amazon is deploying clusters of hundreds of thousands of Trainium2 chips.17 While NVIDIA GPUs remain the general-purpose "gold standard" for training, hyperscalers have a strong financial incentive to offload internal, predictable workloads (like Alexa or Search) to their own optimized silicon. This imposes a "pricing ceiling" on NVIDIA; if the Blackwell premium becomes too high, the ROI calculation for custom silicon becomes undeniable.

7. Fiscal Q3 2026 Financial Preview and Modeling

Revenue Outlook:
Consensus estimates for Q3 FY26 revenue range from $54 billion to $57 billion.1 We project NVIDIA will report at the upper end of this range ($56.5 billion), driven by:
H200 Sustained Demand: The H200 is effectively bridging the gap to Blackwell, with strong uptake due to its memory upgrade over the H100.41
Sovereign AI Shipments: Revenue recognition from the initial waves of Japan and Middle East deployments.
Gross Margin Dynamics:
Consensus expects gross margins between 73.5% and 75.0%.42 We model a slight contraction toward the 72.5% - 73.0% range.
Reasoning: The ramp of Blackwell introduces initial yield inefficiencies (the "learning curve" cost). Furthermore, the shift to rack-scale systems (NVL72) introduces a mix-shift dilemma. A rack includes metal, piping, and other non-silicon components which typically carry lower margins than pure GPU silicon. As revenue from systems grows, gross margin percentage may structurally tick down, even as gross profit dollars explode.
The Q2 Tax Anomaly & Cash Flow:
Investors must contextualize the cash flow metrics. Q2 FY26 saw an $8.1 billion tax payment that artificially depressed operating cash flow.43 This was a discrete event. We anticipate Q3 Free Cash Flow (FCF) to rebound aggressively, likely exceeding $22 billion for the quarter. This massive liquidity injection supports the newly authorized $60 billion share repurchase program (updated from $50 billion) 44, providing a strong floor for the stock price.
OpEx and R&D:
Operating expenses are forecast to grow in the mid-30% range.47 This is necessary to support the accelerated roadmap (Rubin architecture in 2026) and the expansion of the CUDA software ecosystem. Given the revenue growth rate, this OpEx expansion is well-controlled and demonstrates operating leverage.
Table 2: Fiscal Q3 2026 Forecast
Metric
Consensus Est.
Our Forecast
YoY Growth
Rationale
Revenue
~$55.0B
$56.5B
+88%
Better-than-expected H200 tail & Sovereign AI.
Gross Margin
74.5%
73.2%
-190 bps
Product mix shift (Systems) & Blackwell yield ramp.
Data Center Rev
~$48.0B
$49.8B
+96%
Networking revenue (NVLink switches) upside.
EPS (Non-GAAP)
$1.17
$1.24
+85%
Strong operating leverage despite tax/OpEx.


8. Scenario Analysis & Risk Assessment


8.1 The "Air Pocket" Risk (Bear Case)

There is a tangible risk of a revenue "air pocket" in late Q3/early Q4 FY26. If customers decide to pause H100/H200 orders to wait for the superior Blackwell TCO, and Blackwell volume is simultaneously constrained by CoWoS or HBM3e yields 29, revenue could temporarily flatten. However, the robust demand for H200 (due to memory constraints on older models) appears to be successfully bridging this gap.

8.2 The "China Loophole" Closure (Tail Risk)

The "Indonesian Backdoor" 30 represents a regulatory fragility. Should the US Department of Commerce aggressively close third-party routing loopholes or sanction intermediaries like Aivres, NVIDIA could lose access to the $12-$15 billion in annualized revenue currently flowing through these proxy channels.48 While the market has largely written off direct China revenue, it has not priced in the loss of "RoW" revenue that is secretly Chinese.

8.3 Power Constraints and Deployment Delays

The physical reality of the GB200 NVL72 (120kW per rack) creates a deployment bottleneck. If data centers cannot be built or retrofitted fast enough to support liquid cooling, shipments of finished goods could stall. This would lead to an inventory bloat on NVIDIA's balance sheet, even if "demand" remains high. The disparity between "orders" and "installations" is the most critical operational metric to watch in 2026.

9. Conclusion

The Fiscal Q3 2026 earnings report is poised to be another validation of NVIDIA's dominance, but the narrative is shifting. The investment thesis is moving away from the sheer volume of chips sold to the strategic capture of the data center architecture. By forcing a transition to the NVL72 rack-scale standard, NVIDIA is effectively converting the world's data centers into proprietary NVIDIA supercomputers, creating a moat that is deeper and wider than silicon performance alone.
While fears of an "AI Bubble" regarding end-user monetization are valid, they are premature regarding infrastructure spend. The hyperscalers are locked into an arms race where capital expenditure is the price of admission, and Sovereign AI actors provide a new, price-insensitive layer of demand. The complex supply chain maneuvers—from the stacking of HBM3e by SK Hynix to the routing of servers through Indonesia—demonstrate a market that is finding ways to clear the market at any price.
Key Takeaway: The immediate upside is protected by the $300B+ hyperscale capex commitments and the deflationary TCO of Blackwell. The long-term risk is not a collapse in demand, but the gradual margin normalization as NVIDIA transitions from a component designer to a systems integrator. For Q3 FY26, the setup remains favorable, provided the Blackwell production ramp is reaffirmed without significant delay.
Recommendation: Maintain OVERWEIGHT. Investors should utilize any volatility stemming from the $8.1B tax-impacted cash flow numbers or geopolitical headlines to accumulate positions, as the structural transformation of the data center into an "AI Factory" is still in its early deployment phase.
Works cited
Nvidia earnings preview: NVDA stock prepares for crucial Q3 FY2026 results — here's how Nvidia stock may react post-earnings - The Economic Times, accessed November 18, 2025, https://m.economictimes.com/news/international/us/nvidia-earnings-preview-nvda-stock-prepares-for-crucial-q3-fy2026-results-heres-how-nvidia-stock-may-react-post-earnings/articleshow/125388456.cms
Why Amazon’s $125 Billion AI Bet Is Different From Meta’s, accessed November 18, 2025, https://www.investing.com/analysis/meta-plunged-12-amazon-jumped-11--same-ai-race-different-economics-200669410
Comparing Blackwell vs Hopper | B200 & B100 vs H200 & H100 | Exxact Blog, accessed November 18, 2025, https://www.exxactcorp.com/blog/hpc/comparing-nvidia-tensor-core-gpus
Comparing NVIDIA's B200 and H100: What's the difference? - Civo.com, accessed November 18, 2025, https://www.civo.com/blog/comparing-nvidia-b200-and-h100
Blackwell vs Hopper: A Deep Dive GPU Architecture Comparison | IntuitionLabs, accessed November 18, 2025, https://intuitionlabs.ai/articles/blackwell-vs-hopper-gpu-architecture-comparison
NVIDIA Blackwell vs Hopper: A Deep Dive into AI and HPC Performance - NexGen Cloud, accessed November 18, 2025, https://www.nexgencloud.com/blog/performance-benchmarks/nvidia-blackwell-vs-nvidia-hopper-a-detailed-comparison
TCO of NVIDIA GPUs and falling barriers to entry | Continuum Labs, accessed November 18, 2025, https://training.continuumlabs.ai/infrastructure/the-modern-data-centre/tco-of-nvidia-gpus-and-falling-barriers-to-entry
Deep dive into NVIDIA Blackwell Benchmarks — where does the 4x training and 30x inference performance gain, and 25x reduction in energy usage come from? - adrian cockcroft, accessed November 18, 2025, https://adrianco.medium.com/deep-dive-into-nvidia-blackwell-benchmarks-where-does-the-4x-training-and-30x-inference-0209f1971e71
GB200 NVL72 vs H100: When to choose which - WhiteFiber, accessed November 18, 2025, https://www.whitefiber.com/compare/nvidia-gb200-nvl72-vs-nvidia-h100
Nvidia Suppliers Send Mixed Signals for Delays on GB200 Systems – What It Means for NVDA Stock - IO Fund, accessed November 18, 2025, https://io-fund.com/semiconductors/supply-chain/nvidia-gb200-delays-mixed-signals-nvda-stock-analysis
Rack scale is on the rise, but it's not for everyone... yet - The Register, accessed November 18, 2025, https://www.theregister.com/2025/06/17/rack_scale_ai/
NVIDIA Blackwell GB200 Superchip to Cost up to 70,000 US Dollars | TechPowerUp, accessed November 18, 2025, https://www.techpowerup.com/322498/nvidia-blackwell-gb200-superchip-to-cost-up-to-70-000-us-dollars
Nvidia's Jensen Huang says Blackwell GPU to cost $30,000 - $40,000, later clarifies that pricing will vary as they won't sell just the chip | Tom's Hardware, accessed November 18, 2025, https://www.tomshardware.com/pc-components/gpus/nvidias-jensen-huang-says-blackwell-gpu-to-cost-dollar30000-dollar40000-later-clarifies-that-pricing-will-vary-as-they-wont-sell-just-the-chip
[P] B200 vs H100 Benchmarks: Early Tests Show Up to 57% Faster Training Throughput & Self-Hosting Cost Analysis - Reddit, accessed November 18, 2025, https://www.reddit.com/r/MachineLearning/comments/1jw3b9b/p_b200_vs_h100_benchmarks_early_tests_show_up_to/
NVIDIA Blackwell B200 vs H100: Real-World Benchmarks, Costs, and Why We Self-Host, accessed November 18, 2025, https://www.lightly.ai/blog/nvidia-b200-vs-h100
Amazon, Microsoft, Google, Meta Bet Big on AI Infrastructure Investment 2025, accessed November 18, 2025, https://lucidityinsights.com/infobytes/big-tech-ai-infrastructure-investment-2025
Amazon Follows Google, Meta, and Microsoft With Plans To Boost Spending on AI, accessed November 18, 2025, https://www.investopedia.com/amazon-follows-google-meta-and-microsoft-with-plans-to-boost-spending-on-ai-8787507
Amazon Q3 2024 Earnings: CEO Jassy Says AI 'Once In A Lifetime' Opportunity - CRN, accessed November 18, 2025, https://www.crn.com/news/cloud/2024/amazon-q3-2024-earnings-ceo-jassy-says-ai-once-in-a-lifetime-opportunity
Big tech has spent $155bn on AI this year. It's about to spend hundreds of billions more | Artificial intelligence (AI) | The Guardian, accessed November 18, 2025, https://www.theguardian.com/technology/2025/aug/02/big-tech-ai-spending
FY25 Q1 - Press Releases - Investor Relations - Microsoft, accessed November 18, 2025, https://www.microsoft.com/en-us/investor/earnings/fy-2025-q1/press-release-webcast
META Meta Platforms, Inc. Earnings Call Transcripts - Seeking Alpha, accessed November 18, 2025, https://seekingalpha.com/symbol/META/earnings/transcripts
Meta's AI spending spree has even the most bullish stock analysts wondering: How much capex is too much?, accessed November 18, 2025, https://www.fastcompany.com/91444071/meta-ai-spending-stock-analysts-cut-price-target-capex-too-high
META Q3 2025 Prepared Remarks, accessed November 18, 2025, https://s21.q4cdn.com/399680738/files/doc_financials/2025/q3/META-Q3-2025-Prepared-Remarks.pdf
Alphabet Inc. (GOOG) Morgan Stanley Technology, Media & Telecom Conference (Transcript) | Seeking Alpha, accessed November 18, 2025, https://seekingalpha.com/article/4585742-alphabet-inc-goog-morgan-stanley-technology-media-and-telecom-conference-transcript
2025 Predictions: AI Finds a Reason to Tap Industry Data Lakes | NVIDIA Blog, accessed November 18, 2025, https://blogs.nvidia.com/blog/industry-ai-predictions-2025/
SK Hynix closes in on Samsung as AI chip demand surges - Tech in Asia, accessed November 18, 2025, https://www.techinasia.com/news/sk-hynix-closes-in-on-samsung-as-ai-chip-demand-surges
SK hynix reportedly making High Bandwidth Storage (HBS): stacked chips for next-gen smartphones - TweakTown, accessed November 18, 2025, https://www.tweaktown.com/news/108806/sk-hynix-reportedly-making-high-bandwidth-storage-hbs-stacked-chips-for-next-gen-smartphones/index.html
Samsung reportedly slashes HBM3 prices to woo Nvidia — cuts could put the heat on rivals SK hynix and Micron as company attempts to spur AI turnaround | Tom's Hardware, accessed November 18, 2025, https://www.tomshardware.com/pc-components/gpus/samsung-reportedly-slashes-hbm3-prices-to-woo-nvidia-cuts-could-put-the-heat-on-rivals-sk-hynix-and-micron-as-company-attempts-to-spur-ai-turnaround
[News] Samsung Reportedly Unable to Supply HBM3E to NVIDIA in 2024 as Gap with SK hynix Widens | TrendForce News : r/AMD_Technology_Bets - Reddit, accessed November 18, 2025, https://www.reddit.com/r/AMD_Technology_Bets/comments/1hhd2v2/news_samsung_reportedly_unable_to_supply_hbm3e_to/
How subsidiary of a blacklisted Chinese company 'fooled' America to get banned Nvidia chips into China, accessed November 18, 2025, https://timesofindia.indiatimes.com/technology/tech-news/how-subsidiary-of-a-blacklisted-chinese-company-fooled-america-to-get-banned-nvidia-chips/articleshow/125381317.cms
The WSJ says it's tracked how 2,300 Nvidia Blackwell chips ended up in the hands of a Chinese AI company, accessed November 18, 2025, https://www.pcgamer.com/software/ai/a-wall-street-journal-investigation-claims-to-have-tracked-how-2-300-nvidia-blackwell-ai-chips-made-their-way-to-china-via-an-indonesian-telecoms-provider/
China taps Nvidia kit through a maze of middlemen, accessed November 18, 2025, https://www.fudzilla.com/news/memory-and-storage/62032-china-taps-nvidia-kit-through-a-maze-of-middlemen
National Transformation With Sovereign AI - NVIDIA, accessed November 18, 2025, https://www.nvidia.com/en-us/industries/global-public-sector/
Microsoft says UAE AI chip approval 'first step' for Emirati access | Semafor, accessed November 18, 2025, https://www.semafor.com/article/11/10/2025/microsofts-uae-ai-chip-approval-a-first-step-for-emirati-access-executive
US 'approves first Nvidia chips' to the UAE to deepen AI partnership - The National News, accessed November 18, 2025, https://www.thenationalnews.com/future/technology/2025/10/09/us-approves-first-nvidia-chips-to-uae-to-deepen-ai-partnership/
NVIDIA and SoftBank Corp. Accelerate Japan's Journey to Global AI Powerhouse, accessed November 18, 2025, https://nvidianews.nvidia.com/news/nvidia-and-softbank-accelerate-japans-journey-to-global-ai-powerhouse
NVIDIA and RIKEN Advance Japan's Scientific Frontiers With New Supercomputers for AI and Quantum Computing, accessed November 18, 2025, https://investingnews.com/nvidia-and-riken-advance-japan-s-scientific-frontiers-with-new-supercomputers-for-ai-and-quantum-computing/
AMD Accelerates Pace of Data Center AI Innovation and Leadership with Expanded AMD Instinct GPU Roadmap, accessed November 18, 2025, https://ir.amd.com/news-events/press-releases/detail/1201/amd-accelerates-pace-of-data-center-ai-innovation-and-leadership-with-expanded-amd-instinct-gpu-roadmap
AMD Unveils Vision for an Open AI Ecosystem, Detailing New Silicon, Software and Systems at Advancing AI 2025 - Stock Titan, accessed November 18, 2025, https://www.stocktitan.net/news/AMD/amd-unveils-vision-for-an-open-ai-ecosystem-detailing-new-silicon-0n1cen7nnaue.html
Oracle and AMD Expand Partnership to Help Customers Achieve Next-Generation AI Scale, accessed November 18, 2025, https://www.oracle.com/news/announcement/ai-world-oracle-and-amd-expand-partnership-to-help-customers-achieve-next-generation-ai-scale-2025-10-14/
Nvidia Blackwell Shines, AMD MI325X Debuts in Latest MLPerf - XPU.pub, accessed November 18, 2025, https://xpu.pub/2025/04/07/mlperf-5-0/
NVIDIA Announces Financial Results for Fourth Quarter and Fiscal 2025, accessed November 18, 2025, https://nvidianews.nvidia.com/news/nvidia-announces-financial-results-for-fourth-quarter-and-fiscal-2025
September 2025, accessed November 18, 2025, https://s201.q4cdn.com/141608511/files/doc_financials/2026/q2/NVDA-F2Q26-Quarterly-Presentation-FINAL.pdf
CFO Commentary on Second Quarter Fiscal 2026 Results, accessed November 18, 2025, https://s201.q4cdn.com/141608511/files/doc_financials/2026/Q226/Q2FY26-CFO-Commentary.pdf
CFO Commentary on - SEC.gov, accessed November 18, 2025, https://www.sec.gov/Archives/edgar/data/1045810/000104581025000207/q2fy26cfocommentary.htm
NVIDIA Announces Financial Results for Second Quarter Fiscal 2026, accessed November 18, 2025, https://nvidianews.nvidia.com/news/nvidia-announces-financial-results-for-second-quarter-fiscal-2026
March 2025, accessed November 18, 2025, https://s201.q4cdn.com/141608511/files/doc_financials/2025/q4/NVDA-F4Q25-Quarterly-Presentation-FINAL.pdf
Nvidia’s $500B AI Bet: Huang’s Forecast Faces Q3 Earnings Heat, accessed November 18, 2025, https://www.webpronews.com/nvidias-500b-ai-bet-huangs-forecast-faces-q3-earnings-heat/
