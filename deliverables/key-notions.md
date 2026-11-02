# Key Notions

* Model Run
    * Rationale: A single execution of the CAE with its own seed; needed to say which run flagged what and which runs processed a tile (CQ1, CQ2, CQ4, CQ5, CQ8, CQ9, CQ10). The seed and threshold are parameter instantiation properties of the run.
    * Connected Pattern: Computational Observation ODP ([Shimizu, C., Hitzler, P., & Vardeman, C. F. (2023). A Pattern for Modeling Computational Observations. CEUR Workshop Proceedings, 3352.](https://corescholar.libraries.wright.edu/cse/709))
    * Source Dataset(s): Run and Anomaly Results

* Anomaly
    * Rationale: A patch the model flagged in a run; the central entity linking runs, tiles, sites, and assessments (CQ1 to CQ10). This includes a reconstruction error value.
    * Connected Pattern: Computational Observation ODP ([Shimizu, C., Hitzler, P., & Vardeman, C. F. (2023). A Pattern for Modeling Computational Observations. CEUR Workshop Proceedings, 3352.](https://corescholar.libraries.wright.edu/cse/709)), Observation ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/observation))
    * Source Dataset(s): Run and Anomaly Results

* Patch
    * Rationale: The area the model flags; shared across runs and identified by its tile plus row and column of said tile (CQ1 thru CQ10).
    * Connected Pattern: Part-Whole ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/part-whole))
    * Source Dataset(s): Run and Anomaly Results
 
  
* Tile
    * Rationale: The LiDAR image unit that contains patches; the main join point across datasets (CQ2 to CQ10). It carries the survey year, county, CRS, and resolution in feet used to compare tiles (CQ3, CQ7, CQ8, CQ10) as properties.
    * Connected Pattern: Part-Whole ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/part-whole))
    * Source Dataset(s): LiDAR Tiles, Run and Anomaly Results


* Verified Hopewell Site
    * Rationale: A known earthwork location used as a reference for comparing anomalies (CQ4, CQ5, CQ6, CQ8). Its point location in its geometry, and a site is “in” a tile when that point falls inside the tile’s bounds.
    * Connected Pattern: Spatial Object ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/spatial-object))
    * Source Dataset(s): Verified Hopewell Sites
 
  
* Anomaly Assessment
    * Rationale: A reviewer's judgment about an anomaly; needed for every question about candidates and other features (CQ6, CQ7, CQ9). There is only one reviewer for this project at this time and the date is irrelevant for this iteration. There will be no ground-truthing in the current project either.
    * Connected Pattern: Observation ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/observation))
    * Source Dataset(s): Anomaly Assessments
 

* Determination
    * Rationale: The fixed set of outcomes of an assessment (CQ6, CQ7, CQ9) not a candidate, possible candidate.
    * Connected Pattern: None - controlled vocabulary
    * Source Dataset(s): Anomaly Assessments
 

* Feature Type
    * Rationale: The kind of non-earthwork feature a reviewer identified (CQ7): road, rail, creek, river, pond, other.
    * Connected Pattern: None - controlled vocabulary
    * Source Dataset(s): Anomaly Assessments
