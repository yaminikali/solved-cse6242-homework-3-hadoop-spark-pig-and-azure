Download Link: https://assignmentchef.com/product/solved-cse6242-homework-3-hadoop-spark-pig-and-azure
<br>
<h3>Analyzing a Graph with Hadoop/Java</h3>

Imagine that your boss gives you a large dataset which contains an entire email communication network from a popular social network site. The network is organized as a directed graph where each node represents a person’s email address and an edge between two nodes (e.g., address A and address B) has a weight stating how many times A has written to B. You have been tasked with finding the person that each person has written to the most, along with that count (see the example below for more clarification). Your task is to write a MapReduce program in Java to report, for each node X (the “source”, or “src” for short) in the graph, the person Y (the “target” or “tgt” for short) that X has written to the most, and the number of times X has written to Y (the outbound “weight”, from X to Y). <strong>If a person has written to multiple targets that have exactly the same (largest) number of times,  return the target with smallest node id.</strong>

First, go over the <a href="https://www.google.com/url?q=https://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html%23Example:_WordCount_v1.0&amp;sa=D&amp;ust=1574830363283000">Hadoop word count tutorial</a> to familiarize yourself with Hadoop and some Java basics. You will be able to complete this question with only some knowledge about Java. You should have already loaded two graph files into HDFS and loaded into your HDFS file system in your VM. Each file stores a list of edges as tab-separated-values. Each line represents a single edge consisting of three columns: (source node ID, target node ID, edge weight), each of which is separated by a tab (t). Node IDs and weights are positive integers. Below is a small toy graph, for illustration purposes (on your screen, the text may appear out of alignment).

src        tgt        weight

10        110        3

10        200        1

200        150        30

100        110        10

110        130        15

110        200        67

10        70        3

Your program should not assume the edges to be sorted or ordered in any ways (i.e., your program should work even when the edge ordering is random).

Your code should accept two arguments. The first argument (<em>args[0]</em>) will be a path for the input graph file on HDFS (e.g., data/graph1.tsv), and the second argument (<em>args[1]</em>) will be a path for output directory on HDFS (e.g., data/q1output1). The default output mechanism of Hadoop will create multiple files on the output directory such as part-00000, part-00001, which will be merged and downloaded to a local directory by the supplied run script. Please use the run1.sh and run2.sh scripts for your convenience.

The format of the output: each line contains a node ID, followed by a tab (t), and the expected “target node ID,weight” tuple (without the quotes; and note there is no space character before and after the comma). Lines do not need to be sorted. The following example result is computed based on the toy graph above. Please exclude nodes that do not have outgoing edges (e.g., those email addresses which have not sent out any communication).

For the toy graph above, the output is as follows.

10        70,3

200        150,30

100        110,10

110        200,67

<h4><strong>Deliverables</strong></h4>

<ol>

 <li><strong>Your Maven project directory including Q1.java.</strong> Please see detailed submission guide at the end of this document. You should implement your own MapReduce procedure and should not import external graph processing library.</li>

 <li><strong> q1output1.tsv</strong>: the output file of processing graph1.tsv by run1.sh.</li>

 <li><strong>q1output2.tsv</strong>: the output file of processing graph2.tsv by run2.sh.</li>

</ol>

<h2>Q2 Analyzing a Large Graph with Spark/Scala on Databricks</h2>

<strong>Tutorial</strong><strong>: </strong>First, go over this <a href="https://www.google.com/url?q=https://databricks.com/spark/getting-started-with-apache-spark/quick-start&amp;sa=D&amp;ust=1574830363288000">Spark on Databricks Tutorial</a><a href="https://www.google.com/url?q=https://databricks.com/spark/getting-started-with-apache-spark/quick-start&amp;sa=D&amp;ust=1574830363288000">,</a> to get the basics of creating Spark jobs, loading data, and working with data.

You will analyze <a href="https://www.google.com/url?q=https://www.dropbox.com/s/oqy7o8c1qfr3xkh/mathoverflow.csv?dl%3D0&amp;sa=D&amp;ust=1574830363288000">mathoverflow.csv</a><sup>[<u>3</u>]</sup> using Spark and Scala on the Databricks platform. This graph is a temporal network of interactions on the stack exchange web-site <a href="https://www.google.com/url?q=http://mathoverflow.net/&amp;sa=D&amp;ust=1574830363289000">MathOverflow</a>. <strong>The dataset has three columns in the following format: ID of the source node (a user), ID of the target node (a user),  Unix timestamp (seconds since the epoch).</strong>

Your objectives:

<ol>

 <li>Remove the pairs where the questioner and the answerer are the same person. Very important: all subsequent operations must be performed on this filtered</li>

</ol>

dataframe.

