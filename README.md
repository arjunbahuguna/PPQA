# PPQA - A Privacy-preserving Querying & Analysis Platform for Clinical Trials Data
For the Vivli Datathon 2019, we've created a project that allows users to query and analyze clinical trials data, with granular control over privacy loss. **Dataset Owners**, who contribute datasets to the platform, can set a privacy budget. When an **Analyst** later requests the data, the querying and analysis algorithms on our platform will maintain the privacy required by the Dataset Owner and adjust the accuracy automatically. This gives Dataset Owners granular control over the privacy of their dataset, while analysts can still get the results they want.

## The Privacy Budget
A metric, between 0 & 1, to inform the platform how much privacy is required. Higher privacy budget means stricter privacy guarantees, and as a consequence lower usability/accuracy on the queries and models running on our platform. Higher privacy budgets can be used in smaller datasets (like the one provided in this Datathon) where the risk of re-construction & re-identification attacks is greater. Lower privacy budgets are suitable for less important data like patient inflow/outflow data & hospital OPD data.

## STEP 1: UPLOAD 
### Automatic Sanitization using L-diversity
If the dataset owner hasn't already sanitized the dataset when uploading it to the platform, the platform automatically runs Mondrian algorithm for L-diversity anonymization on the data during uploading. This groups quasi-identifiers like Pin Code, Nationality, Age, etc to make it more difficult to uniquely identify individuals from one or some combination of these quasi-identifiers. We chose Mondrian L-diversity because it's fast and provides a stronger privacy guarantee than K-anonymity.

## STEP 2: QUERY
### Differentially-private Query Mechanism
The data never leaves the platform. The query and analysis tools are in-built into the platform. For querying, we use a differentially-private masking mechanism built for SQL Queries. All SQL queries that go into this mechanism are turned into differentially-private queries (using the [elastic sensitivity approach](http://www.cse.psu.edu/~ads22/pubs/NRS07/NRS07-full-draft-v1.pdf)), and therefore the data returned by the query preserves user privacy. Using the privacy budget feature, the amount of noise injected into making the queries differentially private can be tuned (epsilon value can be changed using a single command). This provides granular control over user privacy, depending on the kind of accuracy the Analyst wishes to get from his/her/their queries.


## STEP 3: ANALYZE
### Differentially-private Statistical Analysis Tools
To provide differentially-private statistical analysis, we had to build the analysis algorithms into the platform. This allowed us to only provide a few basic but powerful algorithms like random forests and . Using these algorithms, the analyst can classify, aggregate, do regression tests, and perform general analysis on the clinical trials dataset. Again, the privacy can be set using epsilon which allows the user granular control over the privacy vs usability tradeoff.

## References
1. [Mondrian implementation by qiyuangong](https://github.com/qiyuangong/Mondrian_L_Diversity)
2. [Differentially-private SQL by Uber](https://github.com/uber/sql-differential-privacy)
3. [Differentially-private Decision Forests implementation by Sam Fletcher](https://github.com/sam-fletcher/Smooth_Random_Trees)
