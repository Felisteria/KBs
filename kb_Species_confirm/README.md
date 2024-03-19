# Example knowledgebase: minhash based

This is an example knowledgebase for the minhash based feature 'Species confirmation' of the Custom Genotyping plugin.


## Contents

### Info file

The `info.json` file is a [JSON] format file that must, at minimum,
contain string values for the keys `name` and `version`. It may
optionally contain a key `description` with a string value. It may also
optionally contain a key `changelog`, which is an object mapping strings
to strings. Each key in the changelog object corresponds to a version,
and each value a description of what happened for that version.

Example: 

```json
{
  "version": "2.0",
  "name": "minhash based example knowledgebase",
  "description": "An example knowledgebase for minhash based features",
  "changelog": {
    "1.0": "First version",
    "1.1": "corrected typo in genome_info.tsv",
    "2.0": "added the Escherichia marmotae fake_subspecies sample"
  }
}
```

### Sourmash params file

The `sourmash_params.json` file is a [JSON] formatted file that
includes the kmer size and scaling factor

Example:

```json
{
	"kmer_size": 31,
	"scaling_factor": 5000
}
```

### Signature file

The `genomes.sig` is a [JSON] formatted file that includes the minhash
signatures. It can be generated with the [sourmash] sketch function or
the "Export Minhash Signatures" menu item in BIONUMERICS (Genotyping
Tools>Export Minhash Signatures). The BN export function will label
each signature with the filename "{entry_key}.fasta". Additionally,
you need to copy the used kmer size and scaling factor into the
[sourmash params file](#Sourmash-params-file).

### Genomes info file

The `genome_info.tsv` file is a [TSV] formatted file that includes the
following columns:
- identifier: Always required. Must be unique within the file! Must
  be equal to "filename" in the [signature file](#Signature-file) without
  '.fasta'. This is the entry key from the BIONUMERICS db when you
  create the signatures with the "Export Minhash Signatures" menu item.
- genome_accession: Optional. The accession corresponding to the
  sequence. [Genbank] and [RefSeq] accessions may be automatically
  hyperlinked in the report.
- genome_name: description of the genome
- taxid: [taxid] number
- genus_name: genus name
- genus_threshold: a mash containment threshold between '0.0' and
  '100.0' - thresholds lower than 80 are however not recommended as the
  accuracy of minhashing-based similarity becomes unreliable.
- species_name: species name ("-" if unknown)
- species_threshold: a mash containment threshold between '0.0' and
  '100.0' or "-" if species is unknown. Should be smaller or equal than
  the genus threshold.
- subspecies_name: subspecies name ("-" if unknown)
- subspecies_threshold: a mash containment threshold between '0.0' and
  '100.0' or "-" if subspecies is unknown. Should be smaller or equal
  than the species threshold.

Example:

```tsv
CP033092	CP033092.2	Escherichia coli DSM 30083 = JCM 1649 = ATCC 11775	866789	Escherichia	93	coli	95	-	-
CP026802	CP026802.1	Shigella sonnei strain ATCC 29930	624	Shigella	99	sonnei	99	-	-
CP025979	CP025979.1	Escherichia marmotae strain HT073016	1499973	Escherichia	93	marmotae	95	fake_subspecies	98
```

[taxid]: https://www.ncbi.nlm.nih.gov/taxonomy
[sourmash]: https://sourmash.readthedocs.io
[JSON]: https://en.wikipedia.org/wiki/JSON
[TSV]: https://en.wikipedia.org/wiki/Tab-separated_values
[Genbank]:  https://www.ncbi.nlm.nih.gov/Sequin/acc.html
[RefSeq]: https://www.ncbi.nlm.nih.gov/books/NBK21091/table/ch18.T.refseq_accession_numbers_and_mole/?report=objectonly