<ol start="2">

 <li>List the top 3 <strong>answerers</strong> who answered the highest number of questions, sorted in descending order of questions answered count. If there is a tie, list the individual with smaller node ID first.</li>

 <li>List the top 3 <strong>questioners</strong> who <strong>asked</strong> the highest number of questions, sorted in descending order of questions asked count. If there is a tie, list the individual with the smaller node ID first.</li>

 <li>List the top 5 most common answerer-questioner pairs, sorted in descending order of pair count. If there is a tie, list the pair with the smaller answerer node ID first. If there is still a tie, use the questioner node ID as the tie-breaker by listing the smaller questioner ID first.</li>

 <li>List, by month, the number of interactions (questions asked/answered) from September 1, 2010 (inclusively) to December 31, 2010 (inclusively).</li>

 <li>List the top 3 individuals with the most overall activity (i.e., highest total questions asked and questions answered).</li>

</ol>

You should perform this task using the <a href="https://www.google.com/url?q=https://spark.apache.org/docs/2.3.1/api/scala/index.html%23org.apache.spark.sql.Dataset&amp;sa=D&amp;ust=1574830363291000">DataFrame API</a> in Spark. <a href="https://www.google.com/url?q=https://spark.apache.org/docs/2.3.1/&amp;sa=D&amp;ust=1574830363291000">Here</a> is a guide that will help you get started on working with data frames in Spark.

A template Scala notebook, q2-skeleton.dbc has been included in the HW3-Skeleton that reads in a sample graph file <em>examplegraph.csv</em>.  In the template, the input data is loaded into a dataframe, inferring the schema using reflection (Refer to the guide above).

<strong>Note</strong>: You <strong>must </strong>use only Scala DataFrame operations for this task. You will lose points if you use SQL queries, Python, or R to manipulate a dataframe.

You may find some of the following DataFrame operations helpful: toDF, join, select, groupBy, orderBy, filter

Upload the data file examplegraph<strong>.</strong>csv and q2-skeleton.dbc to your Databricks workspace before continuing.  Follow the <a href="https://www.google.com/url?q=https://docs.google.com/document/d/e/2PACX-1vSYNg55nenwhmQ6yNbtk1alMAkzHU2V5uHHVpFzM5W6nBGKPb0yUm9T_p_V6alc2w/pub&amp;sa=D&amp;ust=1574830363292000">Databricks Setup Guide</a> for further instructions. Consider the following directed graph example where we show the result of achieving the objectives on <em>examplegraph.csv</em>.

<table width="463">

 <tbody>

  <tr>

   <td width="232"></td>

   <td width="232">+——–+———-+———-+|answerer|questioner| timestamp|+——–+———-+———-+|       1|         4|1283296645||       3|         4|1283297908||       1|         4|1283298280||       2|         2|1283298467||       3|         4|1283299092||       1|         2|1283300824||       2|         1|1283300967||       1|         2|1283301485||       3|         1|1283302207||       2|         4|1283303844||       4|         1|1283304158||       3|         1|1283304547||       1|         2|1283305468||       2|         1|1283305625||       1|         7|1283306548||       3|         3|1283306910||       7|         2|1283309524||       4|         1|1283310284||       1|         4|1283310295||       2|         7|1283310872|+——–+———-+———-+</td>

  </tr>

 </tbody>

</table>

<ol>

 <li><strong> Remove the pairs where the questioner and the answerer are the same person.</strong> For example, the instance of the edge answerer: 2 – questioner: 2 and answerer: 3 – questioner: 3 should be removed from <em>examplegraph</em>.</li>

</ol>

+——–+———-+———-


|answerer|questioner| timestamp|

+——–+———-+———-


|       1|         4|1254192988|

|       3|         4|1254194656|

|       1|         4|1254202612|

<span style="text-decoration: line-through;">|       2|         2|1254232804| </span>|       3|         4|1254263166|

…

|       1|         7|1254392595|

<span style="text-decoration: line-through;">|       3|         3|1254395022| </span>|       7|         2|1254396925|

…

|       2|         7|1254436186|

+——–+———-+———-


<ol start="2">

 <li><strong>List the top 3 answerers who answered the highest number of questions, sorted in descending order of question count</strong>. If there is a tie, list the individual with the smaller node ID first. For the above examplegraph the results would look like this:</li>

</ol>

+——–+——————


|answerer|questions_answered|

+——–+——————


|       1|                 7|

|       2|                 4|

|       3|                 4|

+——–+——————


<ol start="3">

 <li><strong>List the top 3 questioners who asked the highest number of questions, sorted in descending order of question count. </strong>If there is a tie, list the individual with the smaller node ID first. For the above examplegraph the results would look like this:</li>

</ol>

+———-+—————


|questioner|questions_asked|

+———-+—————


|         1|              6|

|         4|              6|

|         2|              4|

+———-+—————


