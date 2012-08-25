Create TM1 Server
=================

The Problem
-----------

You want to create a TM1 Server, aka ICAS (IBM Cognos Analytic Server).


The Solution
------------

- [Architect](/Tools+of+the+Trade.html#architect)

### The Steps
1. [Setting Up tm1s.cgf File](#step1)
2. [Create TM1 Windows Service](#step2)
3. [Run TM1 Windows Service](#step3)
4. [Login to TM1 Server](#step4)

<strong>To automate setps 1 through 4, go to <a href="#downloads">downloads</a> and execute create_server file. It'll ask you for server name and port number you wish to use for the TM1 server. </strong> 

<br><br>

<div class="note"><b>Note</b>: 
This tutorial assumes your Cognos installation is in <b>C:\Program Files (x86)\IBM\Cognos Express</b> and you are signed in as the local Administrator for your Windows machine. And in some cases, you need to execute commands in command prompt which is located in:
</div>

```c
Start > All Programs > Accessories > Command Prompt
```

<br>

<div id="step1"></div>

### Step 1: Setting Up tm1s.cgf File

1. Create a folder called *foodmart* in C:\Program Files (x86)\IBM\Cognos Express\Xcelerator\Custom\TM1Data\

2. Inside the foodmart directory, create a file called ***tm1s.cfg***

3. Open *tm1s.cfg* and input the following:

    <div class="textcode">
    [TM1S]<br>
    <br>
    AllowSeparateNandCRules = T<br>
    CAMPortalVariableFile = portal/variables_TM1.xml<br>
    ServerCAMURI = http://<b>[hostname]</b>:19300/p2pd/servlet/dispatch<br>
    IntegratedSecurityMode = 1<br>
    DataBaseDirectory = .<br>
    UseSSL = T<br>
    ClientCAMURI = http://<b>[hostname]</b>:19300/p2pd/servlet/dispatch<br>
    PortNumber = <b>[port number]</b><br>
    ClientPingCAMPassport = 900<br>
    ServerName = foodmart<br>
    </div>

The text in bold need to be changed:

- hostname: the name of your computer. Execute the following in command prompt to find the computer name.

```c
echo %computername%
```

- port number: port number has to be unused and in the range that Cognos can access. By default, range is 19301-19500.

![tm1_1](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/createtm1_1.png)

<div id="step2"></div>

### Step 2: Create TM1 Windows Service

In command prompt, execute:

```c
"C:\Program Files (x86)\IBM\Cognos Express\bin64\tm1sd.exe" -install -n foodmart 
-z "C:\Program Files (x86)\IBM\Cognos Express\Xcelerator\Custom\TM1Data\foodmart"
```

![tm1_2](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/createtm1_2.png)

<div id="step3"></div>

### Step 3: Run TM1 Windows Service

In command prompt, execute:

```c
net start "IBM Cognos TM1 Server x64 / foodmart"
```

![tm1_3](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/createtm1_3.png)

<div id="step4"></div>

### Step 4: Login to TM1 Server

Open Architect.

```c 
Start > All Programs > IBM Cognos Express > Architect
```

Collapse *Servers* and double click *foodmart*. Login as *admin* with no password and you should be able to see the objects in the server.

![tm1_4](http://i1254.photobucket.com/albums/hh616/jcabrra/cognos%20cookbook/createtm1_4.png)

<div id="downloads"></div>

Downloads
---------

- [TM1-Server-Create-Remove.zip](https://docs.google.com/open?id=0B8bnF9QulzZgMFN2d3BVLUVuejg)

<hr>