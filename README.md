# ImmunoMap
Applies a model of negative selection to identify regions of given proteins that will trigger immune response

Project Summary (ImmunoMap)
This project aims to develop a computational tool that predicts how likely a foreign protein is to trigger an immune response in humans. The program will analyze the protein sequence and identify small peptide fragments that are typically presented by MHC molecules to T cells. It will then compare these fragments against a comprehensive library of human peptides that are normally displayed during immune development—a process that teaches the immune system to ignore “self” proteins. By calculating how different each foreign peptide is from the closest human counterpart, the tool will assign a score to each fragment, representing its potential to be recognized as foreign and therefore immunogenic. The ultimate goal is to generate a heat map of the protein, highlighting areas most likely to provoke an immune response, and to guide mutations that can reduce immunogenicity while maintaining function.
The Pipeline: Step-by-Step
1. Build "Self" Library (Human Proteome)
	• Source: UniProt complete human proteome 
		○ https://www.uniprot.org/proteomes/UP000005640 
			§ Future reference:
			§ Rats:
				□ https://www.uniprot.org/proteomes/UP000002494
			§ Mice:
				□ https://www.uniprot.org/proteomes/UP000000589 
	• Process:
		○ Generate overlapping peptides (8-11mers for MHC I, 12-25mers for MHC II)
		○ Filter to peptides predicted to bind MHC (using NetMHCpan or MHCflurry)
	• Result: A library of "expected" self MHC-presented peptides
		○ We can make this a hashed dictionary or a BLAST-able database

2. Analyze the Foreign Protein
	• Input: Viral, bacterial, or therapeutic protein
	• Process:
		○ Generate overlapping peptides (same lengths as above)
		○ Predict which of these bind MHC
	• Next:
		○ For each predicted binder, compare it to the "self" library

3. Scoring the Peptides ("Substitution Distance" Metric)
	• For each peptide, compare against the self-library:
		○ Find the closest match (minimum Hamming/Levenshtein distance)
		○ Score = number of substitutions (edit distance)
	• Direct match (distance = 0): low/no immunogenicity
	• Higher distance: potentially more immunogenic
We can also potentially factor in MHC binding affinity to weigh things (e.g., high-affinity binding + high distance = big red flag).

4. Visualize as a Heatmap
	• Map scores back to protein position
	• Color by distance score (or even use a multi-layered map for affinity + distance)

Optional Advanced Ideas
	• MHC allele-specific negative selection: We could build separate "self-peptide" libraries per HLA allele since thymic selection is allele-specific
	• Anchor residue consideration: Not all positions in MHC-bound peptides are equally important (e.g., T-cell receptor contacts vs. MHC anchor positions). We could weight mismatches differently depending on position
	• Structure preservation scoring: Use tools like FoldX, Rosetta, or AlphaFold2 to predict if mutations preserving immunogenicity reduction still preserve protein folding and generate most useful future mutations.
Expand library to encompass other organisms![image](https://github.com/user-attachments/assets/59769a57-e762-4219-a58c-ffdf3207fa0c)
