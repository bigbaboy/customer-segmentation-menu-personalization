# Customer Segmentation & Menu Personalization

An academic Streamlit application exploring how customer interaction history can inform restaurant menu recommendations and placement.

**Context:** Individual academic project by Lê Minh Đạt. I designed and implemented the application, with AI tools assisting parts of the coding.

## Business question

Can browsing and ordering behavior help distinguish customer preferences and organize menu suggestions? The prototype explores this question using behavioral features, KMeans clustering and configurable recommendation rules.

## Implemented features

- Load five related worksheets from `final_with_new_items.xlsx`.
- Derive customer features from viewing duration, interest in recently launched items, revisits, order diversity and menu zones.
- Standardize features and fit KMeans with four clusters.
- Assign heuristic segment labels: Explorers, Conservatives, Impulsive and Loyalists.
- Recommend items to existing customers using segment-specific rules.
- Distribute recommendations across five menu positions: Top-Left, Center, Top-Right, Bottom-Left and Bottom-Right.
- Collect manually entered interactions for new customers and show zone-based suggestions after an interaction-time threshold.
- Display segment distributions with Plotly.

## Important implementation distinction

`recommend_knn()` defines a nearest-neighbor recommendation method using similar customers' orders. The current UI does **not** call this function. New-customer suggestions currently use entered interaction durations and menu zones, not the KNN function. Facial expression and head pose are manually selected fields; no camera-based emotion or gaze recognition is implemented.

## Data and workflow

| Worksheet | Role |
| --- | --- |
| `Menu_Items` | Item metadata, category, menu zone and launch date |
| `Menu_Interaction` | Browsing duration, revisits and session interactions |
| `Session_Outcome` | Customer/session mapping and decision time |
| `Order_Details` | Items associated with sessions |
| `Customers` | Customer identifiers |

The main script is `streamlit_app3.py`. See [Implementation flow](docs/flow.md) for the two active UI paths.

## Run locally

```bash
git clone https://github.com/bigbaboy/customer-segmentation-menu-personalization.git
cd customer-segmentation-menu-personalization
python -m venv .venv
```

Activate `.venv`, then run:

```bash
python -m pip install -r requirements.txt
python -m streamlit run streamlit_app3.py
```

Keep `final_with_new_items.xlsx` in the repository root. Dependencies include Streamlit, pandas, scikit-learn, Plotly and openpyxl. These instructions were checked against file paths and imports, not a complete runtime test.

## Demo walkthrough

1. Select the existing-customer mode and choose a customer ID.
2. Inspect its assigned segment and the suggested menu placements.
3. Switch to the new-customer mode and enter interaction durations and zones.
4. After the threshold is reached, inspect suggestions and try the accept/reject controls.

## Assumptions and limitations

- Segment names are heuristic interpretations of cluster centers, not validated customer personas. The assignment rules can select the same cluster for multiple labels and need stronger conflict handling.
- New-item eligibility depends on today's date. An old workbook can produce an empty recommendation pool.
- The private Streamlit `RerunException` API used by the script may be incompatible with other versions.
- Empty histories, missing features and small datasets need additional validation.
- No conversion uplift, recommendation accuracy or production experiment is established by this repository.

## Next steps

- [ ] Make the evaluation date configurable for reproducible demonstrations.
- [ ] Connect and compare the existing KNN method with the rule-based recommendations.
- [ ] Add tests for empty pools, repeated segment labels and missing customer history.
- [ ] Add screenshots from the running application.
