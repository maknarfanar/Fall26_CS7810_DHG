# Hopewell Anomaly Detection Ontology

![all-schemas](relative/path/to/all/schemas)

## Module 1: Core Spatial Objects
![schema-diagram](relative/path/to/schema/diagram)

### Axioms
* `SpatialObject DisjointWith ModelRun DisjointWith Anomaly DisjointWith AnomalyAssessment DisjointWith Result DisjointWith Determination DisjointWith FeatureType` <br />
Top-level structural classes are completely mutually exclusive. Reasoning: Prevents structural individuals from shifting across separate architectural tracks of the pipeline, preventing reasoner contradictions.
* `VerifiedHopewellSite SubClassOf SpatialObject` <br />
A verified Hopewell Site is a type of Spatial Object. Reasoning: Ground-truth sites are spatial entities inheriting standard topographic positioning features.
* `VerifiedHopewellSite SubClassOf hasSiteName exactly 1 xsd:string` <br />
There is exactly one official name accepted for each location. Reasoning: Aligns with standard UNESCO reference lists to enforce identity naming constraints.
* `VerifiedHopewellSite SubClassOf hasLat exactly 1 xsd:double` <br />
Each site points to exactly one representative latitude coordinate value. Reasoning: Bounds the location to a fixed physical reference point on a coordinate map projection.
* `VerifiedHopewellSite SubClassOf hasLong exactly 1 xsd:double` <br />
Each site points to exactly one representative longitude coordinate value. Reasoning: Bounds the location to a fixed physical reference point on a coordinate map projection.

## Module 2: Spatial Metadata Container Grid
![schema-diagram](relative/path/to/schema/diagram)

### Axioms
* `Tile SubClassOf SpatialObject` <br />
A Tile is a type of Spatial Object. Reasoning: Digital Elevation Model files represent specific geographic bounds on a map grid.
* `Tile SubClassOf hasCRS exactly 1 xsd:string` <br />
Each tile belongs to exactly one Coordinate Reference System (CRS). Reasoning: Digital geographic layers require a single, uniform coordinate system grid projection to calculate terrain bounds correctly.
* `Tile SubClassOf hasResolutionInFeet exactly 1 xsd:double` <br />
Each Tile has a single pixel resolution step value measured in feet. Reasoning: Every individual cell in a given LiDAR data grid represents a fixed spatial size.
* `Tile SubClassOf hasCounty exactly 1 xsd:string` <br />
Each tile maps to exactly one administrative county folder. Reasoning: Matches data ingestion directories structured on OGRIP administrative county boundaries.
* `Tile SubClassOf hasPatch exactly 4 Patch` <br />
Each parent Tile file is broken into exactly 4 sub-window matrices. Reasoning: Grid preprocessing logic splits larger tile files into a predictable layout set of four matrices for training.
* `Patch SubClassOf SpatialObject` <br />
A Patch is a type of Spatial Object. Reasoning: Patches maintain local grid coordinate references derived from parent topographic layers.
* `Patch SubClassOf partOf exactly 1 Tile` <br />
Each processing patch matrix points back to exactly one parent Tile. Reasoning: A subset matrix window is cropped entirely from an explicit parent file source without crossing grid lines.
* `Patch SubClassOf hasRow exactly 1 xsd:integer` <br />
Points to exactly one integer entry denoting grid row placement (0 or 1). Reasoning: Identifies vertical cell index coordinates within the grid container.
* `Patch SubClassOf hasColumn exactly 1 xsd:integer` <br />
Points to exactly one integer entry denoting grid column placement (0 or 1). Reasoning: Identifies horizontal cell index coordinates within the grid container.
* `Tile DisjointWith Patch` <br />
A Tile cannot be a Patch, and a Patch cannot be a Tile. Reasoning: A structural parent file container must remain distinct from its processing window pieces.

## Module 3: Human Verification and Assessment Records
![schema-diagram](relative/path/to/schema/diagram)

