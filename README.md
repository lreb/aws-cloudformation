aws cloudformation deploy --template template.json --stack-name lreb-template

 aws cloudformation describe-stack-events --stack-name lreb-template

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