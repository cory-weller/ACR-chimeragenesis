# Anti-CRISPR Chimeragenesis

## Download singularity image file

#sha512sum 9727eb881d22b8ac91c06437869b0838e76fed7f73675e018c61bc88d2d0332f3e2eb6eb4975747311c3767e95ac1a7024af3796486c1c43cdf37ce1e75c3d0b


| Construct | Length (bp) | Link |
| --------- | ----------- | ---- |
| [`AcrIIA2-AcrIIA2b`](seqs/AcrIIA2-AcrIIA2b.gb) | 2817 | [benchling](https://benchling.com/s/seq-jQnwdnFpRApYpqCL6SLl?m=slm-KpvQKcjvuqFJGRQfMLUm) |
| [`AcrIIA2b-AcrIIA2`](seqs/AcrIIA2b-AcrIIA2.gb) | 2817 | [benchling](https://benchling.com/s/seq-8R2tVWz0f1KbBus1obbL?m=slm-wOxhs5d2YrBRigocjJzP) |
| [`AcrIIA2b-AcrIIA4`](seqs/AcrIIA2b-AcrIIA4.gb) | 2709 | [benchling](https://benchling.com/s/seq-jmDiSVMmQSIZvNU4WZox?m=slm-8oDPlbvbtke5rsSF3dvw) |
| [`AcrIIA4-AcrIIA2b`](seqs/AcrIIA4-AcrIIA2b.gb) | 2709 | [benchling](https://benchling.com/s/seq-2Gg3WaO4baiNH1RI8IEK?m=slm-VhadRnBonmEsfo7gAyUF) |
| [`AcrIIA4-deletion-scan`](seqs/AcrIIA4-deletion-scan.gb) | 2580 | [benchling](https://benchling.com/s/seq-4DlGBn1wo3uptGECPzN8?m=slm-FZpJ573JdKSTSq7CIxaZ) | 

See HO locus [here](https://benchling.com/s/seq-CAOyHSUOz6dnhy7o6HHB?m=slm-uYry081ZAM5nOQ45Sffn)


## Build Repair Templates

### Standard Chimeras for 2A2 and 2A2b

Generate repair templates for aligned chimeras between AcrIIA2 and AcrIIA2b, saving a [`AcrIIA2-AcrIIA2b-aligned-RTs.fasta`](AcrIIA2-AcrIIA2b-aligned-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2-cds seqs/AcrIIA2b-cds \
    --mode aligned \
    --unique dna \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 200 \
    --primer-length 15 \
    --oligo-length 230 \
    > AcrIIA2-AcrIIA2b-aligned-RTs.fasta

grep '^>' AcrIIA2-AcrIIA2b-aligned-RTs.fasta | wc -l
```

Generate repair templates for aligned chimeras between AcrIIA2b and AcrIIA2, saving as [`AcrIIA2b-AcrIIA2-aligned-RTs.fasta`](AcrIIA2b-AcrIIA2-aligned-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2b-cds seqs/AcrIIA2-cds \
    --mode aligned \
    --unique dna \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 200 \
    --primer-length 15 \
    --oligo-length 230 \
    > AcrIIA2b-AcrIIA2-aligned-RTs.fasta

grep '^>' AcrIIA2b-AcrIIA2-aligned-RTs.fasta | wc -l
```

Generate repair templates for unaligned chimeras between AcrIIA2 and AcrIIA2b, saving a [`AcrIIA2-AcrIIA2b-unaligned-RTs.fasta`](AcrIIA2-AcrIIA2b-unaligned-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2-cds seqs/AcrIIA2b-cds \
    --mode all \
    --max-indel -1 \
    --unique dna \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 200 \
    --primer-length 15 \
    --oligo-length 230 \
    > AcrIIA2-AcrIIA2b-unaligned-RTs.fasta

grep '^>' AcrIIA2-AcrIIA2b-unaligned-RTs.fasta | wc -l
```

Generate repair templates for unaligned chimeras between AcrIIA2b and AcrIIA2, saving as [`AcrIIA2b-AcrIIA2-unaligned-RTs.fasta`](AcrIIA2b-AcrIIA2-unaligned-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2b-cds seqs/AcrIIA2-cds \
    --mode all \
    --max-indel -1 \
    --unique dna \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 200 \
    --primer-length 15 \
    --oligo-length 230 \
    > AcrIIA2b-AcrIIA2-unaligned-RTs.fasta

grep '^>' AcrIIA2b-AcrIIA2-unaligned-RTs.fasta | wc -l
```


## Mad Scientist Experiment
Generate repair templates for all-possible chimeras between AcrIIA2b and AcrIIa4, saving as [`AcrIIA2b-AcrIIA4-RTs.fasta`](AcrIIA2b-AcrIIA4-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2b-cds seqs/AcrIIA4-cds \
    --mode extensive \
    --unique dna \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 200 \
    --primer-length 15 \
    --oligo-length 230 \
    > AcrIIA2b-AcrIIA4-RTs.fasta

grep '^>' AcrIIA2b-AcrIIA4-RTs.fasta | wc -l
```

Generate repair templates for all-possible chimeras between AcrIIA4 and AcrIIA2b, saving as [`AcrIIA4-AcrIIA2b-RTs.fasta`](AcrIIA4-AcrIIA2b-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA4-cds seqs/AcrIIA2b-cds \
    --mode extensive \
    --unique dna \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 200 \
    --primer-length 15 \
    --oligo-length 230 \
    > AcrIIA4-AcrIIA2b-RTs.fasta

grep '^>' AcrIIA4-AcrIIA2b-RTs.fasta | wc -l
```

Generate repair templates for aligned chimeras between AcrIIA2 and AcrIIA2b *with variable length homology arms* saving as [`AcrIIA2-AcrIIA2b-variable-arm-RTs.fasta`](AcrIIA2-AcrIIA2b-variable-arm-RTs.fasta)
```bash
for i in $(seq 40 10 200); do
    ./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2-cds seqs/AcrIIA2b-cds \
        --mode aligned \
        --unique dna \
        --upstream seqs/GAL-promoter.fasta \
        --downstream seqs/Tsynth8-HO.fasta \
        --repair-template-length ${i} \
        --primer-length 15 \
        --oligo-length 230 \
        --five-prime-padding ccaagtcactaaaaagaagaggattcgtggccaggccgtgttgcgccacatatagctcgccgggtctctggcttcgacatggatacccgccacaatcgggcgaaacagtttattgagaactggctgcggtagtgatgggaattcgctgcttttaggcactgaggctgaaatggttcaagtaaaacgcgatccaaccccgt \
        --three-prime-padding catggtatgctctcctaatgaagtgccgtgagcttgtagatcaacgggacatacttgagtttaagagcgtaagtgacccctgatatttctccccaatcccgatagtcaagcatgtagtattcgtcataaactggcgcataaacttccgcaatacattctagtgtacggctggcggttgggctaacttaagtcgggcagta
done > AcrIIA2-AcrIIA2b-variable-arm-RTs.fasta

grep '>' AcrIIA2-AcrIIA2b-variable-arm-RTs.fasta | wc -l
```


Generate repair templates for aligned chimeras between AcrIIA2b and AcrIIA2 *with variable length homology arms* saving as [`AcrIIA2b-AcrIIA2-variable-arm-RTs.fasta`](AcrIIA2b-AcrIIA2-variable-arm-RTs.fasta)
```bash
for i in $(seq 40 10 200); do
    ./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2b-cds seqs/AcrIIA2-cds \
        --mode aligned \
        --unique dna \
        --upstream seqs/GAL-promoter.fasta \
        --downstream seqs/Tsynth8-HO.fasta \
        --repair-template-length ${i} \
        --primer-length 15 \
        --oligo-length 230 \
        --five-prime-padding ccaagtcactaaaaagaagaggattcgtggccaggccgtgttgcgccacatatagctcgccgggtctctggcttcgacatggatacccgccacaatcgggcgaaacagtttattgagaactggctgcggtagtgatgggaattcgctgcttttaggcactgaggctgaaatggttcaagtaaaacgcgatccaaccccgt \
        --three-prime-padding catggtatgctctcctaatgaagtgccgtgagcttgtagatcaacgggacatacttgagtttaagagcgtaagtgacccctgatatttctccccaatcccgatagtcaagcatgtagtattcgtcataaactggcgcataaacttccgcaatacattctagtgtacggctggcggttgggctaacttaagtcgggcagta
done > AcrIIA2b-AcrIIA2-variable-arm-RTs.fasta

grep '^>' AcrIIA2b-AcrIIA2-variable-arm-RTs.fasta | wc -l
```


### Deletion Scan

Generate repair templates for AcrIIA4 deletion scan, saving as [`AcrIIA4-deletion-scan-RTs.fasta`](AcrIIA4-deletion-scan-RTs.fasta)

```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA4-min-homology seqs/AcrIIA4-cds \
    --mode extensive \
    --unique dna \
    --deletion \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 200 \
    --primer-length 15 \
    --oligo-length 230 \
    > AcrIIA4-deletion-scan-RTs.fasta

grep '^>' AcrIIA4-deletion-scan-RTs.fasta | wc -l
```