<ol start="4">

 <li><strong>List the top 5 most common questioner-answerer pairs, sorted in descending order of pair count.</strong> If there is a tie, list the pair with the <strong>smaller answerer node ID</strong> If there is still a tie, use the questioner node ID as the tie-breaker by listing the smaller questioner ID first. For the above examplegraph the results would look like this:</li>

</ol>

+——–+———-+—–


|answerer|questioner|count|

+——–+———-+—–


|       1|         2|    3|

|       1|         4|    3|

|       2|         1|    2|

|       3|         1|    2|

|       3|         4|    2|

+——–+———-+—–


<ol start="5">

 <li><strong>List, by month, the number of interactions (questions asked/answered) from September 1, 2010 (inclusively) to December 31, 2010 (inclusively</strong>). The month of September is represented by the number 9, month of October by 10 and so on. For the above examplegraph the results would look like this:</li>

</ol>

+—–+——————+ |month|total_interactions| +—–+——————


|    9|                14|

+—–+——————


<ol start="6">

 <li><strong>List the top 3 individuals with the most overall activity</strong>, i.e., highest total questions asked and questions answered. For the above examplegraph the results would look like this:</li>

</ol>

+——+————–


|userID|total_activity|

+——+————–


|     1|            13|

|     2|             8|

|     4|             8|

+——+————–


We have provided you with the walkthrough of the steps you need to perform with an example graph. Now it is your turn to<strong> replace the examplegraph with the mathoverflow graph</strong> and list the results of your experiments in the provided <strong><em>q2_results.csv</em></strong> file.

<h3><strong>Deliverables</strong></h3>

<ol>

 <li>

  <ol start="2">

   <li><strong>dbc </strong>Your solution as Scala Notebook archive file (.dbc) exported from Databricks. See the Databricks Setup Guide on creating an exportable archive for details.</li>

   <li><strong>scala</strong>, Your solution as a Scala source file exported from Databricks. See the Databricks Setup Guide on creating an exportable source file for details.</li>

  </ol></li>

</ol>

<strong>Note: </strong>You should export your solution as both a .dbc &amp; a .scala file.

<ol start="2">

 <li><strong>[15 pts] q2_results.csv:</strong> The output file of processing <strong><em>csv</em></strong> from the q2 notebook file. You must copy the output of the display()/show() function into the file titled <strong><em>q2_results.csv</em> </strong>into the relevant sections.</li>

</ol>

<h3>Q3 Analyzing Large Amount of Data with Pig on AWS</h3>

You will try out <a href="https://www.google.com/url?q=http://pig.apache.org&amp;sa=D&amp;ust=1574830363304000">Apache Pig</a> for processing n-gram data on Amazon Web Services (AWS). This is a fairly simple task, and in practice you may be able to tackle this using commodity computers (e.g., consumer-grade laptops or desktops). However, we would like you to use this exercise to learn and solve it using distributed computing on Amazon EC2, and gain experience (very helpful for your career), so you will be prepared to tackle problems that are more complex.

The services you will primarily be using are Amazon S3 storage, Amazon Elastic Cloud Computing (EC2) virtual servers in the cloud, and Amazon Elastic MapReduce (EMR) managed Hadoop framework.

For this question, you will only use up a very small fraction of your $100 credit. AWS allows you to use up to 20 instances in total (that means 1 master instance and up to 19 core instances) without filling out a “limit request form”. For this assignment, you should not exceed this quota of 20 instances<strong>.</strong> Refer to details about <a href="https://www.google.com/url?q=https://aws.amazon.com/ec2/instance-types/&amp;sa=D&amp;ust=1574830363305000">instance types</a>, their specs, and <a href="https://www.google.com/url?q=https://aws.amazon.com/ec2/pricing/&amp;sa=D&amp;ust=1574830363305000">pricing</a><a href="https://www.google.com/url?q=https://aws.amazon.com/ec2/pricing/&amp;sa=D&amp;ust=1574830363305000">.</a> In the future, for larger jobs, you may want to use <a href="https://www.google.com/url?q=http://calculator.s3.amazonaws.com/index.html&amp;sa=D&amp;ust=1574830363306000">AWS’s pricing calculator</a><a href="https://www.google.com/url?q=http://calculator.s3.amazonaws.com/index.html&amp;sa=D&amp;ust=1574830363306000">.</a>

AWS Guidelines

Please read the <a href="https://www.google.com/url?q=https://docs.google.com/document/d/e/2PACX-1vTpYRjidXovgb2vfPqZJSGXjc8Lr1y9jHk5skI8lxA6_Y8Yh4X-o2T2b-WwRRueqg/pub&amp;sa=D&amp;ust=1574830363307000">AWS Setup Guidelines</a> provided to set up your AWS account.

<h4>Datasets</h4>

In this question, you will use a dataset of over 130 million customer reviews from Amazon Customer Reviews. (Further details on this dataset are available <a href="https://www.google.com/url?q=https://registry.opendata.aws/amazon-reviews/&amp;sa=D&amp;ust=1574830363307000">here</a>).

