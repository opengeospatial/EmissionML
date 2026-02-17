```mermaid
classDiagram
%% EmissionML Abstract Conceptual Model (2026-02-04)
%% ISO 19103/19107/19108/19156/19157 aligned
%%
%% Type conventions (ISO 19103):
%%   CharacterString - text values
%%   Real - decimal numbers
%%   URI - resource identifiers
%%   Any - unconstrained type
%%
%% Geometry (ISO 19107): GM_Object
%% Temporal (ISO 19108): TM_Instant
%% Quality (ISO 19157): DQ_Element
%% Observation pattern: ISO/OGC 19156:2023 (OMS 3.0)

  class EmissionEvent {
    +pollutantType: URI
  }

  class EmissionQuantity {
    +value: Real
    +quality: DQ_Element [0..*]
  }

  class UnitOfMeasure {
    +label: CharacterString
    +symbol: CharacterString
    +definition: URI
  }

  class TemporalBound {
    +time: TM_Instant
    +quality: DQ_Element [0..*]
  }

  class Observation {
    <<ISO 19156:2023>>
  }
  note for Observation "Observation per ISO/OGC 19156:2023 (OMS 3.0)\nSee standard for complete specification"

  class Source {
    +name: CharacterString [0..1]
    +geometry: GM_Object
  }
  note for Source "Stereotyped as GFI_Feature"

  class SourceType {
    +label: CharacterString
    +description: CharacterString [0..1]
    +definition: URI
  }

  class Mechanism {
    +label: CharacterString
    +description: CharacterString [0..1]
  }

  class EmissionIntent {
    <<CodeList>>
    intentional
    unintentional
    unknown
  }

  class DeterminationMethod {
    +label: CharacterString
    +description: CharacterString [0..1]
    +definition: URI [0..1]
  }

  %% --- Relationships ---

  %% EmissionEvent composition
  EmissionEvent "1" *-- "1" EmissionQuantity : quantity
  EmissionEvent "1" *-- "1" TemporalBound : startTime
  EmissionEvent "1" *-- "0..1" TemporalBound : endTime
  EmissionEvent "*" --> "1" Source : source
  EmissionEvent "*" --> "1" Mechanism : mechanism

  %% Evidence: Observations supporting derived values
  EmissionEvent "1" --> "*" Observation : startTimeEvidence
  EmissionEvent "1" --> "*" Observation : endTimeEvidence
  EmissionEvent "1" --> "*" Observation : quantityEvidence

  %% Basis: How each value was determined
  EmissionEvent "1" --> "1" DeterminationMethod : startTimeBasis
  EmissionEvent "1" --> "0..1" DeterminationMethod : endTimeBasis
  EmissionEvent "1" --> "1" DeterminationMethod : quantityBasis

  %% Observation target
  Observation "*" --> "1" Source : ultimateFeatureOfInterest

  %% Units
  EmissionQuantity "1" *-- "1" UnitOfMeasure : unit

  %% Source classification
  Source "*" --> "0..1" SourceType : type

  %% Mechanism intent
  Mechanism "*" --> "1" EmissionIntent : intent
```

## ISO Alignment Notes

### Referenced Standards

| Standard | Types Used |
|----------|-----------|
| ISO 19103 | `CharacterString`, `Real`, `URI`, `Any` |
| ISO 19107 | `GM_Object` |
| ISO 19108 | `TM_Instant`, `TM_Object` |
| ISO/OGC 19156:2023 (OMS 3.0) | `Observation` (by reference) |
| ISO 19157 | `DQ_Element` |

### Design Decisions

1. **`label` + `definition` pattern**: Classes use `label` for human-readable display and `definition` (URI) as the universal identifier. No `name` property needed — URI provides vocabulary control without requiring local namespace management.

### Changes from Previous Version

1. **Primitive types** aligned to ISO 19103:
   - `String` → `CharacterString`
   - `double` → `Real`
   - `any` → `Any`

2. **CodeList convention**: `EmissionIntent` uses lowercase values per ISO codelist style

3. **Attribute naming**: `quantity` → `value` in EmissionQuantity (more generic)

4. **Observation by reference**: Class shown without attributes; full specification per ISO/OGC 19156:2023 (OMS 3.0)

### Encoding Profiles (to be developed)

| Encoding | Maps ISO types to |
|----------|-------------------|
| JSON | `string`, `number`, GeoJSON geometry, ISO 8601 datetime |
| CSV | String columns, WKT for geometry |
| RDF/TTL | `xsd:string`, `xsd:double`, GeoSPARQL geometry |
| GML | Native ISO/GML types |
