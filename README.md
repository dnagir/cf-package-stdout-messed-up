## aws cloudformation package - stdout bug repro

This demonstrates the problem with the `package` command.

It outputs the `Uploading to 758969f492ff840d3480428add7047dc  188 / 188.0  (100.00%)` and as such can no longer be used
with the `aws cloudformation deploy` command.


Run `./package your-test-bucket-123`

This produces:

```
updating: code (stored 0%)
Generating CloudFormation package:
Uploading to 242ae609bc1d294683119c544172880c  188 / 188.0  (100.00%)
Description: Example
Resources:
  ExampleLambda:
    Properties:
      Code:
        S3Bucket: test-dima
        S3Key: 242ae609bc1d294683119c544172880c
      FunctionName: exampleFunction
      Handler: hello.handler
```

The expected output MUST NOT include the `Uploading to ...` in the STDOUT of the package command.


## Environment

- macOS
- `aws --version #=> aws-cli/1.16.20 Python/3.7.0 Darwin/17.7.0 botocore/1.12.10`
