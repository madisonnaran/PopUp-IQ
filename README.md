# PopUp-IQ
PopUp IQ is a tool that scores NYC neighborhoods to help decide where to place a pop-up bar. It uses public NYC data and combines a few factors into one score per neighborhood.

What it does

If you're opening a pop-up bar, picking the right neighborhood matters — and it's hard to know without doing a lot of digging. PopUp IQ does that digging for you by pulling together four public datasets into one PopupIQ Score per neighborhood, based on:

Competition — how many bars/nightlife venues are already in the area
Subway access — how easy it is for people to get there
Noise & safety complaints — how nightlife-friendly and low-risk the area is

Each neighborhood gets a score from 0–100 on each of these, then they're combined into one final score (Safety 40%, Subway Access 40%, Competition 20%) so you can quickly compare areas side by side.

Data used
Dataset	Where it's from	Why I used it
Active liquor licenses	NY State Liquor Authority	Find existing bars/competition
MTA Subway Entrances & Exits (2024)	NYC Open Data	Measure how easy an area is to get to
NYPD Complaint Data (Year to Date)	NYC Open Data — filtered to noise/safety complaints, ~15 months of data	Measure risk and noise level by area
2020 Neighborhood Tabulation Areas (NTAs)	NYC Dept. of City Planning	Defines the neighborhood boundaries I used to group everything

Note: the raw NYPD complaint file is about 76MB, too big to include in this repo. I included the cleaned, filtered version instead (cleaned_complaints.csv) — the original can be downloaded from NYC Open Data.

How it works
Clean each dataset on its own — fix column names, keep only NYC data, remove rows that don't apply (like non-bar businesses or subway exits with no entry), and pull out latitude/longitude where needed.
Match each location to a neighborhood — I checked which neighborhood box (using its min/max latitude and longitude) each bar, subway entrance, and complaint falls inside, then double-checked the match against the listed borough to catch mistakes.
Group everything by neighborhood — count bars, average nearby subway entrances, and average nearby complaints per neighborhood. I only kept neighborhoods with at least 5 bars so the numbers were meaningful.
Score and rank — scale each number to 0–100, then combine them into the final PopupIQ Score using the weights above.
Save the results — final rankings are saved to popupiq_scores.csv.
Tools used
Python (pandas, scikit-learn for scaling the scores)
Jupyter Notebook (popupiq_pipeline.ipynb has the whole process)
Public data from NYC Open Data, MTA, and NY State Liquor Authority
What's in this repo
popupiq_pipeline.ipynb — the full notebook: cleaning, matching, and scoring
cleaned_venues.csv, cleaned_subway.csv, cleaned_complaints.csv, cleaned_nta.csv — cleaned versions of each dataset
popupiq_scores.csv — the final neighborhood rankings
liquor licenses active.csv, MTA_Subway_Entrances_and_Exits...csv, 2020_Neighborhood_Tabulation_Areas...csv — the original raw files (small enough to include as-is)
A couple notes on my approach
The NYPD complaint data only goes back about 15 months. That's fine for this — noise complaint patterns don't shift much year to year, so it's still a solid signal.
Instead of doing an exact map-shape match to figure out which neighborhood each location falls in, I used a simpler bounding-box method (checking if a point falls inside a neighborhood's min/max lat and lon) and then double-checked it against the borough to catch errors. It's faster than a full geographic match and worked well for this project.
