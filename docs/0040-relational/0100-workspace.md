Workspace aka Dashboards
========================

The Problem
-----------

Put together the reports you've created and present the results in a working dashboard. 

The Solution
------------

- [Business Insight](/Tools+of+the+Trade.html#business_insight)
- [Business Insight Advanced](/Tools+of+the+Trade.html#business_insight_advanced)

### The Steps

1. [Starting Cognos Business Insight](#step1)
2. [Dragging Reports to the Workspace](#step2)
3. [The Toolbox](#step3)
3. [Cleanup](#step4)

<div id="step1"></div>

### Step 1: Starting Cognos Business Insight

1. Launch Internet Explorer and go to *http://127.0.0.1:19300/cognos_express/manager/welcome.html*. Log in if prompted. 

2. Click *Create my workspaces with Business Insight*

    ![bi1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi1.png)

3. Click *Create New* button to create new project.

    ![bi2](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi2.png)

4. A blank workspace is created. To the right is a panel where you can drag and drop *Content* and items from the *Toolbox* into the workspace.

    ![bi3](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi3.png)

5. Go to *Content*, and expand *My Folders* and *foodmart*. You should now see all the reports and queries that have been saved in *foodmart* package.

    ![bi4](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi4.png)

<div id="step2"></div>

### Step 2: Dragging Reports to the Workspace

If you've completed the previous recipes from this cookbook, you should have at least 3 reports inside of *foodmart* package: *facts 1997 for supermarkets*, *top10 customers by unit sales*, and *Units sold in 1997 by store type*. 

1. Drag and drop *top10 customers by unit sales* to the canvas.

    ![bi5](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi5.png)
    ![bi6](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi6.png)

2. Drag and drop *facts 1997 for supermarkets* to the canvas.

    ![bi7](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi7.png)
    ![bi8](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi8.png)

3. In the right hand content pane, expand *Units sold in 1997 by store type*.

    ![bi9](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi9.png)

4. Drag and drop *Crosstab1* to the canvas.

    ![bi10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi10.png)

5. Drag and drop *Pie Chart1* to the canvas.

    ![bi11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi11.png)

<div id="step3"></div>

### Step 3: The Toolbox

If you've used Report or Query Studio already, you probably already know about the *Toolbox*. They're simply objects that one can drag and drop on the canvas and do something cool. Take the *Slider Filter* for example. It links a query item from one of the reports on the dashboard and creates a range or single filter on that query.

1. Click the *Toolbox* tab.

    ![bi11-1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi11-1.png)

2. Drag and drop *Slider Filter* to the canvas.

    ![bi12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi12.png)

3. In *Properties - Slider Filter* dialog, choose *Quarter* under the list of data items. *Quarter* links *Crosstab1* and *Pie Chart1* widgets on the canvas because they're all part of *Units sold in 1997 by store type* report.

4. For *Show descriptive text* textfield, type "Select a range of Quarters". Click *OK*

    ![bi13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi13.png)

    You should see the following:

    ![bi14](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi14.png)

5. To make it look better expand the slider widget to fill in the square gap.

    ![bi15](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi15.png)
    ![bi16](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi16.png)

    Test it out.

    ![bi17](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi17.png)
    ![bi18](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi18.png)

<div id="step4"></div>

### Step 4: Cleanup

Some personal modifications:

1. Click *Layout and Style* drop down located in top bar of Business Insight, and choose *Edit Workspace Style...*

    ![bi19](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi19.png)

2. In *Edit Workspace Style* dialog, choose the color white for the background.

    ![bi20](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi20.png)
    ![bi21](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi21.png)

3. Go to Widgets tab

    ![bi22](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi22.png)

4. Uncheck *Borders* and click *OK*

    ![bi23](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi23.png)

The *facts 1997 for supermarkets* report does not vertically fit the canvas. 

1. Click on the *top10 customers by unit sales* report and expand it to the right height.

    ![bi24](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi24.png)

Now everything fits perfectly. One more minor tweak. Apparently I forgot to change the summary rows' color to purple in the *facts 1997 for supermarkets* report. 

1. Click the *Do More...* button for that widget.

    ![bi25](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi25.png)

2. Business Insight Advanced will be launched. Select all the grouped summary rows (North West and South West). Click the Bucket Fill drop down, and go to *Custom Color* tab, uncheck *Hexadecimal values* and enter red=99, green=101, blue=206. Click *Apply*

    ![bi26](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi26.png)

3. Set the font color to white.

    ![bi27](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi27.png)

4. Select the entire Summary row (last row). Repeat step 2 and 3, but set the background color to red=0, green=0, blue=132. Click *Done*.

    ![bi28](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi28.png)

    Final Result.

    ![bi29](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi29.png)

    Save the workspace in foodmart-reduced package and name it dashboard.

    ![bi30](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/bi30.png)

  
