# Drug Response Project Lab Note
```/extraspace/ychen42/Drug_Response/```

## 11/10/2020
### 1. Set up working environment
 Installing packages: ```conda install -c anaconda django```

 Create environment: ```conda env create -f environment_cpu_linux.yml```

 **Activate environment: ```source activate pytorch3drugcell```**

!!Install packages under environment!!



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



# 11/15/2020



conda create -n myenv

source activate myenv

R

install.packages("car")



Installing SVA: ``` conda install -c bioconda bioconductor-sva```

Installing MGCV : ```conda install r-mgcv```



Gene expression data: ```/extraspace/ychen42/Drug_Response/Bohans Input data/CCLE_expression_profile.txt```

Drug response matrix: ```/extraspace/ychen42/Drug_Response/Bohans Input data/GDSC_AUC_matrix.txt```

Installing R packages on server: conda install -c bioconda bioconductor-genefilter

conda install r-dplyr

conda install -c bioconda bioconductor-sva

conda install -c bioconda bioconductor-RDRToolbox

conda install r-kernlab

conda install r-mice

time Rscript file\ processing.R



```
 sort -n -k4 -t, orders.csv
```

| option | explanation                      |
| :----- | :------------------------------- |
| `-n`   | sort numerically                 |
| `-k4`  | sort on the 4th field            |
| `-t,`  | use comma as the field separator |



sort -n -k1,1 -k2,2 -k3,3 GDSC_long.txt > GDSC_long_sorted.txt



multiple core:

```
 s <- system.time({
+         mn <- mclapply(specdata, function(df) {
+                 quantile(df$sulfate, 0.9, na.rm = TRUE)
+         }, mc.cores = 4)
+ })
```