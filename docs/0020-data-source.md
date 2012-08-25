Setting Up Data Source
======================

The Problem
-----------

You need to connect Microsoft SQL Server database to Cognos.

The Solution
------------

- [ODBC](http://en.wikipedia.org/wiki/ODBC)

### The Steps

1. [Run ODBC](#step1)
2. [Add System Data Source](#step2)
3. [Connect Cognos to Data Source](#step3)

<div id="step1"></div>

### Step 1: Run ODBC

This step can be confusing if you're using a 64-bit machine because there's two ODBC drivers in Windows:  
  
32-bit:

```c
%WINDIR%\SysWOW64\odbcad32.exe
```

64-bit:

```c
%WINDIR%\System32\odbcad32.exe
```

The problem is that all shortcuts in 64-bit Windows machines point to the 64-bit ODBC driver by default, and that's fine, but Cognos ignores the 64-bit driver. Instead it only accepts 32-bit so we have to set up SQL Server with that.

1. Go to *Start* and type *run* and execute the *Run* application. Or enter Alt+F2.

    ![data1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data1.png)

2. Execute the 32-bit ODBC driver.

    ![data2](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data2.png)

<div id="step2"></div>

### Step 2: Add System Data Source

1. Click *Add* button under *System DSN* tab to create ODBC data source name (DSN).

    ![data3](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data3.png)

    <div class="note"><b>Note</b>: There's three kinds of DSN: User, System, and File. If created under User, only the user currently creating the ODBC can access it, but this is a problem because Informix (Cogno's content store) runs under icognosexpress user, not as you. File is for networking purposes, but you're on a single machine so we can ignore that. System allows all users in your machine to use that data source.</div>

2. *Create New Data Source* dialog will open. Choose *SQL Server* from the list of available drivers.

    ![data4](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data4.png)    

3. In *Create New Data Source to SQL Server*, give it a name and point to the SQL Server you want to connect to. Click *Next*

    ![data5](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data5.png)

4. If you're using Windows Authentication to access SQL Server, click *Next*, otherwise, enter the username and password.

    ![data6](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data6.png)

5. Change the default database to the one you want to analyze. In this case, *foodmart-reduced*. Click *Next*

    ![data7](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data7.png)

    Click *Finish*.

    ![data8](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data8.png) 

6. Click *Test Data Source...* to check if it connects.

    ![data9](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data9.png)

    Should say *TESTS COMPLETED SUCCESSFULLY!* Click *OK* until you exit out of ODBC.

    ![data10](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data10.png)

<div id="step3"></div>

### Step 3: Connect Cognos to Data Source

1. Open Internet Explorer, and go to Cognos Express Manager *http://127.0.0.1:19300/cognos_express/manager*.

2. Log in as *administrator*

3. Go to *Data* tab under *Administrator* and click *Add...* at the bottom of the window.

    ![data11](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data11.png)

4. Set the textfield attributes to the following:

    <table>
      <tr>
        <th>Data Source Type</th>
        <td>Microsoft SQL Server (ODBC)</td>
      </tr>
      <tr>
        <th>Name</th>
        <td>foodmart-reduced</td>
      </tr>
      <tr>
        <th>ODBC Data Source</th>
        <td>foodmart-reduced</td>
      </tr>
      <tr>
        <th>Database Name</th>
        <td>foodmart-reduced</td>
      </tr>
      <tr>
        <th>User ID</th>
        <td>Enter the username to log in to SQL Server</td>
      </tr>
      <tr>
        <th>Password</th>
        <td>Enter the password to log in to SQL Server</td>
      </tr>
    </table>

    Click *Retrieve Database Objects*

    <div class="note"><b>Note</b>: If you get an exception, it may be that Cognos does not have permission to access foodmart-reduced database. I don't know a lot about configuring SQL, but since you're running Cognos on a stand alone server, we can get away with weak security. Launch SQL Server Management Studio, log in, right click foodmart-reduced database, go to properties, go to Permissions, add guest as a user, and grant him access to all the explicit permissions. Click ok and try again.</div>

    ![data12](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data12.png)

5. Then for *Database Object*, select *foodmart-reduced*. Click *OK*

    ![data13](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/data13.png)



Now you can connect to the *foodmart-reduced* data source connection when creating models.

Do It Yourself
--------------

Connect Foodmart-2008 SQL Server to Cognos Express.

<hr>









