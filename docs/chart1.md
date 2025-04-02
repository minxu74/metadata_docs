
# This is topic 

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```

``` mermaid
pie title Public Index
    "Used" : 71
    "Available" : 29
```

<div style="display: flex; justify-content: space-between;">


<div style=style="height: 500px;">
``` mermaid
%%{init: {"pie": {"textPosition": 0.5}, "themeVariables": {"pieOuterStrokeWidth": "5px"}, "useMaxWidth":false}, "useWidth":500 }%%
pie title CMIP6Plus Index
    "Datasets" : 386
    "Files" : 85
    "Empty" : 15
```

</div>


<div style="height: 500px;">
```mermaid
%%{init: {"pie": {"textPosition": 0.5}, "themeVariables": {"pieOuterStrokeWidth": "5px"}, "useMaxWidth":false}, "useWidth":500 }%%
pie showData
    title Key elements in Product X
    "Calcium" : 42.96
    "Potassium" : 50.05
    "Magnesium" : 10.01
    "Iron" :  5
```
</div>
</div>

??? note "Comparison Diagrams"

    ```mermaid
    pie showData title CMIP6 Dataset
        "ANL" : 5686552
        "LLNL" : 9057750
        "ORNL" : 5963081
        "Imbalance" :  1
    ```

    ```mermaid
    pie showData title CMIP6 File
        "ANL" : 386
        "LLNL" : 85
        "ORNL" : 15
        "Imbalance" : 1
    ```

