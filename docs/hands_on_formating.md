# 🛠 Hands-On Notebook Formatting Troubleshooting

## Case: GitHub Preview Fails (Invalid Notebook: Additional properties are not allowed ('id' was unexpected))

### 🚨 Symptoms
When viewing a Jupyter notebook (`.ipynb`) in GitHub, the preview fails with an error like:
> Invalid Notebook
> Additional properties are not allowed ('id' was unexpected)
> Using nbformat v5.x and nbconvert v7.x

### 🔍 Cause
The `.ipynb` uses standard schema version `4` (or `4.0` to `4.4`), but edits made by modern tools or IDEs (like VS Code or custom scripts) auto-populate cell `"id"` properties. In older `.ipynb` schema standards, `id` was not allowed. GitHub's strict validator rejects files with cells having `id` if `nbformat_minor` is set to `0` or less than `5`.

### 🛠 Fix
Upgrade `nbformat_minor` from `0` to `5` (to set it to version `4.5` which officially permits the `"id"` field).

Run the following Python script to patch it:

```python
import json

notebook_path = "hands-on/Perceptron_Hands_ON.ipynb"

with open(notebook_path, 'r', encoding='utf-8') as f:
    nb = json.load(f)

# Upgrade nbformat_minor to 5 to permit cell 'id's
nb['nbformat_minor'] = 5

with open(notebook_path, 'w', encoding='utf-8') as f:
    json.dump(nb, f, indent=1, ensure_ascii=False)
```

Push changes to GitHub. The preview should render normally.
