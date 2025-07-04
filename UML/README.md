Store UML content in this directory. Feel free to use any organizational scheme that you like.
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
