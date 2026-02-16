# Boto3 -
- Boto3 is the official AWS SDK (Software Development Kit) for Python.
- It allows you to connect and control AWS services using Python code.
- Because instead of manually clicking in AWS Console, we can:
   - Automate tasks
   - Write scripts
   - Use it inside AWS Lambda
   - Build DevOps automation
   - Create infrastructure tools.
 
# Main Components of Boto3:
- Boto3 mainly works with:
1. Session
2. Client
3. Resource

# 1] Session -
- A Session is the starting point for working with AWS in boto3.
- It manages authentication process.

## Types of Sessions -
### Default Session:
- Created automatically when you call boto3.client() or boto3.resource() without a predefined session.
- It uses the credentials found in your default environment or local ~/.aws/ files.

import boto3
var = boto3.client('service')

  
### Custom Session:
- Manually instantiated via boto3.Session(). 
- This is recommended for managing multiple AWS accounts, regions, or configurations in a single script.


      import boto3

      session = boto3.Session(
          aws_access_key_id="YOUR_KEY",
          aws_secret_access_key="YOUR_SECRET",
          region_name="ap-south-1"
      )
      

