# MIR

A PyTorch implementation of RL-MolGAN: RL-based Transformer GAN for Molecular Generation: A Reinforcement Learning-Driven Transformer GAN for Molecular Generation.


## Installation
First, download the code.  
Then, execute the following command:
```
$ conda env create -n MIR_env -f env.yml
$ source activate MIR_env
```
Next, unzip the **DRD2_score.sav.zip** to  **DRD2_score.sav**.


## File Description

  - **datasets:** contains the original datasets and preprocessed datasets. Each dataset contains three columns, separated by ";" into scaffolds, decorations, and SMILES strings.
	  - QM9_10k_LEN_3.csv
    	  - GEN_QM9_10k_LEN_3.csv
	  - ZINC_10k_LEN_10.csv
    	  - GEN_ZINC_10k_LEN_10.csv
  - **results:** all generated datasets, saved models, and experimental results are saved in this folder.
	  - **save_models:** all training results, pre-trained and trained filler and discriminator models are saved in this folder.
	  - **test:** all test results are saved in this folder.

## Experimental Reproduction

  - MIR on the QM9 dataset with drug-likeness as the optimized property:
  ``` 
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train
  ```
  - MIR on the QM9 dataset with solubility as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --properties 'solubility'
  ```
  - MIR on the QM9 dataset with synthesizability as the optimized property:
  ```  
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --properties 'synthesizability'
  ```
  - MIR on the ZINC dataset with drug-likeness as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dataset_name 'ZINC_10k' --dec_min_len 10 --filler_epochs 200 --decoration_max_len 50 --filler_d_model 256 --filler_max_lr 1e-4 --filler_optimizer 'Adam' --adv_epochs 50
  ```
  - MIR on the ZINC dataset with solubility as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dataset_name 'ZINC_10k' --dec_min_len 10 --filler_epochs 200 --decoration_max_len 50 --filler_d_model 256 --filler_max_lr 1e-4 --filler_optimizer 'Adam' --adv_epochs 50 --properties 'solubility'
  ```	
  - MIR on the ZINC dataset with synthesizability as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dataset_name 'ZINC_10k' --dec_min_len 10 --filler_epochs 200 --decoration_max_len 50 --filler_d_model 256 --filler_max_lr 1e-4 --filler_optimizer 'Adam' --adv_epochs 50 --properties 'synthesizability'
  ```
  - WGAN on the QM9 dataset with drug-likeness as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dis_wgan --dis_minibatch --dis_max_lr 1e-4
  ```
  - WGAN on the QM9 dataset with solubility as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dis_wgan --dis_minibatch --properties 'solubility' --dis_max_lr 1e-4
  ```
  - WGAN on the QM9 dataset with synthesizability as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dis_wgan --dis_minibatch --properties 'synthesizability' --dis_max_lr 1e-4
  ```
  - WGAN on the ZINC dataset with drug-likeness as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dis_wgan --dis_minibatch --dataset_name 'ZINC_10k' --dec_min_len 10 --filler_epochs 200 --decoration_max_len 50 --filler_optimizer 'Adam' --filler_d_model 256 --filler_max_lr 1e-4 --dis_max_lr 1e-4 --adv_epochs 50
  ```
  - WGAN on the ZINC dataset with solubility as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dis_wgan --dis_minibatch --dataset_name 'ZINC_10k' --dec_min_len 10 --filler_epochs 200 --decoration_max_len 50 --filler_optimizer 'Adam' --filler_d_model 256 --filler_max_lr 1e-4 --dis_max_lr 1e-4 --adv_epochs 50 --properties 'solubility'
  ```
  - WGAN on the ZINC dataset with synthesizability as the optimized property:
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dis_wgan --dis_minibatch --dataset_name 'ZINC_10k' --dec_min_len 10 --filler_epochs 200 --decoration_max_len 50 --filler_optimizer 'Adam' --filler_d_model 256 --filler_max_lr 1e-4 --dis_max_lr 1e-4 --adv_epochs 50 --properties 'synthesizability'
  ```

## Case Studies on Optimization of Bioactivity (BIO)
  
  - Training process on the ZINC dataset using MIR
  ```
  $ python main.py --filler_pretrain --dis_pretrain --adversarial_train --dataset_name 'ZINC_10k' --dec_min_len 10 --filler_epochs 200 --decoration_max_len 50 --filler_d_model 256 --filler_max_lr 1e-4 --filler_optimizer 'Adam' --adv_epochs 50 --properties 'DRD2'
  ```
  - Test process on the ZINC dataset using SpotGAN: we provide five scaffolds and generate novel molecules with high biological activities on them. The scaffold names can be set to A1, A2, B1, B2, B3, C1, C2, D1, D2, D3, D4, E1, and E2. Numbers represent the number of attachment points on the given scaffold. Experimental results can be reproduced using A2, B3, C2, D4, and E2.
  ```
  $ python main.py --test --scaffold_name 'A2'
  $ python main.py --test --scaffold_name 'B3'
  $ python main.py --test --scaffold_name 'C2'
  $ python main.py --test --scaffold_name 'D4'
  $ python main.py --test --scaffold_name 'E2'
  ```
  
  ```
