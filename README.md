# GenScore
GenScore is a generalized protein-ligand scoring framework extended from RTMScore, and it exhibits balanced scoring, ranking, docking and screening powers on multiple datasets.

<div align=center>
<img src="https://github.com/sc8668/GenScore/blob/main/zzz-3.jpg" width="600px" height="300px">
</div> 



### Requirements
   
```
conda create -n genscore python=3.8.11 
conda activate genscore
conda install pytorch==1.11.0 torchvision==0.12.0 torchaudio==0.11.0 cudatoolkit=11.3 -c pytorch
conda install pandas==1.0.3  
conda install prody==2.1.0   -c conda-forge
conda install rdkit==2021.03.5 -c conda-forge
conda install openbabel==3.1.0 -c conda-forge
conda install numpy==1.23.4 # downgrade for pandas compatibility; numpy==1.20.3  looks incompatible
conda install mdanalysis==2.0.0 -c conda-forge
pip install torch-geometric==2.0.3
pip install torch-scatter==2.0.9
pip install torch-sparse==0.6.15
```
### Datasets
[PDBbind](http://www.pdbbind.org.cn)       
[CASF-2016](http://www.pdbbind.org.cn)    
[docking poses for DEKOIS2.0 and DUD-E](https://www.zenodo.org/record/6859325)   
[CSAR NRC-HiQ benchmark](http://www.csardock.org/)    
[Merck FEP benchmark](https://github.com/MCompChem/fep-benchmark)   
[PDBbind-CrossDocked-Core](https://www.zenodo.org/record/5525936)         

### Examples for using the trained model for prediction
```
cd example
```
___# input is protein (need to extract the pocket first)___
```
python genscore.py -p ./1qkt_p.pdb -l ./1qkt_decoys.sdf -rl ./1qkt_l.sdf -gen_pocket -c 10.0 -e gt -m ../trained_models/GT_0.0_1.pth
```
___# input is pocket___
```
python genscore.py -p ./1qkt_p_pocket_10.0.pdb -l ./1qkt_decoys.sdf -e gatedgcn -m ../trained_models/GatedGCN_0.5_1.pth
```
___# calculate the atom contributions of the score___
```
python genscore.py -p ./1qkt_p_pocket_10.0.pdb -l ./1qkt_decoys.sdf -e gatedgcn -ac -m ../trained_models/GatedGCN_ft_1.0_1.pth
```
___# calculate the residue contributions of the score___
```
python genscore.py -p ./1qkt_p_pocket_10.0.pdb -l ./1qkt_decoys.sdf -e gatedgcn -rc -m ../trained_models/GatedGCN_ft_1.0_1.pth
```