You will perform your analysis on two datasets based off of this data, which we have prepared for you: a small one (~1GB) and a large one (~32GB).

<strong>VERY IMPORTANT</strong>: Both the datasets are in the <strong>US East (N. Virginia)</strong> region. Using machines in other regions for computation would incur data transfer charges. Hence, set your region to <strong>US East (N. Virginia) </strong>in the beginning (not Oregon, which is the default). <strong>This is extremely important, otherwise your code may not work and you may be charged extra.</strong>

The files in these two S3 buckets are stored in a tab (‘t’) separated format. <strong>An example of their structure is available </strong><a href="https://www.google.com/url?q=https://s3.amazonaws.com/amazon-reviews-pds/tsv/sample_us.tsv&amp;sa=D&amp;ust=1574830363309000"><strong>here</strong></a><strong>.</strong>

<h4>Goal</h4>

Output the top 15 product categories having the highest <strong>average star rating per review</strong> along with their corresponding averages, in <strong>tab-separated format</strong>, sorted in descending order. Only consider entries whose review bodies are 100 characters or longer, have 30 or more total votes, and were verified purchases. If multiple product categories have the same average, <strong>order them alphabetically on product category</strong>. Refer to the example and calculations below:

product_id                review_id                star_rating

Toys                        RDIJS7QYB6XNR        3

Toys                        BAHDID7JDNAK0        4

Toys                        YHFKALWPEOFK4        2

Books                        BZHDKTLJYBDNE        4

Books                        ZZUDNFLGNALDA        3

Books                (4 + 3 ) / 2 = 5.5

Toys                (3 + 4 + 2) / 3        = 3.0

<strong>Note: </strong>The small dataset only includes 5 categories, so you will only get 5 rows for its output.

<h4>Sample Output</h4>

To help you evaluate the correctness of your output, we provide you with <a href="https://www.google.com/url?q=https://www.dropbox.com/s/dvpnmia50i3jsc9/pig-output-small.txt?dl%3D0&amp;sa=D&amp;ust=1574830363312000">the output for the small dataset</a>

<strong>Note</strong>: Please strictly follow the formatting requirements for your output as shown in the small dataset output file. You can use <a href="https://www.google.com/url?q=https://www.diffchecker.com/&amp;sa=D&amp;ust=1574830363312000">https://www.diffchecker.com/</a> to make sure the formatting is correct. Improperly formatting outputs may not receive any points.

<h4>Using PIG (Read these instructions carefully)</h4>

There are two ways to debug PIG on AWS (all instructions are in the <a href="https://www.google.com/url?q=https://docs.google.com/document/d/e/2PACX-1vTpYRjidXovgb2vfPqZJSGXjc8Lr1y9jHk5skI8lxA6_Y8Yh4X-o2T2b-WwRRueqg/pub&amp;sa=D&amp;ust=1574830363313000">AWS Setup Guidelines</a>):

<ol>

 <li><strong>Use the interactive PIG shell</strong> provided by EMR to perform this task from the command line (grunt). Refer to Section 8: Debugging in the AWS Setup</li>

</ol>

Guidelines for a detailed step-by-step procedure. You should use this method if you are using PIG for the first time as it is easier to debug your code. However, as you need to have a persistent ssh connection to your cluster until your task is complete, this is suitable only for the smaller dataset.

<ol start="2">

 <li><strong>Upload a PIG script </strong>with all the commands which computes and direct the output from the command line into a separate file. Once you verify the output on the smaller dataset, use this method for the larger dataset. You don’t have to ssh or stay logged into your account. You can start your EMR job, and come back after when the job is complete!</li>

</ol>

<strong>Note</strong>: In summary, verify the output for the smaller dataset with Method 1 and submit the results for the bigger dataset using Method 2.

<h4>Sample Commands: Load data in PIG</h4>

To load data for the <strong>small example</strong> use the following command:

grunt&gt; reviews = LOAD ‘s3://amazon-reviews-pds/tsv/amazon_reviews_us_M*’ AS

(marketplace:chararray,customer_id:chararray,review_id:chararray,product_id:chararray,product_parent:chararray,product_title:c review_date:chararray);

To load data for the <strong>large example</strong> use the following command:

grunt&gt; reviews = LOAD ‘s3://amazon-reviews-pds/tsv/*’ AS

(marketplace:chararray,customer_id:chararray,review_id:chararray,product_id:chararray,product_parent:chararray,product_title:c review_date:chararray);

<strong>Note:</strong>

