
# Scripts - Tesltra IoT Prototype

Below, a description how the application was created. <br> 
These commands can be easily translated for any platform (Azure, Cumulocity, AWS) standalone or integrated in a provisioning/deployment stack (e.g. Ansible, CHEF, SaltStack, Cloudformation)   

## Device Details

Get the device ID DEVICE_ID=esp8266_140B29


## AWS Script Components

Scripts to fill the gaps in the standard AWS templates:

npm --prefix ../helpers/cloudformation-helpers install ../helpers/cloudformation-helpers

Also need to create a separate S3 bucket for this scripts functions:

aws s3 mb s3://prot-helper


Get the endpoint address for the AWS account to provide it as
a parameter for the stack:

AWS_IOT_ENDPOINT=(aws iot describe-endpoint --output text)

## Package the Template 
Packaging includes copying source code of the helper functions from the local repository to the s3 bucket created above, and adjusting the template appropriately. It's all done in one step:

aws cloudformation package 
    --template-file Telstra_iot_template.yaml <br>
    --s3-bucket prot-helper <br>
    --output-template-file packaged_template.yaml <br>

## Create and Instantiate the AWS Stack

STACK_NAME=telstraproto

The command above has created a new template file: packaged-template.yaml. 
Now, instantiate AWS stack using this template.  

aws cloudformation create-stack 
    --stack-name STACK_NAME<br> 
    --parameters<br>
        ParameterKey=DeviceID,ParameterValue=DEVICE_ID <br>
        ParameterKey=EndpointAddress,ParameterValue=AWS_IOT_ENDPOINT <br> 
    --capabilities CAPABILITY_IAM <br>
    --template-body file://packaged_template.yaml<br> 

Use the web UI to check the status and read event details:<br>
 (https://console.aws.amazon.com/cloudformation/home)

Get the name of the created S3 bucket:
aws cloudformation describe-stacks --stack-name STACK_NAME

Get the following parameters:

S3_BUCKET_NAME=GENERATED_S3_BUCKET_NAME
APP_URL=GENERATED_APP_URL


## Configure the Web Interface
Copy the actual value of "S3_BUCKET_NAME", and use it to put two files on the S3 bucket:

aws s3 cp bucket/index.html s3://S3_BUCKET_NAME --acl public-read<br>
aws s3 cp bucket/index.js s3://S3_BUCKET_NAME --acl public-read<br>
aws s3 cp aws-cognito-sdk.min.js s3://S3_BUCKET_NAME --acl public-read<br>
aws s3 cp amazon-cognito-identity.min.js s3://S3_BUCKET_NAME --acl public-read<br>


## Provisioning the Device 

After the platform side configutarion, some details must be provisioned into the device.<br>


## Navigate

Go to APP_URL or http://orgsensor.com

