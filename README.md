# Large-Scale Data Analysis of Netflix Performance Over IPv6

> **Master's Thesis by Abhishek Kapoor**
> Technical University of Munich (TUM)
> *This work forms the basis to the research paper: "A Longitudinal View of Netflix: Content Delivery over IPv6 and Content Cache Deployments" published at INFOCOM 2020*

## 📋 Abstract

This thesis presents a comprehensive analysis of Netflix content delivery performance over IPv6 compared to IPv4 using a 22-month longitudinal dataset (July 2016 - May 2018) collected from ~100 SamKnows probes across 66 different Autonomous Systems (ASes). The study examines key performance indicators including TCP connect times, prebuffering duration, achievable throughput, stall rates, and the benefits of ISP content caches for Netflix streaming.

## 🎯 Research Questions

### RQ 1: IPv6 vs IPv4 Performance Comparison
- How does IPv6 performance compare with IPv4 for Netflix content delivery?
- Analysis of success rates, TCP connect times, throughput, and stall characteristics

### RQ 2: ISP Content Cache Benefits
- How beneficial are ISP content caches for Netflix streaming?
- Performance comparison between IPv4 and IPv6 when accessing these caches

### RQ 3: Speedtest Performance Analysis
- How do IPv4 and IPv6 Speedtest results compare for Netflix vs Measurement Lab?
- Comparative analysis of throughput measurements

### RQ 4: Network Path Analysis
- How do path length, latency, and delay compare over IPv4 and IPv6?
- Traceroute analysis and network topology insights

## 📊 Key Findings

### IPv6 Performance Characteristics
- **Success Rate**: 79% of probes achieved >90% success rate over IPv4, while only 63% achieved this over IPv6
- **Happy Eyeballs Preference**: Strong 93% preference for IPv6 during initial TCP connection establishment
- **Performance Gap**: Consistent higher TCP connection times (~40ms more) and prebuffering duration over IPv6
- **Throughput**: Lower achieved throughput over IPv6 compared to IPv4
- **Stall Rates**: <10% stall rates observed over both address families

### ISP Content Cache Benefits
- **Latency Reduction**: 10-20ms reduction in TCP connect times when using ISP caches
- **Prebuffering Improvement**: 0-750ms reduction in prebuffering duration
- **Throughput Enhancement**: 66% of measurements showed higher throughput with ISP caches
- **Path Length**: ISP caches reachable within 5 hops and 21ms
- **Cache Hit Performance**:
  - IPv4: 1801ms prebuffering (cache hit) vs 2428ms (cache miss)
  - IPv6: 1992ms prebuffering (cache hit) vs 2752ms (cache miss)

### Network Topology Insights
- **Path Length**: Shorter paths over IPv6 in many cases
- **AS Classification**: Transit/Access and Content ASes separated around TTL value of 5
- **Cache Identification**: Netflix traceroute likely to be ISP cache if ending in <5 hops
- **Geographic Distribution**: 60 probes in Europe, 32 in America, 8 in other regions

## 🗂️ Dataset Overview

### Data Collection Methodology
- **Duration**: 22 months (July 2016 - May 2018)
- **Probes**: ~100 dual-stacked SamKnows probes
- **Geographic Coverage**: 66 different origin ASes
- **Measurement Frequency**: Hourly measurements
- **Test Protocol**: Netflix-specific test mimicking real client behavior

### Dataset Structure
```
data/
├── Ipv4.txt                    # IPv4 destination IPs
├── Ipv6.txt                    # IPv6 destination IPs
├── Ipv4_hits.csv              # IPv4 hit statistics
├── Ipv6_hits.csv              # IPv6 hit statistics
├── Unique ASes.txt            # AS distribution analysis
└── Holder Names.txt           # AS holder information
```

### Key Metrics Analyzed
- **Success Rate**: Percentage of successful measurements
- **TCP Connect Times**: Connection establishment latency
- **Prebuffering Duration**: Time to buffer content before playback
- **Throughput**: Achievable download speeds
- **Stall Rate**: Percentage of measurements experiencing stalls
- **Stall Duration**: Length of playback interruptions
- **Path Length (TTL)**: Number of network hops to destination
- **Error Rates**: Classification and analysis of various error types

