ICS 325 Fall 2016 - Assignment 5
=================

Purpose
-------
* Continue to learn how to use github.com and GitKraken.
* Practice more object-oriented PHP

Collaboration
-------------
You can talk about the assignment with your peers in the class.  However, you should perform the work yourself and turn in a copy of your own work.

Prerequisites
-------------
Use git to clone your private assignment 5 repo to your computer.  Then in PhpStorm, use `File->Open Directory` and select your local repo.  This assignment is based off of your work from assignment 3, so copy your assignment 3 files into your assignment 5 directory.

Instructions
------------
### Instructions to set up the code to run
First you need to clone your git repository to your computer.  Open GitKraken and make sure you are logged into your github.com account.  Next go to `File->Clone Repo`.  Select the `GitHub.com` icon.  A list of your repositories in github.com should pop up.  Select the one for assignment 5.  If you want, change `Where to clone to` by clicking browser and selecting a folder for your git repo to be cloned into.  Finally, hit the `Clone the repo!` button.  Your repo should now clone to your computer.  Next copy your files from assignment 3 into your assignment 5 directory.

Next you need to set up PhpStorm. First make sure you have the git repo open in PhpStorm by using the Open Directory menu item under File in PhpStorm (`File->Open Directory`).  Then open the PHP file you want to run, right-click in the window, go to `Run` and select the 2nd run option to run your PHP file on the command line within PhpStrom.

### Assignment Instructions
You need to make various changes to your assignment 3 work.  You will be adding more functionality to your Report abstract class and therefore each child class.  A summary of each change and the associated point value is listed below in the grading section.

#### Add a report recipient
We would like to know which person a report should be sent to.  To make things simple, we will allow the report to be sent to 1 person.  We will store the person's e-mail address and name.  We will represent that information using a new class named Person.

The Person class has:
* 2 private attributes (also known as instance variables): name and email
* public functions that get the value of the name and email attributes (these functions are known as getters)
* a constructor that requires 2 parameters: name and email which should each have their value assigned to the instance variables name and email
* there should be no way to change the name or e-mail address once the object is instantiated

Next modify the abstract Report class so that the constructor takes a Person object as its sole argument.  Because this is an object, you can preface the argument with the class name you require.  For example:<br />
`public function __construct(Person $person)`

This person object passed into the constructor should be saved to an instance variable named person as well.  Since the definition of the Report class has been changed, each child class must be modified to pass a person object to its parent's constructor.  For example:<br />
`parent::__construct($person);`

Each child class must now accept a person object as an argument to its constructor.  You should make the first argument to the constructor the person object.  For example, for the RangeReport constructor:
`public function __construct(Person $person, $start, $end)`

Finally, modify the `printToTerminal()` method in the Report class to print out the recipient of the report as:<br />
Report recipient: Name Email

You can use the public getter methods for the Person class in order to get the name and email address of the person from the Person object.

#### Add a `run()` method
We'd like to break up the work of the Report class into 3 parts:
* Report instance creation and validation of the parameters
* Run the code that calculates the results
* Report on the results

The constructor should take care of validating the parameters for reports that require validation.  The parameters should then be stored to instance variables to be later used by the `run()` method.

You need to add a new abstract protected method named `run()` to the Report abstract class.  Each child class should implement the method and perform any work that is necessary in order to generate the report results.  The results should be stored in an instance variable for later retrieval.

The report results should be retrievable via the `getReportResultString()` method.  If the results haven't yet been generated, an exception should be thrown with the message:<br />You must run a report before calling its getReportResultString() method.

#### Example use
Here's an example of how to use the refactored classes:
```
$jason = new Person('jason', 'jason@example.com');
$my_sum_report = new SumReport($jason, [2, 4, 6]);
$my_sum_report->run();
$my_sum_report->printToTerminal();
```
Which will output:
```
Report recipient: Jason jason@example.com
Report title: Sum Calculator
Report generated at: Tue, 13 Sep 2016 14:45:09 -0500
Report description: Sums the given integers.
Report parameters:
INTEGERS: 2, 4, 6

Report result:
12
```

#### How to Turn in Assignment 5
You need to clone your private git repo for assignment 5 to your computer, copy your assignment 3 code into the assignment 5 directory, and then make the required changes.  Once you are done, commit your modifications to your master branch and push them to GitHub.  Then go to D2L and turn in the assignment to let me know I can go look at your repo and grade you.  D2L requires you to upload a file, so place a link to your git repo in a text file and upload it to D2L.  You can also put the link in the assignment comments and upload an empty file to D2L.  Either way is fine, but having the link makes it much easier for me to find your repo and grade it quickly.

Grading
-------
Points|Requirement
------|-----------
7 | Person class definition
4 | Report class modified to use the Person class
3 | Each child class of Report modified to pass a Person object to its parent's constructor
1 | Add abstract protected method `run()` to the Report class
1 | Validation of the RangeReport parameters happens in its constructor
3 | Calculations for the results for each child class implemented in a `run()` method
3 | No calculation is perform when returning results with the `getReportResultString()` in the child classes
1 | An exception is thrown if `getReportResultString()` is called before `run()`
2 | Turn in the assignment via github.
**25**|**Total**
