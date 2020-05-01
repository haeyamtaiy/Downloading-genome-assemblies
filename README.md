# Downloading-genome-assemblies
A fast and easy way to download many genome assemblies of organisms with a mutual taxanomic group at a time from ncbi.
In this example we will be downloading all the Rodentia genome assemblies.

## Creating your assembly summary text
Use the ncbi genome information by organism [page](https://www.ncbi.nlm.nih.gov/genome/browse/#!/overview/) to search for the desired organism taxanomic group e.g. ['Rodentia'](https://www.ncbi.nlm.nih.gov/genome/browse/#!/eukaryotes/rodentia)
- Left corner there is a download button, this will download the summary text file for the specific search (Rodentia)
- This file is downloaded in a csv format.

## Converting csv to tsv
This step is necessary in order to be able to separate the fields of the summary text file to have just the GenBank ftp field. 
- This is done by replacing the commas (CSV = comma-separated value file) to tabs (TSV = tab-separated value field)
- Need to also remove the first line as it contains the column title 'GenBank ftp'.
```
cat eukaryotes.csv | tr "," "\\t" | awk NR\>1 > eukaryotes.tsv
```

## Cutting the links and changing the format of them
- The 'GenBank ftp' field is numbered 15, this makes it easy to cut this field out into a new file.
- However the links are placed in quatation marks "",therefore need to replace these with nothing.
- In order to make the ftp link downloadable need to include the function 'wget' (this is a function which extracts the contents of a link) at the beginning of each line and 'genomic.fna.gz' (this ensures that you are downloading the zipped FASTA format of the genomic assembly) at the end of each link.

```
cat eukaryotes.tsv | cut -f 15 | sed 's/"//g' | awk 'BEGIN{FS=OFS="/";filesuffix="genomic.fna.gz"}{ftpdir=$0;asm=$10;file=asm"_"filesuffix;print "wget "ftpdir,file}' > links_fna_files.sh
```

## Run download
The 'links_fna_file.sh' has been saved as a script with a 'wget' command at each line. This allows you to run the script which downloads all the zipped FASTA files 

```
source links_fna_files.sh
```
Each file is not as big as you are downloading the compressed version.

