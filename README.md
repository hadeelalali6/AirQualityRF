# Air Quality Classification Using Random Forest

## Project Overview
# Air Quality Classification Using Random Forest

## Hyperparameter Optimization Techniques Comparison

### 1. Project Overview

المشروع عبارة عن بناء نموذج **Random Forest Classifier** لتصنيف جودة الهواء بالاعتماد على مجموعة من الخصائص البيئية.

الهدف الأساسي هو مقارنة خمس تقنيات من **Hyperparameter Optimization** لمعرفة أي تقنية تستطيع إيجاد أفضل إعدادات للنموذج بأعلى أداء وأقل **Computational Cost**.

التقنيات المستخدمة:

1. Grid Search
2. Random Search
3. Bayesian Optimization
4. Genetic Algorithm
5. Particle Swarm Optimization

---

### 2. Classification Problem

المشروع عبارة عن **Multiclass Classification**، لأن النموذج يتنبأ بأربع فئات:

| Class | Description |
|---|---|
| Good | جودة الهواء جيدة |
| Moderate | جودة الهواء متوسطة |
| Poor | جودة الهواء سيئة |
| Hazardous | جودة الهواء خطيرة |

### 3. Machine Learning Model

**Random Forest Classifier**

هو نموذج من نوع **Ensemble Learning** يعتمد على مجموعة من **Decision Trees**.

كل شجرة تقوم بعملية **Prediction**، وبعدها يتم تحديد الفئة النهائية باستخدام **Majority Voting**.

اخترنا هذا النموذج لأنه:

- يستطيع التعامل مع **Non-linear Relationships**.
- يساعد في تقليل **Overfitting** مقارنة باستخدام شجرة واحدة.
- مناسب لمشكلات **Multiclass Classification**.
- يحتوي على عدة **Hyperparameters** يمكن تحسينها.

استخدمنا نفس **Random Forest Model** في جميع التجارب حتى تكون المقارنة بين تقنيات التحسين عادلة.

### 4. Project Workflow

**Step 1: Data Loading**

تحميل الـ Dataset باستخدام مكتبة Pandas.

**Step 2: Data Inspection**

فحص البيانات من ناحية:

- Missing Values
- Duplicate Records
- Class Distribution
- Features

**Step 3: Data Preprocessing**

تجهيز البيانات للتدريب والتعامل مع المشاكل الموجودة فيها.

**Step 4: Feature and Target Separation**

فصل الـ Features عن الـ Target الذي يمثل مستوى جودة الهواء.

**Step 5: Train-Test Split**

تقسيم البيانات إلى:

- Training Set: 80%
- Testing Set: 20%

مع استخدام **Stratified Split** للحفاظ على نسب الفئات.

**Step 6: Baseline Model**

تدريب Random Forest باستخدام Default Hyperparameters للحصول على نتائج مرجعية.

**Step 7: Hyperparameter Optimization**

تطبيق كل تقنية للبحث عن أفضل Hyperparameters.

**Step 8: Model Evaluation**

تقييم النموذج المحسّن ومقارنته مع Baseline Model.

---

### 5. Hyperparameters Used

استخدمنا سبعة Hyperparameters في مساحة البحث:

| Hyperparameter | Values | Purpose |
|---|---|---|
| n_estimators | 100, 200 | تحديد عدد Decision Trees |
| max_features | sqrt, None | تحديد عدد Features المستخدمة عند كل Split |
| max_depth | 10, None | تحديد أقصى عمق للشجرة |
| max_leaf_nodes | 50, None | تحديد أقصى عدد Leaf Nodes |
| max_samples | 0.8, None | تحديد حجم العينة المستخدمة لتدريب كل شجرة |
| min_samples_split | 2, 5 | تحديد أقل عدد Samples مطلوب لتنفيذ Split |
| criterion | gini, entropy | تحديد طريقة قياس جودة الـ Split |

كل Hyperparameter يحتوي على قيمتين، وبالتالي:

**Total Combinations = 2⁷ = 128**

### 6. Optimization Techniques

#### 6.1 Grid Search

**Concept**

تعتمد Grid Search على تجربة جميع Hyperparameter Combinations الموجودة داخل Search Space.

في مشروعنا:

- Total Combinations: 128
- Cross-Validation: 3 Folds
- Total CV Fits: 384

**How It Works**

تجرب الخوارزمية كل Combination، وتحسب Macro F1-Score باستخدام Cross-Validation، ثم تختار الإعدادات التي تحقق أعلى متوسط Score.

**Advantages**

- تفحص جميع التركيبات المحددة.
- تعطي مقارنة شاملة بين الحلول.

**Disadvantages**

- تحتاج Execution Time مرتفعًا.
- تزداد Computational Cost عند زيادة عدد Hyperparameters.

