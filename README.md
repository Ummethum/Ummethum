<h1 align="center">Hi 👋, I'm Henning Ummethum</h1>
<h2 align="center">Data and Molecular Biology Scientist</h2>

<h2>👨‍💻 About Me </h2>

After 7 years of studying how cells protect their genomes from falling apart, I decided it was time to do the same for messy datasets.

I'm currently completing a 17-week full-time Data Science programme at WBS Coding School, working through the full stack:

- **SQL (MySQL) & Tableau**: business analytics and data visualisation
- **Python (Pandas, Matplotlib, Seaborn)**: data wrangling and storytelling
- **Statistics & A/B Testing**: evidence-based decision making
- **ETL Pipelines, Web Scraping & APIs**: data extraction and transformation
- **Google Cloud Platform**: scalable data infrastructure
- **Scikit-learn**: supervised and unsupervised machine learning
- **Generative AI & RAG**: building retrieval-augmented chatbots grounded in domain-specific sources (LlamaIndex, LLM APIs)

The transition felt natural: modern biology runs on data, and some of my most satisfying moments in the lab were less about pipetting and more about making sense of what the numbers were actually saying.

<h2>🧰 Techstack </h2>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4EABE1?style=for-the-badge&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)
![Interactive Dashboards](https://img.shields.io/badge/Interactive_Dashboards-blueviolet?style=for-the-badge&logo=tableau&logoColor=white)
![LlamaIndex](https://img.shields.io/badge/LlamaIndex-RAG-purple?style=for-the-badge)
![Groq](https://img.shields.io/badge/Groq-LLM_Inference-orange?style=for-the-badge)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)



<h1>👨‍💻 Projects</h1>

<h2>Machine Learning</h2>

## [<b>RespiWatch</b>](https://github.com/Ummethum/respi-watch)
  - End-to-end forecasting system predicting Influenza incidence 1-2 weeks into the future for all ~400 German Kreise, combining ~20 years of RKI surveillance data with weather, pollen, and Google Trends signals, served through a public Streamlit dashboard.
  - ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![XGBoost](https://img.shields.io/badge/XGBoost-red?style=for-the-badge) ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
  - Details
    - <b>Approach</b>: Prophet seasonal baseline per Kreis, log-transformed to prevent off-season overshoot, corrected by an XGBoost residual model trained on weather, search trends, wastewater surveillance, and holiday data — deliberately excluding recent raw case counts as a feature, since those carry the same real-world reporting lag the whole project works around.
    - <b>Result</b>: Validated against a genuinely held-out final 15% of the historical data. Reliably detects the onset and timing of a seasonal wave; exact peak height is still systematically underestimated, a known tree-ensemble limitation only partially mitigated here.
    - <b>Data engineering</b>: Automated weekly pipeline across 8+ heterogeneous sources (SOAP APIs, GitHub-hosted open data, REST weather APIs)
    - <b>Deployment</b>: Weekly cron pipeline pushes data to a Hugging Face Dataset repo; the Streamlit app reads exclusively from there at runtime

## [<b>Audio Feature Clustering</b>](https://github.com/Ummethum/audio-feature-clustering)
  - Unsupervised machine learning pipeline that clusters 5,114 Spotify songs by audio features and automatically creates playlists via the Spotify API. Each playlist contains between 50 and 250 songs with similar audio profiles.
  - ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white) ![Spotipy](https://img.shields.io/badge/Spotipy-1DB954?style=for-the-badge&logo=spotify&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
  - Details
    - <b>Approach</b>: K-Means clustering with iterative subclustering &rarr; oversized clusters (>250 songs) are recursively split at k=4, clusters below 50 songs are discarded.
    - <b>Result</b>: 36 playlists with 58–228 songs each. Clusters are internally consistent by audio profile, though some span multiple genres &rarr; audio features alone cannot substitute a human curator.
    - <b>Scaling</b>: Compared MinMaxScaler, StandardScaler, and RobustScaler &rarr; MinMaxScaler and StandardScaler performed best.
    - <b>Spotify Integration</b>: Authenticated via SpotifyOAuth and uploaded playlists automatically using Spotipy, with batched track additions to stay within API limits.

<h2>Generative AI</h2>
 
## [<b>Respiratory Disease Knowledge Assistant</b>](https://github.com/Ummethum/chatbot)
  - Retrieval-augmented chatbot answering questions about respiratory diseases in Germany strictly from official sources (RKI Falldefinitionen, the AMELAG wastewater-surveillance guide, the Infektionsschutzgesetz, the RKI Jahrbuch 2024) plus curated Wikipedia articles. Companion knowledge layer for the RespiWatch forecasting project.
  - ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![LlamaIndex](https://img.shields.io/badge/LlamaIndex-RAG-purple?style=for-the-badge) ![Groq](https://img.shields.io/badge/Groq-Llama_3.3_70B-orange?style=for-the-badge) ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
  - Details
    - <b>Approach</b>: Source-aware chunking (different chunk size/overlap per document type), multilingual HuggingFace embeddings, and targeted page-range extraction from a 200+ page annual report instead of indexing it wholesale.
    - <b>Result</b>: A grounded chatbot with conversational memory (`CondensePlusContextChatEngine`) that answers only from retrieved context and explicitly says so when the context is insufficient, important for anything touching legal or medical definitions.
    - <b>Deployment</b>: Index built and embedded offline, published to a Hugging Face Dataset repo; the Streamlit app reads exclusively from there at runtime, same pattern as RespiWatch.

<h2>Data Engineering</h2>

## [<b>Data Acquisition Pipeline</b>](https://github.com/Ummethum/data-acquisition-pipeline)
  - Local ETL pipeline collecting city demographics, weather forecasts, and flight arrivals from Wikipedia and two REST APIs, storing results in a normalised MySQL database. Built as Phase 1 of a cloud migration project for a fictional e-scooter company optimising fleet deployment.
  - ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white) ![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=for-the-badge&logo=sqlalchemy&logoColor=white) ![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup4-4EABE1?style=for-the-badge&logo=python&logoColor=white)
  - Details
    - <b>Business Context</b>: E-scooter demand is shaped by weather, tourist arrivals, and city geography. The pipeline feeds those signals into fleet repositioning decisions.
    - <b>Web Scraping</b>: Extracted city metadata and population from Wikipedia infoboxes using BeautifulSoup, navigating inconsistent HTML structures.
    - <b>API Integration</b>: Used OpenWeatherMap (5-day / 3-hour forecasts) and AeroDataBox (airport discovery, tomorrow's arrivals)
    - <b>Data Modelling</b>: Designed a SQL schema with foreign key chains across five tables: <code>cities</code>, <code>city_populations</code>, <code>city_weather_forecast</code>, <code>airports</code>, <code>flights</code>.

<h2>Data Analytics</h2>

## [<b>Market Expansion Data Study</b>](https://github.com/Ummethum/ecommerce-expansion-analysis)
  - SQL & Tableau analysis evaluating a Brazilian SaaS logistics partner for European tech e-commerce expansion into Brazil, covering product fit, delivery performance, and customer satisfaction across 99k orders and 74 product categories.
  - ![SQL](https://img.shields.io/badge/SQL-336791?style=for-the-badge&logo=postgresql&logoColor=white) ![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)
  - Details
    - <b>Business Context</b>: Real-world scenario: a European tech company exploring Brazilian market entry with one year to decide and no local infrastructure.
    - <b>SQL Analysis</b>: Explored an unfamiliar database from scratch, progressing from exploratory queries to targeted business questions (tech revenue share, delivery times, premium product reviews).
    - <b>Tableau Visualisations</b>: Built dashboards communicating delivery performance, geographic patterns, and category revenue breakdowns.
    - <b>Key Findings</b>: 
      - Tech accounts for ~23% of platform GMV
      - high-end products (>€750) rated 4.0–4.3/5
      - 93% on-time delivery; average 13 days nationwide (9 days southeast, 26 days remote north).
    - <b>Recommendation</b>: Sign the contract: a low-risk market entry point with a reliable, scaling platform.

## [<b>Discount Strategy Analysis</b>](https://github.com/Ummethum/ecommerce-discount-strategy-analysis)
  - Python-based analysis investigating whether discounts help or hurt an e-commerce company, covering discount depth, seasonal revenue patterns, and price distribution across a heavily cleaned four-table dataset.
  - ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white) ![Seaborn](https://img.shields.io/badge/Seaborn-4EABE1?style=for-the-badge&logo=python&logoColor=white) ![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)
  - Details
    - <b>Business Context</b>: Marketing and the Board disagree on whether discounting drives growth or erodes revenue; the data was used to settle it.
    - <b>Data Cleaning</b>: Raw data reduced from 226k to 41k orders through duplicate removal, missing value handling, and format filtering; cleaning was a core deliverable, not a footnote.
    - <b>Python Analysis</b>: Used Pandas and Seaborn to analyse discount prevalence, revenue impact, and seasonal patterns across products and order lines.
    - <b>Key Findings</b>:
      - 93% of products are discounted
      - higher discounts do not increase demand or revenue
      - seasonality, not discounting, drives revenue spikes.
    - <b>Recommendation</b>:
      - Phase out blanket discounts run A/B tests
      - redirect discount spend to targeted channels such as newsletter sign-up offers.

<!--
**Ummethum/Ummethum** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
