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
Generate [`AcrIIA2b-AcrIIA4-RTs.fasta`](AcrIIA2b-AcrIIA4-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2b-cds seqs/AcrIIA4-cds \
    --mode all \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 160 \
    --primer-length 15 \
    --oligo-length 190 \
    > AcrIIA2b-AcrIIA4-RTs.fasta
```

Generate [`AcrIIA4-AcrIIA2b-RTs.fasta`](AcrIIA4-AcrIIA2b-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA4-cds seqs/AcrIIA2b-cds \
    --mode all \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 160 \
    --primer-length 15 \
    --oligo-length 190 \
    > AcrIIA4-AcrIIA2b-RTs.fasta
```

Generate repair templates for aligned chimeras between AcrIIA2 and AcrIIA2b, saving a [`AcrIIA2-AcrIIA2b-RTs.fasta`](AcrIIA2-AcrIIA2b-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2-cds seqs/AcrIIA2b-cds \
    --mode aligned \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 160 \
    --primer-length 15 \
    --oligo-length 190 \
    > AcrIIA2-AcrIIA2b-RTs.fasta
```

Generate repair templates for aligned chimeras between AcrIIA2b and AcrIIA2, saving as [`AcrIIA2b-AcrIIA2-RTs.fasta`](AcrIIA2b-AcrIIA2-RTs.fasta)
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA2b-cds seqs/AcrIIA2-cds \
    --mode aligned \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 160 \
    --primer-length 15 \
    --oligo-length 190 \
    > AcrIIA2b-AcrIIA2-RTs.fasta
```

Generate repair templates for AcrIIA4 deletion scan

TODO: create new --mode in `buildRTs.py` to only include deletions, i.e. second position <= the first position.
```bash
./Xmera.sif ./Xmera/src/buildRTs.py seqs/AcrIIA4-min-homology seqs/AcrIIA4-cds \
    --mode all \
    --upstream seqs/GAL-promoter.fasta \
    --downstream seqs/Tsynth8-HO.fasta \
    --repair-template-length 160 \
    --primer-length 15 \
    --oligo-length 190 \
    > AcrIIA4-min-homology-AcrIIA4-RTs.fasta
```