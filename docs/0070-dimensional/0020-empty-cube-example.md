Manual Cube Creation
====================

Problem
-------

Learn how cubes work in TM1 by manually creating a cube.

Solution
--------

- [Architect](/Tools+of+the+Trade.html#architect)

### The Steps

1. [First Dimension](#step1)
2. [Second Dimension](#step2)
3. [Build Cube](#step3)
4. [Explore the Cube](#step4)
5. [Fiddling with Attributes](#step5)
6. [Subsets](#step6)

<div id="step1"></div>

### Step 1: First Dimension

Before creating a cube, you need to have at least two dimensions. This first dimension will be a time dimension called *Months*. Months will have elements with the 12 months of the year that will roll up to quarters, and quarters will roll up to year.

1. Launch Cognos Architect.

    ```c
        Start > All Programs > IBM Cognos Express > Architect
    ```

2. Login to the *foodmart* TM1 server.

    ![sc1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc1.png)

3. Right click *Dimensions* and choose *Create New Dimension*.

    ![sc2](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc2.png)

4. In *Dimension Editor*, go to *Edit* > *Insert Element*

    ![sc3](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc3.png)

5. In *Insert Element Name*, type *Jan*. 

6. Dimension elements have one type out of three:

    <table>
      <tr>
        <td>Simple</td>
        <td>The very last child node in the hierarchy. It has no child elements.</td>
      </tr>
      <tr>
        <td>Consolidated</td>
        <td>Contains child nodes.</td>
      </tr>
      <tr>
        <td>String</td>
        <td>Elements in the measure dimension that have string data. ie. "New York"</td>
      </tr>
    </table>

7. Set *Jan* and all the following to *Simple*, and click *Add* until you have all of the following:

    <table>
      <tr><td>Jan</td></tr>
      <tr><td>Feb</td></tr>
      <tr><td>Mar</td></tr>
      <tr><td>Apr</td></tr>
      <tr><td>May</td></tr>
      <tr><td>Jun</td></tr>
      <tr><td>Jul</td></tr>
      <tr><td>Aug</td></tr>
      <tr><td>Sep</td></tr>
      <tr><td>Oct</td></tr>
      <tr><td>Nov</td></tr>
      <tr><td>Dec</td></tr>
      <tr><td>Q1</td></tr>
      <tr><td>Q2</td></tr>
      <tr><td>Q3</td></tr>
      <tr><td>Q4</td></tr>
      <tr><td>Total Year</td></tr>
    </table>

8. Click *OK*

    ![sc4](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc4.png)

9. Next step is to drag and drop elements around so we can construct the hierarchy we want. Select all quarters and drag and drop it into *Total Year*.

    ![sc5](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc5.png)

    ![sc6](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc6.png)

10. Drag and drop the months to their appropriate quarter. Final result should be the following:

    ![sc7](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc7.png)

11. Click *OK* and name the dimension *Months*. Click *OK* one more time to save the dimension.

    ![sc8](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc8.png)

<div id="step2"></div>

### Step 2: Second Dimension

The second dimension will be a common one: *Region*. Cities will roll up to states, and states will roll up to country.

<br>
Repeat steps 3-11 when creating first dimension except, the elements will be the following:

<table>
      <tr><td>United States</td></tr>
      <tr><td>New York</td></tr>
      <tr><td>Florida</td></tr>
      <tr><td>New York City</td></tr>
      <tr><td>Poughkeepsie</td></tr>
      <tr><td>Miami</td></tr>
      <tr><td>Orlando</td></tr>
</table>

And final result:

![sc9](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc9.png)

Name the dimension *Cities*

![sc10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc10.png)

<div id="step3"></div>

### Step 3: Build Cube

Now that we have at least two dimensions we can create a cube (with no data).

1. Right click on *Cubes* and choose *Create New Cube*

    ![sc11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc11.png)

2. Under *Available Dimensions*, select the two available dimensions we just created and click on the right-pointing arrow.

    ![sc12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc12.png)

    ![sc13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc13.png)

3. Click *Properties...* button.

    ![sc14](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc14.png)

4. Leave *Measures Dimension* blank since we haven't created one yet. For *Time Dimension*, choose *Months*. Click *OK*

    ![sc15](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc15.png)

5. Under *Cube Name*, name it *Test* and Click *Create Cube* button.

    ![sc16](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc16.png)

<div id="step4"></div>

### Step 4: Explore the Cube 

1. Double click on *Test*, the newly created cube.

2. *Cube Viewer* opens. Click on the *Recalculate* button. 

    ![sc17](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc17.png)

    Recalculate will generate the latest numbers that are stored in memory. You can expand cities and months.

    ![sc18](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc18.png)

    They're all zeros because we have nothing to measure.

3. Exit out of cube viewer. A pop up will ask you to save changes. If you save, Tm1 will save the instance you're currently viewing (all the zeros) as a view (aka virtual cube) so you can come back to it later.

    ![sc19](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc19.png)

    Name the view as *Zeros* and click *OK*

    ![sc20](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc20.png)

<div id="step5"></div>

### Step 5: Fiddling with Attributes

Attributes describe elements, while elements describe the data. ie. The car type can be a string element, and its attribute may be the color of the car. Attributes are convenient, but if you find yourself creating multiple attributes for an element, consider creating a new element so you can measure data against that attribute. ie. You can measure car sales by car type and car sales by car color.

<br>
Let's create a *Next* attribute for the elements in the *Month* dimension. It should match the following
:

<table>
  <tr>
    <th>Elements</th>
    <th>Next Attribute</th>
  </tr>
  <tr>
    <td>Jan</td>
    <td>Feb</td>
  </tr>
  <tr>
    <td>Feb</td>
    <td>Mar</td>
  </tr>
  <tr>
    <td>Mar</td>
    <td>Apr</td>
  </tr>
  <tr>
    <td>Apr</td>
    <td>May</td>
  </tr>
  <tr>
    <td>etc.</td>
  </tr>
</table>
 
1. Right click on *Months* dimension and choose *Edit Element Attributes...*

    ![sc21](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc21.png)

2. In *Attributes Editor* window, go to *Edit* > *Add New Attribute*

    ![sc22](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc22.png)

3. Under *Name* type *Next* and leave the type as *Text*. Click *OK*

    ![sc23](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc23.png)

4. Under the Next column, fill in each space with the appropriate values and click *OK*

    ![sc24](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc24.png)

<div id="step6"></div>

### Step 6: Subsets

To test the new attribute we created in our previous step, let's create a subset of the *Months* dimension that filters by attribute. A subset is simply a portion of the elements in a dimension.

1. Right click *Months* dimension and choose *Insert New Subset...*

    ![sc25](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc25.png)

2. In *Subset Editor* window, click on *Filter By Attribute* button.

    ![sc26](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc26.png)

3. Under *Attribute*, choose *Next*, and *Q1* as the attribute value. Click *OK*

    ![sc27](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc27.png)

    And the result should be the key element to the value attribute which is the consolidated *Q4*. 

    KEY -> VALUE

    Q4  -> Q1

    ![sc28](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc28.png)

4. In *Subset Editor*, click on the *Save Subset* button.

    ![sc29](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc29.png)

    Name it *Quarter4* and click *OK* 

    ![sc30](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc30.png)

    ![sc31](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/sc31.png)  
