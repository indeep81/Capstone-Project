
# Early Outage Detection Using Synthetic Monitoring Data Executive Summary

This project explores how ThousandEyes synthetic monitoring data—specifically Ping and HTTP metrics—can be used to identify early signals of network outages and performance degradation. Using real-world data associated with a Spotify outage, the goal is to uncover patterns and correlations that can improve proactive detection of issues before they impact end users.

ThousandEyes Concepts Used
•	Agent: A probe (cloud, enterprise, or endpoint) that runs synthetic tests from various locations.
•	Test: An active measurement (e.g., Ping, HTTP Server) configured to monitor performance between agents and targets.
•	Ping Test: Measures basic network health via ICMP packets, capturing loss, latency, and jitter.
•	HTTP Server Test: Emulates user access to web services and records metrics like availability, response time, and server errors.
•	Loss: Percentage of packets dropped during transmission.
•	Latency: Time taken for packets to travel round trip between source and target.
•	Response Time: Time to receive the full HTTP response after connection is established

# Data Sources: Anonymized Raw Synthetic Test Data
Source: Internal ThousandEyes monitoring infrastructure
 **Ping Data**: Synthetic ping test results from ThousandEyes agents (`ping_spotify_*.csv`)
 **HTTP Data**: Synthetic HTTP test results from ThousandEyes agents (`http_spotify_*.csv`)
All datasets are anonymized and include metrics such as latency, packet loss, timing breakdowns, and test identifiers.

# Problem Statement
Ensuring optimal network and application performance is essential for maintaining reliable digital experiences. At large scale, even minor degradations in network quality—such as increased packet loss or latency—can ripple into user-facing outages. ThousandEyes provides deep network visibility using active monitoring via global vantage points known as agents, which execute tests like HTTP and Ping to measure performance from end to end.
Despite the richness of this data, current outage detection methods tend to be reactive, relying on threshold-based alerts and fragmented metric views. There is a missed opportunity to proactively surface patterns or early warning signals by analyzing relationships among key quality metrics such as packet loss (data that fails to reach its destination), latency(time taken for a packet to travel between source and destination), and response time (in HTTP tests, the total duration to receive a full response from a target server).
This project investigates whether anonymized time series data from ThousandEyes synthetic tests—primarily Ping—can be harnessed to improve proactive outage detection and metric correlation understanding. The goal is to build a structured framework that uses statistical and machine learning techniques to:
•	Detect anomalies that precede or align with known incidents
•	Reveal correlations among loss, latency, and response metrics
•	Improve the accuracy and interpretability of quality monitoring tools
This work not only supports internal reliability engineering but could also shape more intelligent alerting strategies that better align with real-world degradation and user impact.

## Rationale

As enterprises scale digital experiences globally, the ability to detect outages before users are affected is critical. Traditional alerting often misses early signals due to noise or isolated metric analysis. This project aims to demonstrate the value of structured exploratory data analysis (EDA) and statistical methods to extract proactive insights from ThousandEyes data.

## Research Question

Can we use synthetic Ping and HTTP metrics from ThousandEyes tests to detect early signals of network degradation or outages, particularly in relation to a known incident involving Spotify?

## Methodology: Adapted CRISP-DM Framework

This project follows the **CRISP-DM (Cross-Industry Standard Process for Data Mining)** methodology—an iterative, structured approach widely used in applied machine learning and analytics projects. The steps below have been tailored to align with our outage detection context using ThousandEyes synthetic monitoring data.

### Business Understanding

The primary objective is to **detect early indicators of network and service degradation**, using data from ThousandEyes synthetic tests that simulate user activity. Specifically, we aim to determine if **Ping and HTTP metrics** can be used to forecast or preemptively detect outage conditions, such as the one that affected Spotify. This work supports a broader goal of moving from reactive alerting to **proactive diagnostics** in network monitoring.

### Data Understanding

Raw data was collected from multiple ThousandEyes synthetic test runs—both Ping and HTTP types—targeting Spotify endpoints. These datasets included:
- Latency and packet loss metrics (Ping)
- Connection time, TTFB, and response breakdown (HTTP)
- Metadata such as virtual agent ID and test ID

Initial exploration involved:
- Identifying metric distributions and outliers
- Segmenting performance by `vAgentId` and `testId`
- Understanding inter-metric relationships (e.g., loss vs. timing)

### Data Preparation

To prepare the data for analysis and modeling:
- Multiple CSVs were merged to form consolidated datasets (`ping_df`, `http_df`)
- Missing values were checked and handled
- Features were scaled using `MinMaxScaler` where appropriate
- Summary statistics and plots were used to validate consistency
- Additional features were derived (e.g., agent/test performance profiles)

### Modeling

Initial modeling was done using **Linear Regression** to predict HTTP timing metrics (e.g., Total Request Time, TTFB) from Ping-related features (e.g., latency, loss). This phase was exploratory in nature, focused on evaluating whether a predictive signal exists.

**Techniques used**:
- Feature scaling (MinMax)
- Train-test split (80/20)
- Simple regression modeling with `sklearn`
- Performance**:
  - **R² Score**: ~1.0 for Total Request Time (indicative of moderate correlation)
  - **RMSE**: Low to moderate, depending on HTTP metric
  - Model underfitting observed—suggesting need for non-linear techniques

### Evaluation

While the linear model provided only **moderate predictive power** (R² values varied across target metrics), results validated that **Ping loss and latency can explain some variance in HTTP degradation**. Specific agents and tests emerged as consistent underperformers.

This confirms the feasibility of future, more advanced modeling using:
- Ensemble techniques (Random Forests, Gradient Boosting)
- Time-series forecasting (LSTM, ARIMA)
- Multivariate anomaly detection

### Deployment (Planned)

Though not deployed in this phase, recommendations are made for operational use:
- Integrate findings into internal dashboards (e.g., highlighting worst-performing agents)
- Automate metric tracking and alert thresholds based on learned patterns
- Use model results to guide synthetic test coverage planning

## Findings


## Future Research and Development

- Advanced modeling techniques like Ensemble techniques (Random Forests, Gradient Boosting)
- Time-series forecasting (LSTM, ARIMA)
- Multivariate anomaly detection
- Identify internally if there is URL/geo-location information for the agents and tests for the HTTP data sets

## Outline of Project

1. Introduction & Background  
2. Data Loading and Consolidation  
3. Ping Metrics Analysis (Loss & Latency)  
4. Agent-Level Performance Visualization  
5. HTTP Timing Analysis by Agent and Test ID  
6. Statistical Summary and Correlation Matrix  
7. Modeling and Prediction  
8. Conclusion and Recommendations  

## Contact Information

**Author**: Indeep Kaur  
**Program**: UC Berkeley Professional Certificate in Machine Learning and Artificial Intelligence  
**LinkedIn**: [Your LinkedIn Profile]  
**Email**: [your.email@example.com]  
**GitHub**: [github.com/yourusername]







