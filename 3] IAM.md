# 1] IAM User Creation-
## Using Client:

      import boto3
      
      USER_NAME = "simple-console-user"
      PASSWORD = "StrongPassword@123"
      
      # Create IAM client
      iam = boto3.client("iam")
      
      # Create IAM User
      response = iam.create_user(
          UserName=USER_NAME
      )
      
      print("IAM User Created Successfully")
      
      Give Console Access (Login Profile)
      iam.create_login_profile(
          UserName=USER_NAME,
          Password=PASSWORD,
          PasswordResetRequired=True
      )
      
      print("Console Access Enabled")

#### Using try catch for error handling:

      import boto3
      from botocore.exceptions import ClientError
      
      USER_NAME = "demo-console-user"
      PASSWORD = "StrongPassword@123"   # Must meet AWS password policy
      FORCE_PASSWORD_RESET = True
      
      iam = boto3.client("iam")
      
      try:
          response = iam.create_user(
              UserName=USER_NAME
          )
          print(f"IAM User '{USER_NAME}' created successfully.")
      
          iam.create_login_profile(
              UserName=USER_NAME,
              Password=PASSWORD,
              PasswordResetRequired=FORCE_PASSWORD_RESET
          )
      
          print("Console access enabled successfully.")
          print("User must change password at first login:", FORCE_PASSWORD_RESET)
      
          print("Policy attached successfully.")
      
          print("\n===== USER DETAILS =====")
          print("Username:", USER_NAME)
          print("Login URL: https://<your-account-id>.signin.aws.amazon.com/console")
      
      except ClientError as e:
          print("Error occurred:", e)
