### 提取chr和position转换SNP

```shell
nohup wget -c ftp://ftp.ncbi.nih.gov/snp/latest_release/VCF/GCF_000001405.25.gz &

zcat meta-AAAgen-final-sumstat.txt.gz | awk '{print "chr"$1"\t"$2}' > positions.txt
# 删除第一行
tail -n +2 positions.txt > temp && mv temp positions.txt

# 将空格替换为制表符
# sed 's/ /	/g' positions.txt > temp && mv temp positions.txt

# 使用 bcftools 查询 dbSNP VCF 文件中的 SNP ID
bcftools query -f '%CHROM\t%POS\t%ID\n' -R positions.txt GCF_000001405.25 > snp_ids.txt

# 使用 bcftools 查询 dbSNP VCF 文件中的 SNP ID
bcftools query -f '%CHROM\t%POS\t%ID\n' -R positions.txt GCF_000001405.25.vcf > snp_ids.txt

```

### bcftools报错及解决

```shell
## 方法一
ldconfig -p | grep libgsl
# 直接创建软链接使得libgsl.so.25链接到已有的/lib/x86_64-linux-gnu/libgsl.so.23
ln -s ~/miniconda3/lib/libcrypto.so.* ~/miniconda3/lib/libcrypto.so.1.0.0
## 方法二
# 或者，先卸载当前bcftools，创建一个环境再安装指定版本的bcftools
conda uninstall bcftools
conda create -n bcftools_software
conda activate bcftools_software
conda install -c bioconda bcftools=1.9
```



### bcftools

bcftools

