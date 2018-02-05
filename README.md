**Assigning mystery individuals to populations**

Points along a genome which vary in a single nucleotide (A,C,G or T) between individuals are called Single Nucleotide Polynmorphisms (SNPs). For example, at a specific base position in the genome, the C nucleotide may appear in most individuals, but in a minority of individuals, the position is occupied by an A. This means that there is an SNP at this specific position, and the two possible nucleotide variations – C or A – are said to be alleles for this position.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Dna-SNP.svg/457px-Dna-SNP.svg.png">

**Above:** *The upper DNA molecule differs from the lower DNA molecule at a single point along the genome.

Within a population we would expect individuals to be more similar (have less variation in SNPs) than individuals from different populations. For example, the table below shows nucleotides at 6 SNPs for ten different individuals. At no SNP are all individuals all the same, but there are some patterns emerging: at SNP 1 all inviduals from population A are the same (nucleotide A) as are indivuals from population B (nucleotide C). Similarly individuals from the same population share the same nucleotide for SNP 6. 

| Individual  | SNP 1 | SNP2  | SNP3  | SNP4  | SNP 5 | SNP 6 | Pop |
|-------------|-------|-------|-------|-------|-------|-------|-----|
| 1           | **A** | T     | G     | G     | G     | **C** | A   |
| 2           | **A** | T     | T     | G     | G     | **C** | A   |
| 3           | **C** | G     | G     | T     | G     | **A** | B   |
| 4           | **C** | T     | G     | T     | A     | **A** | B   |
| 5           | **A** | T     | G     | G     | G     | **C** | A   |
| 6           | **C** | G     | A     | T     | A     | **A** | B   |   
| 7           | **C** | T     | G     | G     | A     | **A** | B   |
| 8           | **A** | T     | G     | T     | G     | **C** | A   |
| 9           | **A** | G     | G     | G     | G     | **C** | A   |
| 10          | **C** | T     | G     | G     | A     | **A** | B   |

Based on this assumption, we could assign individuals to populations if all we knew about them was which nucleotide they are at each SNP. If we have lots of SNPs (i.e. 1,000s) we could do this very reliably. Luckily for you Mason, we already know which nucleotide individuals from two different silvereye populations are across 112,000 SNPs. 

<img width="400" src="https://asendellprice.github.io/img/Silvereye_in_hand_1.jpg">

**Above:** *This is a silvereye. It is a small bird that is originally from Australia, but is very good at colonising islands accross the Pacific Ocean.*

The file mystery.012 contains nucleotide information for silvereyes from two populations (New Zealand and French Polynesia). I am not going to tell you which individuals are from where but using a programming language called 'R' we are going to assign individuals to populations based on their SNPs! So here goes . . . 

**Step 1:** <br>
Open the program called 'R Studio' <br>

**Step 2:**
Select file, new script <br>

**Step 3:**
Set the working directory (i.e. which folder are we working from) <br>
setwd("~/Documents") <br>

**Step 4:** Load the packages we need <br>

library(gdsfmt) <br>
library(SNPRelate) <br>
library(dplyr) <br>
library(ggplot2) <br>
library(RColorBrewer) <br>
library(genoscapeRtools) <br>
library(devtools) <br>
library(ggthemes) <br>

**Step 5:** Read in the SNP files <br>
SNPs <- read_012("mystery") <br>

**Step 6:** Convert our .012 file into a different format (gds) <br>
snpgdsCreateGeno(gds.fn = "mystery.gds", <br>
                 genmat = SNPs, <br>
                 sample.id = rownames(SNPs), <br>
                 snp.id = colnames(SNPs), <br>
                 snpfirstdim = FALSE) <br>

**Step 7:** Open a connection to the file <br>
mystery_gds <- snpgdsOpen("mystery.gds")

#Compute Princple Components
pca2 <- snpgdsPCA(ZOLA_clean_gds, autosome.only = FALSE)

pc.percent <- pca2$varprop*100
head(round(pc.percent, 2))

#Turn the PCA results in to a dataframe/table
tab2 <- data.frame(sample.id = pca2$sample.id,
                   EV1 = pca2$eigenvect[,1],    # the first eigenvector
                   EV2 = pca2$eigenvect[,2],    # the second eigenvector
                   stringsAsFactors = FALSE) %>%
  tbl_df()

tail(tab2) tail(pop_code)

# Plot the data
# First we colour code the data
pop_code <- read.table("VCFs/Initial_Filtered/FP_plus_NZ/samples_in_vcf_76K.txt", header = TRUE, 
                       stringsAsFactors = FALSE, sep = "\t") %>% 
  tbl_df() %>% select(sample.id, Population)

head(pop_code)

# Then we join the Eigevectors with the population codes using the sample.id column
tab3 <- left_join(tab2, pop_code) 
head(tab3)

cbPalette2 <- c("#999999", "#E69F00")

# Use ggplot to plot the results:
PCA_Plot <- ggplot(tab3, aes(x = EV1, y = EV2, colour = Population)) +
  geom_point(size = 3) +
  stat_ellipse() +
  scale_colour_manual(values=cbPalette2) +
  theme_few()

PCA_Plot + labs(x = "PC1") + labs(y = "PC2")



