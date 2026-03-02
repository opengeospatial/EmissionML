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

  class SourceFeature {
    +name: String
    +geometry: GM_Object
  }
  class SourceFeatureType {
    +name: String
    +description: String
  }

  class Mechanism {
    <<CodeList>>
  }
  class EmissionIntent {
    <<CodeList>>
    +intentional
    +unintentional
    +unknown
  }
  class AbstractDeterminationMethod {
    <<abstract>>
    +label: String
    +definition: URI
  }
  class TemporalDeterminationMethod
  class QuantityDeterminationMethod

  %% --- Relationships (Updated) ---

  %% --- EmissionEvent is the central assertion ---
  EmissionEvent "1" *-- "1" EmissionQuantity : hasQuantity
  EmissionEvent "1" o-- "1" TemporalBound : startTime
  EmissionEvent "1" o-- "0..1" TemporalBound : endTime
  EmissionEvent "1" --> "1" SourceFeature : hasSource
  EmissionEvent "1" --> "1" Mechanism : hasMechanism

  %% --- Provenance: Assertions are based on Evidence (Observations) ---
  EmissionQuantity "1" --> "0..*" Observation : hasEvidence
  TemporalBound "1" --> "0..*" Observation : hasEvidence

  %% --- Observation is of a SourceFeature ---
  Observation "1" --> "1" SourceFeature : featureOfInterest

  %% --- Quantities and Times have their own methods ---
  EmissionQuantity "1" *-- "1" UnitOfMeasure : hasUnit
  EmissionQuantity "1" --> "1" QuantityDeterminationMethod : hasDeterminationMethod
  TemporalBound "1" --> "1" TemporalDeterminationMethod : hasDeterminationMethod

  %% --- Determination Methods Inheritance ---
  TemporalDeterminationMethod --|> AbstractDeterminationMethod
  QuantityDeterminationMethod --|> AbstractDeterminationMethod

  %% --- SourceFeatures and their Types ---
  SourceFeature "1" --> "1" SourceFeatureType : hasType

  %% --- "Honor System" Constraint ---
  SourceFeatureType "1" --> "0..*" Mechanism : allowedMechanism

  %% --- Mechanism defines Intent ---
  Mechanism ..> EmissionIntent : hasIntent
