**Assigning mystery individuals to populations**

Points along a genome which vary in a single nucleotide (A,C,G or T) between individuals are called Single Nucleotide Polynmorphisms (SNPs). For example, at a specific base position in the genome, the C nucleotide may appear in most individuals, but in a minority of individuals, the position is occupied by an A. This means that there is an SNP at this specific position, and the two possible nucleotide variations – C or A – are said to be alleles for this position.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Dna-SNP.svg/457px-Dna-SNP.svg.png">

*The upper DNA molecule differs from the lower DNA molecule at a single base-pair location (a C/A polymorphism)*

Within a population of individuals we would expect individuals to be more similar (have less variation in SNPs) than individuals from different populations. For example, the table below shows nucleotides at 6 SNPs for ten different individuals. At no SNP are any indivuals all the same, but there are some patterns emerging: at SNP 1 all inviduals from population A are the same (nucleotide A) as are indivuals from population B (nucleotide C). Similarly individuals from the same population share the same nucleotide for SNP 6. 

| Individual  | SNP 1 | SNP2  | SNP3  | SNP4  | SNP 5 | SNP 6 | Pop |
|-------------|-------|-------|-------|-------|-------|-------|-----|
| 1           | **A** | T     | G     | G     | G     | **C** | A   |
| 2           | **A** | T     | T     | G     | G     | **C** | A   |
| 3           | **C** | G     | G     | T     | G     | **A** | B   |
| 4           | **C** | T     | G     | T     | A     | **A** | B   |
| 5           | **A** | T     | G     | G     | G     | **C** | A   |
| 6           | **C** | G     | A     | T     | A     | **A** | B   |   
| 7           | **C** | T     | G     | G     | A     | **A** | B   |
| 8           | **A** | T     | G     | C     | G     | **C** | A   |
| 9           | **A** | G     | G     | G     | G     | **C** | A   |
| 10          | **C** | T     | G     | G     | A     | **A** | B   |

Based on this assumption, we could assign individuals to populations (reasonably reliably) if all we knew about them was which nucleotide they had at each SNP. 

The file Mystery.VCF contains 120,000 SNPs (Single Nucleotide Polymorphisms - regions of the genome that vary between individuals). 
