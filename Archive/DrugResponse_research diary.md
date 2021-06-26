# Drug Response Project Lab Note
```/extraspace/ychen42/Drug_Response/```

## 11/10/2020
### 1. Set up working environment
 Installing packages: ```conda install -c anaconda django```

 Create environment: ```conda env create -f environment_cpu_linux.yml```

 **Activate environment: ```source activate pytorch3drugcell```**

!!Install packages under environment!!

### 

### 2. Pipeline in GR paper (2017 Geeleher et al.)

![image-20201111113401204](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201111113401204.png)



### 3. Ran DrugCell sample

<span style="color:red">**Errors in both linux and MacOS**</span>:

./commandline_train.sh     **NVIDIA GPU related**

```python
  File "/extraspace/ychen42/Drug_Response/DrugCell-public/code/train_drugcell.py", line 206, in <module>
    train_model(root, term_size_map, term_direct_gene_map, dG, train_data, num_genes, drug_dim, opt.modeldir, opt.epoch, opt.batchsize, opt.lr, num_hiddens_genotype, num_hiddens_drug, num_hiddens_final, cell_features, drug_features)
  File "/extraspace/ychen42/Drug_Response/DrugCell-public/code/train_drugcell.py", line 54, in train_model
    train_label_gpu = torch.autograd.Variable(train_label.cuda(CUDA_ID))
  File "/extraspace/ychen42/Anaconda3/envs/pytorch3drugcell/lib/python3.7/site-packages/torch/cuda/__init__.py", line 178, in _lazy_init
    _check_driver()
  File "/extraspace/ychen42/Anaconda3/envs/pytorch3drugcell/lib/python3.7/site-packages/torch/cuda/__init__.py", line 99, in _check_driver
    http://www.nvidia.com/Download/index.aspx""")
AssertionError:
Found no NVIDIA driver on your system. Please check that you
have an NVIDIA GPU and installed a driver from
http://www.nvidia.com/Download/index.aspx
```

./commandline_test_cpu.sh   **Torch  package related** 
```Python
Traceback (most recent call last):
  File "/extraspace/ychen42/Drug_Response/DrugCell-public/code/predict_drugcell_cpu.py", line 92, in <module>
    predict_dcell(predict_data, num_genes, drug_dim, opt.load, opt.hidden, opt.batchsize, opt.result, cell_features, drug_features)
  File "/extraspace/ychen42/Drug_Response/DrugCell-public/code/predict_drugcell_cpu.py", line 19, in predict_dcell
    model = torch.load(model_file, map_location=lambda storage, location: storage)
  File "/extraspace/ychen42/Anaconda3/envs/pytorch3drugcellcpu/lib/python3.7/site-packages/torch/serialization.py", line 529, in load
    return _legacy_load(opened_file, map_location, pickle_module, **pickle_load_args)
  File "/extraspace/ychen42/Anaconda3/envs/pytorch3drugcellcpu/lib/python3.7/site-packages/torch/serialization.py", line 692, in _legacy_load
    magic_number = pickle_module.load(f, **pickle_load_args)
_pickle.UnpicklingError: invalid load key, 'v'.

```



### Other Methods

1. Iorio et al. (2016) built **elastic net models** to predict the drug IC50 of cancer cell lines given their profiles of gene mutations and expression levels; a range of predictive accuracy is observed, depending on the compound. 
2. Using the same dataset, Corte´s-Ciriano et al. (2016) showed that predictive performance could in some cases be improved using **a random forest model linked to a measure of statistical confidence in each prediction.** 
3. **Deep neural networks** (Baptista et al., 2020; Chiu et al., 2019; Menden et al., 2013; Sakellaropoulos et al., 2019) and **variational autoencoders** (Rampa´sek et al., 2019) have also been applied to drug response prediction, with significant performance gains noted depending on the drug and disease context.

![image-20201111141805245](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201111141805245.png)


### Novel Methods

<span style="color:green">***Dive into DL PyTorch***</span> inspired thoughts:

~~multilayer perceptron(MLP)~~ or GOOGLENET/DenseNet

![image-20201111114043123](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201111114043123.png)


## 11/11/2020

### Model Comparison - Validation Methods

1. Actual drug response AUC vs. Predicted drug response AUC (Cancer Cell Fig. 2A)
2. Waterfall plot of predict performance (Cancer Cell Fig. 2E)
   ![](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201111113027804.png)
3. K-fold cross-validation if necessary. (To increase the sample size)

**11/16/2020 Update: AUC needs threshold, thus might not be good. Use  root mean squared error (RMSE) + 5 fold CV Instead.**






## To Do List
### Data-wise

- [x] Do we need Bohan's Data? (gene exp: CCLE_expression_profile.txt (ask for authorization); drug response: GDSC_AUC_matrix.txt (in package))

- [x] **Ask for Shengli**

### Method-wise

- After using the methods in GR paper and CC paper, dig in DL methods and the methods mentioned in DrugCell paper (in method table)
- Bohan's methods involves ML, the performance of which needs to be improved. (Would DL be better choice?)

- What's Physio-chemical data? 

- Difference between mutation data and expression data? 

- It seems like comparing to Bayesian method, network has better prediction. (A better understanding of the data structure will lay a better foundation of algorithm development)

- [ ] **Bohan's methods**

- [ ] **GR paper repeat** using Bohan's data

