# `pipeline_runner.py`

This script runs the [Epi2me Labs `wf-single-cell`](https://github.com/epi2me-labs/wf-single-cell) Nextflow pipeline using a YAML configuration file. It sets up the environment, manages output directories, and builds the pipeline command based on user-provided parameters.

## Requirements

- Python 3.7+
- Nextflow
- Singularity (or compatible container runtime)
- Conda (to use `environment.yaml`)

## Setup

Create and activate the conda environment:

```bash
conda env create -f environment.yaml
conda activate epi2me-env
```

## Usage

The conda env must be active and the following modules must be loaded:

```bash
module load openjdk
module load singularity
```

Finally, `nextflow` must be on the path. For our lab group, this can be set as follows:

```bash
export PATH="/nfs/turbo/umms-indikar/Ram/tools:$PATH"
```

Then, the pipeline can be run:

```bash
python pipeline_runner.py --config_path ./config.yaml --overwrite
```


## 🧬 Reference Genome

The reference genome required for this workflow must be obtained from the official 10x Genomics resource page:

[https://www.10xgenomics.com/support/software/cell-ranger/downloads#reference-downloads](https://www.10xgenomics.com/support/software/cell-ranger/downloads#reference-downloads)

After downloading the reference package (e.g., `refdata-gex-GRCh38-2020-A.tar.gz`), extract the contents. The downloaded reference will include a compressed GTF file, typically located at:

```
refdata-gex-GRCh38-2020-A/genes/genes.gtf.gz
```


This GTF file **must be uncompressed** before execution of the pipeline, as the workflow expects a plain-text GTF format. To decompress the file:

```bash
gunzip refdata-gex-GRCh38-2020-A/genes/genes.gtf.gz
```

Then, specify the path to the reference genome directory in your config.yaml file:

```bash
ref_genome_dir: /path/to/refdata-gex-GRCh38-2020-A
```