## 📈 Error Analysis

### Error Distribution
- **No Error**: 74.6% of measurements
- **STALLED_WILL_STEP_DOWN**: 13.5% (most common error)
- **CONNECTION_API_ERROR**: 4.5%
- **NETWORK_CONTENT_ERROR**: 4.3%
- **NETWORK_API_ERROR**: 2.3%
- **DNS Resolution Errors**: 0.7% combined
- **Other Errors**: <1% each

### Error Occurrence Patterns
- Daily error occurrence rate: 15%-45%
- Errors evenly distributed across all probes
- No specific probe bias in error generation

## 🏗️ Technical Architecture

### Netflix Test Sequence
1. **API Call**: Contact Netflix web-based API hosted on AWS
2. **Server Selection**: OCA server selection based on client IP, traffic load, network distance, and location
3. **Content Delivery**: HTTP 302 redirect to 25MB binary file
4. **Performance Measurement**: 20-second test with HTTP pipelining
5. **Metrics Collection**: TCP connect times, throughput, stall detection

### Measurement Infrastructure
- **SamKnows Probes**: Hardware-based measurement devices
- **Dual-Stack Support**: Native IPv4 and IPv6 connectivity
- **Geographic Distribution**: Global probe deployment
- **Traceroute Integration**: Paris-traceroute measurements using scamper

## 📁 Repository Structure

```
TU-Munich-Masters-Thesis-Netflix-IPv6-Performance/
├── README.md                   # This documentation
├── main.tex                    # Main LaTeX document
├── chapters/                   # Thesis chapters
│   ├── 01_introduction.tex     # Introduction and motivation
│   ├── 02_relatedwork.tex      # Related work and literature review
│   ├── 03_datasets.tex         # Dataset description and methodology
│   ├── 04_1.tex               # IPv4 vs IPv6 performance analysis
│   ├── 04_2.tex               # ISP content cache benefits
│   ├── 04_3.tex               # Speedtest comparison analysis
│   ├── 04_4.tex               # Path length and latency analysis
│   ├── 05_conclusion.tex      # Conclusions and future work
│   └── 06_reproducibility.tex # Reproducibility information
├── data/                       # Analysis datasets
├── figures/                    # Generated analysis figures
│   ├── cache/                  # ISP cache analysis figures
│   ├── errors/                 # Error analysis visualizations
│   ├── preference/             # IPv6 preference analysis
│   ├── stall/                  # Stall analysis figures
│   ├── tcp/                    # TCP performance figures
│   ├── throughput/             # Throughput analysis
│   └── traceroute/             # Network path analysis
├── appendix/                    # Additional analysis details
└── references/                 # Research papers and references
```

## 🔬 Analysis Methodology

### Statistical Analysis
- **Longitudinal Analysis**: Time-series analysis over 22-month period
- **Comparative Studies**: IPv4 vs IPv6 performance comparison
- **Cache Impact**: ISP cache vs Netflix OCA performance
- **Geographic Analysis**: Regional performance variations
- **Error Classification**: Systematic error categorization and analysis

### Visualization Techniques
- **Time Series Plots**: Performance trends over time
- **Box Plots**: Statistical distribution analysis
- **CDF Plots**: Cumulative distribution functions
- **Heatmaps**: Geographic performance patterns
- **Scatter Plots**: Correlation analysis

## 📊 Key Results Summary

### Performance Metrics Comparison

| Metric | IPv4 | IPv6 | Improvement with ISP Cache |
|--------|------|------|---------------------------|
| Success Rate | 79% probes >90% | 63% probes >90% | N/A |
| TCP Connect Time | Baseline | +40ms | -10-20ms |
| Prebuffering Duration | Baseline | +40ms+ | -0-750ms |
| Throughput | Higher | Lower | +66% measurements |
| Stall Rate | <10% | <10% | Reduced |

