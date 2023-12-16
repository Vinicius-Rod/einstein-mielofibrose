# einstein-mielofibrose
Trabalho de Anotação de Variantes Somáticos - Curso de Bioinformática HIAE

Pipe para rodar no Google Colab


##Grupo:
1.   Vinicius Garcia Rodolfo
2.   Victor Baca
3.   Victoria Leite
4.   Silas Fernandes Eto


## PREPARANDO O AMBIENTE

Remover diretório 

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

Rodar cada linha em uma célula diferente

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
