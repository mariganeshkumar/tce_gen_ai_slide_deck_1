# 📂 Jupyter Notebook Guide for Students & Deployments

A collection of tips to ensure notebooks run smoothly and display correctly on GitHub.

---

## 🧹 Student Pre-Release Checklist
Before deploying notebooks to students, complete these steps:

### 1. Clear Code Outputs
Reset all variables and outputs to ensure a clean slate. You can run this automated Python script to clear outputs programmatically:

```python
import json

notebook_path = "hands-on/Perceptron_Hands_ON.ipynb"

with open(notebook_path, 'r', encoding='utf-8') as f:
    nb = json.load(f)

for cell in nb.get('cells', []):
    if cell.get('cell_type') == 'code':
        cell['outputs'] = []
        cell['execution_count'] = None

with open(notebook_path, 'w', encoding='utf-8') as f:
    json.dump(nb, f, indent=1, ensure_ascii=False)
```

### 2. Remove Hints & Boilerplate Answers
Ensure students code solutions from scratch and don't receive unfair answers. Run standard search tools to verify file content:

```bash
git grep "# Hint"
```

---

## 🛠 Troubleshooting: GitHub Rendering Errors

### Case: GitHub Preview Fails (Invalid Notebook: Additional properties are not allowed ('id' was unexpected))

#### 🚨 Symptoms
When viewing a Jupyter notebook (`.ipynb`) in GitHub, the preview fails with:
> Invalid Notebook
> Additional properties are not allowed ('id' was unexpected)

#### 🔍 Cause
Standard notebook schema versions older than `4.5` (e.g. 4.0 through 4.4) don't officially support the `"id"` property in cells. Modern IDEs (VS Code, newer colab) often auto-generate cell `"id"`s, causing the GitHub parser to crash if it's running a strict validator on older schema numbers.

#### 🛠 Fix
Upgrade the schema minor version locally to `5` (version `4.5` permits cell `"id"`).

Run the following script to patch it:

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

---

### Case: GitHub Preview Fails ('outputs' is a required property)

#### 🚨 Symptoms
When viewing a Jupyter notebook (`.ipynb`) in GitHub, the preview fails with:
> Invalid Notebook
> 'outputs' is a required property

#### 🔍 Cause
A code cell is missing the `"outputs"` array entirely (the standard schema expects `[]` if run was cleared).

#### 🛠 Fix
Run the following Python script to scan code cells and restore empty outputs:

```python
import json

notebook_path = "hands-on/Perceptron_Hands_ON.ipynb"

with open(notebook_path, 'r', encoding='utf-8') as f:
    nb = json.load(f)

for cell in nb.get('cells', []):
    if cell.get('cell_type') == 'code' and 'outputs' not in cell:
        cell['outputs'] = []

with open(notebook_path, 'w', encoding='utf-8') as f:
    json.dump(nb, f, indent=1, ensure_ascii=False)
```
