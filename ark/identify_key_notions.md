# Identify Key Notions

- CQ1 Which model run flagged anomaly A, and what model, environment, seed, and training batch did it use?

     -- Classes:
        Anomaly, ModelRun, Model, ComputationalEnvironment, TrainingBatch
        
     -- Object Properties:
        flaggedBy, usedModel, ranIn, hasTrainingBatch
        
     -- Data Properties:
        seed

- CQ2 Which patches make up training batch B, and how was it selected (random, curated, hybrid)?

     -- Classes:
        TrainingBatch, Patch, SelectionMethod
        
     -- Object Properties:
        composedOf, selectedBy

- CQ3 Is the patch of anomaly A also flagged in other runs with a different seed or training batch?

     -- Classes:
        Anomaly, Patch, ModelRun, TrainingBatch

     -- Object Properties:
        concernsPatch, flaggedBy, hasTrainingBatch
     
     -- Data Properties:
        seed

- CQ4 Was the patch of anomaly A in the training batch of the run that flagged it?

     -- Classes:
        Anomaly, Patch, ModelRun, TrainingBatch
     
     -- Object Properties:
        concernsPatch, flaggedBy, hasTrainingBatch, composedOf

- CQ5 What reconstruction error and threshold produced the flag for anomaly A, and how was the threshold set?

     -- Classes:
        Anomaly, ModelRun, ThresholdSetMethod
     
     -- Object Properties:
        hasThresholdMethod, flaggedBy
     
     -- Data Properties:
        reconError, thresholdValue	

- CQ6 Which survey year, resolution, and CRS apply to the tile of anomaly A?

     -- Classes:
        Anomaly, Patch, Tile, Survey
     
     -- Object Properties:
        concernsPatch, partOfTile, hasSurvey
     
     -- Data Properties:
        surveyYear, resolution, crs

- CQ7 Does the tile of anomaly A differ in survey year, resolution, or CRS from the tiles in the training batch of the run that flagged it?

     -- Classes:
        Anomaly, Patch, Tile, Survey, ModelRun, TrainingBatch
     
     -- Object Properties:
        concernsPatch, partOfTile, hasSurvey, flaggedBy, hasTrainingBatch, composedOf
     
     -- Data Properties:
        surveyYear, resolution, crs

- CQ8 Which non-earthwork features (roads, rails, creeks, rivers, ponds) are in or adjacent to the patch of anomaly A?

     -- Classes:
        Anomaly, Patch, Feature, FeatureType
     
     -- Object Properties:
        concernsPatch, hasFeature, adjacentTo (Patch-Patch), isOfType

- CQ9 Of the known earthworks in the ArchaeologicalReference covered by run R, which overlap an anomaly and which do not?

     -- Classes:
        ModelRun, Patch, Anomaly, Earthwork, ArchaeologicalReference
     
     -- Object Properties:
        processedPatch, hasAnomaly, concernsPatch, overlapsEarthwork, recordedIn

- CQ10 Which known earthworks overlap an anomaly in some runs but not in others?

     -- Classes:
        see CQ9
     
     -- Object Properties:
        see CQ9

- CQ11 Which anomalies are on patches adjacent to patches of other anomalies (possible continuous earthwork or complex)?

     -- Classes:
        Anomaly, Patch
     
     -- Object Properties:
        concernsPatch, adjacentTo (Patch-Patch)

- CQ12 Which anomalies lie in tiles adjacent to a tile containing a known linear earthwork?

     -- Classes:
        Anomaly, Patch, Tile, Earthwork, EarthworkType
     
     -- Object Properties:
        concernsPatch, partOfTile, adjacentTo (Tile-Tile), containsEarthwork, isOfType

- CQ13 Which anomalies have been assessed, by whom, by what method, and with what outcome (confirmed, rejected, inconclusive)?

     -- Classes:
        Anomaly, AnomalyAssessment, Agent, AssessmentMethod, AssessmentResult
     
     -- Object Properties:
        hasAssessment, assessedBy, hasAssessmentMethod, hasAssessmentResult
     
     -- Data Properties:
        assessedOn

- CQ14 Which anomalies have neither an independent-source assessment nor a field assessment (GroundTruthingTargets)?

     -- Classes:
        Anomaly, AnomalyAssessment, AssessmentMethod, GroundTruthingTarget
     
     --  Object Properties:
        hasAssessment, hasAssessmentMethod

- CQ15 Which rejected anomalies had a non-earthwork feature in or adjacent to their patch?

     -- Classes:
        Anomaly, AnomalyAssessment, Agent, AssessmentResult, Patch, Feature
     
     -- Object Properties:
        hasAssessment, assessedBy, hasAssessmentResult, concernsPatch, hasFeature, adjacentTo (Patch-Patch)

- CQ16 Which unassessed anomalies are on patches flagged in more than one run and adjacent to a patch of another anomaly?

     -- Classes:
        Anomaly, AnomalyAssessment, Patch, ModelRun
     
     -- Object Properties:
        hasAssessment, concernsPatch, flaggedBy, adjacentTo (Patch-Patch)

- CQ17 Does every anomaly have exactly one model run and one threshold?

     -- Classes:
        Anomaly, ModelRun
     
     -- Object Properties:
        flaggedBy
     
     -- Data Properties:
        thresholdValue

- CQ18 Does every patch belong to exactly one tile, and every tile to exactly one survey?

     -- Classes:
        Patch, Tile, Survey
     
     -- Object Properties:
        partOfTile, hasSurvey

- CQ19 Which anomalies have assessments with different results?

     -- Classes:
        Anomaly, AnomalyAssessment, Agent, AssessmentResult
     
     -- Object Properties:
        hasAssessment, assessedBy, hasAssessmentResult

- CQ20 Which anomalies are in tiles threatened by planned land-use change?

     -- Classes:
        Anomaly, Patch, Tile, ThreatType
     
     -- Object Properties:
        concernsPatch, partOfTile, hasPotentialLandUseChange
