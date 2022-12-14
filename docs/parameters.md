# nf-core/callingcards pipeline parameters

An automated processing pipeline for mammalian bulk calling cards experiments

## Hops counting options

Hops quantification related parameters

| Parameter | Description | Type | Default | Required | Hidden |
|-----------|-----------|-----------|-----------|-----------|-----------|
| `min_mapq` | Values with less than or equal to this mapq value will not be counted as transpositions. Defaults to 10 | `integer` | 10 |  |  |

## Read processing options

Options to control how reads are processed prior to alignment

| Parameter | Description | Type | Default | Required | Hidden |
|-----------|-----------|-----------|-----------|-----------|-----------|
| `r1_bc_pattern` | UMITools compliant read 1 barcode pattern. See UMITools documentation | `string` | None |  |  |
| `r2_bc_pattern` | UMITools compliant read 2 barcode pattern. See UMITools documentation | `string` | None |  |  |
| `reduce_to_se` | Once barcodes are extracted, treat reads as single end from alignment step forward. Defaults to true | `boolean` | True |  |  |
| `r1_crop` | If SE or reduce_to_se is True, this option allows the user to crop the R1 read. This occurs after trimming. Defaults to 40 | `integer` | 40 |  |  |

## Alignment options

Alignment parameters

| Parameter | Description | Type | Default | Required | Hidden |
|-----------|-----------|-----------|-----------|-----------|-----------|
| `aligner` | Choose one of the configured aligners: bwamem2, bwaaln, bowtie2, bowtie. Defaults to bwamem2. | `string` | bwamem2 |  |  |

## Input/output options

Define where the pipeline should find input data and save output data.

