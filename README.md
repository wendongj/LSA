# Local Spectral Attention for Full-band Speech Enhancement  
![Visualization of local spectral attention](https://user-images.githubusercontent.com/103247057/222057044-e8cdc198-23c2-4fc7-b548-0ec98da8377d.png)

# Contents
- [Repository description](#repository-description)
- [Rquirements](#rquirements)
- [Network training](#network-training)
	- [Data preparation](#data-preparation)
	- [Start training](#start-training)

## Repository description
This repository conduct ablation studies on local attention (a.k.a band attention) applied in full-band spectrum, namely local spectral attention (LSA). Two full-band speech enhancement (SE) models with spectral attention replace the conventional attention (a global manner) with LSA that only looks at adjacent bands at a certain frequency (a local manner). One model is our previous work called DPARN, whose source code can be found in https://github.com/Qinwen-Hu/dparn.   
The other model is the Multi-Scale Temporal Frequency with Axial Attention (MTFAA) network, which ranked 1st in the DNS-4 challenge for full-band SE, and its detailed description can be found in paper https://ieeexplore.ieee.org/document/9746610. Here we release an unofficial pytorch implementation of MTFAA as well as its modification.  

## Rquirements
soundfile: 0.10.3  
librosa:   0.8.1  
torch:     3.7.10  
numpy:     1.20.3  
scipy:     1.7.2  
pandas:    1.3.4  
tqdm:      4.62.3  

## Network training
### Data preparation
Split your speech and noise audios into ***10 seconds segments*** and generate the .csv files to manage your data. Prepare your RIR audios of .wav format in one folder. Edit the .csv path in [Dataloader.py](https://github.com/ZhongshuHou/LSA/blob/main/Dataloader.py):  
```TRAIN_CLEAN_CSV = './train_clean_data.csv'  
   TRAIN_NOISE_CSV = './train_noise_data.csv'  
   VALID_CLEAN_CSV = './valid_clean_data.csv'  
   VALID_NOISE_CSV = './valid_noise_data.csv'  
   RIR_DIR = 'direction to RIR .wav audios'
```
where the .csv files for clean speech are organized as  

|file_dir|snr|
| ---------- | :-----------:  | 
| ./clean_0001.wav | 4 |
| ./clean_0002.wav | -1 |
| ./clean_0003.wav | 0 |
| ... | ... |

and the .csv files for noise are organized as  

|file_dir|
| ---------- |
| ./noise_0001.wav |
| ./noise_0002.wav |
| ./noise_0003.wav |
| ... |

the 'file_dir' and 'snr' denote the absolute direction to audios and signal-to-noise ratio(SNR) respectively.

### Start training
After environment and data preparation, start to train the model by command:  
```
python Network_Training_MTFAA_full.py -m model_to_train(including MTFAA, MTFAA_LSA or MTFAA_ASqBi) -c Dir_to_save_the_checkpoint_files -e Epochs_for_training(default is 300) -d Device_used_for_training(cuda:0)
```
