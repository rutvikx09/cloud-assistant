AWS Cloud Assistant — AI-Powered Cloud Assistant

An AI-powered cloud assistant built to explore the integration of Artificial Intelligence, AWS serverless services, and Python. This project aims to provide an interactive chat interface that processes user questions, generates AI-powered responses, and stores conversation history.

🚀 My First AI Agent Project

I'm building this project as part of my hands-on learning journey in AI, AWS Cloud Computing, and DevOps.

📌 Project Overview

AWS Cloud Assistant is designed to connect a web-based chat interface with an AWS backend powered by serverless technologies and Amazon Bedrock.

Users can submit questions through the frontend, which sends requests to an AWS backend. AWS Lambda processes the request, communicates with Amazon Bedrock to generate an AI response, and stores conversation data in Amazon DynamoDB.

🎯 Project Goals
Build an interactive AI chat interface.
Integrate a frontend with AWS backend services.
Use Amazon Bedrock for AI-powered responses.
Process requests using AWS Lambda and Python.
Store conversation history in Amazon DynamoDB.
Learn serverless architecture and AWS service integration.
🏗️ Architecture
                  ┌──────────────────────┐
                  │      User / Browser  │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │     Frontend UI      │
                  │    HTML / JavaScript │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │    Amazon API        │
                  │    Gateway           │
                  │      POST /ask       │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │     AWS Lambda       │
                  │    Python + Boto3    │
                  └──────────┬───────────┘
                             │
                    ┌────────┴─────────┐
                    │                  │
                    ▼                  ▼
          ┌─────────────────┐  ┌─────────────────┐
          │ Amazon Bedrock  │  │ Amazon DynamoDB │
          │ AI Responses    │  │ Chat History    │
          └─────────────────┘  └─────────────────┘
🔄 Request Flow
The user enters a question in the web interface.
The frontend sends a POST request to the API endpoint.
Amazon API Gateway forwards the request to AWS Lambda.
Lambda processes the request using Python and Boto3.
Amazon Bedrock generates an AI-powered response.
Amazon DynamoDB stores the conversation, if chat persistence is enabled.
Lambda returns a JSON response to the frontend.
The frontend displays the response to the user.
🛠️ AWS Services and Technologies
Technology	Purpose
HTML, CSS, JavaScript	Frontend chat interface
Python	Backend application logic
AWS Lambda	Serverless backend execution
Amazon API Gateway	HTTP API endpoint
Amazon Bedrock	AI-powered response generation
Amazon DynamoDB	Conversation history storage
AWS IAM	Access control and permissions
Boto3	Python SDK for AWS services
Git and GitHub	Version control and project hosting

The table describes the intended architecture. Only list services as implemented after you have successfully configured and tested them.

✨ Key Features
💬 Interactive Chat Interface: A simple, user-friendly interface for submitting questions.
🤖 AI-Powered Responses: Designed to use Amazon Bedrock to generate responses.
⚡ Serverless Backend: Uses AWS Lambda to process requests without managing servers.
🔗 API Integration: Connects the frontend to the AWS backend through an HTTP API.
💾 Conversation Persistence: Designed to store chat history in DynamoDB.
🔐 AWS IAM Permissions: Supports controlled access to AWS resources.
📈 Extensible Architecture: Can be expanded with authentication, monitoring, and additional AI capabilities.
📂 Project Structure

The exact structure may vary depending on your implementation.

aws-cloud-assistant/
│
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── script.js
│
├── backend/
│   └── lambda_function.py
│
├── architecture/
│   └── aws-architecture.png
│
├── screenshots/
│   ├── frontend-ui.png
│   ├── lambda-test.png
│   └── dynamodb-history.png
│
├── .gitignore
└── README.md
⚙️ Prerequisites

Before setting up the project, make sure you have:

An AWS account.
Basic knowledge of Python.
Python 3.x installed locally if testing the backend locally.
AWS CLI installed and configured if using it for deployment.
An IAM role or credentials with appropriate permissions.
Access to an Amazon Bedrock model in your selected AWS Region.
An API Gateway endpoint connected to your Lambda function.
An Amazon DynamoDB table if conversation storage is enabled.

Recommended AWS Region: ap-south-1 (Mumbai), provided the required Bedrock model is available there.

🚀 Setup and Deployment
Step 1: Clone the Repository
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd aws-cloud-assistant

Replace <YOUR_GITHUB_REPOSITORY_URL> with your actual repository URL.

