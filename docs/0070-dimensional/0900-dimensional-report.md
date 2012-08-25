Dimensional Report
==================

The Problem
-----------

Create a chart that compares supermarkets with the rest of the store types in regards of the products that have of over 800 store sales.

The Solution
------------

- [Framework Manager](/Tools+of+the+Trade.html#framework_manager)
- [Query Studio](/Tools+of+the+Trade.html#query_studio)
- [Architect](/Tools+of+the+Trade.html#architect)

### The Steps

1. [Fix Cube](#step1)
2. [Build Data Source](#step2)
3. [Publish Package](#step3)
4. [Query Data](#step4)
5. [Create Chart](#step5)

<div id="step1"></div>

### Step 1: Fix Cube

In this recipe, we'll be using the cube that was created in the [previous recipe](/Loading+Data+into+Cubes.html). Before we do anything, we need to assign a Time and Measure dimension to the cube directly since that was never done or else when building a package, Cognos will start complaining that there's missing data.

1. Launch Cognos Architect.

    ```c
        Start > All Programs > IBM Cognos Express > Architect
    ```

2. Login to the *foodmart* TM1 server.

    ![sc1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc1.png)

3. Right click *Store Sales* cube and choose *Properties...*

4. We never created a measure dimension because we only had one data variable so we could get away with it. For *measures dimension*, I put *Stores* but it won't matter because the data remains in the cube. Put *Months* for time dimension. Click *OK*

<div id="step2"></div>

### Step 2: Build Data Source

The first step is to connect the TM1 server connection in Cognos Express so it can be used by other tools like Report Studio, Query Studio, and Business Insight Advanced. We'll do this through Framework Manager because we need to publish a package in [Step 3](#step3).

1. Start Framework Manager from your Windows Start Menu:
 
    ```c
        Start > All Programs > IBM Cognos Express > Framework Manager
    ```

2. Click *Create a new project...*.

    ![dr1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr1.png)

3. A *New Project* dialog opens. Give your project a name, "TM1-foodmart". Click *OK*.

    ![dr2](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr2.png)

4. After logging in and selecting a language, the *Metadata Wizard* will start. In *Select Metadata Source*, choose *Data Sources*.

    ![s02](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/fm_screenshot02.png)

5. In *Select Data Source*, there will be a list of data sources that was configured in Cognos. We haven't configured one for the foodmart TM1 server yet. Let's do that now. Click *New* button.

    ![dr3](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr3.png)

    <div class="note"><b>Note</b>: You must be logged in as a Cognos Administrator user to have the privelege of creating a data source connection.</div>

6. *New Data Source Wizard* window opens. Click *Next*. Give the data source a name, "tm1-foodmart". Click *Next*

    ![dr4](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr4.png)

7. For *Type*, choose *IBM Cognos TM1*. Click *Next*

    ![dr5](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr5.png)

8. For *Administration Host*, enter "localhost" since there's no networking involved in our Cognos setup.

9. For *Server Name*, enter "foodmart"; that's the name of the tm1 server we're connecing to.

10. For *Sign On*, enter the credentials of the TM1 foodmart server.

11. Click *Test Connection...*

    ![dr6](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr6.png)

12. Click *Test* button.

    ![dr7](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr7.png)

13. The status should be *Succeeded*. Click *Close*.

    ![dr8](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr8.png)

14. Click *Finish* to complete the new data source.

    ![dr9](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr9.png)


<div id="step3"></div>

### Step 3: Publish Package

Publishing a package that contains a cube allows the data to be accessed from any application that can open a package so it can be analyzed with its extra dimensional features such as drill down, roll up, etc.

1. To publish a package, continue with the *metadata wizard* that we left off from [Step 2](#step2). In *Select Data*, select *tm1-foodmart*. Click *Next*

    ![dr10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr10.png)

2. In *Select Objects*, select *Store Sales*. since that is our only cube. Click *Next*

    ![dr11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr11.png)

3. In *Select Locales*, click *Next*; we don't have any locales.

4. Check *Create a default package* so we can publish one right away. And click *Finish*

    ![dr12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr12.png)

5. *Create Package* window opens. It automatically filled out the name as *Store Sales*. Click *Finish*

    ![dr13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr13.png)

    Click *Yes*

    ![dr14](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr14.png)

6. *Publish Wizard* window opens. It'll store the package in the content store by default, and in my case, I'm saving it in *My Folders*. Click *Next*

    ![dr15](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr15.png)

7. In *Add Security*, click *Next*; that's not necessary now.

8. Finally, click *Publish* and everything will be verified and then click *Finish* to exit out.

    ![dr16](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr16.png)

<div id="step4"></div>

### Step 4: Query Data

1. Launch Internet Explorer and go to *http://127.0.0.1:19300/cognos_express/manager/welcome.html*. Log in if prompted.

2. Click *Query my business data with Query Studio*

    ![q1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/q1.png)

3. Find and open *Store Sales* package. Query Studio should now open a blank project.

    ![dr17](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr17.png)

4. Query Studio should now be open with your Store Sales data.

    ![dr18](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr18.png)

5. Select *Products* and click the *Insert* button with the left, green pointing arrow.

    ![dr19](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr19.png)

    ![dr20](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr20.png)

6. Expand *Stores*, select *total store* and click *Insert*.

    ![dr21](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr21.png)

    ![dr22](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr22.png)

7. Expand *total store*, select *Supermarket* and click *Insert*

    ![dr23](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr23.png)

    ![dr24](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr24.png)

8. Select one of total store's data, right click, and select *Sort...* 

    ![dr25](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr25.png)

9. In *Sort Order*, choose *Descending (9 to 1)* and click *OK*

    ![dr26](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr26.png)

10. Select one of total store's data, right click, and select *Filter...*

    ![dr27](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr27.png)

    Condition should be: *Show only the following*, from 800 to Highest value. Click *OK*

    ![dr28](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr28.png)

    ![dr29](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr29.png)

<div id="step5"></div>

### Step 5: Create Chart

1. Click the chart button.

    ![dr30](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr30.png)

2. Under *Chart Type*, choose *Bar* and pick *100 Percent Stacked*. Check *Show values on the chart*. Click *OK*

![dr31](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr31.png)

![dr32](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/dr32.png)