#### 6.2 Random Search

**Concept**

تختار Random Search مجموعة عشوائية من Hyperparameter Combinations بدل تجربة جميع الاحتمالات.

في مشروعنا:

- Number of Iterations: 32
- Cross-Validation: 3 Folds
- Total CV Fits: 96

**How It Works**

تختار 32 Combination عشوائيًا من Search Space، ثم تقيم أداء كل Combination باستخدام Macro F1-Score.

**Advantages**

- تقلل Execution Time.
- تحتاج عددًا أقل من Model Evaluations.

**Disadvantages**

- ممكن ألا تختار أفضل Combination.

#### 6.3 Bayesian Optimization

**Concept**

تعتمد Bayesian Optimization على نتائج Previous Trials لتحديد أي Hyperparameters يجب تجربتها لاحقًا.

في مشروعنا:

- Number of Trials: 32
- Startup Trials: 8
- Cross-Validation: 3 Folds
- Library: Optuna

**How It Works**

تبدأ الخوارزمية بعدد من Initial Trials، ثم تستخدم نتائجها لتوجيه Search Process نحو Configurations واعدة.

**Advantages**

- تستفيد من Previous Evaluations.
- تستطيع الوصول إلى Good Configurations بعدد تجارب محدود.

**Disadvantages**

- أكثر تعقيدًا من Grid Search وRandom Search.

#### 6.4 Genetic Algorithm

**Concept**

تعتمد Genetic Algorithm على Evolutionary Optimization، حيث تمثل كل مجموعة Hyperparameters حلًا يسمى Individual.

في مشروعنا:

- Population Size: 8
- Generations: 4
- Crossover Rate: 0.8
- Mutation Rate: 0.1
- Candidate Evaluations: 32

**Main Operations**

**1. Selection**

اختيار Individuals ذات Fitness Score مرتفع.

**2. Crossover**

دمج أجزاء من Parent Solutions لإنشاء Offspring جديدة.

**3. Mutation**

إجراء Random Changes على بعض Hyperparameters للحفاظ على Diversity.

**How It Works**

تبدأ الخوارزمية بـ Initial Population، ثم تستخدم Selection وCrossover وMutation لتطوير الحلول عبر Generations.

**Advantages**

- تستكشف مناطق مختلفة من Search Space.
- تساعد Mutation في المحافظة على Diversity.

**Disadvantages**

- تعتمد النتائج على Population Size وNumber of Generations.

#### 6.5 Particle Swarm Optimization

**Concept**

تعتمد Particle Swarm Optimization على Swarm Intelligence.

كل Particle يمثل Hyperparameter Configuration، ويتحرك داخل Search Space للبحث عن أفضل Solution.

في مشروعنا:

- Swarm Size: 8
- Iterations: 4
- Inertia Weight (W): 0.7
- Cognitive Coefficient (C1): 1.5
- Social Coefficient (C2): 1.5
- Candidate Evaluations: 32

**Main Components**

**1. Position**

تمثل Hyperparameter Configuration الحالية للجسيم.

**2. Velocity**

تحدد اتجاه حركة Particle داخل Search Space.

**3. Personal Best (pBest)**

أفضل Solution وصل إليه Particle خلال التجارب السابقة.

**4. Global Best (gBest)**

أفضل Solution وصلت إليه جميع Particles.

**How It Works**

تبدأ الخوارزمية بمجموعة Particles، ثم يتم تحديث Velocity وPosition اعتمادًا على pBest وgBest، بهدف الوصول إلى أفضل Hyperparameter Configuration.

**Advantages**

- تستفيد من Individual Experience وSwarm Experience.
- يمكنها إيجاد Good Solutions بعدد محدود من Evaluations.

**Disadvantages**

- قد يحدث Premature Convergence.
- تتأثر النتائج بإعدادات W وC1 وC2.

---

### 7. Cross-Validation

استخدمنا:

**Stratified 3-Fold Cross-Validation**

يتم تقسيم Training Data إلى ثلاث Folds، مع الحفاظ على Class Distribution.

في كل مرة:

- يتم تدريب النموذج على Foldين.
- يتم تقييمه على Fold واحد.
- تتكرر العملية ثلاث مرات.

ثم نحسب Mean Macro F1-Score.

الهدف هو تقييم Hyperparameter Configuration على عدة تقسيمات بدل الاعتماد على تقسيم واحد.

### 8. Evaluation Metrics

| Metric | Explanation |
|---|---|
| Accuracy | نسبة Correct Predictions من جميع Predictions |
| Precision | نسبة True Positives من جميع العينات المتوقعة لفئة معينة |
| Recall | نسبة True Positives من العينات الفعلية للفئة |
| F1-Score | Harmonic Mean بين Precision وRecall |
| Macro F1-Score | متوسط F1-Score لجميع Classes بأوزان متساوية |
| ROC-AUC | قياس قدرة النموذج على التمييز بين Classes |
| Log Loss | قياس جودة Predicted Probabilities |
| Optimization Time | الوقت المستغرق لتنفيذ Hyperparameter Search |

