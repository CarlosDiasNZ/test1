aws cloudformation create-stack --stack-name TelstraProto --parameters ParameterKey=DeviceID,ParameterValue=esp8266_140B29 ParameterKey=EndpointAddress,ParameterValue=a3ibzoevjeguz7.iot.ap-southeast-2.amazonaws.com:8883 ParameterKey=GoogleClientID,ParameterValue=2360032414-768n85tiqk5507u2j9agtq3igk19m12f.apps.googleusercontent.com --capabilities CAPABILITY_IAM --template-body file://packaged_template.yaml

# Wait until the stack creation is completed (it may take a few minutes).
aws cloudformation wait stack-create-complete --stack-name my-heater

# Alternatively, you can use the web UI to check the status and read event
# details: https://console.aws.amazon.com/cloudformation/home

# When the stack is created, get the name of the created S3 bucket:
aws cloudformation describe-stacks --stack-name $STACK_NAME

# look for the following:
#  ...
#  {
#      "Description": "Name of the newly created S3 bucket", 
#      "OutputKey": "S3BucketName", 
#      "OutputValue": "S3_BUCKET_NAME"
#  },
#  {
#      "Description": "URL of the s3 bucket", 
#      "OutputKey": "S3BucketWebsite", 
#      "OutputValue": "APP_URL"
#  }
#  ...

S3_BUCKET_NAME=GENERATED_S3_BUCKET_NAME
APP_URL=GENERATED_APP_URL


# $S3_BUCKET_NAME is the name of the bucket, and $APP_URL is the URL at
# which your files can be accessed.
#
# Copy the actual value of "$APP_URL", and then enter it in the Google and/or
# Facebook app settings: For Google: go back to the Google Console, and add the
# URL as an Authorized JavaScript origin.  For Facebook: go back to the app's
# dashboard, click "Settings" in the sidebar, then click "Add Platform" at the
# bottom, select "Website", and enter Site URL.
#
# Then, copy the actual value of "$S3_BUCKET_NAME" (from the describe-stacks
# output), and use it to put two files on the S3 bucket:
aws s3 cp bucket/index.html s3://$S3_BUCKET_NAME --acl public-read
aws s3 cp bucket/index.js s3://$S3_BUCKET_NAME --acl public-read

aws s3 cp bucket/index.html s3://telstraproto-mys3bucket-1nf4pu1l6zyfe --acl public-read

