Report - Common Techniques
==========================

The Problem
-----------

Show a list of the success and failures of the types of supermarkets in 1997. Show the *Store Sales*, *Store Cost*, and *Unit Sales* and make it presentable.

The Solution
------------

- [Query Studio](/Tools+of+the+Trade.html#query_studio)
- [Report Studio](/Tools+of+the+Trade.html#report_studio)

### The Steps

1. [Starting Query Studio](#step1)
2. [Build the List](#step2)
3. [Aggregate](#step3)
4. [Grouping](#step4)
5. [Filtering](#step5)
6. [Sorting](#step6)
7. [Formatting](#step7)
8. [Conditional Highlighting](#step8)
9. [Prettify](#step9)

<div id="step1"></div>

### Step 1: Starting Query Studio

1. Launch Internet Explorer and go to *http://127.0.0.1:19300/cognos_express/manager/welcome.html*. Log in if prompted.

2. Click *Query my business data with Query Studio*

    ![q1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q1.png)

3. Find and open *foodmart* package. Query Studio should now open a blank project.

    ![q2](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q2.png)

<div id="step2"></div>

### Step 2: Build the List

1. To the left, you'll see query items. Select or Ctrl+Click *Sales Region*, *Store Type*, *Store Name*, *Store Sales*, *Store Cost*, *Unit Sales*. 

2. Under the list of query items, click *Insert* button with green left pointing arrow. This should build a list.

    ![q3](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q3.png)

<div id="step3"></div>

### Step 3: Aggregate

You may notice there's a *Summary* row. Summary aggregates facts and displays the result. The question is, how does it aggregate it? There's many ways of aggregating: total, average, maximum, etc. If you didn't configure the aggregate value from Framework Manager, your aggregation results may be undesirable. Quickly check how it's aggregating.

1. Right click *Store Sales* column header and choose *Summarize...*

    ![q7](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q7.png)

2. It's *Total* or sum so we'll leave it that way. Just click *Cancel*.

    ![q8](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q8.png)

3. If you do the same for *Store Cost* and *Unit Sales*, you'll see they're *Total* as well. 

<div id="step4"></div>

### Step 4: Grouping

One can select a column and group the data so it can be more visually appealing and easier to locate. Lets group *Sales Region*.

1. Click on the *Sales Region* column header (the blue part). After selecting, it should turn orange.

    ![q4](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q4.png)

2. The toolbar on the top with all the icons. Find *Group* and click it. Look at the image below if you can't find it.

    ![q5](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q5.png)

    And you should see the following:

    ![q6](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q6.png)

<div id="step5"></div>

### Step 5: Filtering


Filtering unnecessary data allows one to minimize the amount of information that is returned. For example, maybe you only want to see stores that sold under 10,000 units. But we only want to analyze results from the types of supermarkets which include *Supermarket*, *Gourmet Supermarket*, and *Deluxe Supermarket*.

1. Right click *Store Type* column header and choose *Filter...*
Report Studio

    ![q9](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q9.png)

2. You should now see bottom panel, *Filter (Pick values from a list)*. Leave the condition as *Show only the following* and from the list, choose the three types of supermarkets. Click *OK*

    ![q10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q10.png)

    You should now have the following list.

    ![q11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q11.png)

<div id="step6"></div>

### Step 6: Sorting

You can sort a fact column in ascending or descending order. We'll sort *Store Sales* in descending order.

1. Right click *Store Sales* column header and choose *Sort...*

    ![q12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q12.png)

2. Bottom panel will open. Choose *Descending (9 to 1)* and click *OK*

    ![q13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q13.png)

    Result should be the following:

    ![q14](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q14.png)
 
<div id="step7"></div>

### Step 7: Formatting

Data may sometimes not be formatted how you want it, but we can help it. Lets format *Store Cost* and *Store Sales*.

1. Right click *Store Sales* column header and choose *Format Data...*

    ![q15](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q15.png)

2. Truncate the value to a whole. Under *Category*, choose *Number*. Under *Number of decimal places*, choose *0*. Under *Thousands separator*, choose *Yes*. Click *OK*
 
    ![q16](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q16.png)

3. Do the same for *Store Cost*, but choose *Currency* for *Category* and keep *2* for *Number of decimal places*. Your end result should be the following:

    ![q17](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q17.png)

<div id="step8"></div>

### Step 8: Conditional Highlighting

Store sales that didn't meet expected rates and those that surpassed expectations should be identified quickly. This task is perfect for conditional highlighting. In this case, expected sales are between 50,000 and 80,000 so anything below 50,000 will be highlighted in red and anything above 80,000 will be highlighted in green.

1. Click on any of the individual cells under the *Store Sales* column. They should be highlighted in orange.

    ![q18](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q18.png)

2. On the left panel, click *Change Layout* and choose *Define Conditional Styles...*

    ![q19](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q19.png)

3. In *Define conditional styles* bottom panel, under *New Value*, enter 80000. Click the *Insert* button with green left pointing arrow.

4. Clear the textfield under *New Value* and enter 50000. Click the *Insert*. 

    ![q20](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q20.png)

5. There are three sections that are in default style. The top section will have the green highlight and the bottom section will have the red highlight. We can create custom styles, but we'll stick with the template they have for now. Choose *Excellent* from the style dropdown for the top section. Choose *Poor* from the style dropdown for the bottom section. Click *OK*

    ![q21](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q21.png)

    ![q22](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q22.png)

<div id="step9"></div>

### Step 9: Prettify

Lets make a pretty report in Report Studio.

1. For reference, save the query studio project in Cogno's content store. Name it "query facts 1997 for supermarkets".

2. On the left panel, click *Manage File* and choose *Open in Report Studio*

    ![q23](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q23.png)

3. In Report Studio, double click the title and name it *1997 Facts for Supermarkets*

4. Select all the parts of the page and center it.

    ![q25](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q25.png)

5. Select the topmost part of the page (where the title is). Click the bucket fill button, select *Custom Color* tab at the bottom of the dialog. Uncheck *Hexadecimal values* and set Red=102, Green=102, Blue=204. Click *Apply*

    ![q26](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q26.png)

6. Set the font to size 20pt with color white.

    ![q28](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q28.png)

7. Select the two page sections under the topmost section and give it a background color of red=204, green=204, blue=255.

    ![q29](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q29.png)

I think you get the idea. Here's my final look. It's pretty, right?

![q30](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q30.png)

Save your report as "facts 1997 for supermarkets"

<hr>