| Parameter | Description | Type | Default | Required | Hidden |
|-----------|-----------|-----------|-----------|-----------|-----------|
| `input` | Path to comma-separated file containing information about the samples in the experiment. <details><summary>Help</summary><small>You will need to
create a design file with information about the samples in your experiment before running the pipeline. Use this parameter to specify its location. It has to be
a comma-separated file with 3 columns, and a header row. See (https://nf-co.re/callingcards/usage#samplesheet-input).</small></details>| `string` |  |  |
| `outdir` | The output directory where the results will be saved. You have to use absolute paths to storage on Cloud infrastructure. | `string` |  |  |  |
| `save_intermediate` | Set this to True to save intermediate files, eg an unsorted bam file prior to a samtools sort step. Defaults to False | `boolean` |  |  |
| `email` | Email address for completion summary. <details><summary>Help</summary><small>Set this parameter to your e-mail address to get a summary e-mail with
details of the run sent to you when the workflow exits. If set in your user config file (`~/.nextflow/config`) then you don't need to specify this on the command
line for every run.</small></details>| `string` |  |  |  |
| `multiqc_title` | MultiQC report title. Printed as page header, used for filename if not otherwise specified. | `string` |  |  |  |

## Reference genome options

Reference genome related files and options required for the workflow.

| Parameter | Description | Type | Default | Required | Hidden |
|-----------|-----------|-----------|-----------|-----------|-----------|
| `genome` | Name of iGenomes reference. <details><summary>Help</summary><small>If using a reference genome configured in the pipeline using iGenomes, use this
parameter to give the ID for the reference. This is then used to build the full paths for all required reference genome files e.g. `--genome GRCh38`. See the (https://nf-co.re/usage/reference_genomes) for more details.</small></details>| `string` |  |  |  |
| `fasta` | Path to FASTA genome file. <details><summary>Help</summary><small>This parameter is *mandatory* if `--genome` is not specified. If you don't have a
BWA index available this will be generated for you automatically. Combine with `--save_reference` to save BWA index for future runs.</small></details>| `string`
|  |  |  |
| `fasta_index` | path to the .fai index file produced by samtools faidx from the fasta file | `string` |  |  |  |
| `bwamem2_index` | path to the bwamem2 index. only used if aligner is bwamem2. if the aligner is bwamem2 and this is not provided, the index is created in the
pipeline | `string` | None |  |  |
| `bwa_aln_index` | path to the bwaaln index. only used if aligner is bwaaln. if the aligner is bwaaln and this is not provided, the index is created in the
pipeline | `string` | None |  |  |
| `bowtie2_index` | path to the bowtie2 index. only used if aligner is bowtie2. if the aligner is bowtie2 and this is not provided, the index is created in the
pipeline | `string` | None |  |  |
| `bowtie_index` | path to the bowtie index. only used if aligner is bowtie. if the aligner is bowtie and this is not provided, the index is created in the
pipeline | `string` | None |  |  |
| `igenomes_base` | Directory / URL base for iGenomes references. | `string` | s3://ngi-igenomes/igenomes |  | True |
| `igenomes_ignore` | Do not load the iGenomes reference config. <details><summary>Help</summary><small>Do not load `igenomes.config` when running the pipeline.
You may choose this option if you observe clashes between custom parameters and those supplied in `igenomes.config`.</small></details>| `boolean` |  |  | True |

## Institutional config options

Parameters used to describe centralised config profiles. These should not be edited.

| Parameter | Description | Type | Default | Required | Hidden |
|-----------|-----------|-----------|-----------|-----------|-----------|
| `custom_config_version` | Git commit id for Institutional configs. | `string` | master |  | True |
| `custom_config_base` | Base directory for Institutional configs. <details><summary>Help</summary><small>If you're running offline, Nextflow will not be able to
fetch the institutional config files from the internet. If you don't need them, then this is not a problem. If you do need them, you should download the files
from the repo and tell Nextflow where to find them with this parameter.</small></details>| `string` | https://raw.githubusercontent.com/nf-core/configs/master |
| True |
| `config_profile_name` | Institutional config name. | `string` |  |  | True |
| `config_profile_description` | Institutional config description. | `string` |  |  | True |
| `config_profile_contact` | Institutional config contact information. | `string` |  |  | True |
| `config_profile_url` | Institutional config URL link. | `string` |  |  | True |

## Max job request options

Set the top limit for requested resources for any single job.

| Parameter | Description | Type | Default | Required | Hidden |
|-----------|-----------|-----------|-----------|-----------|-----------|
| `max_cpus` | Maximum number of CPUs that can be requested for any single job. <details><summary>Help</summary><small>Use to set an upper-limit for the CPU
requirement for each process. Should be an integer e.g. `--max_cpus 1`</small></details>| `integer` | 16 |  | True |
| `max_memory` | Maximum amount of memory that can be requested for any single job. <details><summary>Help</summary><small>Use to set an upper-limit for the
memory requirement for each process. Should be a string in the format integer-unit e.g. `--max_memory '8.GB'`</small></details>| `string` | 128.GB |  | True |
| `max_time` | Maximum amount of time that can be requested for any single job. <details><summary>Help</summary><small>Use to set an upper-limit for the time
requirement for each process. Should be a string in the format integer-unit e.g. `--max_time '2.h'`</small></details>| `string` | 240.h |  | True |

## Generic options

Less common options for the pipeline, typically set in a config file.

| Parameter | Description | Type | Default | Required | Hidden |
|-----------|-----------|-----------|-----------|-----------|-----------|
| `help` | Display help text. | `boolean` |  |  | True |
| `publish_dir_mode` | Method used to save pipeline results to output directory. <details><summary>Help</summary><small>The Nextflow `publishDir` option
specifies which intermediate files should be saved to the output directory. This option tells the pipeline what method should be used to move these files. See
[Nextflow docs](https://www.nextflow.io/docs/latest/process.html#publishdir) for details.</small></details>| `string` | copy |  | True |
| `email_on_fail` | Email address for completion summary, only when pipeline fails. <details><summary>Help</summary><small>An email address to send a summary
email to when the pipeline is completed - ONLY sent if the pipeline does not exit successfully.</small></details>| `string` |  |  | True |
| `plaintext_email` | Send plain-text email instead of HTML. | `boolean` |  |  | True |
| `max_multiqc_email_size` | File size limit when attaching MultiQC reports to summary emails. | `string` | 25.MB |  | True |
| `monochrome_logs` | Do not use coloured log outputs. | `boolean` |  |  | True |
| `multiqc_config` | Custom config file to supply to MultiQC. | `string` |  |  | True |
| `tracedir` | Directory to keep pipeline Nextflow logs and reports. | `string` | ${params.outdir}/pipeline_info |  | True |
| `validate_params` | Boolean whether to validate parameters against the schema at runtime | `boolean` | True |  | True |
| `show_hidden_params` | Show all params when using `--help` <details><summary>Help</summary><small>By default, parameters set as _hidden_ in the schema are not
shown on the command line when a user runs with `--help`. Specifying this option will tell the pipeline to show all parameters.</small></details>| `boolean` |  |
| True |
| `enable_conda` | Run this workflow with Conda. You can also use '-profile conda' instead of providing this parameter. | `boolean` |  |  | True |