<ul>

 <li>Refer to other commands such as LOAD, USING PigStorage, FILTER, GROUP, ORDER BY, FOREACH, GENERATE, LIMIT, STORE, etc.</li>

 <li>Copying the above commands directly from the PDF and pasting on console/script file may lead to script failures due to the stray characters and spaces from the PDF file.</li>

 <li>Your script will fail if your output directory already exists. For instance, if you run a job with the output folder as <strong>s3://cse6242oan-&lt;</strong><strong>GT account username</strong><strong>&gt;/output-small</strong>, the next job which you run with the same output folder will fail. Hence, please use a different folder for the output for every run.</li>

 <li>You might also want to change the input data type for <strong>star_rating </strong>to handle floating point values.</li>

 <li>While working with the interactive shell (or otherwise), you should first test on a small subset of the data instead of the whole data (the whole data is over 100 GB). Once you believe your PIG commands are working as desired, you can use them on the complete data and wait since it will take some time.</li>

</ul>

<h4>Deliverables</h4>

<ul>

 <li><strong>pig-script.txt</strong>: The PIG script for the question (using the <strong>larger</strong> data set). ● <strong>pig-output.txt</strong>: Output <strong>(tab-separated) </strong>(using the <strong>larger</strong> data set).</li>

</ul>

<strong>Note: </strong>Please strictly follow the guidelines below, otherwise your solution may not be graded.

<ul>

 <li>Ensure that file names (case sensitive) are correct.</li>

 <li>Ensure file extensions (.txt) are correct.</li>

 <li>The size of each pig-script.txt and pig-output.txt file should not exceed 5 KB.</li>

 <li>Double check that you are submitting the correct set of files — we only want the script and output from the larger dataset. Also double check that you are writing the right dataset’s output to the right file.</li>

 <li>You are welcome to store your script’s output in any bucket you choose, as long as you can download and submit the correct files. Ensure that unnecessary new lines, brackets, commas etc. aren’t in the file.</li>

 <li>Please do not make any manual changes to the output files</li>

</ul>

<h3><strong>Q4  </strong>Analyzing a Large Graph using Hadoop on Microsoft Azure</h3>

<strong>VERY IMPORTANT</strong>: Use Firefox or Chrome in incognito/private browsing mode when configuring anything related to Azure (e.g., when using Azure portal), to prevent issues due to browser caches. Safari sometimes loses connections.

<h4>Goal</h4>

The goal is to analyze graph using <a href="https://www.google.com/url?q=https://en.wikipedia.org/wiki/Cloud_computing&amp;sa=D&amp;ust=1574830363318000">a</a> <a href="https://www.google.com/url?q=https://en.wikipedia.org/wiki/Cloud_computing&amp;sa=D&amp;ust=1574830363318000">cloud computing </a>service – Microsoft Azure, and your task is to write a MapReduce program to compute the distribution of a graph’s node degree differences (see example below). Note that this question shares some similarities with Question 1 (e.g., both are analyzing graphs). Question 1 can be completed using your own computer. This question is to be completed using Azure. We recommend that you first complete Question 1. Please carefully read the following instructions.

You will use two data files in this questions:

<ul>

 <li><a href="https://www.google.com/url?q=https://www.dropbox.com/s/0up13naldazyc2b/small.zip?dl%3D0&amp;sa=D&amp;ust=1574830363319000">tsv</a><a href="https://www.google.com/url?q=https://www.dropbox.com/s/0up13naldazyc2b/small.zip?dl%3D0&amp;sa=D&amp;ust=1574830363319000"><sup>[</sup></a><u><sup>4</sup></u><sup>]</sup> (zipped as ~3MB small.zip; ~11MB when unzipped)</li>

 <li><a href="https://www.google.com/url?q=https://www.dropbox.com/s/oaobxfp6s8sjukn/large.zip?dl%3D0&amp;sa=D&amp;ust=1574830363319000">tsv</a><sup>[<u>5</u>]</sup> (zipped as 247MB large.zip; ~1GB when unzipped)</li>

</ul>

Each file stores a list of edges as tab-separated-values. Each line represents a single edge consisting of two columns: (Source, Target), each of which is separated by a tab. Node IDs are positive integers and the rows are already sorted by Source.

Source        Target

0                0

<ul>

 <li>1</li>

 <li>1</li>

 <li>2</li>

 <li>3</li>

</ul>

Your code should accept two arguments upon running. The first argument (args[0]) will be a path for the input graph file, and the second argument (args[1]) will be a path for output directory. The default output mechanism of Hadoop will create multiple files on the output directory such as part-00000, part-00001, which will have to be merged and downloaded to a local directory (instructions on how to do this are provided below). The format of the output should be as follows. Each line of your output is of the format diff        count

where

<ul>

 <li>diff is the difference between a node’s out-degree and in-degree (i.e., out-degree minus in-degree); and</li>

 <li>count is the number of nodes that have the value of difference (specified in 1).</li>

</ul>

The out-degree of a node is the number of edges where that node is the Source. The in-degree of a node is the number of edges where that node is the Target. diff and count must be separated by a tab (t), and the lines do not have to be sorted. When the source and target is the same node, such as [0, 0] in the example, node “0” should be counted in both in-degree and out-degree.

