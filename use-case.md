
# Use Case
## Narrative


## Competency Questions
* CQ1 Which run flagged anomaly A, what were that run's seed and threshold, and how do they differ from any other run that flagged the same patch?<br>
Bridges Datasets: Run and Anomaly Results
* CQ2 For tile T, how do the seeds and thresholds of the runs that flagged an anomaly in it differ from those of the runs that processed it and flagged nothing?<br>
Bridges Datasets: Run and Anomaly Results, LiDAR Tiles
* CQ3 Which survey year, resolution, and CRS apply to the tile containing anomaly A, and how do they compare to those of the tile containing anomaly B?<br>
Bridges Datasets: Run and Anomaly Results, LiDAR Tiles
* CQ4 Which entries in Verified Hopewell Sites fall in the same tile as an anomaly, and which run flagged that anomaly?<br>
Bridges Datasets: Verified Hopewell Sites, LiDAR Tiles, Run and Anomaly Results
* CQ5 Which tiles were flagged in at least N runs but contain no entry in Verified Hopewell Sites?<br>
Bridges Datasets: Run and Anomaly Results, LiDAR Tiles, Verified Hopewell Sites
* CQ6 Which anomalies were judged a possible candidate, and does their tile contain an entry in Verified Hopewell Sites?<br>
Bridges Datasets: Anomaly Assessments, Run and Anomaly Results, LiDAR Tiles, Verified Hopewell Sites
* CQ7 Which anomalies were judged not a candidate because they are another kind of feature, what kind of feature, and what are the survey year and resolution of their tiles?<br>
Bridges Datasets: Anomaly Assessments, Run and Anomaly Results, LiDAR Tiles
* CQ8 Which entries in Verified Hopewell Sites sit in a tile that no run flagged, and what are that tile's survey year and resolution?<br>
Bridges Datasets: Verified Hopewell Sites, LiDAR Tiles, Run and Anomaly Results
* CQ9 How do anomalies judged a possible candidate differ in reconstruction error from those judged not a candidate, and which threshold flagged each?<br>
Bridges Datasets: Anomaly Assessments, Run and Anomaly Results
* CQ10 Which county has the most anomalies in run R?<br>
Bridges Datasets: Run and Anomaly Results, LiDAR Tiles

## Potential Datasets
* [LiDAR Tiles]: tile serial, county, survey year, resolution, CRS, and tile bounds, for a small slice of the master set covering the counties used in the project (external, compiling)
* [Verified Hopewell Sites]: UNESCO or other site name, lat/long, and geometry type (point or boundary), plus earthwork type if the source has it (external)
* [Run and Anomaly Results]: run ID, seed, threshold value, list of tiles processed by the run, anomaly ID, patch ID, parent tile serial, window position in the tile, and reconstruction error (created for this project)
* [Anomaly Assessments]: anomaly ID, reviewer, date, determination (not a candidate / possible candidate), feature type if it's something else, and notes (created for this project)
