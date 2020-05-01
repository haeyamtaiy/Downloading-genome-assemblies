# Downloading-genome-assemblies
A fast and easy way to download many genome assemblies of organisms with a mutual taxanomic group at a time from ncbi.
In this example we will be downloading all the Rodentia assemblies.

## Creating your assembly summary text
Use the ncbi genome information by organism [page](https://www.ncbi.nlm.nih.gov/genome/browse/#!/overview/) to search for the desired organism taxanomic group e.g. ['Rodentia'](https://www.ncbi.nlm.nih.gov/genome/browse/#!/eukaryotes/rodentia)
- Left corner there is a download button, this will download the summary text file for the specific search (Rodentia)
- This file is downloaded in a csv format.

## Converting csv to tsv
This step is necessary in order to be able to separate the fields of the summary text file to have just the GenBank ftp field. 
- This is done by replacing the commas (CSV = comma-separated value file) to tabs (TSV = tab-separated value field)

```
cat eukaryotes.csv | tr "," "\\t" > eukaryotes.tsv
```

## Changing the format of the links 

