# cost-optimzation-snapshot
Efficient AWS Cost Management through Stale Resource Detection

Problem :
Sometimes, developers create EC2 instances with volumes attached to them by default. For backup purposes, these developers also create snapshots. However, when they no longer need the EC2 instance and decide to terminate it, they sometimes forget to delete the snapshots created for backup. As a result, they continue to incur costs for these unused snapshots, even though they are not actively using them.

Solution :
We're using AWS to save money on storage costs. We made a Smart Lambda function that looks at our snapshots and our EC2 instances. If Lambda finds a snapshot that isn't connected to any active EC2 instances, it deletes it to save us money. This helps us keep our AWS costs down.

Note :
There are many similar problems like this. For instance, we might attach an Elastic IP to our EC2 instance but forget to delete the Elastic IP after terminating the EC2 instance. In such a case, the Elastic IP continues to incur costs for us.

steps::::1.create ec2 instance by default it attach with volume then go in elastic block store and create snapshot of it---select volume -choose by deafult volume in it and provide a  name to snapshot and create snapshot.
2...after creating a snapshot go to lambda function enter a select author from scratch--function name--in runtime select python 3.11 or latest and remain same all click on create. Below in lambda console page code is given erase it and put the code given in this same snapshot.py file after paste the code deoploy the code and click on the test-create new event- provide test-event name remain all same create it
3. Goto IAm-policies-in select service choose EC2--In the Actions section, grant permissions for the following actions: DescribeInstances, DescribeVolumes, DescribeSnapshots, DeleteSnapshots.
After Creating the Policies , Goto to the Lambda Sections.
Next, go to the page of the Lambda function you've created. In the "Permissions" section, click on the role name.
Click on 'Add Permissions' and then select 'Attach Policy.' and then Choose the correct policy you created.Then scroll down and click 'Add Permissions'.
5 now go to lambda console click on test it show some output but now we terminate the instance volume is automatically delete with it but snapshot remain... now again goto snapshot and test the code in output this time we seen that our snapshot is deleted.....
