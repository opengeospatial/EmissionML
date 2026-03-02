Store UML content in this directory. Feel free to use any organizational scheme that you like.

Note: Mermaid doesn't fully support UML syntax. This is for visualization and discussion only.

## EmissionML UML 2026-02-04

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

## EmissionML UML 2026-01-27
```mermaid
classDiagram
 %% title "EmissionML Refined Model (Updated)"

  class EmissionEvent {
    +pollutantType: URI
  }
  class EmissionQuantity {
    +quantity: double
    +quality: DQ_Element
  }
  class UnitOfMeasure {
    +name: String
    +symbol: String
    +definition: URI
  }
  class TemporalBound {
    <<ValueObject>>
    +time: TM_Instant
    +quality: DQ_Element
  }

  class Observation {
    <<ISO 19156:2023>>
    +result: any
    +time: TM_Instant
  }

  class Source {
    <<Feature>>
    +name: String
    +geometry: GM_Object
  }
   %% class SourceType {
    %%  +name: String
    %% +description: String
  %% }

  class Mechanism {
    <<CodeList>>
  }
  class EmissionIntent {
    <<CodeList>>
    +intentional
    +unintentional
    +unknown
  }
  class DeterminationMethod {
    +label: String
    +definition: URI
  }
  
  %% --- Relationships (Updated) ---

  %% --- EmissionEvent is the central assertion ---
  EmissionEvent "1" *-- "1" EmissionQuantity : hasQuantity
  EmissionEvent "1" o-- "1" TemporalBound : startTime
  EmissionEvent "1" o-- "0..1" TemporalBound : endTime
  EmissionEvent "0..*" --> "1" Source : hasSource
  EmissionEvent "0..*" --> "1" Mechanism : hasMechanism

  %% --- Provenance: Assertions are based on Evidence (Observations) ---
  EmissionQuantity "1" --> "0..*" Observation : hasEvidence
  TemporalBound "1" --> "0..*" Observation : hasEvidence

  %% --- Observation is of a SourceFeature ---
  Observation "0..*" --> "1" Source : ultimateFeatureOfInterest

  %% --- Quantities and Times have their own methods ---
  EmissionQuantity "1" *-- "1" UnitOfMeasure : hasUnit
  EmissionQuantity "1" --> "1" DeterminationMethod : hasDeterminationMethod
  TemporalBound "1" --> "1" DeterminationMethod : hasDeterminationMethod

  %% --- SourceFeatures and their Types ---
   %% Source "1" --> "1" SourceType : hasType

  %% --- "Honor System" Constraint ---
   %% SourceType "1" --> "0..*" Mechanism : allowedMechanism

  %% --- Mechanism defines Intent ---
  Mechanism ..> EmissionIntent : hasIntent
```

## EmissionML UML 2025-07-16
```mermaid
classDiagram
    class EmissionEvent {
        String name
        EmissionIntent intent
        URI pollutantType
        Mechanism mechanism
    }

    class EmissionQuantity {
        UnitOfMeasure unitOfMeasure
        double quantity
        DQ_Element quality
        URI quantityDeterminationMethod
    }

    class SourceFeature {
        String name
        GM_Object geometry
        CodeList attributionGranularity
        SourceFeatureType sourceFeatureType
        Observation observations[0..*]
    }

    class StartEvent {
        TM_Instant startTime
    }

    class EndEvent {
        TM_Instant endTime
    }

    class Observation

    class DeterminationMethod {
        String label
        URI definition
    }

    class SourceFeatureType {
        String name
        String description
        Mechanism mayEmitVia[0..*]
    }

    class EmissionEventPattern {
        EmissionIntent intent
        TM_Duration expectedDuration
        boolean isRecurring
        TM_Duration recurrenceInterval
        EmissionQuantity expectedQuantity
        URI pollutantType
        Mechanism mechanism
    }

    class UnitOfMeasure {
        String name
        String symbol
        URI definition
    }

    class TemporalBoundEvent {
        DeterminationType determinationType
        DQ_AccuracyOfATimeMeasurement quality
        Observation isObservedBy[0..1]
    }

    class EmissionIntent {
    }

    class Mechanism {
    }

    class DeterminationType {
    }

    %% Inheritance
    StartEvent <|-- TemporalBoundEvent
    EndEvent <|-- TemporalBoundEvent

    %% Associations
    SourceFeature --> SourceFeatureType : hasSourceFeatureType
    SourceFeature --> EmissionEvent : emits
    EmissionEvent --> SourceFeature : isOriginatedFrom
    EmissionEvent --> StartEvent : startEvent
    EmissionEvent --> EndEvent : endEvent
    EmissionEvent --> EmissionQuantity : isQuantifiedBy
    EmissionEvent --> Observation : isObservedBy
    Observation --> SourceFeature : UltimateFeatureOfInterest
    TemporalBoundEvent --> Observation : isObservedBy
    EmissionQuantity --> DeterminationMethod : usesMethod
    TemporalBoundEvent --> DeterminationMethod : usesMethod
    SourceFeatureType --> EmissionEventPattern : hasEmissionEventPattern
    EmissionEventPattern --> SourceFeatureType : hasSourceFeatureType

    %% Annotations (non-renderable)
    %% <<CodeList>> stereotypes not directly supported in Mermaid
    %% <<ISO 19156:2023>> and <<ISO 19157>> noted but not displayed
```


## EmissionML UML 2025-07-04
```mermaid
classDiagram

class EmissionEvent {
  +String name
  +EmissionIntent intent
  +URI pollutantType
}

class SourceFeature {
  +String name
  +GM_Object geometry
  +CodeList attributionGranularity
}

class StartEvent {
  +TM_Instant startTime
  +DeterminationType determinationType
  +DQ_AccuracyOfATimeMeasurement quality
}

class EndEvent {
  +TM_Instant startTime
  +DeterminationType determinationType
  +DQ_AccuracyOfATimeMeasurement quality
}

class EmissionQuantity {
  +UnitOfMeasure unitOfMeasure
  +double quantity
  +DQ_QuantitativeAttributeAccuracy quality
  +URI quantityDeterminationMethod
}

class UnitOfMeasure {
  +String name
  +String symbol
  +URI definition
}

class Observation

class DeterminationMethod {
  +URI uri
  +String label
  +String definition
}

class EmissionIntent {
  <<CodeList>>
  intentional
  unintentional
  unknown
}

class DeterminationType {
  <<CodeList>>
  observation
  inference
  other
}

class Mechanism {
  <<CodeList>>
}

%% Relationships
Mechanism <-- EmissionEvent
SourceFeature "1" --> "0..*" EmissionEvent : emits
EmissionEvent "0..*" --> "1" SourceFeature : isOriginatedFrom
EmissionEvent --> "1" StartEvent : hasStartEvent
EmissionEvent --> "1" EndEvent : hasEndEvent
EmissionEvent --> "1" EmissionQuantity : isQuantifiedBy
EmissionEvent --> "0..*" Observation : isObservedBy
Observation --> "1" SourceFeature : hasUltimateFeatureOfInterest
SourceFeature --> "0..*" Observation
StartEvent --> "0..1" Observation : isObservedBy
EndEvent --> "0..1" Observation : isObservedBy
EmissionQuantity --> DeterminationMethod : usesMethod
StartEvent --> DeterminationMethod : usesMethod
EndEvent --> DeterminationMethod : usesMethod
```

Figures derived from UML diagrams should be placed in the "figures" folder.
