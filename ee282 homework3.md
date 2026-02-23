# **HW3 Submission:** 

**Part 1 of homework 3**   
## **Summarize a Genome Assembly**
```r
(base) \[sophid2@login-i15:\~\] $mkdir homework3  
(base) \[sophid2@login-i15:\~\] $mv dmel-all-chromosome-r6.66.fasta.gz homework3/  
(base) \[sophid2@login-i15:\~\] $cd homework3/  
(base) \[sophid2@login-i15:\~/homework3\] $ls  
**dmel-all-chromosome-r6.66.fasta.gz**  
(base) \[sophid2@login-i15:\~/homework3\] $ fasize \-help  
bash: fasize: command not found...  
(base) \[sophid2@login-i15:\~/homework3\] $ srun \-A ecoevo282\_class \-c 1 \--pty bash \-i  
(base) \[sophid2@hpc3-l18-05:\~/homework3\] $ module load miniconda3   
(base) \[sophid2@hpc3-l18-05:\~/homework3\] $ls  
**dmel-all-chromosome-r6.66.fasta.gz**  
(base) \[sophid2@hpc3-l18-05:\~/homework3\] $conda env list  
\# conda environments:  
\#  
\# \* \-\> active  
\# \+ \-\> frozen  
base                 \*   /data/homezvol1/sophid2/miniforge3  
ee282                    /data/homezvol1/sophid2/miniforge3/envs/ee282  
(base) \[sophid2@hpc3-l18-05:\~/homework3\] $conda activate ee282   
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $faSize  
faSize \- print total base count in fa files.  
usage:  
   faSize file(s).fa  
Command flags  
   \-detailed        outputs name and size of each record  
                    has the side effect of printing nothing else  
   \-tab             output statistics in a tab separated format  
   \-veryDetailed    outputs name, size, \#Ns, \#real, \#upper, \#lower of each record  
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $faSize  
faSize \- print total base count in fa files.  
usage:  
   faSize file(s).fa  
Command flags  
   \-detailed        outputs name and size of each record  
                    has the side effect of printing nothing else  
   \-tab             output statistics in a tab separated format  
   \-veryDetailed    outputs name, size, \#Ns, \#real, \#upper, \#lower of each record 
```

### Checking File Integrity 
```r
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $ md5sum dmel-all-chromosome-r6.66.fasta.gz  
ccb86e94117eb4eeaaf70efb6be1b6b9  dmel-all-chromosome-r6.66.fasta.gz  
  
# Output from md5Sumtxt file: ccb86e94117eb4eeaaf70efb6be1b6b9  dmel-all-chromosome-r6.66.fasta.gz
# Confirmed with the md5sumtxt file for dmel-all-chromosome-r6.66.fasta.gz and the output matches what is listed in the txt file.
```
### Calculate Summaries of the Genome
```r
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $faSize dmel-all-chromosome-r6.66.fasta.gz  
143726002 bases (1152978 N's 142573024 real 142573024 upper 0 lower) in 1870 sequences in 1 files  
Total size: mean 76858.8 sd 1382100.2 min 544 (211000022279089) max 32079331 (3R) median 1577  
N count: mean 616.6 sd 6960.7  
U count: mean 76242.3 sd 1379508.4  
L count: mean 0.0 sd 0.0  
%0.00 masked total, %0.00 masked real  

# 1. **Total number of nucleotides \=** mean 616.6 sd 6960.7  
# 2. **Total number of Ns \=**  1152978  
# 3. **Total number of sequences \=** 1870
```
---
**Part 2 of homework 3**

