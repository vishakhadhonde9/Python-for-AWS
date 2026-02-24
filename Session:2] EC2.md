# Using Client Method :

      import boto3
      
      # Create EC2 client
      ec2 = boto3.client('ec2', region_name='ap-south-1')
      
      # Create instance
      response = ec2.run_instances(
          ImageId='ami-0abcdef1234567890',   # Replace with valid AMI ID
          InstanceType='t2.micro',
          KeyName='my-keypair',             # Replace with your key pair name
          MinCount=1,
          MaxCount=1
      )
      
      print("Instance Created!")
      print("Instance ID:", response['Instances'][0]['InstanceId'])

## Wait Until Instance is Running:

    waiter = ec2.get_waiter('instance_running')
    waiter.wait(InstanceIds=[instance_id])
    
    print("Instance is now running.")


## Terminate Instance:

        import boto3
        
        REGION = "ap-south-1"
        INSTANCE_ID = "i-1234567890abcdef0"   # Replace with your instance ID
        
        # Create EC2 Client
        
        ec2 = boto3.client("ec2", region_name=REGION)
        
        print("Terminating instance:", INSTANCE_ID)
        
        # Terminate Instance
        ec2.terminate_instances(InstanceIds=[INSTANCE_ID])
        
        # Wait until terminated
        waiter = ec2.get_waiter("instance_terminated")
        waiter.wait(InstanceIds=[INSTANCE_ID])
        
        print("Instance terminated successfully")

## AMI Creation:

      import boto3
      
      ec2 = boto3.client('ec2', region_name='ap-south-1')
      
      response = ec2.create_image(
          InstanceId='i-1234567890abcdef0',
          Name='My-Custom-AMI',
          Description='Created via SDK',
          NoReboot=True
      )
      
      ami_id = response['ImageId']
      print("Creating AMI:", ami_id)
      
      waiter = ec2.get_waiter('image_available')
      waiter.wait(ImageIds=[ami_id])
      
      print("AMI is available:", ami_id)

## KeyPair Creation:

      import boto3
      ec2 = boto3.client('ec2', region_name='ap-south-1')
      
      response = ec2.create_key_pair(KeyName='my-new-key')
      
      private_key = response['KeyMaterial']
      
      # Save private key to file
      with open('my-new-key.pem', 'w') as file:
          file.write(private_key)
      
      print("Key Pair Created Successfully")

## Error Handling: 

      try:
          response = ec2.create_key_pair(KeyName='my-new-key')
      except ec2.exceptions.InvalidKeyPairDuplicate:
          print("Key already exists!")
      
### Delete Key Pair:

    ec2.delete_key_pair(KeyName='my-new-key')




# Using Resource Method:

      import boto3
      
      ec2 = boto3.resource('ec2', region_name='ap-south-1')
      
      instances = ec2.create_instances(
          ImageId='ami-0abcdef1234567890',
          MinCount=1,
          MaxCount=1,
          InstanceType='t2.micro',
          KeyName='my-keypair'
      )
      
      for instance in instances:
          print("Instance ID:", instance.id)

## Terminate Instance: 

      import boto3
      
      ec2 = boto3.resource('ec2', region_name='ap-south-1')
      
      instance = ec2.Instance('i-1234567890abcdef0')
      
      instance.terminate()
      instance.wait_until_terminated()
      
      print("EC2 Instance Deleted")

## KeyPair Creation:


      import boto3
      
      ec2 = boto3.resource('ec2', region_name='ap-south-1')
      
      key_pair = ec2.create_key_pair(KeyName='my-resource-key')
      
      with open('my-resource-key.pem', 'w') as file:
          file.write(key_pair.key_material)
      
      print("Key Created:", key_pair.name)


### Delete key pair:

      key_pair.delete()



## EC2 Boto3 Important Functions

| Function                             | Purpose               |
|--------------------------------------|-----------------------|
| `run_instances()`                    | Launch EC2 instance   |
| `describe_instances()`               | View instance details |
| `terminate_instances()`              | Delete instance       |
| `stop_instances()`                   | Stop instance         |
| `start_instances()`                  | Start instance        |
| `reboot_instances()`                 | Reboot instance       |
| `create_key_pair()`                  | Create SSH key        |
| `create_security_group()`            | Create security group |
| `authorize_security_group_ingress()` | Add inbound rule      |
| `create_image()`                     | Create AMI            |
| `describe_images()`                  | List AMIs             |