The following result is computed based on the graph above.

-1        1

<ul>

 <li>2</li>

 <li>1</li>

</ul>

The explanation of the above example result:

<table width="414">

 <tbody>

  <tr>

   <td width="79"><strong>Output</strong></td>

   <td width="334"><strong>Explanation</strong></td>

  </tr>

  <tr>

   <td width="79">-1        1</td>

   <td width="334">There are 1 nodes (node 3) whose degree difference is -1</td>

  </tr>

  <tr>

   <td width="79">0        2</td>

   <td width="334">There are 2 nodes (node 1 and node 2) whose degree is 0.</td>

  </tr>

  <tr>

   <td width="79">1        1</td>

   <td width="334">There is 1 node (node 0) whose degree difference is 1.</td>

  </tr>

 </tbody>

</table>

<strong>Hint :</strong> One way of doing it is using the mapreduce procedure twice. The first one for finding the difference between out-degree and in-degree for each node, the second for calculating the node count of each degree difference. You will have to make changes in the skeleton code for this.

In the Q4 folder of the hw3-skeleton, you will find the following files we have prepared for you:

<ul>

 <li><strong>src </strong>directory contains a main Java file that you will work on. We have provided some code to help you get started. Feel free to edit it and add your files in the directory, but the main class should be called “Q4”.</li>

 <li><strong>xml</strong> contains necessary dependencies and compile configurations for the question.</li>

</ul>

To compile, you can run the command in the directory which contains <strong>pom.xml</strong>. mvn clean package

This command will generate a single JAR file in the target directory (i.e. target/q4-1.0.jar).

<h5>Creating Clusters in HDInsight using the Azure portal</h5>

Azure HDInsight is an Apache Hadoop distribution. This means that it handles large amounts of data on demand. The next step is to use Azure’s web-based management tool to create a Linux cluster. Follow the recommended steps shown <a href="https://www.google.com/url?q=https://drive.google.com/file/d/1eme5AuTLO1xfRgfk-Z6opi9A0TYDn78I/view?usp%3Dsharing&amp;sa=D&amp;ust=1574830363325000">here</a> (or the full Azure’s documentation <a href="https://www.google.com/url?q=https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-create-linux-clusters-portal/&amp;sa=D&amp;ust=1574830363325000">here</a><a href="https://www.google.com/url?q=https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-create-linux-clusters-portal/&amp;sa=D&amp;ust=1574830363325000">)</a> to create a new cluster.

At the end of this process, you will have created and provisioned a New HDInsight Cluster and Storage (the provisioning will take some time depending on how many nodes you chose to create). Please record the following important information (we also recommend that you take screenshots) so you can refer to them later:

<ul>

 <li>Cluster login credentials</li>

 <li>SSH credentials Resource group</li>

 <li>Storage account</li>

 <li>Container credentials</li>

</ul>

<strong>VERY IMPORTANT</strong>: HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted. To save the credit, you’d better to delete your cluster when it is no longer in use. You can find all clusters and storages you have created in “All resources” in the left panel.  Please refer <a href="https://www.google.com/url?q=https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-delete-cluster&amp;sa=D&amp;ust=1574830363326000">here</a> for how to delete an HDInsight cluster.

<h5>Uploading data files to HDFS-compatible Azure Blob storage</h5>

We have listed the main steps from the documentation for uploading data files to your Azure Blob storage here:

