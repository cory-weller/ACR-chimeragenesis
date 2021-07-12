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
Requires 2604 repair templates.

Added files `upstream.dna` and `downstream.dna` to the `seqs/` directory, containing DNA strings (no `fasta` header) of the intended neighboring sequences for the original and shuffled sequences.
```
mkdir 02_AcrIIa2_mutagenesis
python3 Xmera/bin/buildMutagenicRTs.py \
    --first seqs/AcrIIa2.min_homology.fasta \
    --second seqs/AcrIIa2.cds.fasta \
    --length 163 \
    --codons seqs/codons.txt \
    --upstream seqs/Acr.upstream.fasta \
    --downstream seqs/Acr.downstream.fasta \
    > 02_AcrIIa2_mutagenesis/AcrIIa2_mutagenesis.fasta

```

## Chimeragenesis of AcrIIa2 and AcrIIa2b

```
mkdir -p 04_RT_length_homology
parallel -j 1 python3 Xmera/bin/buildRTs.py {1} {2} \
    --flanking seqs/Acr \
    --repair-template-length {3} \
    --mode aligned \
    --unique protein \
    --primer-length 15 \
    --oligo-length 190 \
    --five-prime-padding gcgacaacggtttaggtgggtacgggtccccattccttatatagaaatggcatgttagatcggagcttccaaatcacgat \
    --three-prime-padding accgttctttgttggaagaatagctaagcgcagggacttcccgaatctcggtattatcccggtaagtgtggactatattt \
    > 04_RT_length_homology/AcrIIa2_AcrIIa2b.RT-all.fasta  \
    ::: seqs/AcrIIa2.cds \
    ::: seqs/AcrIIa2b.cds \
    ::: 40 50 60 70 80 90 100 120 140 160

parallel -j 1 python3 Xmera/bin/buildRTs.py {2} {1} \
    --flanking seqs/Acr \
    --repair-template-length {3} \
    --mode aligned \
    --unique protein \
    --primer-length 15 \
    --oligo-length 190 \
    --five-prime-padding gcgacaacggtttaggtgggtacgggtccccattccttatatagaaatggcatgttagatcggagcttccaaatcacgat \
    --three-prime-padding accgttctttgttggaagaatagctaagcgcagggacttcccgaatctcggtattatcccggtaagtgtggactatattt \
    > 04_RT_length_homology/AcrIIa2b_AcrIIa2.RT-all.fasta  \
    ::: seqs/AcrIIa2.cds \
    ::: seqs/AcrIIa2b.cds \
    ::: 40 50 60 70 80 90 100 120 140 160

parallel -j 1 python3 Xmera/bin/buildRTs.py {1} {2} --flanking seqs/Acr --repair-template-length {3} --mode aligned --unique protein --primer-length 15 --oligo-length 190 --five-prime-padding gcgacaacggtttaggtgggtacgggtccccattccttatatagaaatggcatgttagatcggagcttccaaatcacgat --three-prime-padding accgttctttgttggaagaatagctaagcgcagggacttcccgaatctcggtattatcccggtaagtgtggactatattt  > 0N_RT_length_homology/AcrIIa2b_AcrIIa2.RT-all.fasta  ::: seqs/AcrIIa2b.cds ::: seqs/AcrIIa2.cds :::  40 50 60 70 80 90 100 120 140 160

```


## Deletion scan of AcrIIa4
Requires 3916 repair templates.

Will generate repair templates only where the second homology arm start position is >= the first homology arm end position.
```bash
mkdir -p 04_AcrIIa4_deletion_scan
python3 Xmera/bin/buildRTs.py seqs/AcrIIa4.cds seqs/AcrIIa4.min_homology \
--mode extensive \
--deletion \
--flanking seqs/Acr \
--repair-template-length 160 \
--primer-length 15 \
--oligo-length 190 > 04_AcrIIa4_deletion_scan/AcrIIa4_deletion_scan.fasta
```


