# LabNote
```/extraspace/ychen42/Drug_Response/```
## 11/10/2020
### 1. Set up working environment
 Installing packages: ```conda install -c anaconda django```
 
 Create environment: ```conda env create -f environment_cpu_linux.yml```
 
 Activate environment: ```source activate pytorch3drugcell```

### 2. Ran DrugCell sample
<span style="color:red">**In both linux and MacOS**</span>.

Errors:
./commandline_train.sh
```
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

./commandline_test_cpu.sh
```
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