<ol>

 <li>Follow the documentation <a href="https://www.google.com/url?q=https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-install/&amp;sa=D&amp;ust=1574830363327000">here</a> to install Azure CLI.</li>

 <li>Open a command prompt, bash, or other shell, and use <sub>az login</sub> command to authenticate to your Azure subscription. When prompted, enter the username and password for your subscription.</li>

 <li><sub>az storage account list</sub> command will list the storage accounts for your subscription.</li>

 <li>az storage account keys list –account-name &lt;storage-account-name&gt; –resource-group &lt;resource-group-name&gt; command should return “key1” and “key2”. Copy the value of “key1” because it will be used in the next steps.</li>

 <li><sub>az storage container list –account-name &lt;storage-account-name&gt; –account-key &lt;key1-value&gt;</sub> command will list your blob containers.</li>

 <li>az storage blob upload –account-name &lt;storage-account-name&gt; –account-key &lt;key1-value&gt; –file &lt;small or large .tsv&gt; –container-name &lt;container-name&gt; –name &lt;new-blob-name&gt;/&lt;small or large .tsv&gt; command will upload the source file to your blob storage container. &lt;new-blob-name&gt; is the folder name you will create and where you would like to upload tsv files to. If the file is uploaded successfully, you should see “Finished [#####] 100.0000%”.</li>

</ol>

Using these steps, upload <strong><em>small.tsv</em></strong> and <strong><em>large.tsv</em></strong> to your blob storage container. The uploading process may take some time. After that, you can find the uploaded files in storage blobs at <a href="https://www.google.com/url?q=http://portal.azure.com&amp;sa=D&amp;ust=1574830363328000">Azure</a> (portal.azure.com) by clicking on “Storage accounts” in the left side menu and navigating through your storage account (&lt;Your Storage Account&gt; -&gt; &lt;”Blobs” in the overview tab&gt; -&gt; &lt;Select your Blob container to which you’ve uploaded the dataset&gt; -&gt; &lt;Select the relevant blob folder&gt;). For example, “jonDoeStorage” -&gt; “Blobs” -&gt; “jondoecluster-xxx” -&gt; “jdoeSmallBlob” -&gt; “small.tsv”. After that write your hadoop code locally and convert it to a jar file using the steps mentioned above.

<h5>Uploading your Jar file to HDFS-compatible Azure Blob storage</h5>

Azure Blob storage is a general-purpose storage solution that integrates with HDInsight. Your Hadoop code should directly access files on the Azure Blob storage.

Upload the jar file created in the first step to Azure storage using the following command: scp &lt;your-relative-path&gt;/q4-1.0.jar &lt;ssh-username&gt;@&lt;cluster-name&gt;-ssh.azurehdinsight.net:

You will be asked to agree to connect by typing “yes” and your cluster login password. Then you will see q4-1.0.jar is uploaded 100%.

SSH into the HDInsight cluster using the following command:

ssh &lt;ssh-username&gt;@&lt;cluster-name&gt;-ssh.azurehdinsight.net

&lt;ssh-username&gt; is what you have created in step 10 in the flow.

<strong>Note</strong>: if you see the warning – REMOTE HOST IDENTIFICATION HAS CHANGED, you may clean /home/&lt;user&gt;/.ssh/known_hosts” by using the command rm

~/.ssh/known_hosts. Please refer to <a href="https://www.google.com/url?q=https://stackoverflow.com/questions/20840012/ssh-remote-host-identification-has-changed&amp;sa=D&amp;ust=1574830363330000">host identification</a><a href="https://www.google.com/url?q=https://stackoverflow.com/questions/20840012/ssh-remote-host-identification-has-changed&amp;sa=D&amp;ust=1574830363330000">.</a>




Run the ls command to make sure that the q4-1.0.jar file is present.

To run your code on the small.tsv file, run the following command:

yarn jar q4-1.0.jar edu.gatech.cse6242.Q4 wasbs://&lt;container-name&gt;@&lt;storage-account-name&gt;.blob.core.windows.net/&lt;new-blob-name&gt;/small.tsv wasbs://&lt;containername&gt;@&lt;storage-account-name&gt;.blob.core.windows.net/smalloutput

Command format: yarn jar jarFile packageName.ClassName dataFileLocation outputDirLocation

<strong>Note</strong>: if “Exception in thread “main” org.apache.hadoop.mapred.FileAlreadyExistsException…” occurs, you need to delete the output folder and files from your Blob. You can do this at portal.azure.com. Click “All resources” in the left panel, you will see you storage and cluster. Click your storage, then “Blobs” and then your container, you will see all folders including the blob created by you and the “smalloutput” folder. You need to click “Load more” at the bottom to see all folders/files. You need to delete output at different places: 1. smalloutput; 2. user/sshuser/*

The output will be located in the directory: wasbs://&lt;container-name&gt;@&lt;storage-account-name&gt;.blob.core.windows.net/smalloutput If there are multiple output files, merge the files in this directory using the following command: hdfs dfs -cat wasbs://&lt;container-name&gt;@&lt;storage-account-name&gt;.blob.core.windows.net/smalloutput/* &gt; small.out

Command format: hdfs dfs -cat location/* &gt;outputFile Then you may exit to your local machine using the command: exit

You can download the merged file to the local machine (this can be done either from <a href="https://www.google.com/url?q=https://portal.azure.com/&amp;sa=D&amp;ust=1574830363333000">Azure Portal</a> or by using the scp command from the local machine). Here is the scp command for downloading this output file to your local machine: scp &lt;ssh-username&gt;@&lt;cluster-name&gt;-ssh.azurehdinsight.net:/home/&lt;ssh-username&gt;/small.out &lt;local directory&gt;

Using the above command from your local machine will download the small.out file into the local directory. Repeat this process for large.tsv. Make sure your output file has exactly two columns of values as shown above. Your output files should be able to be opened and readable in text editors like notepad++.

<h5>Deliverables</h5>

<ol>

 <li>[15pt] <strong>java &amp; q4-1.0.jar: </strong>Your java code and converted jar file. You should implement your own map/reduce procedure and should not import external graph processing library.</li>

 <li>[10pt] <strong>out</strong>: the output file generated after processing small.tsv.</li>

 <li>[10pt] <strong>out</strong>: the output file generated after processing large.tsv.</li>

</ol>

<h2>Q5  Regression: Automobile price prediction, using Azure ML Studio</h2>

<strong>Note</strong>: Create and use a free workspace instance on <a href="https://www.google.com/url?q=https://studio.azureml.net/&amp;sa=D&amp;ust=1574830363336000">Azure Studio</a> instead of your Azure credit for this question. Please use your Georgia Tech username (e.g., jdoe3) to login.

<h3><strong>Goal</strong></h3>

The main purpose of this question is to introduce you to Microsoft Azure Machine Learning Studio and familiarize you with its basic functionality and typical machine learning workflow. Go through the “<a href="https://www.google.com/url?q=https://docs.microsoft.com/en-us/azure/machine-learning/studio/create-experiment&amp;sa=D&amp;ust=1574830363337000">Automobile price prediction</a>” tutorial and complete the tasks below.

You will modify the given file, <strong>results.csv</strong>, by adding your results for each of the tasks below. We will autograde your solution, therefore DO NOT change the order of the questions or anything else.  Report the exact numbers that you get in your output, DO NOT round the numbers.

<ol>

 <li>[3 points] Repeat the experiment mentioned in the tutorial and report the values of the metrics as mentioned in the ‘<em>Evaluate Model’</em> section of the tutorial.</li>

 <li>[3 points] Repeat the same experiment, change the ‘<em>Fraction of rows in the first output’</em> value in the split module to 0.8 (originally set to 0.75) and report the corresponding values of the metrics.</li>

 <li>[4 points] Evaluate the model with the 5-fold cross-validation (<a href="https://www.google.com/url?q=https://docs.microsoft.com/en-us/azure/machine-learning/studio/evaluate-model-performance&amp;sa=D&amp;ust=1574830363338000">CV</a><a href="https://www.google.com/url?q=https://docs.microsoft.com/en-us/azure/machine-learning/studio/evaluate-model-performance&amp;sa=D&amp;ust=1574830363338000">)</a>, select the parameters in the module <em>‘Partition and sample’</em> (<a href="https://www.google.com/url?q=https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/partition-and-sample&amp;sa=D&amp;ust=1574830363339000">Partition and Sample</a>) (see figure below). Report the values of Root Mean Squared Error (RMSE) and Coefficient of Determination for each fold. (1st fold corresponds to fold number 0 and so on).</li>

</ol>

Figure: Property Tab of Partition and Sample Module

Specifically, you need to do the following:

<ol>

 <li>Import the entire dataset (Automobile Price Data (Raw))</li>

 <li>Clean the missing data by removing rows that have any missing values</li>

 <li>Partition and Sample the data.</li>

 <li>Create a new model (Linear Regression) E. Finally, perform cross validation on the dataset.</li>

 <li>Visualize/Report the values.</li>

</ol>

<strong>Deliverables</strong>

<ol>

 <li>[10pt]<strong> results.csv:</strong> a csv file containing results for all of the three parts.</li>

</ol>

<h3>Important: folder structure of the zip file that you submit</h3>

You are submitting a single zip file HW3-GTUsername.zip (e.g., HW3-jdoe3.zip, where “jdoe3” is your GT username), which must unzip to the following directory structure (i.e., a folder “HW3-jdoe3”, containing folders “Q1”, “Q2”, etc.). The files to be included in each question’s folder have been clearly specified at the end of each question’s problem description above.

HW3-GTUsername/

Q1/

src/main/java/edu/gatech/cse6242/Q1.java

pom.xml         run1.sh         run2.sh         q1output1.tsv         q1output2.tsv

<strong>       </strong><strong> (do not attach target directory) </strong>    Q2/         q2.dbc         q2.scala

q2_results.csv            Q3/

pig-script.txt         pig-output.txt

Q4/

src/main/java/edu/gatech/cse6242/Q4.java

pom.xml

q4-1.0.jar <strong>(from target directory) </strong>          small.out           large.out

<strong>       (do not attach target directory)     </strong>Q5/         results.csv

Version 0

<ul>

 <li>Graph1 is a modified version of data derived from the LiveJournal social network dataset, with around 30K nodes and 320K edges.</li>

 <li>Graph2 is a modified version of data derived from the LiveJournal social network dataset, with around 300K nodes and 69M edges.[<u>3</u>] Graph derived from the Stanford Large Network Dataset Collection</li>

 <li>subset of <a href="https://www.google.com/url?q=https://snap.stanford.edu/data/soc-Pokec.html&amp;sa=D&amp;ust=1574830363346000">Pokec social network</a> data</li>

 <li>subset of <a href="https://www.google.com/url?q=http://snap.stanford.edu/data/com-Friendster.html&amp;sa=D&amp;ust=1574830363347000">Friendster</a> data</li>

</ul>