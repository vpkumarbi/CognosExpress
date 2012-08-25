Simple Report with Graph
========================

The Problem
-----------

Create a report showing which of the following types of stores sold the most units in 1997, separated by quarters.

The Solution
------------

- [Report Studio](/Tools+of+the+Trade.html#report_studio)


### The Steps

1. [Start a Report Studio Project](#step1)
2. [Fill Crosstab with Data](#step2)
3. [Add Chart](#step3)

<div id="step1"></div>

### Step 1: Start a Report Studio Project

1. Launch Internet Explorer and go to *http://127.0.0.1:19300/cognos_express/manager/welcome.html*. Log in if prompted. 

2. Click *Create professional reports with Report Studio*

    ![rs01](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs01.png)

3. Cognos Connections will open. Look in your *My Folder* directory and choose the *foodmart* package to start reporting.

    ![rs02](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs02.png)

4. After it's done loading, click on *Create new*.

    ![rs03](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs03.png)

5. Next window allows you to pick a template so you don't have to start from blank. We're going to pick *Crosstab*. Crosstab allows you to view summarized information at the intersecting point of a column and row.

    ![rs04](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs04.png)

<div id="step2"></div>

### Step 2: Fill Crosstab with Data

1. You should now see the following screen below with the query subjects to the left.

    ![rs05](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs05.png)

2. We already have the Sales Facts from 1997 so we simply collapse *1997 Sales Fact* and drag the fact, *Unit Sales* to *Measures* in the crosstab table. 

    ![rs06](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs06.png)

    And then drop it, and you should see the following.

    ![rs07](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs07.png)

3. Your boss specified the time interval to be in the year 1997 so let's drag *Year* in *Columns* so the report can show the unit sales are from 1997.

    ![rs08](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs08.png)

    And then drop it, and you should see the following.

    ![rs09](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs09.png)

4. We chose crosstab so we could display the *Quarters* of the year under *Year*. Drag *Quarter* under *Year* in the *Columns section*. When you see a black bar like in the following image, drop it.

    ![rs10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs10.png)

    ![rs11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs11.png)

5. In the *Rows* area, drag and drop *Store Type* so your end result should be:

    ![rs12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs12.png)

6. Click on the *Run Report* button.

    ![rs13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs13.png)

    By looking at the numbers, you can see that Supermarkets are selling the most units.

    ![rs14](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs14.png)

<div id="step3"></div>

### Step 3: Add Chart

1. To make it easier for your boss to view the information, lets add a pie chart per quarter. Go to the *Toolbox* tab.

    ![rs15](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs15.png)

2. Drag and drop *Chart* object from the Toolbox list to a white space under your crosstab.

    ![rs16](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs16.png)

3. In the *Insert Chart* dialog, pick a pie chart. And at the bottom of the dialog, there will be a checkbox that says *Fill with data*. This will allow you to automatically fill the chart with data from an object that's already on the page. In this case, there's only one crosstab on the page. Click *OK*.

    ![rs17](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs17.png)

4. Click on the *Run Report* button.

    ![rs18](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs18.png)

5. Double click the title of the report, *Double-click to edit text*, and name it "Units Sold in 1997 by Store Type". Click *OK*.

6. Click the save button on the top-left corner, and you can save the report in public folders with the name "Units sold in 1997 by store type". So your boss can later see it.

Do It Yourself
--------------

Create a report that shows and answers the following questions: 

1. Which warehouse shipped the most units in 1998?
2. In what quarter did all warehouses combined ship the least?
3. In what quarter did all warehouses combined ship the most?

Include a chart and a note that explicitly answers questions 1,2,3.

<hr>