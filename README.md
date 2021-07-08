# README

## All possible chimeras of AcrIIa2b and AcrIIa4
This experiment seeks to generate and evaluate function of all 
possible simple chimeras (i.e. single-transition) between 
[`AcrIIa2b`](seqs/AcrIIa2b.cds.fasta) and [`AcrIIa4`](seqs/AcrIIa4.cds.fasta).

```bash
mkdir -p 01_all_chimeras
python3 Xmera/bin/buildRTs.py seqs/AcrIIa2b.cds seqs/AcrIIa4.cds \
--mode extensive \
--flanking seqs/Acr \
--repair-template-length 160 \
--primer-length 15 \
--oligo-length 190 > 01_all_chimeras/AcrIIa2b_AcrIIa4.RT-160.fasta

python3 Xmera/bin/buildRTs.py seqs/AcrIIa4.cds seqs/AcrIIa2b.cds \
--mode extensive \
--flanking seqs/Acr \
--repair-template-length 160 \
--primer-length 15 \
--oligo-length 190 > 01_all_chimeras/AcrIIa4_AcrIIa2b.RT-160.fasta
```


## Initialize codon usage table
Will be used for any saturated mutagenesis or deletion scan. Yeast codon usage table retrieved from [kazusa.or.jp](https://www.kazusa.or.jp/codon/cgi-bin/showcodon.cgi?species=4932&aa=1&style=N) and the body of the table was saved as  `codonTable.txt` which is parsed and processed by [`formatCodons.py`](https://github.com/cory-weller/Xmera/blob/b33db0d/bin/formatCodons.py) into [`codons.txt`](seqs/codons.txt):

```
(
cd seqs && \
if [ ! -f "codons.txt" ]; then python3 ../Xmera/bin/formatCodons.py > "codons.txt"; fi 
)
```

## Generate codon-shuffled AcrIIa2
Shuffling AcrIIa2:
```bash
( cd seqs/ && Rscript ../Xmera/bin/shuffle.R AcrIIa2.cds.fasta AcrIIa2.cds.fasta )
```

The script [`shuffle.R`](https://github.com/cory-weller/Xmera/blob/b33db0d/bin/shuffle.R) generates five new `fasta` files with various % identity shared with [`AcrIIa2.cds.fasta`](seqs/AcrIIa2.cds.fasta):
* [`AcrIIa2.cds.min.fasta`](seqs/AcrIIa2.cds.min.fasta)
* [`AcrIIa2.cds.low.fasta`](seqs/AcrIIa2.cds.low.fasta)
* [`AcrIIa2.cds.medium.fasta`](seqs/AcrIIa2.cds.medium.fasta)
* [`AcrIIa2.cds.high.fasta`](seqs/AcrIIa2.cds.high.fasta)
* [`AcrIIa2.cds.max.fasta`](seqs/AcrIIa2.cds.max.fasta)

We only need the most diverged sequence (`AcrIIa2.cds.min.fasta`) so the others are removed.
```bash
rm seqs/AcrIIa2.cds.low.fasta
rm seqs/AcrIIa2.cds.medium.fasta
rm seqs/AcrIIa2.cds.high.fasta
rm seqs/AcrIIa2.cds.max.fasta
```

The [`homopolymers.py`](https://github.com/cory-weller/Xmera/blob/b33db0d//bin/homopolymers.py) script removes homopolymers. See `class fasta` within the script for exact replacements.
```bash
( cd seqs/ && \
python3 ../Xmera/bin/homopolymers.py AcrIIa2.cds.min.fasta AcrIIa2.cds.fasta > AcrIIa2.min_homology.fasta
)
```
Generating the final shuffled sequence, [`AcrIIa2.min_homology.fasta`](seqs/AcrIIa2.min_homology.fasta)


## Generate codon-shuffled AcrIIa4
Shuffling AcrIIa4:
```bash
( cd seqs/ && Rscript ../Xmera/bin/shuffle.R AcrIIa4.cds.fasta AcrIIa4.cds.fasta )
```
Only the most diverged sequence ([`AcrIIa4.cds.min.fasta`](seqs/AcrIIa4.cds.min.fasta)) is kept; the others are removed.
```bash
rm seqs/AcrIIa4.cds.low.fasta
rm seqs/AcrIIa4.cds.medium.fasta
rm seqs/AcrIIa4.cds.high.fasta
rm seqs/AcrIIa4.cds.max.fasta
```

Homopolymers removed, as with AcrIIa2:
```bash
( cd seqs/ && \
python3 ../Xmera/bin/homopolymers.py AcrIIa4.cds.min.fasta AcrIIa4.cds.fasta > AcrIIa4.min_homology.fasta
)
```
Generating the final shuffled sequence, [`AcrIIa4.min_homology.fasta`](seqs/AcrIIa4.min_homology.fasta)


## Saturated mutagenesis of AcrIIa2
Requires 2480 repair templates
```

```



## Deletion scan of AcrIIa4
* requires 3828 repair templates
* requires codon-shuffled allele of AcrIIa4



```

```


