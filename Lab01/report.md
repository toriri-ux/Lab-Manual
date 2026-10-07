- Performed a 70/30 stratified split with `random_state=42`.

### Models
Two baseline models were trained:

1. **Logistic Regression**  
 `LogisticRegression(max_iter=1000, random_state=42)`

2. **Random Forest Classifier**  
 `RandomForestClassifier(n_estimators=100, random_state=42)`

### Measurements
All measurements follow the lab reproducibility rules:

- **Training time:**  
- 1 warm-up  
- 5 timed runs  
- median reported

- **Inference latency:**  
- single-sample  
- repeated 100 times  
- median reported

- **Model size:**  
- saved using `joblib.dump`  
- size recorded in bytes and KB

- **Peak memory:**  
- measured using `memory_profiler.memory_usage`  
- peak RSS recorded during training

Results were saved to `results/baseline_accuracy.csv`.

---

## 3. Results

| Model | Test Accuracy | Training Time (s) | Peak Memory (MiB) | Inference Time (ms) | Inference Memory (MiB) | Model Size (KB) |
|-------|---------------|-------------------|--------------------|----------------------|-------------------------|------------------|
| Logistic Regression | 0.2822 | 0.2822 | 267.88 | 0.0550 | 266.71 | 1.03 |
| Random Forest | 0.1201 | 0.1201 | 267.19 | 2.2716 | 267.36 | 284.07 |

---

## 4. Deployment Fit Analysis

### Cloud Budget
- Memory ≥ 1 GB  
- Latency ≤ 100 ms  
- Model size ≤ 500 MB  
**Both models fit Cloud deployment easily.**

### Edge Budget
- Memory 256–1024 MB  
- Latency ≤ 50 ms  
- Model size ≤ 50 MB  
**Logistic Regression fits Edge comfortably.**  
Random Forest fits Edge in memory but is significantly larger (284 KB) and slower in inference.

### Mobile Budget
- Memory 64–256 MB  
- Latency ≤ 20 ms  
- Model size ≤ 10 MB  
**Logistic Regression fits Mobile.**  
Random Forest’s inference latency (2.27 ms) is fine, but its memory footprint (~267 MiB) exceeds Mobile limits.

### TinyML Budget
- Memory ≤ 256 KB  
- Latency ≤ 10 ms  
- Model size ≤ 100 KB  
**Neither model fits TinyML.**  
Random Forest is ~284 KB (too large).  
Logistic Regression is small (1 KB) but memory usage (~267 MiB) is far above TinyML constraints.

---

## 5. Conclusions

1. **Logistic Regression is the only model that fits both Edge and Mobile deployment budgets**, thanks to its extremely small size (1 KB) and fast inference (0.055 ms).  
2. **Random Forest is too memory-heavy for Mobile and TinyML**, despite having acceptable inference latency. Its size (284 KB) also exceeds TinyML limits.  
3. **Both models fit Cloud deployment**, but their drastically different resource profiles highlight why model selection must consider deployment constraints, not just accuracy.

---
