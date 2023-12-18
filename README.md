# einstein-mielofibrose
Trabalho de Anotação de Variantes Somáticos - Curso de Bioinformática HIAE

Pipe para rodar no Google Colab

Referência: https://github.com/renatopuga/lmabrasil-hg38


## Grupo:
1.   Vinicius Garcia Rodolfo
2.   Victor Baca
3.   Victoria Leite
4.   Silas Fernandes Eto

## PREPARANDO O AMBIENTE

Remover diretório sample_data

```bash
%%bash
rm -r /content/sample_data/
```

## INSTALAÇÃO

```bash
%%bash
rm -rf einstein-mielofibrose
git clone https://github.com/Vinicius-Rod/einstein-mielofibrose
```

```bash
%%bash
git clone --recurse-submodules https://github.com/samtools/htslib.git
git clone https://github.com/samtools/bcftools.git
cd bcftools
make
make install
```

```bash
%%bash
# Fonte: https://gist.github.com/mwufi/6718b30761cd109f9aff04c5144eb885
pip install udocker
udocker --allow-root install
```

```bash
!udocker --allow-root pull ensemblorg/ensembl-vep
```

## FILTRAGEM

```
#Parametros utilizados
  -filter "(MAX_AF <= 0.01 or not MAX_AF) and
  (FILTER = PASS or not FILTER matches strand_bias,weak_evidence) and
  (SOMATIC matches 1 or (not SOMATIC and CLIN_SIG matches pathogenic)) and
  (not CLIN_SIG matches benign) and \
  (not IMPACT matches LOW) and \
  (Symbol in hpo/$HPO)"
  ```

```bash
!sh einstein-mielofibrose/vep-gc.sh WP048 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP056 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP060 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP064 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP066 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP072 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP078 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP087 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP093 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP126 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP140 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP160 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP162 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP164 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP170 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP180 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP188 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP196 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP204 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP212 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP216 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP270 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP274 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP276 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP280 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP285 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP291 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP295 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP297 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP306 Myelofibrosis.txt
```

### QUANTIDADE DE VARIANTES DE CADA AMOSTRA

```bash
mkdir -p /content/einstein-mielofibrose/analises/ && mv /content/einstein-mielofibrose/vep_output/*.tsv /content/einstein-mielofibrose/analises/
```

```bash
%%bash

diretorio_origem="/content/einstein-mielofibrose/analises/"
find $diretorio_origem -name "*WP*.tsv" -print0 | sort -z | uniq -z | xargs -0 -I {} bash -c '
    numero_arquivo=$(basename "{}" | awk -F"[_.]" "{print tolower(\$2)}" | sed "s/[^0-9]//g")
    linhas=$(($(wc -l < "{}") - 1))

    if [ "$numero_arquivo" != "" ] && [ "$numero_arquivo" != "allelelength" ] && [ "$numero_arquivo" != "tsv" ]; then
        if [ $linhas -gt 0 ]; then
            echo "A amostra WP$numero_arquivo tem $linhas variante(s)"
        else
            echo "A amostra WP$numero_arquivo tem 0 variante(s) - nenhuma variante passou pelo filtro"
        fi
    fi
'
```

##  AMOSTRAS

```BASH
import pandas as pd
pd.set_option('display.max_columns', None)
df_WP048 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP048_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP056 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP056_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP060 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP060_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP064 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP064_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP066 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP066_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP072 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP072_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP078 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP078_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP087 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP087_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP093 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP093_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP126 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP126_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP140 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP140_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP160 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP160_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP162 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP162_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP164 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP164_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP170 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP170_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP180 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP180_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP188 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP188_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP196 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP196_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP204 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP204_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP212 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP212_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP216 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP216_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP270 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP270_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP274 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP274_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP276 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP276_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP280 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP280_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP285 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP285_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP291 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP291_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP295 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP295_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP297 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP297_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
df_WP306 = pd.read_csv('/content/einstein-mielofibrose/analises/liftOver_WP306_hg19ToHg38.vep.filter.tsv', sep='\t', index_col=False, engine='python')
```

```bash
import pandas as pd
dataframes = [
    df_WP048, df_WP056, df_WP060, df_WP064, df_WP066,
    df_WP072, df_WP078, df_WP087, df_WP093, df_WP126,
    df_WP140, df_WP160, df_WP162, df_WP164, df_WP170,
    df_WP180, df_WP188, df_WP196, df_WP204, df_WP212,
    df_WP216, df_WP270, df_WP274, df_WP276, df_WP280,
    df_WP285, df_WP291, df_WP295, df_WP297, df_WP306
]


df_combined = pd.concat(dataframes, ignore_index=True)
colunas_desejadas = ['TumorID','CHROM', 'MAX_AF', 'SYMBOL', 'Consequence', 'BIOTYPE', 'VARIANT_CLASS', 'SIFT', 'PolyPhen', 'IMPACT', 'CLIN_SIG', 'FILTER']
df_combined_subset = df_combined[colunas_desejadas]
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
pd.set_option('display.max_colwidth', None)
display(df_combined_subset)
df_combined_subset.to_csv('/content/einstein-mielofibrose/analises/combined_data_subset.csv', index=False)
```
