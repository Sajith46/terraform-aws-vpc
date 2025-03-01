Method 1


1.create vpc and subnet in aws using terraform code





2.Create a repository in github and push terraform code to github



3.Trigger the github code using github action method



4.Vpc and Subnet are created automatically in aws 

or
 
Method 2
1.create vpc and subnet in aws using terraform code
2.Create a repository in github and push terraform code to github
3.Install git, terraform, jenkins, java in locally using cmd ,powershell
4.Then find the path of all install thing copy it to the System variable in environment setting
5.Login in to the jenkins using local:8080
6.Install terrfaorm ,git other necessary plugin to plugin in Manage Jenkins 
7.create a job in jenkins and select pipline then go the config setting add repository url of github ,add path of jenkins file ,also and branch 
8.add IAM user AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY to the credential in manage
9.Then Trigger the New Create job in jenkins
10.Vpc and Subnet are created automatically in aws