### ISP Cache Benefits
- **Latency Reduction**: 10-20ms improvement in TCP connect times
- **Prebuffering**: 0-750ms reduction in buffering duration
- **Throughput**: 66% of measurements show higher speeds
- **Path Length**: Caches reachable within 5 hops
- **Geographic Advantage**: Local content delivery benefits

## 🌍 Geographic Distribution

### Probe Distribution
- **Europe**: 60 probes (60%)
- **America**: 32 probes (32%)
- **Other Regions**: 8 probes (8%)

### Regional Analysis
- Performance variations across different geographic regions
- IPv6 adoption patterns by region
- ISP cache deployment strategies by geography

## 🔧 Technical Implementation

### Data Processing Pipeline
1. **Data Collection**: SamKnows probe measurements
2. **Data Cleaning**: Error filtering and validation
3. **Aggregation**: Temporal and spatial aggregation
4. **Analysis**: Statistical and comparative analysis
5. **Visualization**: Figure generation and interpretation

### Tools and Technologies
- **Database**: SQLite for data storage
- **Analysis**: Python with pandas, numpy, matplotlib
- **Visualization**: Matplotlib, seaborn
- **Network Analysis**: Paris-traceroute, scamper
- **Documentation**: LaTeX for thesis preparation

## 📚 Research Impact

### Academic Contributions
- **First Study**: First comprehensive study of Netflix performance from residential networks since 2011
- **Longitudinal Analysis**: 22-month dataset providing unique insights
- **Methodology**: Novel approach to measuring CDN performance
- **Cache Analysis**: Systematic analysis of ISP content cache benefits

### Industry Relevance
- **Netflix Optimization**: Insights for content delivery optimization
- **ISP Strategy**: Guidance for ISP cache deployment
- **IPv6 Deployment**: Evidence for IPv6 performance characteristics
- **CDN Design**: Understanding of content delivery network performance

## 🔗 Related Publications

This thesis work contributed to the following research publication:

**"A Longitudinal View of Netflix: Content Delivery over IPv6 and Content Cache Deployments"**
*Published at INFOCOM 2020*
Authors: Trinh Viet Doan, Vaibhav Bajpai, Sam Crawford
DOI: [https://vaibhavbajpai.com/documents/papers/proceedings/netflix-infocom-2020.pdf](https://vaibhavbajpai.com/documents/papers/proceedings/netflix-infocom-2020.pdf)

> **Acknowledgement**: The paper acknowledges "Abhishek Kapoor for helping with an early exploration of the dataset."

## 🚀 Future Work

### Research Extensions
- **Geographic Expansion**: More probes in underrepresented regions (Africa, Western Pacific)
- **Mobile Analysis**: Performance analysis on mobile and IoT devices
- **Real-time Monitoring**: Continuous performance monitoring
- **Advanced Analytics**: Machine learning approaches to performance prediction

### Technical Improvements
- **Better Cache Identification**: Enhanced techniques for ISP cache detection
- **Network Type Analysis**: Performance analysis by network type
- **Temporal Analysis**: Deeper investigation of time-based performance patterns
- **Cross-Platform Analysis**: Performance across different device types

## 📖 Reproducibility

### Data Availability
- Anonymized dataset available for research purposes
- Jupyter notebooks for analysis reproduction
- Complete methodology documentation
- Figure generation scripts included

### Analysis Code
- Python scripts for data processing
- Statistical analysis implementations
- Visualization generation code
- Database schema and queries

## 🎓 Academic Context

### Thesis Information
- **Institution**: Technical University of Munich (TUM)
- **Program**: Master's in Computer Science
- **Supervisor**: Prof. Jörg Ott
- **Duration**: 2017-2018

## 📞 Contact

For questions about this research or collaboration opportunities:

- **Author**: Abhishek Kapoor
- **Institution**: Technical University of Munich

## 📄 License

This research work is part of academic thesis and is available for educational and research purposes. Please cite appropriately when using any findings or methodologies from this work.

---

*This README provides a comprehensive overview of the Netflix IPv6 performance analysis thesis. For detailed technical analysis, please refer to the individual chapters and the complete thesis document.*
