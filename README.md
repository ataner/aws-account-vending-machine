# Account Factory

Forked from https://github.com/aws-samples/account-factory


## Creating an Account Vending Machine with Service Catalog

I found a tutorial and some code to create an Account Vending Machine for your Organization. Unfortunately it was outdated. I did some changes and wrote an updated how-to.

### Do the following steps under your ROOT account:

1. Enable AWS Organizations
2. Enable Service Catalog under AWS Organizations
3. Create a Group for your Service Catalog End Users. Let's call it ServiceCatalogEndUsers
4. Attach the following AWS Managed policies to ServiceCatalogEndUsers
* AWSServiceCatalogEndUserFullAccess
* AWSLambdaFullAccess
* IAMFullAccess
* AmazonS3FullAccess
* AWSCloudFormationReadOnlyAccess

5. Create a user to run Service Catalog - it CANNOT BE THE ROOT ACCOUNT. I'll call it ServiceCatalogUser
6. Add ServiceCatalogUser to ServiceCatalogEndUsers Group
7. Attach the AWS Managed Policy AWSServiceCatalogAdminFullAccess to your own user
8. Create an S3 bucket on the same region you want to run Service Catalog
9. Check-out code from GitHub
10. Edit the code you got from GitHub on accountbuilder.yml
11. Edit sourcebucket Default to match the name of the bucket you created
12. Upload AVM files to S3 Bucket
13. Save the URL of the accountbuilder.yml file on S3. You will need that.
14. Go to Service Catalog.
15. Go to Portfolios, and Create Portfolio. You can use any name you want. Let's go with My Portfolio. Provide a description and put your name under the owner. Press Create.
16. Now it will show up under the list of Portfolios. Click it.
17. Click the Tab "Groups, Roles and Users", and click the orange "Add groups, roles, users" button on the right
18. Select the ServiceCatalogEndUsers group we created above and Administrators under Groups, and click Add Access
19. Now, on the left, click the Products link under Administration
20. Click the orange button "Upload new Product"
21. Fill in the blanks, and under Version Details choose "CloudFormation". Use the URL of the accountbuilder.yml template you saved earlier. Name it "Account Factory". All other fields do not require a specific value or can be left blank.
22. Press "Review", ensure the data is correct and save
23. The Account Factory Product will show up on your list.
24. Now click the radio button on the left of the Product Name
25. Click "Actions" and select "Add Product to Portfolio". By doing that, you're ensuring the users/roles will have the correct access to the Account Factory. It won't work if you skip this step. This is the last step you perform as an administrator. The Account Factory has been successfully created and users with the correct permissions will be able to use it to create accounts.

Now, open an incognito / private window on your browser. These steps are the ones the end-user will have to do to create accounts:
### Steps for the End User 

1. Log in to the AWS Console using the user ServiceCatalogUser
2. Go to Service Catalog, and click Products List on the left
3. You will see the Account Factory Product you just created. Click on it.
4. On the following screen, you will be able to launch the Account Factory. Click "Launch Product"
5. Pick a name for the new product to be provisioned. An account is a provisioned product, so it's a good idea to use the name of the account as the name of Provisioned Product. Let's call it MyNewAccount Click Next.
6. Fill the form on the next screen.
7. Review the information entered, and Launch.
8. Click "Provisioned Products" to review a list of the accounts created, including this one. Click MyNew Account on this screen
9. This screen will provide you status of the account creation process, as well as a link to the CloudFormation stack used to generate it. You can click on it to check if the creation is working.
10. When the account is created, it will say "Succeeded" and on the same screen information like username, Login URL and Account ID will be provided
11. The owner of the e-mail provided will receive an e-mail from AWS informing that the account is ready. You will have to inform them the Login URL and password (that you provided on the form above) so they can login to the newly created account.
And that's it! Wow that was easy.
