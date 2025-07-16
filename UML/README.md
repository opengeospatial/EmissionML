Store UML content in this directory. Feel free to use any organizational scheme that you like.

Note: Mermaid doesn't fully support UML syntax. This is for visualization and discussion only.

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
