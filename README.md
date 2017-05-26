Google NGram dataset - Get Avergae Count Per Book  - Using PIG/AWS
------------------------------------------------------------------

Amazon S3 storage, 
Amazon Elastic Cloud
Computing (EC2) virtual servers in the cloud, 
Amazon Elastic MapReduce (EMR) managed Hadoop framework.


Use less than 20 instances.

Subsets of the Google books n -grams dataset (full dataset is http://storage.googleapis.com/books/ngrams/books/datasetsv2.html) 

An ‘n -gram’ is a phrase with n words; the full n-gram dataset lists n-grams present in the books on books.google.com along with some statistics.

The analysis will be performed on two datasets, extracted from the Google books bigrams (2 - grams),
A large dataset will be in S3 Bucket ( s3://ngrams-english-mega) and a
A smaller dataset will be S3 Bucket ( s3://bigrams-small)

These files are stored in AWS storage in the S3 Buckets.

File format:
ngram TAB year TAB occurrences TAB books NEWLINE

An example for 2grams (or bigram) would be:
I am 1936 342 90
I am 1945 211 10
very cool 1923 500 10
very cool 1980 3210 1000
very cool 2012 9994 3020

This tells us that, 
in 1936, the bigram ‘I am’ appeared 342 times in 90 different books. 
In 1945, ‘I am’ appeared 211 times in 10 different books. And so on.  


Goal
For each unique bigram, compute its average number of appearances per book. For the above
example, the results will be:
I am  - (342 + 211) / (90 + 10) = 5.53
very cool  - (500 + 3210 + 9994) / (10 + 1000 + 3020) = 3.40049628

 - Output the 10 bigrams having the highest average number of appearances per book along with their corresponding averages, in tabseparated format , sorted in descending order. 
 - If multiple bigrams have the same average, order them alphabetically . 

For the example above, the output will be:
I am 5.53
very cool 3.40049628

Solution is by writing a PIG script on Amazon EC2 and save the output from the PIG script.
Upload the PIG script and create a task on your cluster.

In the PIG script we first load data from the S3 bucket n-gram files into a PIG table

Then Rub the Query commands of PIG to get the results and storage them into S3 Bucket.

