flowchart TD
    A[Start: Sub15 “Famous” EEG] --> B{Inverse Solver}
    B --> B1[IID (min‐norm)]
    B --> B2[GS (MSP)]
    
    subgraph Mesh
      B1 --> C1[Template mesh<br/>(with headpoints)]
      B1 --> C2[Individual‐MRI mesh<br/>(no headpoints)]
      B2 --> C1b[Template mesh<br/>(with headpoints)]
      B2 --> C2b[Individual‐MRI mesh<br/>(no headpoints)]
      C1 --> D1[Winner by free energy]
      C2 --> D1
      C1b --> D2[Winner by free energy]
      C2b --> D2
    end

    subgraph ForwardModel
      D1 --> E1[3‐Sphere]
      D1 --> E2[BEM]
      D2 --> E1b[3‐Sphere]
      D2 --> E2b[BEM]
      E1 --> F1[Winner by free energy]
      E2 --> F1
      E1b --> F2[Winner by free energy]
      E2b --> F2
    end

    subgraph Priors
      F1 --> G1[No priors]
      F1 --> G2[fMRI priors]
      F2 --> G1b[No priors]
      F2 --> G2b[fMRI priors]
      G1 --> H1[Winner by free energy]
      G2 --> H1
      G1b --> H2[Winner by free energy]
      G2b --> H2
    end

    H1 --> I[Final IID model]
    H2 --> J[Final GS model]
    I --> K{Compare IID vs GS free energy}
    J --> K
    K --> L[Select overall winner: GS + MRI + BEM + No priors]
