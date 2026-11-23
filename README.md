# Air Quality Classification Using Random Forest

## Hyperparameter Optimization Techniques Comparison

### 1. Project Overview

يهدف المشروع إلى تصنيف جودة الهواء باستخدام **Random Forest Classifier** إلى أربع فئات:

- Good
- Moderate
- Poor
- Hazardous

الهدف الأساسي هو مقارنة خمس تقنيات من **Hyperparameter Optimization** لمعرفة أي تقنية تحقق أفضل **Model Performance** بأقل **Computational Cost**.

### 2. Project Workflow

1. **Data Preprocessing:** فحص البيانات وتنظيفها وتجهيزها للتدريب.
2. **Train-Test Split:** تقسيم البيانات إلى 80% Training و20% Testing.
3. **Baseline Model:** تدريب Random Forest باستخدام Default Hyperparameters.
4. **Hyperparameter Optimization:** تطبيق خمس تقنيات للبحث عن أفضل Hyperparameters.
5. **Cross-Validation:** استخدام Stratified 3-Fold Cross-Validation لتقييم الإعدادات.
6. **Model Evaluation:** تقييم النماذج المحسّنة ومقارنتها مع Baseline Model.

### 3. Optimization Techniques

| Technique | Description |
|---|---|
| **Grid Search** | يجرب جميع Hyperparameter Combinations لاختيار أفضل إعدادات. |
| **Random Search** | يختار 32 Combination عشوائيًا لتقليل عدد التجارب ووقت التنفيذ. |
| **Bayesian Optimization** | يستخدم Previous Trials لتوجيه البحث نحو إعدادات أفضل. |
| **Genetic Algorithm** | يحسن الحلول عبر Selection وCrossover وMutation. |
| **Particle Swarm Optimization** | يستخدم pBest وgBest لتوجيه Particles نحو أفضل Solution. |

### 4. Evaluation Metrics

| Metric | Description |
|---|---|
| Accuracy | نسبة Correct Predictions من جميع التنبؤات. |
| Precision | مدى صحة Predictions الخاصة بكل Class. |
| Recall | قدرة النموذج على اكتشاف العينات الفعلية لكل Class. |
| F1-Score | يجمع بين Precision وRecall. |
| Macro F1-Score | متوسط F1-Score لجميع Classes بأوزان متساوية. |
| ROC-AUC | يقيس قدرة النموذج على التمييز بين Classes. |
| Log Loss | يقيس جودة Predicted Probabilities. |

**Main Optimization Metric: Macro F1-Score**

استخدمناه لأنه يعطي جميع Classes أهمية متساوية، حتى عند وجود Class Imbalance.

### 5. Experimental Results

#### Baseline Random Forest

| Metric | Result |
|---|---:|
| Test Accuracy | 95.10% |
| Test Macro F1 | 92.36% |
| CV Macro F1 | 93.11% |

#### Optimization Comparison

| Technique | Best CV Macro F1 | Test Macro F1 | Time |
|---|---:|---:|---:|
| Grid Search | 93.49% | 92.24% | 230.20s |
| Random Search | 93.32% | 92.30% | 55.28s |
| Bayesian Optimization | 93.37% | 92.32% | 51.66s |
| Genetic Algorithm | 93.13% | 92.24% | 59.02s |
| Particle Swarm Optimization | 93.49% | 92.24% | 66.28s |

### 6. Results Discussion

- **Grid Search:** حقق أعلى CV Macro F1، لكنه احتاج أطول Execution Time.
- **Random Search:** قلل Computational Cost مع المحافظة على Performance جيد.
- **Bayesian Optimization:** حقق أقل Optimization Time وأفضل Test Macro F1 بين Optimized Models.
- **Genetic Algorithm:** حقق تحسنًا بسيطًا في CV Macro F1 مقارنة مع Baseline.
- **Particle Swarm Optimization:** حقق نفس أفضل CV Score الخاص بـ Grid Search باستخدام عدد أقل من Evaluations.

### 7. Conclusion

أظهرت النتائج أن جميع Optimization Techniques حسّنت CV Macro F1 مقارنة مع Baseline Model، لكن لم تتمكن أي منها من تحسين Test Macro F1.

**Key Findings:**

- أفضل CV Performance: Grid Search وParticle Swarm Optimization.
- أسرع Optimization Technique: Bayesian Optimization.
- أفضل Test Performance: Baseline Random Forest.

**Final Conclusion:**

Hyperparameter Optimization لا يضمن دائمًا تحسين Generalization Performance، لذلك يجب الموازنة بين Model Performance وComputational Cost وExecution Time.

### 8. Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Optuna
- Matplotlib
- Jupyter Notebook
