# INF553-Assignment-3-solution

Download Here: [INF553 Assignment 3 solution](https://jarviscodinghub.com/assignment/inf553-assignment-3-solution/)

For Custom/Original Work email jarviscodinghub@gmail.com/whatsapp +1(541)423-7793

1. OverviewoftheAssignment
InAssignment3,youwillcompletetwotasks.ThegoalistoletyoubefamiliarwithMinHash, Locality Sensitive
Hashing (LSH), and different types of collaborative-filtering recommendation systems. The datasetyouaregoing
toplaywithisasubsetfromtheYelpdataset(https://www.yelp.com/dataset)used in the previous assignments.
2. AssignmentRequirements
2.1 Programming Language and Library Requirements
a. YoumustusePythontoimplementalltasks.YoucanonlyusestandardPythonlibraries(i.e.,external librarieslike
Numpy or Pandas are not allowed). There will be a 10% bonus for each task (or case) if you also submit a Scala
implementationandbothyourPythonandScalaimplementationsarecorrect.
b. You are requiredto onlyuse the Spark RDDto understandSpark operations. Youwill notreceive any pointif
youuse SparkDataFrame orDataSet.
2.2 Programming Environment
WewillusePython3.6,Scala2.11,andSpark2.3.3totestyourcode.Therewillbea20%penaltyifwe cannotrun
your codeduetothe libraryversioninconsistency.
2.3 Write your own code
Do not share your code with other students!!
WewillcombineallthecodewecanfindfromtheWeb(e.g.,GitHub)aswellasotherstudents’codefrom thisandother
(previous)sectionsforplagiarismdetection.Wewillreportallthedetectedplagiarism.
2.4 What you need to turn in
Your submission must be a zip file with the naming convention: firstname_lastname_hw3.zip (all lowercase,
e.g., yijun_lin_hw3.zip). You should pack the following required (and optional) files in a folder named
firstname_lastname_hw3 (all lowercase, e.g., yijun_lin_hw3)inthezipfile(Figure1,only thefiles in the red boxes are
requiredto submit):
a. [REQUIRED] two Python scripts containing the main function, named:
firstname_lastname_task1.py, firstname_lastname_task2.py
b1. [OPTIONAL] two Scala scripts containing the main function, named:
firstname_lastname_task1.scala, firstname_lastname_task2.scala
b2. [OPTIONAL] one Jar package, named:
firstname_lastname_hw3.jar
c. [OPTIONAL]Youcanincludeotherscriptstosupportyourprograms(e.g.,callablefunctions),butyou needto
makesureafterunzipping,theyareallinthesamefolder“firstname_lastname_hw3”.
d. Youdon’tneedtoincludeanyresult.Wewillgradeyourcodeusingourtestingdata.Ourtestingdata willbe in
the same format asthevalidationdataset.
Figure 1: The folder structure after your submission file is unzipped.
3. YelpData
We generated the following two datasets from the original Yelp review dataset with some filters such as the
condition: “state” == “CA”. We randomly took 60% of the data as the training dataset, 20% of the data as the
validationdataset,and20%ofthedata asthetestingdataset.
a. yelp_train.csv:thetrainingdata,whichonlyincludethecolumns:user_id,business_id,andstars.
b. yelp_val.csv:thevalidationdata,whichareinthesameformatastrainingdata.
c. We do notshare the testingdataset.
4. Tasks
4.1 Task1:JaccardbasedLSH(4points)
In thistask, you will implement the Locality Sensitive Hashing algorithm with Jaccard similarity using
yelp_train.csv. You can refer to sections 3.3 – 3.5 of the Mining of Massive Datasets book.
Inthistask,wefocusonthe“0or1”ratingsratherthantheactualratings/starsfromtheusers.Specifically, if auserhas
rated a business, the user’s contribution in the characteristic matrix is 1. If the user hasn’t rated the business, the
contribution is 0.Youneedtoidentify similarbusinesseswhose similarity >= 0.5.
Youcandefineanycollectionofhashfunctionsthatyouthinkwouldresultinaconsistentpermutationof therow
entriesofthecharacteristicmatrix.Somepotentialhashfunctionsare:
f(x)=(ax+b)%m or f(x) = ((ax +b)%p)%m
where p is any prime number andmisthe number of bins. You can use any combination forthe parameters
(a, b,p,andm)inyourimplementation.
After youhavedefinedallthehashing functions, youwillbuildthe signaturematrix. Thenyouwilldivide thematrix
into b bandswithrrows each, where b x r =n(nisthenumber ofhash functions). You should carefully selectagood
combinationofbandrinyourimplementation.Rememberthattwoitemsarea candidate pairiftheirsignatures
areidentical inatleastoneband.
YourfinalresultswillbethecandidatepairswhoseoriginalJaccardsimilarityis>=0.5.Youneedtowrite thefinal
resultsintoaCSVfileaccordingtotheoutputformatbelow.
Example of Jaccard Similarity:
user1 user2 user3 user4
business1 0 1 1 1
business2 0 1 0 0
Jaccard Similarity (business1, business2) = #intersection / #union = 1/3
Input format: (we will use the following command to execute your code)
Param: input_file_name:the name ofthe inputfile (e.g., yelp_train.csv), including the file path. Param:
output_file_name:thenameoftheoutputCSVfile,includingthefilepath.
Output format:
IMPORTANT:Pleasestrictly followtheoutputformatsince your codewillbegradedautomatically.We will not
regrade on formatting issues.
a. The output file is a CSV file, containing all business pairs you have found. The header is “business_id_1,
business_id_2,similarity”. Each pairitself must be in the alphabetical order. The entire file also needsto be in the
alphabeticalorder.Thereisnorequirementforthenumberofdecimalsforthesimilarity value. Please referto the
formatin Figure 2.
Figure 2: a CSV output example for task1
Grading:
Wewillcompareyouroutputfileagainstthegroundtruthfileusingtheprecisionandrecallmetrics.
Precision=truepositives/(true positives+falsepositives)
Recall=truepositives/(truepositives+falsenegatives)
ThegroundtruthfilehasbeenprovidedintheGoogledrive,namedas“pure_jaccard_similarity.csv”.You canusethis
filetocompareyourresultstothegroundtruthaswell.
The ground truth dataset only contains the business pairs (from the yelp_train.csv) whose Jaccard
similarity>=0.5.Thebusinesspairitselfissortedinthealphabeticalorder,soeachpaironlyappearsonce in the file
(i.e.,ifpair(a,b)isinthedataset,(b,a)willnotbethere).
Inordertogetfullcreditforthistaskyoushouldhaveprecision=1andrecall>=0.98.Ifnot,then youwillget80%
partial creditwith0.95 <= recall < 0.98:
Your runtime should be less than 120 seconds with 4G driver memory and 4G executor memory. This is the
environment of the grading machine. If yourruntime is more than or equalto 120 seconds, you will not receive
any pointforthistask.
4.2 Task2:RecommendationSystem(8.5points)
In task 2, you are going to build differenttypes ofrecommendation systems using the yelp_train.csv to predictfor
the ratings/stars for given user ids and business ids. You can make any improvement to your recommendation
systemin terms ofthe speed and accuracy. You can use the validation dataset (yelp_val.csv)toevaluatethe
accuracyofyourrecommendationsystems.
There are two options to evaluate your recommendation systems. You can compare your results to the
correspond ground truth and compute the absolute differences. You can divide the absolute differences into 5
levels andcountthenumberforeachlevel asfollowing:
>=0and<1:12345
>=1 and <2: 123
>=2and<3:1234
>=3and<4:1234
>=4: 12
Thismeansthatthere are12345predictionswith<1difference fromthe groundtruth.Thisway youwill be able to
know the error distribution of your predictions and to improve the performance of your recommendation
systems.
Additionally, you can compute the RMSE (Root Mean Squared Error) by using following formula:
Where Predi is the prediction for business i and Ratei isthe true rating for business i. n isthe total number of the
business you are predicting.
In this task, you are required to implement:
Case1:Model-basedCFrecommendationsystemwithSparkMLlib(2.5point)
Case2:User-basedCFrecommendationsystem(3points)
Case 3: Item-based CF recommendation system (3 points)
4.2.1. Model-based CF recommendation system
YouwilluseSparkMLlibtoimplementthistask.YoucanlearnmoreaboutSparkMLlibbythislink:
https://spark.apache.org/docs/latest/mllib-collaborative-filtering.html.
4.2.2. User-basedCFrecommendationsystem
4.2.3. Item-based CF recommendation system
Input format: (we will use the following command to execute your code)
Param:train_file_name:the name ofthe training file (e.g., yelp_train.csv), including the file path Param:
test_file_name:thenameofthetestingfile(e.g.,yelp_val.csv),includingthefilepath Param: case_id:thecase
number(i.e.,1,2,or 3)
Param: output_file_name: the name of the prediction result file, including the file path
Output format:
a. The output file is a CSV file, containing all the prediction results for each user and business pair in the
validation/testing data. The header is “user_id, business_id, prediction”. There is no requirement for the order in this
task. There is no requirement for the number of decimals for the similarity values. Please refer to the format in
Figure 3.
Figure 2: Output example in CSV for task2
Grading:
We will compare your prediction results againstthe ground truth. We will grade on allthe casesin Task2 based on
your accuracy using RMSE. For yourreference,the table below showsthe RMSE baselines and suggested running
timeforpredicting thevalidationdata.
RMSE baseline and suggested running time for predicting the validation data
Case 1 Case 2 Case 3
RMSE 1.31 1.12 1.10
Running Time 40s 150s 100s
For grading, we will use the testing data to evaluate your recommendation systems. If you can pass the RMSE
baselinesintheabovetable,youshouldbeabletopasstheRMSEbaselinesforthetestingdata. However,ifyour
recommendationsystemonlypassestheRMSEbaselinesforthevalidationdata,youwill receive 50%ofthe points
for each case.
In case 2 and 3, if your RMSE can not pass the baseline, you will receive partial credit:
case2: 100% RMSE <= 1.12, 80% 1.12 < RMSE <= 1.18 else 0%
case3: 100% RMSE <= 1.10, 80% 1.10 < RMSE <= 1.17 else 0%
5. Grading Criteria
(% penalty = % penalty of possible points you get)
1. Youcanuseyourfree5-dayextensionseparatelyortogether.
2. Therewillbe10%bonusif youuse bothScala andPython.
3. Ifwecannotrunyourprogramswiththecommandwespecified,therewillbean80%penalty.
4. IfyourprogramcannotrunwiththerequiredScala/Python/Sparkversions,therewillbea20% penalty.
5. Ifourgradingprogramcannotfindaspecifiedtag,therewillbenopointforthisquestion.
6. Iftheoutputsofyourprogramareunsortedorpartiallysorted,therewillbe50%penalty.
7. Iftheheaderoftheoutputfileismissing,therewillbe10%penalty.
8. Wecanregradeonyour assignmentswithinsevendaysoncethescores arereleased.No argueafter oneweek.
Theregradingwillhavea20%penaltyifourgradingis correct.
9. Therewillbea20%penaltyforlatesubmissionswithinaweekandnopointafteraweek.
10. Therewillbenopointifthetotalexecutiontimeforalltasksexceeds20minutes.
11. OnlywhenyourresultsfromPythonarecorrect,thebonusofusingScalawillbecalculated.Thereis no partially
pointfor Scala. Seetheexamplesbelow:
Example situations
Task Score for Python Score for Scala
(10% of previous column if correct) Total
Task1 Correct: 4points Correct: 4 * 10% 4.4
Task1 Wrong: 0 point Correct: 0 * 10% 0.0
Task1 Partially correct: 2 points Correct: 2 * 10% 2.2
Task1 Partially correct: 2 points Wrong: 0 2.0
