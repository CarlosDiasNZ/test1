google api

Telstra_Prot 

client id :
2360032414-768n85tiqk5507u2j9agtq3igk19m12f.apps.googleusercontent.com

Vh-IjgRj1y4O-WnVqDI3ZT7d


aws cloudformation create-stack --stack-name Telstra_stack
    --parameters 
        ParameterKey=DeviceID,ParameterValue=esp8266_140B29
        ParameterKey=EndpointAddress,ParameterValue=a3ibzoevjeguz7.iot.ap-southeast-2.amazonaws.com:8883
        ParameterKey=GoogleClientID,ParameterValue=2360032414-768n85tiqk5507u2j9agtq3igk19m12f.apps.googleusercontent.com
    --capabilities CAPABILITY_IAM
    --template-body file://packaged_template.yaml

aws cloudformation create-stack --stack-name TelstraPrototype1
    --parameters
      ParameterKey=DeviceID,ParameterValue=esp8266_F6604C
      ParameterKey=EndpointAddress,ParameterValue=a3ibzoevjeguz7.iot.ap-southeast-2.amazonaws.com:8883
      ParameterKey=GoogleClientID,ParameterValue=2360032414-of2agbcd0umeo9gr7vq1evd6000asm2c.apps.googleusercontent.com 
    --capabilities CAPABILITY_IAM
    --template-body file://packaged_template.yaml

aws cloudformation create-stack --stack-name TelstraPrototype1 --parameters ParameterKey=DeviceID,ParameterValue=esp8266_F6604C ParameterKey=EndpointAddress,ParameterValue=a3ibzoevjeguz7.iot.ap-southeast-2.amazonaws.com:8883 ParameterKey=GoogleClientID,ParameterValue=2360032414-of2agbcd0umeo9gr7vq1evd6000asm2c.apps.googleusercontent.com  --capabilities CAPABILITY_IAM --template-body file://packaged_template.yaml




{
  "aws": {
    "greengrass": {
      "enable": false,
      "reconnect_timeout_max": 60,
      "reconnect_timeout_min": 2
    },
    "thing_name": ""
  },
  "conf_acl": "*",
  "debug": {
    "factory_reset_gpio": -1,
    "filter": "",
    "level": 2,
    "mbedtls_level": 0,
    "mg_mgr_hexdump_file": "",
    "stderr_topic": "",
    "stderr_uart": 0,
    "stdout_topic": "",
    "std
