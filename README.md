# 14-UNDERREP

This code is created in order to parse ALFA

The actual frequency data, the VCF file has been downloaded from here:
https://ftp.ncbi.nih.gov/snp/population_frequency/latest_release/

ALFA FTP VCF
FTP Directory: https://ftp.ncbi.nih.gov/snp/population_frequency/
VCF Header
##fileformat=VCFv4.0
##build_id=20200227123210
##Population=https://www.ncbi.nlm.nih.gov/biosample/?term=GRAF-pop
##FORMAT=<ID=AN,Number=1,Type=Integer,Description="Total allele count for the population, including REF">
##FORMAT=<ID=AC,Number=A,Type=Integer,Description="Allele count for each ALT allele for the population">
#CHROM  POS     ID      REF     ALT     QUAL    FILTER  INFO    FORMAT  SAMN10492695    SAMN10492696    SAMN10492697    SAMN10492698    SAMN10492699    SAMN10492700    SAMN10492701    SAMN10492702    SAMN11605645    SAMN10492703   SAMN10492704    SAMN10492705
NC_000001.9     146267105       rs1553119693    T       G       .       .       .       AN:AC   33978:26317     36:22   56:44   1378:839        18:14   70:60   10:9    4836:3639       428:303 1414:861        66:53   40810:31247
NC_000001.10    74439690        rs1553119957    A       C       .       .       .       AN:AC   1220:0  4:0     8:0     74:0    2:0     12:0    0:0     0:0     120:0   78:0    8:0     1440:0
NC_000001.11    10498   rs1338146081    G       A,T     .       .       .       AN:AC   2072:0,0        6:0,0   2:0,0   76:0,0  0:0,0   0:0,0   2:0,0   4:0,0   26:0,0  82:0,0  4:0,0   2188:0,0
Standard VCF columns (1-9) as described in the 4.0 spec.
The CHROM and POS contain the RefSeq chrosomosome accessions and position based primariy on the latest human assembly (GRCh38.p13). The latest RefSeq chromosome accessions can be downloaded from here (https://www.ncbi.nlm.nih.gov/assembly/GCF_000001405.39/). If the rs does not map to the latest assembly, it is then mapped to GRCh37 or hg18.
If the variant exists in dbSNP it will have an RefSNP(rs) ID, otherwise it's novel variant at the time the frequency was computed and specificied as '.'. Novel variants will be assigned RefSNP in the next dbSNP build and provided in future release.
QUAL, FILTER, and INFO columns have no data and are specificied with '.'.
Columns 10-21: Observed total REF allele number (AN) and ALT allele count (AC) for each of the 12 populations represented by the BioSamples ID (ie. SAMN10492695). The BioSamples ID and population descriptions are here.
Note:
1) Most of the sites are homoallelic for REF allele and have no frequency. These sites are detected as variants in other dbGaP studies but are not currently included in current release. Example:
NC_000001.11    10001   .       T       C       .       .       .       AN:AC   192:0   0:0     0:0     0:0     0:0     0:0     0:0     0:0     2:0     0:0     0:0     194:0
NC_000001.11    10007   .       T       C       .       .       .       AN:AC   192:0   0:0     0:0     0:0     0:0     0:0     0:0     0:0     2:0     0:0     0:0     194:0
2) The *.tbi file in the directory is created with Tabix for use with SAMtools. See details at: https://samtools.sourceforge.net/. The command options for Tabix are located at: https://samtools.sourceforge.net/tabix.shtml
