Loading Data into Cubes
=======================

Problem
-------

Create a process that creates a cube with its required dimensions. Time dimension *Months* will contain *the_month* element that rolls up to *quarter*, and *quarter* rolls up to *the_year*. Dimension *Products* contains *product_name* that rolls up to *total_products*. Dimension *Stores* contains *store_name* that rolls up to *store_type*, and *store_type* rolls up to *total_stores*. The measure will be the store sales.

Solution
--------

- [Architect](/Tools+of+the+Trade.html#architect)
- [Turbo Integrator](/Tools+of+the+Trade.html#turbo_integrator)

### The Steps

1. [Launch Turbo Integrator](#step1)
2. [Create the Query](#step2)
3. [Set the Variables](#step3)
4. [Map the Variables](#step4)
5. [Run Process](#step5)
6. [View the Data](#step6)

<div id="step1"></div>

### Step 1: Launch Turbo Integrator

1. Launch Cognos Architect.

    ```c
        Start > All Programs > IBM Cognos Express > Architect
    ```

2. Login to the *foodmart* TM1 server.

    ![sc1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc1.png)

3. Right click *Processes* and choose *Create New Process*

    ![lc1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc1.png)

Turbo Integrator should now be open.

![lc2](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc2.png)

<div id="step2"></div>

### Step 2: Create the Query

Our goal here is to create a SQL query that'll group all the data we need into one big table. That way, we can separate each column to its correct dimension and have a fully built cube as an end result.

1. Under *Datasource Type*, pick *ODBC*.

    ![lc3](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc3.png)

2. Click the *Browse* button beside the *Data Source Name* textfield.

    ![lc4](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc4.png)

    And pick *foodmart-reduced* as the data source. Click *OK*

    ![lc5](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc5.png)

    <div class="note"><b>Note</b>: If you get an error that says something about not finding any datasources or it doesn't list foodmart-reduced, make sure you set up a foodmart-reduced ODBC with the 32-bit driver since Turbo Integrator only searches there. <a href="/Setting+Up+Data+Source.html">More Info</a></div>

3. If you log in to your server with Windows authentication, you can leave the *UserName* and *Password* textfields blank if you're logged in with a priveleged user already. If not, enter the credentials.

4. Now for the most important part: the query.

**Months Dimension**: Our cube will contain a time dimension in a hierarchy from year, quarter, and month. So we select *the_year*, *quarter*, and *the_month* columns from the *time_by_day* table. Also, let's just retrieve the data from the year 1997.

![lc7](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc7.png)

**Products Dimension**: This dimension will just have a long list of all the products, but for the sake of calculating something for all products, we need something to represent the total of all products. Hence, we have the statement *'total product' AS 'total_products'*.

![lc8](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc8.png)

**Stores Dimension**: Very similar to products dimension except it'll have an extra level in its hierarchy to consolidate individual stores by the store type. And remove the *HQ* store_name because it contains nothing but nulls.

![lc9](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc9.png)

**Measure** will be the store sales that is located in the *sales_fact_1997* so that'll be in the query as well. It's in a SUM function so that the numbers will add up when we roll up.

![lc10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc10.png)

Finally, in the query, we'll connect the foreign keys with the primary keys and group all columns together into one big table. Here's our final query:

![lc6](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc6.png)

Click the *Preview* 

![lc11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc11.png)

and you should see the following table:

![lc12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc12.png)

<div id="step3"></div>

### Step 3: Set the Variables

1. Click on the *Variables* tab.

    ![lc13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc13.png)

    You should now see a list of all the variables (or columns) that were imported.

    ![lc14](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc14.png)

    
2. Each variable is in a row and two columns that need to be editted are *Variable Type* and *Contents*. For Variable type, the only change we need to make is for *the_year* variable. TI thought it was a numeric because it detected digits, but in reality, *the_year* will not be calculated, it'll be used as a consolidation element so we'll change it to a string.

    ![lc15](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc15.png)

3. For *Contents*, there are more options:

    <table>
      <tr>
        <td>Element</td>
        <td>Single element in the hierarchy that has no children.</td>
      </tr>
      <tr>
        <td>Consolidation</td>
        <td>Element in the hierarchy that has children. Can be drilled down.</td>
      </tr>
      <tr>
        <td>Data</td>
        <td>Value that can be calculated.</td>
      </tr>
      <tr>
        <td>Attribute</td>
        <td>An element's variable. So it's a variable of a variable.</td>
      </tr>
    </table>

4. End result should be:

    ![lc16](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc16.png)

<div id="step4"></div>

### Step 4: Map the Variables

1. Click on the *Maps* tab.

    ![lc17](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc17.png)

2. Now you should see more tabs (Cube, Dimensions, Data, Consolidations, Attributes). In *Cube* tab, under the *Cube Action* section, pick *Create Cube* and name the cube "Store Sales".

    ![lc18](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc18.png)

3. Click *Dimensions* tab. You should see a list of all the variables you labeled as "Element". For each element, create a new dimension so under Dimension column, double click on the blank space and enter the following dimension names for each of the following elements:

    <table>
      <tr>
        <th>Element</th>
        <th>Dimension Name</th>
      </tr>
      <tr>
        <td>store_name</td>
        <td>Stores</td>
      </tr>
      <tr>
        <td>product_name</td>
        <td>Products</td>
      </tr>
      <tr>
        <td>the_month</td>
        <td>Months</td>
      </tr>
    </table>

    ![lc19](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc19.png)

    <div class="note"><b>Note</b>: Action column automatically converts to *Create* since you entered the name of a dimension that doesn't exist.</div>

4. Click *Consolidations* tab. You should see a list of all the variables you labeled as "Consolidation"

    ![lc20](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc20.png)

    <div class="note"><b>Note</b>: Data tab is unselectable because we only have one data variable.</div>

5. Our goal here is to place each consolidation element to their appropriate dimension and give it a child element. Click on the blue arrow to show a list of the possible choices for each blank space.

    ![lc21](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc21.png)

    *total_stores* consolidation element should be in the Stores dimension. Select *Stores* and click *OK*

    ![lc22](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc22.png)

    Do the same for all blank spaces, and the following should be your end result.

    ![lc23](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc23.png)

6. Click the save button.

    ![lc24](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc24.png)

    And name it, "Create Cube Store Sales". Click *OK* and exit out of Turbo Integrator.

    ![lc25](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc25.png)

<div id="step5"></div>

### Step 5: Run Process

Go to Architect. In *foodmart server*, expand *Processes*. Right click *Create Cube Store Sales* and select *Run*

![lc26](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc26.png)

Wait for a few seconds, and you should get a prompt that says, "Process Completed Successfully". Click *OK*

<div class="note"><b>Note</b>: If you get errors, double check that you followed the steps correctly. You can look at the log errors as well. It will point to you where the error is occuring so you won't spend hours wondering what's wrong.</div>

<div id="step6"></div>

### Step 6: View the Data

1. Go to Architect. In *foodmart server*, expand *Cubes*. Double click *Store Sales*.

    ![lc28](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc28.png)

2. *Cube Viewer* window should open now. The data pane is blank because we need to recalculate. Click on the recalculate button.

    ![lc29](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc29.png)

    You should now see the sum of store sales in 1997 for all products.

    ![lc30](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc30.png) 

3. Expand Months and Products dimension to get more detailed data.

    ![lc31](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc31.png)

4. You also have the 3rd dimension, *Stores*, in the top left corner. It currently shows *total_store*, but you can change it and get data for only a specific store type.

    ![lc32](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc32.png)

    You will need to recalculate or you can click *Automatic Recalculate* button so you don't have to do it manually.

    ![lc33](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc33.png)

    ![lc34](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc34.png)

5. You can close cube viewer and save it as a view if you like; lets call it "Supermarkets"

    ![lc35](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc35.png)

    ![lc36](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/lc36.png)

Downloads
---------

- [tm1server-foodmart-reduced.zip](https://docs.google.com/open?id=0B8bnF9QulzZgMW4wZVFGMVBESnc)

<hr>