**Main Optimization Metric: Macro F1-Score**

اخترنا Macro F1-Score لأنه يعطي جميع Classes أهمية متساوية، حتى لو كان هناك Class Imbalance.

### 9. Experimental Results

#### Baseline Random Forest

| Metric | Result |
|---|---:|
| Test Accuracy | 95.10% |
| Test Macro F1-Score | 92.36% |
| CV Macro F1-Score | 93.11% |

#### Hyperparameter Optimization Comparison

| Optimization Technique | Best CV Macro F1 | Test Macro F1 | Optimization Time |
|---|---:|---:|---:|
| Grid Search | 93.49% | 92.24% | 230.20 s |
| Random Search | 93.32% | 92.30% | 55.28 s |
| Bayesian Optimization | 93.37% | 92.32% | 51.66 s |
| Genetic Algorithm | 93.13% | 92.24% | 59.02 s |
| Particle Swarm Optimization | 93.49% | 92.24% | 66.28 s |

### 10. Results Discussion

**Grid Search**

حققت واحدة من أعلى قيم CV Macro F1-Score، لكنها كانت الأبطأ بسبب تقييم جميع Combinations.

**Random Search**

قللت Optimization Time بشكل كبير، مع المحافظة على Performance قريب من Grid Search.

**Bayesian Optimization**

حققت أقل Optimization Time، وأعلى Test Macro F1-Score بين Optimized Models.

**Genetic Algorithm**

حققت تحسنًا بسيطًا في CV Macro F1-Score مقارنة مع Baseline Model.

**Particle Swarm Optimization**

حققت نفس Best CV Macro F1-Score الخاصة بـ Grid Search، لكن بعدد أقل من Candidate Evaluations.

**Important Observation**

جميع Optimization Techniques حسّنت CV Macro F1-Score، لكن لم تتمكن أي منها من تحسين Test Macro F1-Score مقارنة مع Baseline Model.

هذا يوضح أن تحسين Cross-Validation Performance لا يضمن بالضرورة تحسين Generalization Performance.

### 11. Conclusion

قمنا بمقارنة خمس Hyperparameter Optimization Techniques باستخدام نفس Random Forest Classifier.

**Key Findings**

- Grid Search وParticle Swarm Optimization حققتا أعلى CV Macro F1-Score.
- Bayesian Optimization حققت أقل Optimization Time.
- Particle Swarm Optimization وصلت إلى نفس أفضل CV Score للبحث الشامل باستخدام عدد أقل من Evaluations.
- Baseline Random Forest حقق أعلى Test Macro F1-Score.

**Final Conclusion**

Hyperparameter Optimization لا يضمن دائمًا تحسين Test Performance.

لذلك يجب المقارنة بين Optimization Techniques بناءً على ثلاثة عوامل:

- Model Performance
- Computational Cost
- Generalization Ability

### 12. Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Optuna
- Matplotlib
- Jupyter Notebook

### 13. Project Notebooks

| Notebook | Technique |
|---|---|
| 01-grid-search | Grid Search |
| 02-random-search | Random Search |
| 03-bayesian-optimization | Bayesian Optimization |
| 04-genetic-algorithm | Genetic Algorithm |
| 05-particle-swarm-optimization | Particle Swarm Optimization |
This project aims to classify air quality levels using the Random Forest algorithm and evaluate the impact of optimization and hyperparameter tuning on model performance.

## Dataset

The dataset contains 5,000 samples and 9 input features related to environmental conditions and air pollution.

### Features

- Temperature
- Humidity
- PM2.5
- PM10
- NO2
- SO2
- CO
- Proximity to Industrial Areas
- Population Density

### Target Classes

| Class | Samples |
|---|---:|
| Good | 2,000 |
| Moderate | 1,500 |
| Poor | 1,000 |
| Hazardous | 500 |
| **Total** | **5,000** |

## Methodology

- Data inspection and preprocessing
- Exploratory Data Analysis (EDA)
- Label encoding
- Stratified train-test split
- Random Forest classification
- Optimization and hyperparameter tuning
- Model evaluation and performance comparison

## Model Configuration

| Parameter | Value |
|---|---|
| Algorithm | Random Forest |
| Task | Multiclass Classification |
| Training Set | 80% |
| Testing Set | 20% |
| Random State | 42 |
| Cross-Validation | 3 Folds |

## Evaluation Metrics

- Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC
- Log Loss
- Out-of-Bag Score and Error
- Confusion Matrix
- Execution Time

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Kaggle Notebooks
