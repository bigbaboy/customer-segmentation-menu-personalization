# Menu Recommendation Flow

Retrospective documentation of `streamlit_app3.py`; not an original research artifact or Draw.io export.

```mermaid
flowchart TD
    X["Excel workbook"] --> F["Customer behavioral features"]
    F --> K["Scaling and KMeans"]
    K --> S["Heuristic segment labels"]
    S --> R["Existing-customer rules"]
    R --> Z["Five menu zones"]
```

```mermaid
flowchart TD
    I["Manual interaction input"] --> A["Accumulate viewing duration"]
    A --> T{"Threshold reached?"}
    T -->|No| I
    T -->|Yes| Z["Select items from available zones"]
    Z --> D{"Accept or reject?"}
    D -->|Accept| C["Clear session inputs"]
    D -->|Reject| E["Exclude a zone and rerun"]
```

A separate `recommend_knn()` helper exists in the code but is not connected to these active UI paths. The diagrams intentionally distinguish implemented interface behavior from available experimental functions.
