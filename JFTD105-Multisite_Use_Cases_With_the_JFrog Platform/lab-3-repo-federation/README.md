### Prerequisites
## LAB 0 - Configure JFrog CLI

Here we will create the federated repositories setup, using the JFrog CLI and the platform's REST API.

# Method 1 : Use the JFrog CLI to generate an access token, and then call the API using cURL.

## Use CLI to generate an access_token
Create an access token for the user with the swampup@jfrog.com username.
- Run
```
jf rt atc swampup
```
- Run
```
jf rt atc swampup@jfrog.com
```

## Use plain cURL 

 1. Replace {SwampUp JPD host} with valid value
 2. Replace {SwampUp JPD Edge host} with valid value
 3. Replace {SwampUp Second JPD host} with valid value
 4. Replace <TOKEN> with the access-token generated from the previous step
 5. Copy and execute the below command in the terminal
```
curl --location --request PUT 'https://{SwampUp JPD host}.jfrog.io/artifactory/api/repositories/jftd105lab3-maven-dev-local' \
-H "Content-Type: application/json" \
--header 'Authorization: Bearer <TOKEN>' \
--data '{
"key": "jftd105lab3-maven-dev-local",
"rclass": "federated",
"packageType": "maven",
"members": [
{
"url": "https://{SwampUp JPD host}.jfrog.io/artifactory/jftd105lab3-maven-dev-local",
"enabled": true
},
{
"url": "https://{SwampUp EDGE host}.jfrog.io/artifactory/jftd105lab3-maven-dev-local",
"enabled": true
},
{
"url": "https://{SwampUp Second JPD host}.jfrog.io/artifactory/jftd105lab3-maven-dev-local",
"enabled": true
}
]
}'
```
# Method 2 : Use the Jfrog CLI's cURL wrapper
In this scenario, you won't have to generate the access token, as it will use your existing configuration.

## Make sure the JFrog CLI is configured to use your main JPD instance
- Run
```
jf c use swampup
```
## Then create the federated repositories using the `jf rt curl` command 
 
 1. Replace {SwampUp JPD host} with valid value
 2. Replace {SwampUp JPD Edge host} with valid value
 3. Replace {SwampUp Second JPD host} with valid value
```
jf rt curl -XPUT /api/repositories/jftd105lab3-maven-dev-local -H "Content-Type: application/json" --data '{ "key": "jftd105lab3-maven-dev-local", "rclass": "federated", "packageType": "maven", "members": [ { "url": "https://{SwampUp JPD host}.jfrog.io//artifactory/jftd105lab3-maven-dev-local", "enabled": true }, { "url": "https://{SwampUp Edge host}/artifactory/jftd105lab3-maven-dev-local", "enabled": true }, { "url": "https://{SwampUp Second JPD host}.jfrog.io/artifactory/jftd105lab3-maven-dev-local", "enabled": true } ] }'
```

# RUN the Helper SCRIPT [Optional]
- Run 
```
sh lab_3_federation_rescue.sh
```
