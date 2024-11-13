# Run HiTE with Nextflow
Here is a tutorial on running the [HiTE](https://github.com/CSU-KangHu/HiTE) using both Docker and Singularity versions with Nextflow.
### Create a new environment
```sh
# install nextflow
1. conda create -n nextflow -c conda-forge -c bioconda nextflow==22.10.6

# download HiTE-Nextflow
2. git clone https://github.com/CSU-KangHu/HiTE-Nextflow.git

# activate nextflow
3. conda activate nextflow
```
### Option 1: Run HiTE nextflow with Singularity
```sh
# If it is the first time you run with singularity (e.g., using -profile singularity), the following cmd will cache the dafault 
# singularity image (docker://kanghu/hite:3.2.0) to the --singularity_cache directory (default: local_singularity_cache) first.
# There will be a .img file in the --singularity_cache directory.

nextflow run main.nf -profile singularity \
--genome ${genome} \
--outdir ${output_dir}

***
# The downloaded .img file can be used then, without being downloaded again.
nextflow run main.nf -profile singularity \
--singularity_cache local_singularity_cache \
--genome ${genome} \
--outdir ${output_dir}

***
# pull singularity image (once for all) before running the cmd.
singularity pull HiTE.sif docker://kanghu/hite:3.2.0
# run HiTE
nextflow run main.nf -profile singularity \
--singularity_name HiTE.sif \
--genome ${genome} \
--outdir ${output_dir}

# e.g., nextflow run main.nf \
#       -profile singularity \
#       --genome /public/home/hpc194701009/HiTE/demo/genome.fa \
#       --outdir /public/home/hpc194701009/HiTE/demo/test
```
### Option 2: Run HiTE nextflow with Docker
```sh
# pull docker image (once for all).
docker pull kanghu/hite:3.2.0

nextflow run main.nf -profile docker \
--genome ${genome} \
--outdir ${output_dir}

# e.g., nextflow run /public/home/hpc194701009/HiTE -profile docker \
#       --genome /public/home/hpc194701009/HiTE/demo/genome.fa \
#       --outdir /public/home/hpc194701009/HiTE/demo/test
```

## Citations
Please cite our paper if you find `HiTE` useful:

Hu, K., Ni, P., Xu, M. et al. HiTE: a fast and accurate dynamic boundary adjustment approach for full-length transposable element detection and annotation. Nat Commun 15, 5573 (2024). [https://doi.org/10.1038/s41467-024-49912-8](https://doi.org/10.1038/s41467-024-49912-8)