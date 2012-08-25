DMR - Dimensionally Modeled Relational Model
============================================

The Problem
-----------

You want to create a dimensionally modeled relational model from a relational data source so you can publish the data for your business users to query.  

The Solution
------------

- [Framework Manager](/Tools+of+the+Trade.html#framework_manager)

### The Steps
1. [Create a Project](#step1)
2. [Learn the Components](#step2)
3. [Create Relationships](#step3)
4. [Build Business View ](#step4)
5. [Build Presentation View](#step5)
6. [Publish Package](#step6) 

<div id="step1"></div>

### Step 1: Create a Project

Start Framework Manager from your Windows Start Menu:
 
```c
Start > All Programs > IBM Cognos Express > Framework Manager
```

1. Click *Create a new project...*. 

    <div class="note"><b>Note</b>: We can jumpstart a new project with the Model Design Accelerator (MDA) wizard to create a single-fact star-schema model, but it may contain errors that's difficult to catch.</div>

    ![s01](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot01.png)

2. A *New Project* dialog opens. Give your project a name. Click *OK*.

3. After logging in and selecting a language, the *Metadata Wizard* will start. In *Select Metadata Source*, choose *Data Sources*.

    ![s02](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot02.png)

4. In *Select Data Source*, there will be a list of data sources that was configured in Cognos. Choose *foodmart-reduced*. Click *Next*.

5. In *Select Objects*, expand *dbo*, and check *Tables*. In this example, we'll choose all tables.

    <div class="note">Usually, you would only pick the tables necessary for the query or star schema, but the foodmart-reduced data source is small enough.</div>
    
    ![s03](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot03.png)

6. In *Generate Relationships*, uncheck *Use primary and foreign keys* so you can manually create the model. Click *Import*. 
    
    <div class="note"><b>Note</b>: The wizard can create relationships with the joins and cardinality from the data source, but it will still need manual adjustments, and it's possible for one to miss a detail because the lack of knowledge about the model. So it's recommended to take the manual route.</div>
    
    ![s04](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot04.png)

7. When the wizard completes the import process, there should be 8 query subjects (one per table). Click *Finish*. Congratulations. You created a project. Now it's time to get familiar with the different kinds of objects and components so we can improve the model.

<div id="step2"></div>

### Step 2: Learn the Components

So you just created a project which is a set of components that defines metadata from one or multiple data sources. Those components include:

<table>
  <tr>
    <th>Namespace</th>
    <td>location that contains all the metadata.</td>
  </tr>
  <tr>
    <th>Data Sources</th>
    <td>references to data sources defined in Cognos Manager</td>
  </tr>
  <tr>
   <th>Parameter Maps</th>
   <td>key-value pairs that link query items to relational data sources.</td>
 </tr>
  <tr>
   <th>Packages</th>
   <td>collections of objects from the project's namespace that is published for business users to query.</td>
 </tr>
</table>

![s05](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot05.png)  

A Namespace is an object that uniquely identifies stored and organized objects that are found in your model.

<div class="note"><b>Note</b>: Uniquely identifies means that a namespace has its own scope so two different namespaces can have an object with the same name and there won't be any conflict because they do not affect one another. You can link one object to an object in another namespace though. It'll hopefully make more sense by the end of this recipe.</div>

A Namespace can contain:

<table>
  <tr>
    <th>Query Subjects</th>
    <td>they're like tables in relational data sources and usually contains Query Items (which are like columns in a table).</td>
  </tr>
  <tr>
   <th>Relationships</th>
   <td>join and cardinality between two Query Items; similar to relationaships in SQL databases.</td>
 </tr>
  <tr>
   <th>Folders</th>
   <td>nothing special. Just  for organization.</td>
 </tr>
  <tr>
    <th>And More Namespaces</th>
  </tr>
</table> 

![s06](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot06.png)  

<div id="step3"></div>

### Step 3: Create Relationships

In [Step 1](#step1), query subjects were imported. Now we need to create relationships and join the query items with the correct cardinality. It's important to join query items correctly so business users will have the correct results. Since we imported all tables, creating relationships in Framework Manager would be as simple as copying the database schema.
  
![s07](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot07.png)

1. Expand *promotion* and *sales_fact 1997* query subjects.

2. Both *promotion* and *sales_fact 1997* query subjects have a *promotion_id* query item. Single click *promotion_id* in either query subject and single click the other *promotion_id* query item while holding down the Ctrl key.

3. Right click either *promotion_id* query item that's selected. Go to *Create* > *Relationship*.

    ![s08](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot08.png)

4. Under *sales_fact 1997*, change the cardinality to *1..n* and leave promotion's cardinality as *1..1*. You can check the database schema, and notice that *sales_fact 1997* reuses the same promotion_id so it's one-to-many and for *promotion*, *promotion id* is the primary key so it's one-to-one. 

    ![s09](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot09.png)

5. To see sample results of a SQL statement using the relationship, click *Relationship SQL* tab. It should validate automatically. On the top, you'll see the SQL statement Cognos generated. Click on *Test* and you should get the top n rows specified. If nothing shows, something is wrong with your relationship.

    ![s10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot10.png)

6. Do the same for the rest of the query items. Your end result should be the following: 

<table>
  <tr>
    <td>sales_fact_1997.promotion_id (1..n)</td>
    <td>promotion.promotion_id (1..1)</td>
  </tr>
  <tr>
    <td>sales_fact_1997.customer_id (1..n)</td>
    <td>customer.customer_id (1..1)</td>
  </tr>
  <tr>
   <td>sales_fact_1997.store_id (1..n)</td>
   <td>store.store_id (1..1)</td>
  </tr>
  <tr>
   <td>sales_fact_1997.product_id (1..n)</td>
   <td>product.product_id (1..1)</td>
  </tr>
  <tr>
   <td>sales_fact_1997.time_id (1..n)</td>
   <td>time_by_day.time_id (1..1) </td>
  </tr>
  <tr>
   <td>product.product_class_id (1..n)</td>
   <td>product_class.product_class_id (1..1)</td>
  </tr>
  <tr>
   <td>store.region_id (1..n)</td>
   <td>region.region_id (1..1)</td>
  </tr>
  <tr>
   <td>customer.customer_region_id (1..n)</td>
   <td>region.region_id (1..1)</td>
  </tr>
</table>  

That was easy! You should now have 8 valid relationships.

![s11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot11.png)

And your schema should look like the following:

![s12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot12.png)

<div class="note"><b>Note</b>: The foodmart-reduced data source schema is not the same from the one we have now. That's because customer has a customer_region_id that is obviously a foreign key of region. Also, some tables have a foreign key for a table named district, but it's not in the data source. That's okay. You can just delete it in the next step.</div>

<div id="step4"></div>

### Step 4: Build Business View

In step 3, you created almost the same schema as what you will find in your database schema, and that's okay, but not for your business users. You don't want them to work with a database schema. You want to provide a very basic layout of query subjects for business users so they can comfortably create queries, and produce reports or workspaces. Hence the guys at Cognos recommend the:   

<br>
<table>
  <tr><th>Three Tier Design</th></tr>
  <tr>
    <td>Physical View</td>
    <td>holds the query subjects and relationships used to build the model. Query subjects should be unmodified views of the source tables. It's what you have now.</td>
  </tr>
  <tr>
    <td>Business View</td>
    <td>contains optimized query subjects for use by business users. Query subjects can be by renamed, moved around, consolidated, merged, etc.</td>
  </tr>
  <tr>
   <td>Presentation View</td>
   <td>this view will be presented to the business user. Query subjects are organized in a way that business users can understand.</td>
 </tr>
</table>  


Lets try this with Foodmart-reduced.

1. Right click on the only namespace in the project *foodmart-reduced*, and *Create* > *Namespace*. Name the namespace, "Physical View".

2. Move all subject queries into *Physical View* namespace. Your project should be structured like the following:

    ![s13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot13.png)

3. Right click on *foodmart-reduced* namespace, and *Create* > *Namespace*. Name the namespace, "Business View".

4. Right click *Business View*, and *Create* > *Query Subject*.

    ![s14](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot14.png)

    A dialog will appear. Name the subject query, "Time" and mark it as a *Model* query subject. Click *OK*. 

    ![s15](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot15.png)

    <div class="note"><b>Note</b>: The subject queries that were created at the beginning of this recipe are known as data source query subject which is comparable to a table in SQL. In the other hand, model query subjects are made from one or more data source subject queries. This means the query subjects in Physical View should be data source while the query subjects in Business View should be model.</div>

5. A dialog will open. To the left you will find your project hierarchy. Collapse *Physical View* and drag *time by day* to the white area on the right. 

6. Make adjustments like renaming or removing query items for simplicity. You can do the following:

    <table>
      <tr><th>Remove the following</th></tr>
      <tr><td>month_of_year</td></tr>
      <tr><td>fiscal_period</td></tr>
      <tr><td>SSMA_TimeStamp</td></tr>
    </table>

    <table>
      <tr><th>Rename the following</th></tr>
      <tr>
        <td>the_date</td>
        <td>Date</td>
      </tr>
      <tr>
        <td>the_day</td>
        <td>Day of the Week</td>
      </tr>
      <tr>
        <td>the_month</td>
        <td>Month</td>
      </tr>
      <tr>
        <td>the_year</td>
        <td>Year</td>
      </tr>
      <tr>
        <td>day_of_month</td>
        <td>Day of the Month</td>
      </tr>
      <tr>
        <td>week_of_year</td>
        <td>Week of the Year</td>
      </tr>
      <tr>
        <td>quarter</td>
        <td>Quarter</td>
      </tr>
    </table>

    ![s16](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot16.png)

7. For *Customer* repeat step #4, but name the subject query, "Customer". Repeat step #5, but drag  *customer* to the white area on the right and then at the bottom right-hand corner, click on *Add* to add a new Query Item. Name it, "Name". From the *Available Components* white area, drag *fname* query item from *customer* in *Physical View* to *Express Definition* white area to the right. And then drag *lname* after *fname*, separated by " + ' ' + " (excluding double quotes). You can do a lot with expressions in Cognos. You can check all of their many functions and parameters by clicking on the tabs on the lower left-hand corner, but we will cover that some other time. Your final expression definition should be:  

    ```c 
        [Physical View].[customer].[fname] + ' ' + [Physical View].[customer].[lname]
    ```


    To test it, click on the blue play button and it should show you the correct results like in the picture below:

    ![s17](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot17.png)

    In *Customer* from *Business View* namespace:

    <table>
      <tr><th>Remove the following</th></tr>
      <tr><td>fname</td></tr>
      <tr><td>lname</td></tr>
      <tr><td>mi</td></tr>
      <tr><td>address2</td></tr>
      <tr><td>address3</td></tr>
      <tr><td>address4</td></tr>
      <tr><td>SSMA_TimeStamp</td></tr>
    </table>

    <table>
      <tr><th>Rename the following</th></tr>
      <tr>
        <td>account_num</td>
        <td>Account Number</td>
      </tr>
      <tr>
        <td>address1</td>
        <td>Address</td>
      </tr>
      <tr>
        <td>state_province</td>
        <td>State / Province</td>
      </tr>
      <tr>
        <td>postal_code</td>
        <td>Postal Code</td>
      </tr>
      <tr>
        <td>country</td>
        <td>Country</td>
      </tr>
      <tr>
        <td>phone1</td>
        <td>Phone #1</td>
      </tr>
      <tr>
        <td>phone2</td>
        <td>Phone #2</td>
      </tr>
      <tr>
        <td>birthdate</td>
        <td>Date of Birth</td>
      </tr>
      <tr>
        <td>marital_status</td>
        <td>Marital Status</td>
      </tr>
      <tr>
        <td>yearly_income</td>
        <td>Annual Income</td>
      </tr>
      <tr>
        <td>gender</td>
        <td>Gender</td>
      </tr>
      <tr>
        <td>total_children</td>
        <td>Total Children</td>
      </tr>
      <tr>
        <td>num_children_at_home</td>
        <td>Number of Children at Home</td>
      </tr>
      <tr>
        <td>education</td>
        <td>Education</td>
      </tr>
      <tr>
        <td>date_accnt_opened</td>
        <td>Date Account Opened</td>
      </tr>
      <tr>
        <td>member_card</td>
        <td>Member Card</td>
      </tr>
      <tr>
        <td>occupation</td>
        <td>Occupation</td>
      </tr>
      <tr>
        <td>houseowner</td>
        <td>House Owner</td>
      </tr>
      <tr>
        <td>num_cars_owned</td>
        <td>Number of Cars Owned</td>
      </tr>
    </table>

8. We know the schema in the *Physical View* namespace is a snowflake, but we want it simpler and faster. This means less joins: Star schema. Customer is joined to region, lets merge them. In *Query Subject Definition*, collapse *Physical View* from *Available Model Objects* and drag *region* to *Query Items and Calculations*. Now you can remove query items: *customer region id* and *region id* since they're not needed anymore. Rename the newly imported query items and test to see if it works.<br><br>
  
    For organizational purposes, you can put the merged query items in a folder. The scope still remains the same. Ctrl + Click all merged query items and then right click on a selected items: *New Parent* > *Query Item Folder*. In this case, you can name it "Region".

9. Before we continue to the other data source query subjects, lets fix the properties for the query items in our Business View. We will focus on one property setting for query item which is *Usage*. There are other important properties that we can talk about on another recipe like *Regular Aggregate*, *Format*, *Precision*, etc.

    A query item can have one of four different usage types:

    <table>
      <tr>
        <th>Icon</th>
        <th>Type</th>
        <th>When to Use</th>
      </tr>
      <tr>
        <td> <img src="http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot19.png" alt="s19" /> </td>
        <td>Identifier</td>
        <td>Database key, date/datetime</td>
      </tr>
      <tr>
        <td> <img src="http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot20.png" alt="s20" /> </td>
        <td>Fact</td>
        <td>Numeric value that can be calculated</td>
      </tr>
      <tr>
        <td> <img src="http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot21.png" alt="s21" /> </td>
        <td>Attribute / Unknown</td>
        <td>Is not an Identifier or Fact, it's an attribute.</td>
      </tr>
    </table>

    With the rule of thumb table above, try to correct the usage type for all query items in Customer. Some of them are correct already. Property settings can be found at the bottom of Framework Manager after selecting a query item.

    ![s18](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot18.png) 
    
    Take a look at my Customer's query item icons and see if it matches yours:

    ![s22](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot22.png) 

10. Do steps 4-9 for the rest of the query subjects.

<div id="step5"></div>

### Step 5: Build Presentation View

Now that we have created all query subjects for *Business View*, lets finish up by creating the Presentation View. In *Presentation View*, there will only be shortcut links that point to the query subjects in *Business View*. Then we'll group the shortcut links in a star schema. This allows you to easily modify what business users see without modifying any of the query subjects, and when query subjects are modified in the Business View, changes take effect in the Presentation View as well. 

1. Ctrl + Click fact and all dimension subject queries. When all are selected, right click on one of them, and choose *Create Star Schema Grouping...*

    ![s23](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot23.png)

2. *Create Star Schema Grouping* Dialog will appear. Accept default settings and name the namespace, "1997 Sales".

    ![s24](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot24.png)

3. Right click *foodmart-reduced* namespace and *Create* > *Namespace*. Name it "Presentation View" and move *1997 Sales* to *Presentation View*.

    ![s25](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot25.png)

<div id="step6"></div>

### Step 6: Publish Package

The content is now ready for the business user to use in the form of a star schema grouping. Let's publish the Presentation View:

1. Right click on *Packages* and *Create* > *Package*

    ![s26](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot26.png)

2. *Create Package* dialog will appear. Name your package "foodmart". Click *Next*.

    ![s27](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot27.png)

3. Now you have to define your objects. The green checkmark means the object will be included, red X means it will be excluded, and the third option means it's included, but it's hidden. We only want business users to have access to Presentation View, not Physical or Business View, but we cannot exclude Physical or Business because Presentation depends on it. Your setting should look like the following image:

    ![s28](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot28.png)
 
4. Remember when we created the expression to concatenate first and last name to a full name query item? There's a list of functions that you can use to create more sophisticated expressions when you click the *functions* tab. There's also vendor specific functions that we won't be using at all except for SQL Server. By default, they're all included, lets just keep SQL Server specific functions. Click the top most option in the list, Shift + Click the bottom most option in the list, Ctrl + Click *SQL Server*. Then click the arrow pointing to the left. The lists should look like the following image and click *Finish*.

    ![s29](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot29.png)

5. You created your package, now you should get a prompt asking if you want to open the *Publishing Package Wizard*. Click ***Yes***.

    ![s30](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot30.png)

6. In *Select Location Type* window, you need to choose where you're going to store your package. The typical place to store packages is in Cognos Content Store. There are two folders in the Content Store you can save your package or pretty much any file type:  

    <table>
      <tr>
        <td>Public Folders</td>
        <td>stores files, packages, and folders that is viewable to ALL users.</td>
      </tr>
      <tr>
        <td>My Folder</td>
        <td>stores files, packages, and folders that is viewable to ONLY you and the administrator.</td>
      </tr>
    </table>  

    To save it in your *My Folder*, open the Cogno's Content Store explorer:

    ![s31](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot31.png)

    Click on Cognos on the top left corner and choose *My Folder*:

    ![s32](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot32.png)

    Click *Next* twice.

7. Click *Publish*.

    ![s33](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot33.png)

8. By default, Framework Manager verifies packages when they're published and alerts you if any errors or warning were found. If you didn't get any warnings or errors, Congratulations! You successfully published your first, no-error package!

Downloads
---------

- [Framework Manager Project Example Above](https://docs.google.com/open?id=0B8bnF9QulzZgbzlVNTlFelFsejQ)

Do It Yourself
--------------

Create a DMR Model with the FoodMart 2008 db. FoodMart 2008 has lots of more tables, but don't worry. As long as you create a snowflake or star schema that has relationships of many-to-one from the inside out, clean things up, denormalize it, and etc, you should be okay.  
<br>
**Fact Table**: *inventory_fact 1997* 
<br><br>
**Other Tables**: *product, product_class, warehouse,* and *time_by day*.

<hr>