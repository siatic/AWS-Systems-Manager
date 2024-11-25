Password saving Application using **AWS Parameter Store**


1. Head to the AWS Console
   
2. Search for a Systems Manager Service

3. Under the Application Management, click on Parameter Store

4. We will create 4 parameters of which 2 will be encrypted

5. Click on Create Parameter

6. A) Parameter Name: /demo-app/dev/db-url
      Parameter Type: String
      Parameter Value: dev.database.demoapp.com:3306

   B) Parameter Name: /demo-app/dev/db-password
      Parameter Type: SecureString
      Parameter Value: thisisthedevpassword

      - This is the First encrypted parameter

   C) Parameter Name: /demo-app/prod/db-url
      Parameter Type: String
      Parameter Value: prod.database.demoapp.com:3306

   D) Parameter Name: /demo-app/prod/db-password
      Parameter Type: SecureString
      Parameter Value: thisistheprodpassword

      - This is the Second encrypted parameter
  
7. To view the parameter values, We will use CLI (Command Line Interface)

8. Configure your AWS over CLI:
```
   aws configure
```

9. Enter Access Key, Secret Access Key, Region-name and Output Format

10. Run the following command to view the parameter values: 
``` 
   aws ssm get-parameters --names /demo-app/dev/db-url /demo-app/dev/db-password
```

11. To view the decrypted parameter values, run the command:
```
   aws ssm get-parameters --names /demo-app/dev/db-url /demo-app/dev/db-password --with-decryption
```

12. We can get all the parameters value which are stored in a tree like structure by the following command:
```
   aws ssm get-parameters-by-path --path /demo-app/dev/
```

13. To view all the parameters, we can use the root path by following command:
```
   aws ssm get-parameters-by-path --path /demo-app/ --recursive
```

14. To view the decrypted values of encrypted parameters, we can use the following command:
```
   aws ssm get-parameters-by-path --path /demo-app/ --recursive –-with-decryption
```
