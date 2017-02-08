# Data Inspection
1. File Size
$ du -h fang_et_al_genotypes.txt
$ du -h snp_position.txt
# fang_et_al_genotypes.txt= 11M
# snp_position.txt= 84K
2. Number of lines/colums/
$ awk -F "\t" '{print NF; exit}' fag_et_al_genotypes.txt
$ cat snp_position.txt
$ tail -n +2 snp_position.txt
$ wc snp_position.txt 
$ du -h snp_position.txt
$ awk -F "\t" '{print NF; exit}' snp_position.txt
# Data Processing
1. Extracting Maize Data
$ grep -E "(ZMMIL|ZMMLR|ZMMMR)" fang_et_al_genotypes.txt > maize_genotypes.txt
2. Extracting Teosinte Data
$ grep -E “(ZMPBA|ZMPIL|ZMPJA)”fang_et_al_genotypes.txt > teosinte_genotypes.txt
3. Reput in the header
$ grep "Group" fang_et_al_genotypes.txt > header.txt
$ cat header.txt maize_genotypes.txt > maize.txt
$ cat header.txt teosinte_genotypes.txt > teosinte.txt
4. Cut files
$ cut -f 1,3,4 snp_position.txt > snp_position_needed_columns.txt
$ cut -f 3-968 maize.txt > maize_F.txt
$ cut -f 3-968 teosinte.txt > teosinte_F.txt
5. Transpose Files
$ awk -f transpose.awk maize_F.txt > transposed_maizeF.txt
$ awk -f transpose.awk teosinte_F.txt > transposed_teosinteF.txt
6. Sort files
$ sort -k1,1 snp_position_needed_columns.txt > snp_position_needed_columns_sorted.txt
$ sort -k1,1 transposed_maizeF.txt >sorted_maizeF.txt
$ sort -k1,1 transposed_teosinteF.txt > sorted_teosinteF.txt
7. Join files
$ join -t $'\t' -1 1 -2 1 snp_position_needed_columns_sorted.txt sorted_teosinteF.txt > teosinteF_SNP_genotypes.txt
$ join -t $'\t' -1 1 -2 1 snp_position_needed_columns_sorted.txt sorted_maizeF.txt > maizeF_SNP_genotypes.txt
8. Sort Files
$ sort -k2,2n teosinteF_SNP_genotypes.txt > teosinteF_sorted_chrom.txt
$ sort -k2,2n maizeF_SNP_genotypes.txt > maizeF_sorted_chrom.txt
9. Substitution
$ sed 's/<TAB>/?/g' maizeF_sorted_chrom.txt > maizeF_sorted_chrom_sub.txt
$ sed 's/<TAB>/?/g' teosinteF_sorted_chrom.txt > teosinteF_sorted_chrom_sub.txt
$ sed 's/?/-/g' maizeF_sorted_chrom.txt > maizeF_sorted_chrom_sub_dash.txt
$ sed 's/?/-/g' teosinteF_sorted_chrom.txt > teosinteF_sorted_chrom_sub_dash.txt
10. Creating all Maize files
$ awk '$2 == 1' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr1_decreasing.txt
$ awk '$2 ~ /2/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr2_ decreasing.txt 
$ awk '$2 ~ /3/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr3_decreasing.txt
$ awk '$2 ~ /4/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr4_decreasing.txt
$ awk '$2 ~ /5/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr5_decreasing.txt
$ awk '$2 ~ /6/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr6_decreasing.txt
$ awk '$2 ~ /7/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr7_decreasing.txt
$ awk '$2 ~ /8/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr8_decreasing.txt
$ awk '$2 ~ /9/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr9_decreasing.txt
$ awk '$2 ~ /10/' maizeF_sorted_chrom_sub_dash.txt | sort -k3,3nr > maize_chr10_decreasing.txt
$ awk '$2 == 1' maizeF_sorted_chrom_sub.txt |sort -k3,3n > maize_chr1_increasing.txt
$ awk '$2 ~ /2/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr2_increasing.txt 
$ awk '$2 ~ /3/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr3_increasing.txt 
$ awk '$2 ~ /4/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr4_increasing.txt 
$ awk '$2 ~ /5/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr5_increasing.txt 
$ awk '$2 ~ /6/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr6_increasing.txt 
$ awk '$2 ~ /7/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr7_increasing.txt 
$ awk '$2 ~ /8/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr8_increasing.txt 
$ awk '$2 ~ /9/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr9_increasing.txt 
$ awk '$2 ~ /10/' maizeF_sorted_chrom_sub.txt | sort -k3,3n > maize_chr10_increasing.txt 
11. Creating all Teosinte files
$ awk '$2 == 1' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr1_decreasing.txt
$ awk '$2 ~ 2' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr2_decreasing.txt
$ awk '$2 ~ 3' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr3_decreasing.txt
$ awk '$2 ~ 4' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr4_decreasing.txt
$ awk '$2 ~ 5' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr5_decreasing.txt
$ awk '$2 ~ 6' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr6_decreasing.txt
$ awk '$2 ~ 7' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr7_decreasing.txt
$ awk '$2 ~ 8' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr8_decreasing.txt
$ awk '$2 ~ 9' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr9_decreasing.txt
$ awk '$2 ~ 10' teosinteF_sorted_chrom_sub_dash.txt | sort -k3,3n > teosinte_chr10_decreasing.txt
$ awk '$2 == 1' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr1_increasing.txt
$ awk '$2 ~ 2' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr2_increasing.txt
$ awk '$2 ~ 3' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr3_increasing.txt
$ awk '$2 ~ 4' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr4_increasing.txt
$ awk '$2 ~ 5' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr5_increasing.txt
$ awk '$2 ~ 6' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr6_increasing.txt
$ awk '$2 ~ 7' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr7_increasing.txt
$ awk '$2 ~ 8' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr8_increasing.txt
$ awk '$2 ~ 9' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr9_increasing.txt
$ awk '$2 ~ 10' teosinteF_sorted_chrom_sub.txt | sort -k3,3nr > teosinte_chr10_increasing.txt
