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
      

# 2] Client -
- Clients provide a direct, low-level 1:1 mapping to AWS API actions.
- It directly talks to AWS API
- It returns raw dictionary response (JSON format).

        client = boto3.client('service_name')

        e.g.: s3 = boto3.client('s3')
              ec2 = boto3.client('ec2')

## Response -
- response is a Python dictionary returned by AWS.

      ec2 = boto3.client('ec2')
      response = ec2.describe_instances()


# 3] Resource -
- The resource interface in Boto3 provides a high-level, object-oriented API that simplifies interaction with AWS services.
- It makes AWS interaction more Pythonic, readable.
- You interact with AWS resources as Python objects.
- Automatic Pagination: When AWS returns large data, it sends results in multiple pages instead of all at once.

         ec2 = boto3.resource('ec2')
         
         for instance in ec2.instances.all():
             print(instance.id)

## Client vs Resource in Boto3

| Feature                    | Client     | Resource       |
|----------------------------|------------|----------------|
| Level                      | Low-level  | High-level     |
| Returns                    | Dictionary | Python objects |
| Parsing                    | Manual     | Easy           |
| Available for all services | Yes        | No             |

 

