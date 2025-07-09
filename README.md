# How to get genome-wide heatmap of FASTQ.hic data using HiGlass

### Where to find .hic file 
- ` cd /research_jude/rgs01_jude/groups/abrahgrp/projects/Software_Dev_Sandbox/common/apatino/HiC_TRANS/CHLA90-Cas9/HicFile`
- look for `fastq.allValidPairs.hic`

### Converting .hic to .mcool
- use hic2cool -> `module load hic2cool`
- `hic2cool -r 10000 /research_jude/.../fastq.allValidPairs.hic CHLA90-Cas9.10k.cool`
- use zoomify -> `module load cooler`
- `cooler zoomify CHLA90-Cas9.10k.cool`

### Copying .mcool to local desktop to avoid using singularity container
- copying into `higlass-data` `scp apatinop@splprhpc12:/research_jude/.../CHLA90-Cas9.10k.mcool ~/higlass-data/`

### Installing docker 
- make sure brew is installed
- `brew install --cask docker`

### Running HiGlass container 
- `docker run -p 8989:80 -v ~/higlass-data:/data higlass/higlass-docker`

### Ingesting .mcool file into HiGlass
- `docker exec -it <container_id> \
  python3 higlass-server/manage.py ingest_tileset \
    --filename /data/CHLA90-Cas9.10k.mcool \
    --filetype cooler \
    --datatype matrix`
- Ex. `docker exec -it 1f9e6cea74ff \
  python3 higlass-server/manage.py ingest_tileset \
    --filename /data/CHLA90-Cas9.10k.mcool \
    --filetype cooler \
    --datatype matrix`

  ### Opening HiGlass in browser
  - `localhost:PATH`
 - Ex. `localhost:8989`
  
