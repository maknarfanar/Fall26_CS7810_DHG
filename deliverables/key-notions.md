# Key Notions

* Model Run
    * Rationale: A single execution of the CAE with its own seed; needed to say which run flagged what and which runs processed a tile (CQ1, CQ2, CQ4, CQ5, CQ10). The seed is a plain property of the run.
    * Connected Pattern: Event ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/event)), Provenance ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/provenance))
    * Source Dataset(s): Run and Anomaly Results
 
* Threshold
    * Rationale: The cutoff on reconstruction error that decides whether a patch is flagged; needed to compare runs (CQ1, CQ2, CQ9).
    * Connected Pattern: Quantity ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/quantity))
    * Source Dataset(s): Run and Anomaly Results
 

* Anomaly
    * Rationale: A patch the model flagged in a run; the central entity linking runs, tiles, sites, and assessments (CQ1 to CQ10).
    * Connected Pattern: Observation ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/observation))
    * Source Dataset(s): Run and Anomaly Results
 
  
* Reconstruction Error
    * Rationale: The score that caused a patch to be flagged; needed to compare possible-candidate and not-a-candidate anomalies (CQ9).
    * Connected Pattern: Quantity ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/quantity))
    * Source Dataset(s): Run and Anomaly Results
 

* Patch
    * Rationale: The window of a tile that the model examines; the unit that gets flagged and can be flagged again by other runs (CQ1).
    * Connected Pattern: Part-Whole Contextualized ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/part-whole-contextualized)), Spatial Extent ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/spatial-extent))
    * Source Dataset(s): Run and Anomaly Results
 
  
* Tile
    * Rationale: The LiDAR image unit that contains patches; the main join point across datasets (CQ2 to CQ10). It carries the survey year and resolution used to compare tiles (CQ3, CQ7, CQ8) as plain properties.
    * Connected Pattern: Spatial Object ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/spatial-object)), Spatial Extent ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/spatial-extent)), Part-Whole ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/part-whole))
    * Source Dataset(s): LiDAR Tiles, Run and Anomaly Results
 

* County
    * Rationale: Groups tiles for the county comparison (CQ10).
    * Connected Pattern: Part-Whole ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/part-whole)), Sequence ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/sequence))
    * Source Dataset(s): LiDAR Tiles
 
  
* Coordinate Reference System
    * Rationale: The spatial reference a tile or site location is expressed in; compared between tiles (CQ3) and needed to convert site lat/long into tile coordinates so sites can be placed in tiles (CQ4, CQ5, CQ6, CQ8).
    * Connected Pattern: Spatial Extent ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/spatial-extent))
    * Source Dataset(s): LiDAR Tiles, Verified Hopewell Sites
 

* Verified Hopewell Site
    * Rationale: A known earthwork location used as the reference to compare anomalies against (CQ4, CQ5, CQ6, CQ8). Its lat/long is a plain property, and a site counts as "in" a tile when that location falls inside the tile's bounds.
    * Connected Pattern: Spatial Object ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/spatial-object)), Name Stub ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/name-stub))
    * Source Dataset(s): Verified Hopewell Sites
 
  
* Anomaly Assessment
    * Rationale: A reviewer's judgment about an anomaly; needed for every question about candidates and other features (CQ6, CQ7, CQ9). The reviewer and date are plain properties. There will be no ground-truthing in the current project. 
    * Connected Pattern: Observation ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/observation)), Provenance ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/provenance))
    * Source Dataset(s): Anomaly Assessments
 
  
* Determination (controlled vocabulary)
    * Rationale: The fixed set of outcomes of an assessment (CQ6, CQ7, CQ9) not a candidate, possible candidate.
    * Connected Pattern: Name Stub ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/name-stub)), Taxonomy Alignment ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/taxonomy-alignment))
    * Source Dataset(s): Anomaly Assessments
 

* Feature Type (controlled vocabulary)
    * Rationale: The kind of non-earthwork feature a reviewer identified (CQ7): road, rail, creek, river, pond, other.
    * Connected Pattern: Name Stub ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/name-stub)), Taxonomy Alignment ([MODL](https://github.com/kastle-lab/modular-ontology-design-library/tree/master/modl/taxonomy-alignment))
    * Source Dataset(s): Anomaly Assessments
