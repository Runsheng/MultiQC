<img src="multiqc/templates/default/assets/img/MultiQC_logo.png" width="300" title="MultiQC">

### Aggregate bioinformatics results across many samples into a single report.

##### Find [documentation](http://multiqc.info/docs) and [example reports](http://multiqc.info/examples/rna-seq/multiqc_report.html) at [http://multiqc.info](http://multiqc.info)

[![PyPI Version](https://img.shields.io/pypi/v/multiqc.svg?style=flat-square)](https://pypi.python.org/pypi/multiqc/)
[![Conda Version](https://anaconda.org/bioconda/multiqc/badges/version.svg)](https://anaconda.org/bioconda/multiqc)
[![Build Status](https://img.shields.io/travis/ewels/MultiQC.svg?style=flat-square)](https://travis-ci.org/ewels/MultiQC)
[![Gitter](https://img.shields.io/badge/gitter-%20join%20chat%20%E2%86%92-4fb99a.svg?style=flat-square)](https://gitter.im/ewels/MultiQC)
[![DOI](https://img.shields.io/badge/DOI-10.1093%2Fbioinformatics%2Fbtw354-lightgrey.svg?style=flat-square)](http://dx.doi.org/10.1093/bioinformatics/btw354)


-----

MultiQC is a tool to create a single report with interactive plots
for multiple bioinformatics analyses across many samples.

MultiQC is written in Python (tested with v2.7 / v3.4 / v3.5). It is
available on the [Python Package Index](https://pypi.python.org/pypi/multiqc/)
and through conda using [Bioconda](http://bioconda.github.io/).

Reports are generated by scanning given directories for recognised log files.
These are parsed and a single HTML report is generated summarising the statistics
for all logs found. MultiQC reports can describe multiple analysis steps and
large numbers of samples within a single plot, and multiple analysis tools making
it ideal for routine fast quality control.

Currently, supported tools include:



|Read QC & pre-processing     | Aligners / quantifiers | Post-alignment processing | Post-alignment QC    |
|-----------------------------|------------------------|---------------------------|----------------------|
|[Cluster Flow][clusterflow]  | [Bismark][bismark]     | [Bamtools][bamtools]      | [methylQA][methylqa] |
|[Cutadapt][cutadapt]         | [Bowtie][bowtie-1]     | [Bcftools][bcftools]      | [Peddy][peddy]       |
|[FastQC][fastqc]             | [Bowtie 2][bowtie-2]   | [GATK][gatk]              | [Preseq][preseq]     |
|[FastQ Screen][fastq-screen] | [HiCUP][hicup]         | [HTSeq][htseq]            | [Qualimap][qualimap] |
|[Skewer][skewer]             | [Kallisto][kallisto]   | [Picard][picard]          | [QUAST][quast]       |
|[SortMeRNA][sortmerna]       | [Salmon][salmon]       | [Prokka][prokka]          | [RNA-SeQC][rna_seqc] |
|[Trimmomatic][trimmomatic]   | [Slamdunk][slamdunk]   | [Samblaster][samblaster]  | [RSeQC][rseqc]       |
|                             | [STAR][star]           | [Samtools][samtools]      | [BUSCO][busco]       |
|                             | [Tophat][tophat]       | [SnpEff][snpeff]          | [goleft][goleft]     |
|                             |                        | [Subread featureCounts][featurecounts] |         |

MultiQC can also easily parse data from custom scripts, if correctly formatted / configured.
See the [MultiQC documentation](http://multiqc.info/docs/#custom-content) for more information.

Please note that some modules only recognise output from certain tool subcommands. Please follow the
links in the above table to the [module documentation](http://multiqc.info/docs/#multiqc-modules)
for more information.

More modules are being written all of the time. Please suggest any ideas as a new
[issue](https://github.com/ewels/MultiQC/issues) _(include an example log file if possible)_.

## Installation

You can install MultiQC from [PyPI](https://pypi.python.org/pypi/multiqc/)
using `pip` as follows:
```bash
pip install multiqc
```

Alternatively, you can install using [Conda](http://anaconda.org/)
from the [bioconda channel](https://bioconda.github.io/):
```bash
conda install -c bioconda multiqc
```

If you would like the development version instead, the command is:
```bash
pip install --upgrade --force-reinstall git+https://github.com/ewels/MultiQC.git
```

MultiQC is also available in the
[Galaxy Toolshed](https://toolshed.g2.bx.psu.edu/view/engineson/multiqc/).

## Usage
Once installed, you can use MultiQC by navigating to your analysis directory
(or a parent directory) and running the tool:
```bash
multiqc .
```

That's it! MultiQC will scan the specified directory (`.` is the current dir)
and produce a report detailing whatever it finds.

The report is created in `multiqc_report.html` by default. Tab-delimited data
files are also created in `multiqc_data/`, containing extra information.
These can be easily inspected using Excel (use `--data-format` to get `yaml`
or `json` instead).

For more detailed instructions, run `multiqc -h` or see the
[documentation](http://multiqc.info/docs/#running-multiqc).

## Citation
Please consider citing MultiQC if you use it in your analysis.

> **MultiQC: Summarize analysis results for multiple tools and samples in a single report** <br/>
> _Philip Ewels, Måns Magnusson, Sverker Lundin and Max Käller_ <br/>
> Bioinformatics (2016) <br/>
> doi: [10.1093/bioinformatics/btw354](http://dx.doi.org/10.1093/bioinformatics/btw354) <br/>
> PMID: [27312411](http://www.ncbi.nlm.nih.gov/pubmed/27312411)

```TeX
@article{doi:10.1093/bioinformatics/btw354,
author = {Ewels, Philip and Magnusson, Måns and Lundin, Sverker and Käller, Max},
title = {MultiQC: summarize analysis results for multiple tools and samples in a single report},
journal = {Bioinformatics},
volume = {32},
number = {19},
pages = {3047},
year = {2016},
doi = {10.1093/bioinformatics/btw354},
URL = { + http://dx.doi.org/10.1093/bioinformatics/btw354},
eprint = {/oup/backfile/Content_public/Journal/bioinformatics/32/19/10.1093_bioinformatics_btw354/3/btw354.pdf}
}
```

## Contributions & Support

Contributions and suggestions for new features are welcome, as are bug reports!
Please create a new [issue](https://github.com/ewels/MultiQC/issues) for any
of these, including example reports where possible. MultiQC has extensive
[documentation](http://multiqc.info/docs) describing how to write new modules,
plugins and templates.

There is a chat room for the package hosted on Gitter where you can discuss
things with the package author and other developers:
https://gitter.im/ewels/MultiQC

If in doubt, feel free to get in touch with the author directly:
[@ewels](https://github.com/ewels) (phil.ewels@scilifelab.se)

### Contributors
Project lead and main author: [@ewels](https://github.com/ewels)

Code contributions from:
[@moonso](https://github.com/moonso),
[@lpantano](https://github.com/lpantano),
[@dakl](https://github.com/dakl),
[@robinandeer](https://github.com/robinandeer),
[@mlusignan](https://github.com/mlusignan),
[@HLWiencko](https://github.com/HLWiencko),
[@guillermo-carrasco](https://github.com/guillermo-carrasco),
[@avilella](https://github.com/avilella),
[@vladsaveliev](https://github.com/vladsaveliev),
[@t-neumann](https://github.com/t-neumann),
[@ahvigil](https://github.com/ahvigil),
[@bschiffthaler](https://github.com/bschiffthaler)
and many others. Thanks for your support!

[bamtools]:       http://multiqc.info/docs/#bamtools
[bcftools]:       http://multiqc.info/docs/#bcftools
[bismark]:        http://multiqc.info/docs/#bismark
[bowtie-1]:       http://multiqc.info/docs/#bowtie-1
[bowtie-2]:       http://multiqc.info/docs/#bowtie-2
[busco]:          http://multiqc.info/docs/#busco
[clusterflow]:    http://multiqc.info/docs/#cluster-flow
[cutadapt]:       http://multiqc.info/docs/#cutadapt
[fastq-screen]:   http://multiqc.info/docs/#fastq-screen
[fastqc]:         http://multiqc.info/docs/#fastqc
[featurecounts]:  http://multiqc.info/docs/#featurecounts
[gatk]:           http://multiqc.info/docs/#gatk
[goleft]:         http://multiqc.info/docs/#goleft-indexcov
[hicup]:          http://multiqc.info/docs/#hicup
[htseq]:          http://multiqc.info/docs/#htseq
[kallisto]:       http://multiqc.info/docs/#kallisto
[methylqa]:       http://multiqc.info/docs/#methylqa
[peddy]:          http://multiqc.info/docs/#peddy
[picard]:         http://multiqc.info/docs/#picard
[preseq]:         http://multiqc.info/docs/#preseq
[prokka]:         http://multiqc.info/docs/#prokka
[qualimap]:       http://multiqc.info/docs/#qualimap
[quast]:          http://multiqc.info/docs/#quast
[rna_seqc]:       http://multiqc.info/docs/#rna_seqc
[rseqc]:          http://multiqc.info/docs/#rseqc
[salmon]:         http://multiqc.info/docs/#salmon
[samblaster]:     http://multiqc.info/docs/#samblaster
[slamdunk]:       http://multiqc.info/docs/#slamdunk
[skewer]:         http://multiqc.info/docs/#skewer
[snpeff]:         http://multiqc.info/docs/#snpeff
[sortmerna]:      http://multiqc.info/docs/#sortmerna
[star]:           http://multiqc.info/docs/#star
[samtools]:       http://multiqc.info/docs/#samtools
[trimmomatic]:    http://multiqc.info/docs/#trimmomatic
[tophat]:         http://multiqc.info/docs/#tophat

