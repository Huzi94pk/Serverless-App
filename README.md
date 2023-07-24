# WildRyde
A serverless app that mimics how ride share app works. This ride share app will be built and deployed using AWS Amplify which is an AWS developlment platform that allows users to build full-stack mobile/web applications. The repository will be hosted on AWS CodeCommit. The components for this app are Cognito, Lambda, DynamodB and REST API. 

To access the application: 
App Link: https://master.d22f4rkymvc7q3.amplifyapp.com/
1. Click on Giddy up found at the web app link given above
2. Register using username, email and password
3. Sign in to Giddy up
4. You should be directed to the endpoint https://master.d22f4rkymvc7q3.amplifyapp.com/ride
5. Set a pick-up location and the unicron will arrive

APPLICATION DEVELOPMENT 

In summary, the following AWS services were used to create and deploy the WildRyde App

1. AWS Amplify
2. AWS CodeCommit
3. AWS IAM Roles
3. AWS Cognito UserPool
4. AWS Lambda
5. AWS DynamodB
6. AWS API Gateway 

This project was built using AWS Shell CLI. Following are the steps that must be implemented to build the serverless app. 

1. Install AWS shell on PowerShell in Visual Studio
pip install aws-shell

2. Configure AWS shell
aws configure
// add Access Key & Secret Access Key and relevant aws region

3. Create a repository on AWS CodeCommit and name it wild-rydes
aws codecommit create-repository --repository-name wild-rydes

4. Clone the source code from publicily available Github repository
git clone https://github.com/aws-samples/aws-serverless-webapp-workshop

5. Split the WildRydes app into a branch as the other files are not required
cd aws-serverless-webapp-workshop
git subtree split --prefix resources/code/WildRydesVue --branch WildRydesVue


6. Create a git repo and populate it with source code of WildRydesVue
mkdir ../wild-rydes
cd ../wild-rydes
git init
git pull ../aws-serverless-webapp-workshop WildRydesVue

7. Connect to AWS CodeCommit repository and push this source code
git remote add origin codecommit://wild-rydes
git push -u origin master

8. Build the application on Amplify 
    - Connect anplify to the codecommit repo. Create IAM role to grant permission to backened      environment to read from codecommit.
    - Attach AWSCodeCommitReadOnly and AdministratorAccess-Amplify policy to the role
    - Deploy the app

9. Install amplify cli to be able to connect to amplify and create cognito userpool
npm install -g @aws-amplify/cli
amplify init

10. Craete Cognito UserPool to allow user sign up and sign in options at Giddy Up 
amplify add auth

11. Push changes to the codecommit
git add .
git commit -m "made changes"
git push

12. Create IAM role for Lambda to write to CloudWatch and PutItem to DynamodB
    - Attach AWSLambdaBasicExecutionRole policy to the role 
    - Create inline policy within the role to PutItem to dynamoDB

13. Create DynamodB

14. Create Lambda Function using RequestUnicorn.js file in this repository and attach the IAM role created in step 12. 

15. Test the Lambda Function using the TestRequestUnicorn.js file 

16. Deploy REST-API using API Gateway
    - Setup an Authorizer
    - create resource at endpoint /ride with POST method integrated with Lambda
    - Enable CORS
    - connect method request with AUTH

17. Use the App! 
