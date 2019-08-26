# Aws Notes and more

* If you need to store a parameter using put-parameter in ssm and the value is url starting with http or https you need to edit ~/.aws/config and add the following line cli_follow_urlparam = false
or else you will not get the url in the ssm

* How to secure links to s3 files https://medium.com/runascloud/creating-a-secure-url-with-an-expiration-date-from-s3-11c7b2fe7206

* Serverless warmup links:
https://medium.com/clarityhub/warm-up-those-slow-startup-times-8f78ad65517a
https://www.youtube.com/watch?v=1j7USsviHpg
http://d0.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf
https://www.awsgeek.com/
https://github.com/sdras/awesome-actions
https://blog.epsagon.com/how-to-handle-aws-lambda-errors-like-a-pro

node_modules/serverless/bin/serverless offline --skipCacheInvalidation --port 3001
SLS_DEBUG=*

* For the slack record… if cognito user / service pool change the public key of the pool is at this address:
https://cognito-idp.{region}.amazonaws.com/{userPoolId}/.well-known/jwks.json

* Localization editor: https://poeditor.com/

* Celndar interaction:
https://github.com/txwkx/book-room
https://github.com/sivadass/react-meeting-room

* how to store / retrive private key in ssm ?
store:
how to save keyfile.key.pub containg the public key in ssm
aws ssm put-parameter --name "$SSM_PATH_PUBLIC_KEY" --type SecureString --overwrite --region $AWS_REGION --value "`cat keyfile.key.pub | base64`"

serverless.yml
provider:
  environment:
     MY_PUBLIC_KEY_ENCODED: ${ssm:/${self:provider.stage}/......./PUBLIC_KEY~true}

retrive in the lambda code:
MY_PUBLIC_KEY_ENCODED is env variable containing the key
const MY_PUBLIC_KEY = Buffer.from(MY_PUBLIC_KEY_ENCODED, 'base64').toString();

