# einstein-mielofibrose
Trabalho de Anotação de Variantes Somáticos - Curso de Bioinformática HIAE

Pipe para rodar no Google Colab


Grupo:
1.   Vinicius Garcia Rodolfo
2.   Victor Baca
3.   Victoria Leite
4.   Silas Fernandes Eto


## Preparando o ambiente

Remover diretório 

```bash
!rm -r /content/sample_data/
```

## Instalação

```bash
!rm -rf einstein-mielofibrose
!git clone https://github.com/Vinicius-Rod/einstein-mielofibrose
```

```bash
%%bash
git clone --recurse-submodules https://github.com/samtools/htslib.git
git clone https://github.com/samtools/bcftools.git
cd bcftools
make
make install
```
