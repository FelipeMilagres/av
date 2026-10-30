Thanks for the clarification!

I've been reviewing the "LambdaTest Test Manager API documentation" (https://swagger-api-support.lambdatest.com/test_management/index.html), but I couldn't identify the exact API endpoint or the request body structure required to specify the target folder when creating a Test Run.

Could you please provide a complete cURL example showing:

1. The exact API endpoint (HTTP method and URL) used to create a Test Run.
2. The complete JSON request body, including the "folder_id" parameter.
3. Where exactly the "folder_id" should be placed in the request payload.
4. Whether this is the folder ID obtained from the Test Runs folder structure in Test Manager.

For example, I'd like to understand how to include the "folder_id" in the following request:

curl --location --request POST '<API_ENDPOINT>' \
--header 'Authorization: Basic <BASE64_AUTH>' \
--header 'Content-Type: application/json' \
--data '{
  "project_id": "<PROJECT_ID>",
  "folder_id": "<TARGET_FOLDER_ID>"
}'

My goal is to create Test Runs programmatically through our CI/CD pipeline and ensure they are automatically organized in the correct target folders, without requiring any manual intervention through the UI.

Thanks for your help!