## **Summarize an annotation file**  
```r
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $ls  
dmel-all-chromosome-r6.66.fasta.gz  dmel-all-r6.66.gtf.gz  
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $zcat dmel-all-r6.66.gtf.gz \\  
| bioawk \-c gff '$feature=="gene"{print $seqname}' \\  
| sort \\  
| uniq \-c  
      1 211000022278279  
      1 211000022278436  
      1 211000022278449  
      1 211000022278760  
      1 211000022279165  
      1 211000022279188  
      1 211000022279264  
      1 211000022279392  
      1 211000022279681  
      1 211000022280328  
      1 211000022280341  
      1 211000022280347  
      1 211000022280481  
      2 211000022280494  
      1 211000022280703  
   3508 2L  
   3649 2R  
   3481 3L  
   4226 3R  
    114 4  
     38 mitochondrion\_genome  
     21 rDNA  
      2 Unmapped\_Scaffold\_8\_D1580\_D1567  
   2704 X  
    113 Y  
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $ls  
**dmel-all-chromosome-r6.66.fasta.gz**  **dmel-all-r6.66.gtf.gz**  homework3.sh  
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $nano [homework3.sh](http://homework3.sh)  
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $chmod \+x homework3.sh  
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $ls \-l homework3.sh  
\-rwxr-xr-x 1 sophid2 sophid2 101 Feb 19 16:19 **homework3.sh**  
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $  
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $md5sum dmel-all-r6.66.gtf.gz  
ea600dbb86f1779463f69082131753cd  dmel-all-r6.66.gtf.gz
```
## Checking File Integrity
### **Verify the file integrity of the gzipped gtf annotation using a checksum**
```r
(ee282) \[sophid2@hpc3-l18-05:\~/homework3\] $md5sum dmel-all-r6.66.gtf.gz
ea600dbb86f1779463f69082131753cd  [dmel-all-r6.66.gtf.gz](http://dmel-all-r6.66.gtf.gz)

#The output from Flybase: ea600dbb86f1779463f69082131753cd  dmel-all-r6.66.gtf.gz
#The output matches the md5Sumtxt file from Flybase.

# Checking file integrity using checksum (cksum command) 
(ee282) [sophid2@login-i17:~/homework3] $cksum dmel-all-r6.66.gtf.gz
3717293822 4059663 dmel-all-r6.66.gtf.gz

```

## Compiling a Report Summarizing the Annotation

### 1. **Total number of features of each type, sorted from the most common to the least common:** 
```bash
(base) \[sophid2@login-i17:\~/homework3\] $zcat dmel-all-r6.66.gtf.gz | \\  
awk '$0 \!\~ /^\#/ {print $3}' | \\  
sort | uniq \-c | sort \-nr

**OUTPUT:**

190176 exon

 163377 CDS  
  46856 5UTR  
  33778 3UTR  
  30922 start\_codon  
  30862 stop\_codon  
  30836 mRNA  
  17872 gene  
   3059 ncRNA  
    485 miRNA  
    365 pseudogene  
    312 tRNA  
    270 snoRNA  
    262 pre\_miRNA  
    115 rRNA  
     32 snRNA
```
### **Total number of genes per chromosome arm (X, Y, 2L, 2R, 3L, 3R, 4\) \=**   
```bash 
(base) \[sophid2@login-i17:\~/homework3\] $zcat dmel-all-r6.66.gtf.gz | \\  
awk '  
BEGIN { FS="\\t" }  
\!/^\#/ && $3 \== "gene" {  
    chr\[$1\]++  
}  
END {  
    for (arm in chr)  
        printf "%s\\t%d\\n", arm, chr\[arm\]  
}  
' | sort

#OUTPUT:  
211000022278279	1  
211000022278436	1  
211000022278449	1  
211000022278760	1  
211000022279165	1  
211000022279188	1  
211000022279264	1  
211000022279392	1  
211000022279681	1  
211000022280328	1  
211000022280341	1  
211000022280347	1  
211000022280481	1  
211000022280494	2  
211000022280703	1  
2L	3508  
2R	3649  
3L	3481  
3R	4226  
4	114  
mitochondrion\_genome	38  
rDNA	21  
Unmapped\_Scaffold\_8\_D1580\_D1567	2  
X	2704  
Y	113
```
### Answers for question 2
**X**: 2704  
**Y**: 113  
**2L**: 3508  
**2R**: 3649  
**3L**: 3481  
**3R**: 4226  
**4**: 114
