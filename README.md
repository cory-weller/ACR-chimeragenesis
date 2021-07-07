# README

## All possible chimeras of IIa2 and IIa4
This experiment seeks to generate and evaluate function of all 
possible simple chimeras (i.e. single-transition) between 
[`AcrIIa2`](seqs/AcrIIa2.cds.fasta) and [`AcrIIa4`](seqs/AcrIIa4.cds.fasta).

```
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


## Saturated mutagenesis of AcrIIa2
Requires 2480 repair templates
```

```

## Deletion scan of AcrIIa4
requires 3828 repair templates
```

```


