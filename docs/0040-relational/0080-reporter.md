Report - with Some Scripting
============================

The Problem
-----------

Retrieve the top ten customers that bought the most units in 1997 and also find out if promotions had any effect.

The Solution
------------

- [Report Studio](/Tools+of+the+Trade.html#report_studio)

### The Steps

1. [Starting Report Studio](#step1)
2. [Build the List](#step2)
3. [Top 10 Customers](#step3)
4. [Drill-Through Reporting](#step4)
5. [Master Detail Relationship](#step5)
6. [Inline Prompt](#step6)

<div id="step1"></div>

### Step 1: Starting Report Studio

1. Launch Internet Explorer and go to *http://127.0.0.1:19300/cognos_express/manager/welcome.html*. Log in if prompted. 

2. Click *Create professional reports with Report Studio*

    ![rs01](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs01.png)

3. Cognos Connections will open. Look in your *My Folder* directory and choose the *foodmart* package to start reporting.

    ![rs02](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs02.png)

4. After it's done loading, click on *Create new*. Pick *List* as your template.

    ![rs03](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/rs03.png)

<div id="step2"></div>

### Step 2: Build the List

1. To the left, you'll see query items. Select or Ctrl+Click *Name* under *Customer* and *Unit Sales*.

2. Drag and drop query items to list.

    ![p9](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p9.png)

    If you *Run* your report, you should see the following: 

    ![p10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p10.png)

<div id="step3"></div>

### Step 3: List Top 10 Customers

1. First, sort. Single click *Unit Sales* column header to select it and click the sort icon and choose *Descending*.

    ![p11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p11.png)

    Run the report. List should now show the top customers with the most *Unit Sales*.

    ![p12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p12.png)

2. Second, filter. Lay cursor on *Query Explorer* icon until panel expands and click on *Query1*

    ![p13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p13.png)

3. Click *Toolbar* tab.

    ![p14](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p14.png)

    Drag a *Data Item* in *Toolbox* and drop it in the list of data items.

    ![p15](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p15.png)

4. *Detail Filter Expression* dialog will open. Here you write the expression on what you want to filter. The Expression is:

    ```c
        running-count( rank( [Name] ) )
    ```

    Test with green checkmark button on top. No errors should appear. Click *OK*

    ![p16](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p16.png)

5. Drag *Data Item1* and drop it in *Detail Filters* section.

    ![p17](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p17.png)

    *Detail Filter Expression* dialog will open. Enter expression: 

    ```c
        [Data Item1] <= 10
    ```

    Test it. Click *OK*. Run it. You should have your top 10 customers with the most unit sales.

    ![p18](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p18.png)

<div id="step4"></div>

### Step 4: Drill-Through Reporting

Drill through is the process of clicking a cell in a report to be redirected to another report. This allows one to make simpler reports and keep overhead information in seperate reports. The way it works is that there's a source and target report. The target report takes a parameter; the parameter can be an identifier or attribute. When you click on a cell from the cell report, the source report sends the cell value to the target report and filters the content by that parameter.

1. Save the current report to *top10_customers by unit sales*. Start a new report. And choose List when it prompts you for what kind of reports.

2. When your new report is ready to use, Ctrl+Click each query item in the *Customer* query subject. Then drag them over to the list.

    ![p1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p1.png)

    You should have the following:

    ![p2](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p2.png)

3. Lay your cursor on the *Query Explorer* icon until panel expands. You'll see a list of queries. Double click on *Query1*.

    ![p3](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p3.png)

4. In the *Data Items* section, drag *Name* and drop it in *Detail Filters* section to the right.

    ![p4](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p4.png)
    ![p5](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p5.png)

5. *Detail Filter Expression* dialog will open. Enter expression:

    ```c
        [Name] = ?p_Name?
    ```

    The surrounding question marks declares p_Name to be a parameter. The paramater value will be assigned to the data item, *Name*. Every time the report opens, it requires a value so that it'll filter in that value. The equal sign means there should only be one result. Test it with the green checkmark button on top and another window should open with a dropdown of all the customers' names. After choosing a name, click *OK* at the very bottom.

    ![p6](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p6.png)

    Now you should be back where you were before. Under *Information*, it should say no errors. Click *OK*

    ![p7](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p7.png)

6. Lay your cursor on *Page Explorer* icon until panel expands. Double click on *Page1*. 

    ![p8](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p8.png)

    Edit the title to "Customer" and save it. You're done building your target report. Reopen *top10_customers by unit sales* report.

7. Now to prepare the source report. Right click the cells of *Name* column and choose *Drill-Through Definitions...*

    ![p19](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p19.png)

    Create a new definition.

    ![p20](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p20.png)

    Set *Report* to the target report: *customer*; *Action* as *Run the report*, and *Format* as *HTML*. Check *Open in new window*. Then click the edit button (pencil icon).

    ![p21](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p21.png)

    Dialog will open listing all of the parameters of the target report. In this case, it's only *p_Name*. Set *Method* to *Pass data item value* and *Value* to *Name*. Click *OK*

    ![p22](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p22.png)

    Click *OK* to save definition.

    ![p23](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p23.png)

8. Run and test it.

    ![p24](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p24.png)

    ![p25](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p25.png)

<div id="step5"></div>

### Step 5: Master Detail Relationship

Master detail relationships link two data containers together within a report: a master data container and detail data container. We'll add *Promotion Name* as the detail for the customers' unit sales.

1. Click the *Toolbar* tab and drag *List* and drop it between *Name* and *Unit Sales*.

    ![p26](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p26.png)

2. There should be a list in a column named *List*. Double click the column title and rename it to *Promotions*.

    ![p27](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p27.png)

3. Select or Ctrl+Click *Name* under *Customer*, *Promotion Name* and *Unit Sales*. Drop it in the new list under *Promotions* column.

    ![p28](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p28.png)

    Run it. You'll see that the results are not correct. That's because we haven't created a relationship among them.

    ![p29](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p29.png)

4. Select the inner (Promotion) list by clicking the three orange dots in the corner.

    ![p30](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p30.png)

    Right click and choose *Master Detail Relationship...*

    ![p31](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p31.png)

    Click on the *New Link* button. Link *Name* to *Name*. Click *OK*

    ![p32](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p32.png)

5. Run it. 

    ![p33](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p33.png)

    If you group *Name* and sort *Unit Sales*, it'll look better.

    ![p34](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p34.png)

<div id="step6"></div>

### Step 6: Inline Prompt

Our goal here is to provide a textfield that allows the user to enter a number that limits how many promotions to display per customer.

1. Lay your cursor on *Query Explorer* icon until panel expands. Click on *Query2*. 

    ![p38](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p38.png)

    In *Toolbox*, drag *Query Calculation* to the list of of data items.

    ![p39](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p39.png)

2. Enter expression: 

    ```c
        running-count( rank([Unit Sales] for [Promotion Name]) )
    ```

    Test with green checkmark button on top. No errors should appear. Click *OK*

    ![p40](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p39.png)

3. Go back to *Page1* from *Page Explorer*. In *Toolbox*, drag and drop a *Text Item* above the list in the page.

    ![p35](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p35.png)

    *Text* dialog will appear. Enter "Specify the Maximum number of Promotions to view."

4. Add a *Block* under the text item you just created and add a *Text Box Prompt* under that block.

    ![p36](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p36.png)

    *Prompt Wizard* dialog will appear. Adding a text box creates a parameter for the report. Name the parameter *promotions_rank*. Click *Finish*

    ![p37](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p37.png)

5. Add a *Prompt Button* beside text box prompt you just added.

    ![p41](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p41.png)

    Select the button, and in the *Properties* pane (lower right side of Report Studio), set the *Type* to *Reprompt* so that the button re-runs the report when clicked.

    ![p42](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p42.png)

6. Select *promotions_rank* text box and in *Properties* pane set: *Required*=*No*, *Numbers Only*=*Yes*, *Default Selections*=*Yes*

    ![p43](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p43.png)

7. Lay cursor on *Query Explorer* icon and click *Query2*. In the list of *Data Items*, drag and drop *Data Item1* to *Detail Filters*. Enter expression:

    ```c
        [Data Item1] <= ?promotions_rank?
    ```

    Test with green checkmark button on top. No errors should appear. Click *OK*

    ![p44](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p44.png)

    Select the newly created detail filter and in *Properties* pane, *Application* property to *After Auto Aggregate* so that rank is determined before the filter is applied.

    ![p45](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p45.png)

8. Run it and voila!

    ![p46](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p46.png)

    ![p47](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/p47.png)

