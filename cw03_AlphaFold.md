# Przewidywanie struktur biomolekół z Alpha Fold


## Potrzebne adresy

- baza danych białek UniProt: https://www.uniprot.org
- baza danych predykcji AF: https://alphafold.ebi.ac.uk
- AlphaFold server (AF3): https://alphafoldserver.com
- ColabFold (AF2): https://github.com/sokrypton/ColabFold


## Białkowe adresy 

znajdź TATA binding protein (TBP) P20226 w bazie:
- predykcji AF
  - jakie są wartości PAE i pLDDT, o czym to świadczy
- UniProt:
  - znajdź sekwencję i pobierz plik FASTA
  - znajdź struktury, pobierz wybrany plik pdb

## AlphaFold Serwer

### Przeglądanie przykładów

![](resources/AFS_examples01.png)

![](resources/AFS_examples02.png)

### Ćw 1: Białko
GB1 https://www.rcsb.org/structure/1GB1 - fragment białka P06654

Sekwencja: `MTYKLILNGKTLKGETTTEAVDAATAEKVFKQYANDNGVDGEWTYDDATKTFTVTE`

Zastąp region alfa helisy (`AATAEKVFKQYANDN`) sekwencją luźnego łącznika: `GSGSGSGSGSGSGSG`

Jak zmieniła się struktura?
Jak zmmieniły się wartości PAE?

### Ćw 2: Białko + ligand

Białko: kinaza ADK

```
>sp|P69441|KAD_ECOLI Adenylate kinase OS=Escherichia coli (strain K12) OX=83333 GN=adk PE=1 SV=1
MRIILLGAPGAGKGTQAQFIMEKYGIPQISTGDMLRAAVKSGSELGKQAKDIMDAGKLVT
DELVIALVKERIAQEDCRNGFLLDGFPRTIPQADAMKEAGINVDYVLEFDVPDELIVDRI
VGRRVHAPSGRVYHVKFNPPKVEGKDDVTGEELTTRKDDQEETVRKRLVEYHQMTAPLIG
YYSKEAEAGNTKYAKVDGTKPVAEVRADLEKILG
```

ligand: ATP


1. Sprawdź, jakie aminokwasy wiążą ATP
2. Wyświetl białko jako powierzchnię Gaussowską: ATP jest eksponowane czy schowane?
3. zamień pętlę wiążącą ATP `GAPGAGKG` (motyw Walkera A) na sztywny motyw `PAPPAAPA` 

```
>P69441 mut
MRIILLPAPPAAPATQAQFIMEKYGIPQISTGDMLRAAVKSGSELGKQAKDIMDAGKLVT
DELVIALVKERIAQEDCRNGFLLDGFPRTIPQADAMKEAGINVDYVLEFDVPDELIVDRI
VGRRVHAPSGRVYHVKFNPPKVEGKDDVTGEELTTRKDDQEETVRKRLVEYHQMTAPLIG
YYSKEAEAGNTKYAKVDGTKPVAEVRADLEKILG
```

4. Sprawdź, jakie aminokwasy wiążą ATP
5. Wyświetl białko jako powierzchnię Gaussowską: ATP jest eksponowane czy schowane?
6. Czy zmieniła się struktura białka? Czy zminiła się macierz Expected Position Error? 


### Ćw 3: Białko + DNA

TATA-box-binding protein

```fasta
>sp|P20226|TBP_HUMAN TATA-box-binding protein OS=Homo sapiens OX=9606 GN=TBP PE=1 SV=2
MDQNNSLPPYAQGLASPQGAMTPGIPIFSPMMPYGTGLTPQPIQNTNSLSILEEQQRQQQ
QQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQAVAAAAVQQSTSQQATQGTSGQAPQ
LFHSQTLTTAPLPGTTPLYPSPMTPMTPITPATPASESSGIVPQLQNIVSTVNLGCKLDL
KTIALRARNAEYNPKRFAAVIMRIREPRTTALIFSSGKMVCTGAKSEEQSRLAARKYARV
VQKLGFPAKFLDFKIQNMVGSCDVKFPIRLEGLVLTHQQFSSYEPELFPGLIYRMIKPRI
VLLIFVSGKVVLTGAKVRAEIYEAFENIYPILKGFRKTT
```

DNA 1: `GGCTATAAAAGGG`
DNA 2: `CCCTTTTATAGCC` (sekwencja komplementarna od tyłi)

**Zmiana sekwencji DNA**

DNA 1: `GGCGCGCGCGCGG`
DNA 2: `CCGCGCGCGCGCC`

### Ćw 4: Białko + peptyd + jony

Kalmodulina P0DP23 + peptyd (fragment MLCK - Myosin Light Chain Kinase `KRRWKKNFIAVSAANRFKKISS`) + jony Ca2+

Z eksperymentów wiemy, że jony wapnia są potrzebne do stabilnego wiązania Kalmoduliny i MLCK. Wydaje się, że MLCK może łączyć się z kalmoduliną bez Ca2+.

Przeprowadź predykcję struktury kalmodulina + peptyd z 4 jonami Ca2+ oraz bez


## AlphaFold2

### ColabFold
Otwórz https://github.com/sokrypton/ColabFold wybierz notatnik `AlphaFold2.ipynb`

Utwórz kopię na własnym dysku i uruchom całość

- Obejrzyjmy wykres i plik MSA
- Ile struktur białka zostało wytworzonych?

#### Ćw 1: Białko
Jak w AlphaFold Server

#### Ćw 2: Własne MSA
Edytuj MSA z poprzedniego punktu i pobierz
W komórce `MSA options` wybierz "msa_mode" jako "custom", użyj edytowanego MSA

### ColabFold  z Docker/Apptainer(Singularity)
ColabFold nie wymaga pobierania baz danych, wyszukuje MSA online (ograniczona liczba wyszukań)

Dla krótkich sekwencji wystarczy karta graficzna z pamięcią 12GB lub mniejsza

https://github.com/sokrypton/ColabFold/wiki/Running-ColabFold-in-Docker

Uruchomienie w kontenerze to 3 kroki. Tutaj przykład z Apptainerem (instalowanym na klastrach obliczeniowych, np w ICM)
```bash
# create container (this will create a `colabfold_1.6.0-cuda12.sif` file)
singularity pull docker://ghcr.io/sokrypton/colabfold:1.6.0-cuda12

#download weights
singularity run -B /local/path/to/cache:/cache \
  colabfold_1.6.0-cuda12.sif \
  python -m colabfold.download

# uruchomienie predykcji
singularity run --nv \
  -B /local/path/to/cache:/cache -B $(pwd):/work \
  colabfold_1.6.0-cuda12.sif \
  colabfold_batch /work/test.fa /work/output

```
