Instructions:

Main Task---------------------------------------------------------------------------------------------------------------
1. Change the Email Address from meiyappan1990@gmail.com to your preferred email address in the Line Number - 79 (LambdaFunction2 Resources).
2. Upload this updated yaml file to the cloudformation.
3. Test the following input in API Gateway -> Test. Then click Test.
    
   {
   
         "team_country":"Australia",
   
         "team_name":"Rockers",
    
         "team_desc":"Cricket",
   
         "team_rating":"10"
   
}
   
4. Go to DynamoDb and check the table. In the Items Tab, The data should be updated/created.

Secondary Task-------------------------------------------------------------------------------------------------------------

5.Repeat step 3 with the following input.

   {
   
         "team_country":"Aussie",
   
         "team_name":"Beast",
    
         "team_desc":"footy",
   
         "team_rating":"7"
   
}
   
6. Go to the given email address and click on the confirm subcription email. Confirm the Subscription.
7. You also received the notifications email with the message 'A Row has been updated/Added'.

Improvements---------------------------------------------------------------------------------------------------------------------

1. We can also be specific to the Resource in the IAM Role (LambdaExecutionRole).
2. Based on the functionality, we can be more specific in the policies of IAM Role (LambdaExecutionRole).
3. Lambda code can be given in a seperate file instead of including in the cloudformation template.

Solution Design--------------------------------------------------------------------------------------------------------------------

For Main Task

1.Found that the provided cloudformation template missing relavent IAM policies for the Lambda to communicate to the DynamoDb.Therefore, Added the relevant policies in the lambda execution role (IAM Role).
2.DynamoDb Tablename in the Lambda Code(LambdaFunction) was different from the actual DynamoDb TableName (DynamoTable) in the resources. Therefore, Changed the DynamoDb table name in the lambda code to match the actual dynamoDb table name.


For Secondary Task

	DynamoDb ---- trigger ----- Lambda ------ SNS publish ------ Email Notification

1. Added a data stream trigger in DynamoDb table in order to trigger lambda whenever there is an update or addition of a row in the dynamoDb table.
2. Lambda code intially creates the SNS topic during cold start up of lambda so that the topic is created only once.
3. SNS subscrpition for Email is also added during the cold start up of lambda.
4. Lambda handler contains the code to perform SNS publish whenever the lambda is triggered by DynamoDb


