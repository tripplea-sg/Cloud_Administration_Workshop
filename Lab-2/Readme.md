# Login to Cloud & Setup Compartment and VCN 

Watch this video for steps to login to Oracle cloud and Create compartment / Policy /VCN: https://www.youtube.com/watch?v=dasutiDLTkM </br>
Do **step 1 (create Compartment), step 2 (create policy), and step 3 (Create Virtual Cloud Network or VCN)**. </br>
**DO NOT** do step 4 (provision th MySQL Database Service / MDS), we wil be doing it later today (but not now). </br>
</br>
## Login to Oracle Cloud
1.	To Sign in to Oracle Cloud, please visit https://www.oracle.com/cloud/sign-in.html, enter Cloud Account Name
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture1.png)
</br>
2.	On Oracle Cloud Account Sign in, enter User Name, that is the e-mail address 

![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture2.png)
</br>
3.  When you sign in to the Oracle Cloud you'll see the Console home page. 

![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture3.png)
</br>
## Create Compartment
(Refer to Step-1 on the video) </br>
1.	On the Navigation Menu, under Governance and Administration, select Identity -> Compartments. 
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture4.png)
</br>
2.	On Compartments Page, click on Create Compartment. </br>
Note:  Two Compartments, named Oracle Account Name (root) and a Managed CompartmentForPaaS, were automaticatly created by the Oracle Cloud. 

![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture5.png)
</br>
3.	On Create Compartment, enter Name, Description, select Parent Compartment, and click on Create Compartment. 
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture6.png)
</br>
## Create Policy
(Refer to Step-2 on the video) </br>
1.	On the Navigation Menu, under Governance and Administration, select Identity -> Policies. 
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture6.png)
</br>
2.	On Policies Page, under List Scope, select the Compartment(root).

![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture6.png)
</br>
3.	On Create Policy, enter Name, Description, and add the following Policies Statements: </b>
-	Policy Statement 1:
	- Allow group Administrators to {COMPARTMENT_INSPECT} in tenancy
-	Policy Statement 2:
 	- Allow group Administrators to {VCN_READ, SUBNET_READ, SUBNET_ATTACH, SUBNET_DETACH} in tenancy
-	Policy Statement 3:
  -	Allow group Administrators to manage mysql-family in tenancy
  ![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-2/Picture6.png)
</br>

## Create Virtual Cloud Network (VCN)
</br>
(Refer to Step-3 on the video) </br>
1.	On the Navigation Menu, under Core Infrastructure, select Networking -> Virtual Cloud Networks. 

