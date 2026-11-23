. Project Objective
هدف المشروع هو تصنيف جودة الهواء إلى أربع فئات:

Good – Moderate – Poor – Hazardous

استخدمنا نموذج Random Forest Classifier، وطبقنا خمس تقنيات من Hyperparameter Optimization لمقارنة أدائها من حيث دقة التنبؤ ووقت التنفيذ.
2. Project Workflow
1. Data Preprocessing: فحص البيانات وتنظيفها وتجهيزها.
2. Train-Test Split: تقسيم البيانات إلى 80% تدريب و20% اختبار.
3. Baseline Model: تدريب Random Forest بالإعدادات الافتراضية.
4. Hyperparameter Optimization: تطبيق خمس تقنيات لتحسين إعدادات النموذج.
5. Cross-Validation: استخدام 3-Fold للتحقق من أداء الإعدادات.
6. Model Evaluation: مقارنة النموذج الأساسي بالنماذج المحسّنة.
3. Optimization Techniques
Technique	الفكرة الأساسية
Grid Search	يجرب جميع Hyperparameter Combinations لاختيار الأفضل.
Random Search	يختار 32 Combination عشوائيًا بدل تجربة جميع الاحتمالات.
Bayesian Optimization	يستفيد من Previous Trials لتحديد أفضل إعدادات للتجارب التالية.
Genetic Algorithm	يحسن الحلول باستخدام Selection وCrossover وMutation.
Particle Swarm Optimization	يعتمد على pBest وgBest لتوجيه Particles نحو أفضل حل.

4. Evaluation Metrics
استخدمنا عدة مقاييس:
- Accuracy: نسبة التنبؤات الصحيحة.
- Precision: مدى صحة التنبؤات لكل فئة.
- Recall: قدرة النموذج على اكتشاف العينات الفعلية لكل فئة.
- F1-Score: مقياس يجمع بين Precision وRecall.
- Macro F1-Score: متوسط F1 لجميع الفئات بأوزان متساوية.
- ROC-AUC: قدرة النموذج على التمييز بين الفئات.
- Log Loss: جودة الاحتمالات المتوقعة.
المقياس الأساسي المستخدم في Optimization هو Macro F1-Score.
5. Results Comparison
Technique	CV Macro F1	Test Macro F1	Time
Grid Search	93.49%	92.24%	230.20s
Random Search	93.32%	92.30%	55.28s
Bayesian Optimization	93.37%	92.32%	51.66s
Genetic Algorithm	93.13%	92.24%	59.02s
Particle Swarm	93.49%	92.24%	66.28s

Baseline Model: حقق 92.36% على Test Macro F1.
6. Conclusion
- Grid Search: حقق أعلى CV Score، لكنه الأبطأ.
- Random Search: قلل عدد التجارب ووقت التنفيذ.
- Bayesian Optimization: كان الأسرع وحقق أفضل Test Macro F1 بين النماذج المحسّنة.
- Genetic Algorithm: حقق تحسنًا بسيطًا في CV Score.
- Particle Swarm: حقق نفس أفضل نتيجة Grid Search باستخدام عدد أقل من Evaluations.
الاستنتاج النهائي: رغم تحسن Cross-Validation Results، بقي Baseline Model الأفضل على Test Macro F1، وهذا يوضح أن Hyperparameter Optimization لا يضمن دائمًا تحسين Generalization.
