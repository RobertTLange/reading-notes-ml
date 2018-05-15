# Title: Data-efficient inference of hierarchical structure in sequential data by information-greedy grammar inference

# Author: Schoenhense and Faisal

#### General Content: Combat "overfitting" of greedy grammatical inference algos such as sequitur by introducing decision rule based on  Shannon entropy decrease. This way they introduce form of regularizer.         Show that IGGI does not fit noise when sequence is generated without any underlying hierarchical rules.


#### Keypoints: 

* Algos: Sequitur, MDLcompress, G-Lexis
* Iterative repeat replacement (IRR): Longest-match, byte-pair coding, compressive
* CFG + MDL = grammar-based universal source code
* Info theory approach: More symbols used = more info needed to give meaning to symbol - average info/entropy needed per symbol increases
* Idea: Greedily + iteratively replace bigrams by minimizing info content of coding string
* New definition of size of grammar: Previously - based on concatenated string of all symbols needed to write out production rules and coding sequence - now: based on info content 
* Testing on random data shows: no overfitting of noise - compression ration around 1