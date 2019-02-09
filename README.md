# Web-Scraping-the-Koran-Bill-Congress-Information

Our dataset includes information on the gender of the bill’s sponsor, whether they were elected under
SMD or PR rules, and whether or not the legislation was enacted into law. To determine whether women in
the South Korean legislature substantively represent women’s issues, we categorized approximately 63,000
bills introduced between 1948 and 2015. The bills data were scraped from an online government archive
which provides comprehensive information about each bill introduced, including its sponsor, the date of introduction,
the title of the bill, and the bill’s outcome.5 We use the Comparative Policy Agendas coding
scheme, which lists 24 separate categories of bill topics, and has been applied to numerous national leg-
4The exact number of PR seats can slightly vary every election as the total seats change
islatures (Baumgartner & Jones 2013). A supervised machine learning process, using a train-validate-test
procedure, categorized each of the bills into one of the 24 categories over five iterations.
Each iteration proceeded as follows. First, a few thousand bills were hand-coded by the authors into
one of the 24 categories using the text of the bill titles. (Unlike in many legislatures, bill titles in Korea are
highly descriptive and the bills encompass only one topic area.)6 The hand-coded bills are then split into
three categories: train, validate, and test. The first subset of bills is used to train the algorithm, which uses
the text in the already classified data to determine how to classify additional bills.7 The validate subset of the
hand-coded data is used to determine how well the algorithm is classifying bills as compared to the human
coder. That is, it compares its own classification to the hand-coded classification and generates an error rate
(bills classified in different topic areas by the algorithm and the human coder). Finally, the last subset of data
is classified using the algorithm. The algorithm does not have access to the test set of bills until the error rate
for the validation set is sufficiently low, to ensure that the error rate will be generalizable to the test set. Thus,
the error rate is a measure of how well the algorithm will do in classifying the next set of uncategorized bills
a priori.
For each iteration, our rate was less than 2%, meaning for the subset of data on which the algorithm
classification was compared to the human classification, there was a topic area discrepancy for less than 2%
of the bills. We repeated the above process through five iterations, with a sixth iteration in which the remaining
bills were human coded. Iterations are necessary because the algorithm classifies bills into one of the 24 topic
areas and assigns a probability that each bill falls into that category. We required that the algorithm be more
than 90% confident that bill fit into that category, a highly conservative (i.e., bills are highly unlikely to be
misclassified) threshold. If the algorithm was not 90% sure that a bill fit into a category it was not classified.
Thus, each iteration finishes with a successful classification of a certain number of bills, and remaining bills
which cannot be classified with 90% certainty. A subset of these additional bills were hand-coded, and the
process repeated. Bills which could not previously be classified by the algorithm can be classified in a future
iteration because as more bills are hand-coded, the algorithm “learns” how to classify additional bills. We
set the 90% certainty threshold because that maintained an error rate under 2%; as the threshold declines, the
6In the United States, for example, many bills are composed of a combination of smaller bills, making them harder to categorize.
7Note that the different types of classifiers can be used. We found multinomial logistic regression was the most successful
algorithm. See the Appendix for more details.
12
algorithm assigns codes to a greater set of bills for which it is less confident, but more discrepancies between
human coding and machine coding occur. Table 1 shows the results of each iteration.
