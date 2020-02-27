aws cloudformation deploy --template template.json --stack-name lreb-template

 aws cloudformation describe-stack-events --stack-name lreb-template


 aws cloudformation deploy --template common-stack.json --stack-name lreb --capabilities CAPABILITY_NAMED_IAM

## full exmaple

aws cloudformation deploy --template-file /path_to_template/template.json --stack-name my-new-stack --parameter-overrides Key1=Value1 Key2=Value2 --tags Key1=Value1 Key2=Value2


,
      "MockMethod": {
        "Type": "AWS::ApiGateway::Method",
        "Properties": {
            "RestApiId": {
                "Ref": "apiGateway"
            },
            "ResourceId": {
                "Fn::GetAtt": [
                    "apiGateway",
                    "RootResourceId"
                ]
            },
            "AuthorizationType": "NONE",
            "Integration": {
                "Type": "HTTP",
                "IntegrationHttpMethod":"ANY" 
            }
        }
      },
      "ProxyResource": {
        "Type": "AWS::ApiGateway::Resource",
        "Properties": {
            "RestApiId": {
                "Ref": "apiGateway"
            },
            "ParentId": {
                "Fn::GetAtt": [
                    "apiGateway",
                    "RootResourceId"
                ]
            },
            "PathPart": "{proxy+}"
        }
      },
      "ProxyResourceANY": {
        "Type": "AWS::ApiGateway::Method",
        "Properties": {
            "RestApiId": {
                "Ref": "apiGateway"
            },
            "ResourceId": {
                "Ref": "ProxyResource"
            },
            "HttpMethod": "ANY",
            "AuthorizationType": "NONE",
            "Integration": {
                "Type": "AWS_PROXY",
                "IntegrationHttpMethod": "POST"
            }
        }
      }



      "StackMain": {
    "Type" : "AWS::CloudFormation::Stack",
    "Properties" : {
        "Tags":[
            { "Key": "Name", "Value": {
                "Fn::Sub" : [ "${Project}-${ServPrefix}-${AccountId}-${ProjectNumber}", { 
                    "Project":  { "Ref": "projectName" },
                    "ServPrefix":  { "Fn::Select" : [ "6", {"Ref" : "prefixListName"} ] }, 
                    "AccountId": { "Ref" : "AWS::AccountId" },
                    "ProjectNumber": { "Ref": "projectNumber" }
                    } 
                ]
            } },
            { "Key": "Project", "Value": {"Fn::Sub" : [ "${Project}", { "Project":  { "Ref": "projectName" } } ]} }
        ]
      }
},




"Outputs" : {
    "s3Bucket1" : {
      "Description" : "The ID of the s3",
      "Value" : { "Ref" : "s3Bucket" },
      "Export" : {
        "Name" : {  "Fn::Sub": ["${StackName}-${TopicARN}-${TopicRegion}-${TopicUrlSuffix}", {
            "StackName": { "Ref": "AWS::StackName" },
            "TopicARN": { "Ref" : "AWS::NotificationARNs" },
            "TopicRegion": { "Ref": "AWS::Region" },
            "TopicUrlSuffix": { "Ref": "AWS::URLSuffix" }
        } ] }
      }
    }
  }


"lambdaExecutionRole1": {
           "Type": "AWS::IAM::Role",
           "Properties": {
              "RoleName" : "rolelambda",
              "AssumeRolePolicyDocument": { 
                "Version": "2012-10-17",
                "Statement": [
                    {
                        "Effect": "Allow",
                        "Principal": {
                            "Service": "lambda.amazonaws.com"
                        },
                        "Action": "sts:AssumeRole"
                    }
                ]
               },
              "Path": "/",
              "Policies": [ "" ]
           }
        }


   