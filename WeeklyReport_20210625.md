# 2021_06_25_WeeklyReport

Detailed daily diary online: https://github.com/EvalunaC/LabNote/blob/main/1.%20Diary%202021-06-21.md

## To-do list last week:
- [x] Discussion on Top Ranked ERBB2 Related Drugs.
- [x] Evaluate VAEN using statistical mesaurements and compare with our methods.
- [x] Apply our methods to clinical datasets VAEN provided.
- [x] Literature review and discussion

## Whats done and current progress:
1. **Method Validation - GR Clinical Data - Discussion on Top Ranked ERBB2 Related Drugs**: 
    - Interaction between predicted top ranked ERBB2 related drugs and ERBB2 were summarized in Google sheet and discussed. 
    - **Conclusion**: Not a good way to evaluation methods. It is repurposing rather than validation, which is off the right track.
2. **Method Validation - GR Clinical Data - Inhibitor Status**: Tried to find other inhibitor status in GR data besides the one used in article. However the related resource only included ERBB2 status, PR status, ER status in BRCA data. 
    - Idea: Find other clinical data with genetic inhibitor status? Can we summarize the validation result given by different clinical data?
3. **Method Validation - VAEN Clinical Data**: 
    1. *(Fig.5)* GSE33072-Erlotinib data in VAEN were used to evaluate our 9 methods.
        - **Method**: 9 methods and VAEN were compared in this analysis. Our GDSC and CCLE were used as training data. GSE33072-Erlotinib were used as testing data. COX regression were performed, p value was obtained by treating prediction as continuous variable rather than binary as in GR article. Survival curve were generated (not matching the p value, just for for illustration). Due to output issue, random forest (RF) was replaced by RF ranger, K neighbor(KNN) by weighted KNN.
        - **Result**: Both p values and survival plots suggested quite different conclusions comparing to the ones from other evaluation methods. In our output RF ranger ranks top 1, while all other methods did not perform good. PLS, GR method, SVM, Lasso GLM were in wrong direction while PLS even showed significance. Others failed to distinguish two groups at all from plot. It needs to be noticed that, using the same input mentioned in previous section, even VAEN itself could not distinguish the two groups. This result may related to the issue mentioned in following section.
        - **Issue: Both in VAEN, RF, and KNN, methods output same predictions given different test data**, which leads to:
            - RF & KNN: All patients have same predicted value. 
            - VAEN: More than half model candidcates are missing.
            - Potential solution: 
                1.  Peer code review.
                2.  Check for input data (for VAEN this is the only difference between the article.) 
    2. *(Fig.5)* GSE20194, GSE65185 were skipped due to similarity to GSE33072. 
    3. *(Fig.4B)* TCGA-STAD sample data survival analysis can be the next step.
    - Idea: *(Fig.2)* Gene Set Enrichment Analysis (GSEA) with Normalized Enrichment Score and P values?
    ```
    Survival plots for 9 methods ordered by p value in Dropbox: /Dropbox/2020.DrugResponse/Results/GSE33072-Erlotinib.pdf 
    ```
4. **Reading Shared Articles**: The methods mentioned in the shared articles can not be directly applied to our data. In my point of view, the articles shared a similarity that they paid lots of effort in method evaluation under biological background, trying to illustrate that their predicted result have significant clinical or biological meaning, which lead to a thought that how can we persuade our readers that our evaluation method can benchmark the methods, although some of which performed better in their own article. The evaluation in articles shows the comprehansive understanding in not only biological data but also in this field, which is my shortness. The paper shared by Qiang (*Hou, Wenpin, et al. "A systematic evaluation of single-cell RNA-sequencing imputation methods." Genome biology 21.1 (2020): 1-30.*) discussed about comparison across methods and input data, which may give a insight of benchmarking.
 

## To-do list next week:
- [ ] Our method validation using VAEN TCGA-STAD sample data.
- [ ] Use validation criteria we used to evaluate RF ranger and KKNN. If performance better will be our replacement of RF and KNN. 
- [ ] Review Qiang's VAEN code, meanwhile Qiang will review mine for VAEN clinical data. 
- [ ] If possible, find other clinical data with inhibitor status.
- [ ] Literature review and discuss about method benchmarking.

## Discussion Needed - Issues and Throughts:
- [ ] What's other potential factors causing the prediction issue?
- [ ] Benchmarking and universality: How do we summary the result from different clinical data? Especially when conclusions differ. If there is a possibility that some methods were only including the validation result that performance good, does it mean that two or three small sample clinical data might not be enough? 
