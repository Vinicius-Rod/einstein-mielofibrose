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

### QUANTIDADE DE VARIANTES DE CADA AMOSTRA

```bash
mkdir -p /content/einstein-mielofibrose/analises/ && mv /content/einstein-mielofibrose/vep_output/*.tsv /content/einstein-mielofibrose/analises/
```

```bash
diretorio_origem="/content/einstein-mielofibrose/analises/"
!find $diretorio_origem -name "*WP*.tsv" | sort | uniq | xargs -I {} sh -c 'numero_arquivo=$(basename "{}" | awk -F"[_.]" "{print tolower(\$2)}" | sed "s/[^0-9]//g"); linhas=$(($(wc -l < "{}") - 1)); if [ "$numero_arquivo" != "" ] && [ "$numero_arquivo" != "allelelength" ] && [ "$numero_arquivo" != "tsv" ]; then echo "A amostra WP$numero_arquivo tem $linhas variante(s)."; fi' _
```
!sh einstein-mielofibrose/vep-gc.sh WP291 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP295 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP297 Myelofibrosis.txt
!sh einstein-mielofibrose/vep-gc.sh WP306 Myelofibrosis.txt

```
