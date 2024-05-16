###### logRegDeletionProbability.R ######
using data from Kristina and Victor's folding data
=> Bublic

score_out_matrix.text - number of folding for logistic regression
2020-02-12
Victor Shamanskiy
Kristina Ushakova 
Alina Mikhailova
Konstantin Popadin



###### SlipAndJump.R ######
1: READ microhomology from pair-wise alignments
- make long vertical table from the matrix
the matrix is symmetric - I need to keep only one triangle: X>Y (don't need also diagonal, which is made by '500's)
2: READ density of direct repeats per window
# make long vertical table from the matrix
the matrix is symmetric - I need to keep only one triangle: X>Y (don't need also diagonal, which is made by '500's)
3: correlate MicroHomology and  DirectRepDensity, derive HomologyAndRepeats dataset
4: READ MITOBREAK AND FILTER (KEEP ONLY MAJOR ARC DELETIONS):
#may be add perfect repeats of Orlov - yes or no for each deletion? and see, if microhomology still important?
5: READ GLOBAL FOLDING:
# make long vertical table from the matrix
the matrix is symmetric - I need to keep only one triangle: X>Y (don't need also diagonal, which is noizy and bold)
5.1: READ GLOBAL FOLDING WITH WINDOW = 100 bp: (it automaticaly rewrites the GlobalFolding matrix from the previous point 5)
# make long vertical table from the matrix
the matrix is symmetric - I need to keep only one triangle: X>Y (don't need also diagonal, which is made by '500's)
# Should we delete bold diagonal or erase it to zeroes??? If delete, dimension will be decreased - try this. delete 5 windows next to diagonal (500)
# GlobalFolding - is the whole genome without bold diagonal, not only the major arc!! Keep only major arc in downstream analyses.
# will do it when merge with InvRepDens.
6: READ INVERTED REPEATS WITH STEP 1000
6.1: READ INVERTED REPEATS WITH STEP 100 bp (it automatically rewrites InvRepDens from previous point 6)
6.2: READ INVERTED REPEATS WITH STEP 100 bp WITH OVERLAPS (it automatically rewrites InvRepDens from previous point 6.1)
not nice results - use 6.1 
7: CORRELATE GlobalFolding$Score and InvRepDens$Score - weak positive!
8: ADD InfinitySign parameter into HomologyAndRepeats dataset (13 - 16 kb vs 6-9 kb):
merge HomologyAndRepeats with merged(InvRepDens + GlobalFolding)
is GlobalFoldingScore higher within the cross according to our InfinitySign model? YES!!! 
Note: 95% CI for effect size estimate was computed with 10000 bootstrap samples
Note: Shapiro-Wilk Normality Test for in silico folding score: p-value = < 0.001
Note: Bartlett's test for homogeneity of variances for factor "3D" Position: p-value = < 0.001
we have to link better global folding and InfinitySign model - till now it was done by eye. Clusterisation? One cluster? 
9: LOGISTIC REGRESSION: HomologyAndRepeats$Deletion as a function of HomologyAndRepeats$MicroHomologyScore and HomologyAndRepeats$InfinitySign:
non significant - may be I have to take it on bigger scale! (1kb without diagonal, because this is global parameter not precise)
to reconstruct 100 bp matrix back from 1 kb matrix!!!!!
reconstruct Global folding 100 bp back from 1kb resolution (GlobalFolding1000) assuming that global folding can work remotely enough.
another idea - to use a distance from a given cell to closest contact (from global matrix) - so, infinity sign is not zero or one, but continuos!
run many log regr in the loop and find the Contact Point with the best AIC 
Heatmap merged microhomology and AIC scores 
Again: Heatmap merged microhomology and AIC scores with actual deledions circles ####