### Axioms
* `AnomalyAssessment SubClassOf hasAssessedFeature exactly 1 Patch` <br />
An individual evaluation session logs exactly one target patch. Reasoning: Bounds an analyst's workflow view context frame cleanly to a single matrix space.
* `Patch SubClassOf inverse (hasAssessedFeature) max 1 AnomalyAssessment` <br />
A single patch maps back to at most one evaluation record. Reasoning: Blocks duplicate reviews or competing analyst entries from cluttering the same area.
* `AnomalyAssessment SubClassOf hasResult exactly 1 Result` <br />
Each review session generates exactly one result outcome block. Reasoning: Ensures clear tracking where each verification workflow session links to an un-duplicated block of findings.
* `Result SubClassOf hasDetermination exactly 1 Determination` <br />
An assessment result holds exactly one pipeline validation determination category. Reasoning: Enforces a single ultimate status resolution step on a validated file.
* `Result SubClassOf hasFeatureType min 1 FeatureType` <br />
Each logged verification result tracks at least one identifiable landscape feature category. Reasoning: Because window sizes span a large footprint area, entries must list a physical baseline feature, and can hold multiple overlapping categories.
* `Result SubClassOf (:hasDetermination some :EarthworkDetermination and :hasFeatureType only :NonEarthworkFeatureType) or (not (:hasDetermination some :EarthworkDetermination))` <br />
If a verification outcome selects an Earthwork status, it is policed from listing unrelated modern terrain features. Reasoning: Prevents structural cross-contamination. Validated archaeological site records are logic-locked from holding competing modern infrastructure tags, while multi-labeling remains functional for false positives.

## Module 4: Autoencoder Anomalies
![schema-diagram](relative/path/to/schema/diagram)

### Axioms
* `Anomaly SubClassOf generatedBy exactly 1 ModelRun` <br />
An automated anomaly footprint points back to exactly one model run instance. Reasoning: Separate model outputs evaluating identical spatial bounds are isolated as unique individuals to retain model track metadata.
* `Anomaly SubClassOf hasFeatureOfInterest exactly 1 Patch` <br />
An individual anomaly points to exactly one target evaluation patch window. Reasoning: Identifies the precise terrain space flagged by the autoencoder model.
* `Anomaly SubClassOf hasReconError exactly 1 xsd:double` <br />
An anomaly logs exactly one floating-point reconstruction error score. Reasoning: Captures the structural loss metrics used for validation threshold analysis.

## Module 5: Deep Learning Execution Metadata
![schema-diagram](relative/path/to/schema/diagram)

### Axioms
* `ModelRun SubClassOf trainedOn min 1 Tile` <br />
A convolutional autoencoder run requires at least one terrain tile file for its training set. Reasoning: Identifies training scope lineage; models can evaluate across a shared training base.
* `ModelRun SubClassOf processed min 1 Tile` <br />
An individual run evaluates at least one terrain tile matrix block. Reasoning: Execution traces are only captured if a model processes data to parse out anomalies.
* `ModelRun SubClassOf hasSeed exactly 1 xsd:integer` <br />
Tracks exactly one integer seed value. Reasoning: Records pseudorandom configurations to keep deep learning training runs repeatable.
* `ModelRun SubClassOf hasThreshold exactly 1 xsd:double` <br />
Logs exactly one validation error threshold flag. Reasoning: Tracks the specific model filter used to declare an anomaly.

## Module 6: Automated Inference Pipeline (Defined Classes)
![schema-diagram](relative/path/to/schema/diagram)

### Axioms
* `:FlaggedPatch EquivalentTo :Patch and (inverse (:hasFeatureOfInterest) some :Anomaly)` <br />
A patch is dynamically inferred as flagged if an anomaly targets it. Reasoning: Automatically flags intersecting map tiles without relying on manual database scripts.
* `:UnassessedFlaggedPatch EquivalentTo :FlaggedPatch and not (inverse (:hasAssessedFeature) some :AnomalyAssessment)` <br />
An unassessed patch collects anomalies that do not link back to any completed evaluation sessions. Reasoning: Creates a dynamic, reasoner-driven task queue for analysts by hiding previously verified records.