- [ ] Drug Cell Debug (who's familiar with NVIDIA GPU coding in Python?)



# 11/15/2020

conda create -n myenv

source activate myenv

R

install.packages("car")



Installing SVA: ``` conda install -c bioconda bioconductor-sva```

Installing MGCV : ```conda install -c r-mgcv```



Gene expression data: ```/extraspace/ychen42/Drug_Response/Bohans Input data/CCLE_expression_profile.txt```

Drug response matrix: ```/extraspace/ychen42/Drug_Response/Bohans Input data/GDSC_AUC_matrix.txt```

Installing R packages on server: conda install -c bioconda bioconductor-genefilter

conda install r-dplyr

conda install -c bioconda bioconductor-sva

conda install -c bioconda bioconductor-RDRToolbox

conda install r-kernlab

conda install r-mice

time Rscript file\ processing.R



## GDSC Data

- [x] Is GDSC_AUC_matrix.imputed.csv and GDSC_AUC_matrix.txt the same file? How was the imputation achieved?

The meaning of values in GDSC data

![image-20201116015234293](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201116015234293.png)

The IC50 and AUC are estimated using a non-linear mixed effect model fitting a sigmoid curve to the experimental dose response data. We are screening a large collection of cell lines with a diverse selection of anti-cancer drugs and consequently observe a wide-range of drug responses in our experimental data. The curve-fitting algorithm readily models sensitivity to a drug that falls within the range of experimental screening concentrations. In many instances however, a significant proportion of cell lines will be only partial responsive or resistant to a given drug within the range of experimental screening concentrations. For completeness we have reported these IC-values but they should be interpreted carefully because the confidence in the reported value is reduced. For certain downstream analyses it may be appropriate to restrict the IC50 value to the reported maximum screening concentration, or use an alternative output such as AUC. 



The model error can be estimated by the **root mean squared error (RMSE)** which is indicative of how far the model approximation deviates from the measured observations. Where the RMSE is > 0.3 the fit is considered poor and the results have been filtered from further analysis.

The screening concentration for each compound can be found in the download page.



**1-GDSC_AUC**

![image-20201116012127418](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201116012127418.png)

percentage of cell **survive**? 



**log(1-GDSC_AUC)**

![image-20201116151342461](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201116151342461.png)



## CCLE Data

**CCLE gene expression** 

![image-20201116151454479](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201116151454479.png)

## Questions

- [ ] Is taking BOX-COX or log a good way to manipulate the data?
- [ ] Is the meaning of the value linear? Is the difference between different value linear?
  - [ ] If so, we can not use log transformation
- [ ] Is DGSC AUC a proper dataset to use?
- [ ] Does normalize the data make sense?

Before using machine learning method, we need to understand the meaning of the data. Because of the data distribution, not all machine learning methods are capable.

![image-20201116152236753](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201116152236753.png)

## Binomial modeling (undergoing)

- Outcome of interest: Drug response AUC (range 0 to 1)
- Predictor: 
  - Cell line, 
  - drug name, GDSC
  - gene symbol, CCLE
  - gene expression level, CCLE
  - **gene symbol*gene expression level**(interaction term) CCLE.
- Time consuming 



## Ridge (undergoing)

Pro: **Deal with collinearity**

Same input 



## Lasso and Elastic-Net Regularized Generalized Linear Models (undergoing)

**Shouldn't use mgaussian if violate normality assumption. Use Binomial Models instead.**

![image-20201116155330310](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201116155330310.png)



## Random forest 

- Use Corte´s-Ciriano et al. (2016), predictive performance could in some cases be improved using **a random forest model linked to a measure of statistical confidence in each prediction.** 

![image-20201116155007886](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201116155007886.png)

## IDWAS (undergoing)

Authorization required. 





**Need to validate:** 

- Multask Elastic Net + PCA Random Forest 
- Xgboost (normality assumption?) https://xgboost.readthedocs.io/en/latest/R-package/xgboostPresentation.html



 Youqiong, aski the meaning of AUC

use GR paper validation data to test the performance.





## validation Datasets

TCGA_BRCA_Gene fpkm profile tumor symbol.txt 

​	gene patient

clinical TCGA_BRCA_NTE.txt her2 inhibitor 

positive negative equivocal intermediate. 





compare code difference: notepad++ plugins compare.

cell line specific to BCRA? 

drug

package needed from jason: glmnet, IDWAS. 





language using: Python? R?

CCLE&GDSC cell line intersect # = 635

https://www.datasciencemadesimple.com/in-operator-in-r/

```
### Create a new variable using %in% operator in R

my_basket1=within(my_basket,{
IS_DAIRY='NO'
IS_DAIRY[ITEM_NAME %in% c('Milk',"Curd","Cheese","Paneer")]='YES'
IS_DAIRY[ITEM_GROUP %in% c("Dairy")]='YES'
IS_DAIRY[ITEM_GROUP %in% c("Fruit","Vegetable")]='NO'
})

my_basket1
```

```
### Drop column using %in% operator in R

my_basket[, !(colnames(my_basket) %in% c("Tax"))]
```

```
### select columns using %in% operator in R

my_basket %>% 
  select_if(names(.) %in% c('Price', 'ITEM_GROUP', 'ITEM_NAME'))
```

![image-20201118070726511](C:\Users\YCHEN42\AppData\Roaming\Typora\typora-user-images\image-20201118070726511.png)



negative binomial

gamma 

beta (r-betareg)

