# AWS-Boto3-Practice
Playing around w/ Boto3 

# What is Boto3?
-SDK for AWS.    
-Connects Python scripts to your AWS resources/apps/tools, a CRUD app for AWS resources.    

# What is AWS S3?
-'Simple Storage Service'.    
-Cloud directory to hold objects, basically allows us to store files in folders.

# Generate s3 instance
s3 = boto3.client('s3', 
                  region='us-west-1', 
                  aws_access_key_id=AWS_KEY_ID, 
                  aws_secret_access_key=AWS_SECRET)

buckets = s3.list_buckets()
print(buckets)

---------------------------------------------------------------------------------------------------------------------------

# Generate sns instance 
sns = boto3.client('sns', 
                    region='us-west-1', 
                    aws_access_key_id=AWS_KEY_ID, 
                    aws_secret_access_key=AWS_SECRET)
topics = sns.list_topics()
print(topics)

--------------------------------------------------------------------------------------------------------------------------
# S3
**Simple storage service**

**Basic Idea:**     
    Buckets: Folders that contain objects     
    Objects: Files    

**Specifics:**     
    Buckets: Own permission policies, website storage, generate self-logs, contain objects!
    
# Create a Bucket

```Python3
import boto3

s3 = boto3.client('s3', 
                  region='us-west-1', 
                  aws_access_key_id=AWS_KEY_ID, 
                  aws_secret_access_key=AWS_SECRET)
```
# Use s3 instance to create a new bucket, parameter Bucket='bucket name'

```Python3
new_bucket = s3.create_bucket(Bucket='bucket_name')
```
# Listing Buckets

```Python3
bucket_response = s3.list_buckets()
for each_bucket in response['Buckets']:
    print(f'Bucket: {each_bucket['Name']}')
```


# Deleting Buckets 
s3.delete_bucket(Bucket='name_of_bucket_you_want_to_delete')

# Compare and contrast buckets and objects

**Buckets**:     
              Has a **Name**, which is a string             
              Unique name in all of s3    
              Contains many objects    
             
**Objects**:     
              Has a **Key**    
              the Name is the full path from the bucket root    
              Unique Key in each bucket    
              Can only belong to one bucket    
# Uploading Files(Objects) to S3 Bucket


`s3.upload_file(Filename='', Bucket='', Key='')`
`Params`: Filename - name of file, String
        Bucket - Name of Bucket, String
        Key - Name of Object in S3

```Python
    s3.upload_file(Filename='Filename', Bucket='Your_Bucket', Key='Your_Object')
```

# Object Metadata
## Get object metadata and print it

```Python
response = s3.head_object(Bucket='gid-staging', 
                          Key='2019/final_report_01_01.csv')

#View all MetaData Tags
print(response)

#Print the size of the uploaded object
print(response['ContentLength'])
```
# Deleting Buckets
Specify the bucket name to remove the bucket

```Python
s3.delete_bucket(Bucket='Name')

```
# Deleting Objects
To delete objects contained within a particular bucket, you specify the bucket and then the key of the associated object. 
```Python
s3.delete_bucket(Bucket='Name', Key='Key')
```

# Listing Objects
```Python
s3.list_objects(Bucket='Bucket_name')
```
# Filter Objects Using Prefix
```Python
s3.list_objects(Bucket='Bucket_name', Prefix='Pattern')
```
