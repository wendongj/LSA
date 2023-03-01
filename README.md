# Local Spectral Attention for Full-band Speech Enhancement  

# Contents
- [Repository description](#repository-description)
- [Rquirements](#rquirements)
- [Network training](#network-training)
	- [Data preparation](#data-preparation)
	- [bbb](#bbb)

## 1. Repository description
This repository conduct ablation studies on local attention (a.k.a band attention) applied in full-band spectrum, namely local spectral attention (LSA). Two full-band speech enhancement (SE) models with spectral attention replace the conventional attention (a global manner) with LSA that only looks at adjacent bands at a certain frequency (a local manner). One model is our previous work called DPARN, whose source code can be found in   
https://github.com/Qinwen-Hu/dparn.   
The other model is the Multi-Scale Temporal Frequency with Axial Attention (MTFAA) network, which ranked 1st in the DNS-4 challenge for full-band SE, and its detailed description can be found in paper  
https://ieeexplore.ieee.org/document/9746610.  
Here we release an unofficial pytorch implementation of MTFAA as well as its modification.  

## 2. Rquirements
soundfile: 0.10.3  
librosa:   0.8.1  
torch:     3.7.10  
numpy:     1.20.3  
scipy:     1.7.2  
pandas:    1.3.4  
tqdm:      4.62.3  

## 3. Network training
### 3.1. Data preparation
Split your speech and noise audios into 10 seconds segments and generate the .csv files to manage your data. Edit the .csv path in [Dataloader.py](https://github.com/ZhongshuHou/LSA/blob/main/Dataloader.py)