Step 2: Configure Amazon Bedrock
Open the AWS Management Console.
Navigate to Amazon Bedrock.
Select a supported model in your chosen Region.
Confirm that your account has permission to invoke the model.
Note the model ID for your Lambda configuration.

Model availability and access requirements vary by Region and model.

Step 3: Create the DynamoDB Table

Create a table named:

CloudAssistantConversations

A suggested key configuration is:

Setting	Value
Partition key	userId — String
Sort key	timestamp — String

Use this schema only if it matches the DynamoDB operations in your Lambda code.

Step 4: Configure AWS Lambda

Create a Lambda function using Python.

Configure the required environment variables:

TABLE_NAME=CloudAssistantConversations
MODEL_ID=<YOUR_BEDROCK_MODEL_ID>

The Lambda execution role should have only the permissions required by the application, such as:

Permission to invoke the selected Bedrock model.
Permission to write conversation records to DynamoDB.
Permission to query DynamoDB if retrieving chat history.
Permission to write logs to Amazon CloudWatch.

Avoid placing AWS access keys directly in your source code.

Step 5: Create the API Endpoint

In Amazon API Gateway:

Create an HTTP API.
Integrate it with your Lambda function.
Configure the POST /ask route.
Configure CORS for your frontend origin.
Deploy the API.
Copy the generated API endpoint.

Your frontend will send requests to the deployed endpoint.

Step 6: Connect the Frontend

Configure your frontend with the API endpoint.

For a Vite application, you can use an environment variable:

VITE_CLOUD_ASSISTANT_API_URL=https://YOUR_API_ID.execute-api.ap-south-1.amazonaws.com/ask

Replace the example URL with your actual deployed endpoint.

Restart the frontend development server after updating the environment variable.

Security note: Frontend environment variables are visible to users in the browser. Never store AWS credentials, secret keys, or other private secrets in them.

Step 7: Test the Application

Verify each component independently:

The frontend loads successfully.

API Gateway receives the request.

Lambda executes without errors.

Amazon Bedrock returns a response.

The frontend displays the complete response.

DynamoDB stores the conversation if persistence is implemented.

Errors are handled gracefully.

🔐 Security Considerations

Security is an important part of building cloud applications.

Follow the principle of least privilege when configuring IAM roles.
Never commit AWS access keys, secret keys, or passwords to GitHub.
Configure API Gateway CORS for trusted frontend origins.
Add authentication and authorization before exposing a production application.
Validate user input and handle errors safely.
Review AWS service quotas and costs before deploying.
Use CloudWatch logs to troubleshoot errors without exposing sensitive data.
💰 Cost Considerations

This project uses AWS services that may incur charges.

Potential cost sources include:

Amazon Bedrock model usage.
AWS Lambda invocations and execution duration.
Amazon API Gateway requests.
Amazon DynamoDB storage and operations.
Amazon CloudWatch logs.

Actual costs depend on usage, model pricing, Region, and configuration. Check the current AWS pricing pages and monitor your AWS Billing dashboard before running workloads.

🚧 Future Improvements

The following are potential enhancements for future versions:

Add secure user authentication.

Retrieve previous conversations from DynamoDB.

Add a conversation sidebar with recent chats.

Improve response formatting and error handling.

Add streaming AI responses.

Integrate Amazon CloudWatch monitoring and alarms.

Add automated tests.

Create a CI/CD pipeline using GitHub Actions.

Provision infrastructure using Terraform.

Add usage limits and safeguards against excessive requests.

📚 What I'm Learning

Through this project, I'm exploring:

How AI applications interact with cloud infrastructure.
How to integrate Amazon Bedrock with Python.
How serverless applications work on AWS.
How API Gateway connects frontend applications to backend services.
How DynamoDB can persist application data.
How IAM permissions help secure cloud resources.
How to structure, test, and improve a real-world cloud project.
👨‍💻 About Me

I'm a postgraduate student interested in Cloud Computing, AWS, DevOps, and AI. I'm building hands-on projects to strengthen my technical skills and understand how modern cloud applications are designed and deployed.

This is my first AI agent project, and I plan to continue improving it as I learn.

Connect With Me
GitHub: https://github.com/rutvikx09
LinkedIn: https://www.linkedin.com/in/rutvik-ingle-248905240/
⭐ Support

If you find this project interesting, consider giving the repository a star ⭐ and sharing suggestions for improvement.# cloud-assistant
