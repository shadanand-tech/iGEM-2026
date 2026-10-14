
Scripts:

Wavelet Packet Transforms:

This script converts each protease into a signal using the cpvh vector used and defined at the beginning of the script. We then go on to decompose  the signal up to 3 levels, then run a correlation with the decompositions of Hip1. The final output is a cross correlation score between the proteases and Hip1.

Protease Substrate Acquisition:

This script very simply accepts a set of UniProt IDs of the serine proteases we had, and first converts the UniProt IDs to Merops IDs, and then tabulates the substrates of each protease along with the substrates and their Merops IDs.

ESM2 embedding:

This script runs the PLM, which accepts the protease and substrate data and encodes it onto the drive. This data is then used by the LightGBM model to train.

LightGBM training:

This is a CPU-based decision tree model that is trained based on the encoded data provided by ESM2. This model, when trained, can then predict the cleavability of the given substrate provided a protease. The negative samples used here are the different windows within which the protease does not cleave the substrate. The positives, then, are obviously the binding windows of the proteases.

REWARD FUNCTION

1)SOLUBILITY: The script accepts a amino acid sequence where each amino acid has a numeric score, After summing up the scored an average calculated. This is the solubility score for that particular sequence.More the score more soluble

2)HYDROPHOBICITY: Based on Kyte-Doolittle Table for Hydrophobicity,GRAVY of an input amino acid sequence is calculated.

3)PH: scripts calculates the iso-electric pH of an amino acid sequence , find the absolute difference between them. Library used is Bio.SeqUtils.ProtParam

4)CLEAVABILTY
    1)serine cleavablity: predicts if a given amino acid sequence is serine protease cleavable or not.Output 0 if not and 1 if cleavable
    2)Models Used :logistic regression,knn,Support Vector Machine(svm),Random Forest and decison Tree
    
TRANSITION PROBABILITY MATRIX AND SEQUENCE GENERATION

DATA: ~1800 LINKER SEQUENCES

Scripts creates an Transition probability Matrix using first order Markov chain principle

Based on this TPM insertion,substitution and deletion probabilities for generating daughter sequences from parent sequences is engineered
The amount of daughter sequences generated is a changeable parameter

FINAL CODE:

script combines all the reward function into a single vector, the sequence generation and the most important pareto optimzation which is required for filtering out / evaluation " GOOD" sequences 
The initial parent sequence , the top k good sequences per generation and number of generation are the changeable parameters

