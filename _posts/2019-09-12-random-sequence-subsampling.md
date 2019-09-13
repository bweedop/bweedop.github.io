---
layout: article
title: Random Subsampling Sequences (FASTA format)
key: 20190912
---

This is a pretty simple script but one that I have seen a number of people request out on Biostars and StackOverflow.

Sometimes you have a bit too much sequence data and you would like to subsample prior to your analysis. You can use this script to do just this. You will need give it fasta file your a subsetting, the number of sequences you would like, and the output file name.

```{python}
import sys
from random import sample
from Bio import SeqIO
from Bio.Seq import Seq
from Bio.SeqRecord import SeqRecord

def main ():
	seq_file = sys.argv[1]
	num_seqs = int(sys.argv[2])
	subset_file = sys.argv[3]
	   
	seqs = [x for x in SeqIO.parse(seq_file, "fasta")]
			
	subsample = sample(seqs, num_seqs)
						
	SeqIO.write(subsample, subset_file, "fasta")
							        
									
if __name__ == '__main__':
	main()
```

```
# Example of how to call the script
python3 subsample-seqs.py input.fasta 200 output.fasta
```

However, you might want to get a bit more creative with your subsampling rather than purely random. Suppose you have sequences that fall into distinct groups (spatially or temporally) and you want to sample from the groups equally. With a little more work this could be done (as long as you have some informative labels in your fasta file). This is something for future me to work on.
