# Language Translation using Amazon Lex

## Description
This project gives hands-on knowledge on using different AWS services to build a langauge translation chatbot. The chatbot will give the output translation.

## Services used
* Amazon Lex: Is used to build chatbot and define conversation flow.
* AWS Lambda: Used to get recommendations using third party API.
* AWS IAM: Ensure secure access for user permissions.
* Amazon Translate: Is used to translate sentence according to input langauge.

## Creating an Empty Chatbot
1. Search 'Amazon Lex' in AWS Manageemnt Console and click on 'Create Bot'.
2. The suitable option for this project is to choose 'Create a blank bot' method.
3. Provide a suitable name to the chatbot.
4. And for IAM role, select 'Create role with basic Amazon Lex Permission' which will automatically create a role.
5. The user can choose the langauge which the bot can interact and also choose between different voice interaction modules.
6. Keep the Intent classification confidence score threshols as 'Default' and click Done. The empty chatbot has been created and will lead on the intent page where the user can work on the conversational flow of the chatbot.

## Specify Intents and Slots
 * Amazon Lex terminologies
- Intent: The specific pupose of what user intends to do.
- Utterence: The input given by the user.
- Slots: Specific parts of information or variables within user;s utterence that needs to be extracted by the system.
- Fulfulment: Action which the system takes based on user's intent and information provided in the slots.

 *For example, foe burger ordering chatbot. The intent reflects what theuser wants like ordering or just to check an order. Utterances are what users would like to customize their order. Slots are specific details in utterrances like extra cheese or customizing the toppings. Fulfillment is the chatbot's response, confirming the order and providing information.*

1. In the Intent details, fill in the name and description. Amazon Lex will try to understand the user input by aligning the input with the given utterances.
2. Go to slots option and click on 'Add Slot', choose the langauge in which the text needs to be translated as a slot. Now create the Slot type and Save Intent.
3. Click on back to the Intents list and navigate to slot type, to add Slot type. Choose 'Add blank slot type' and give a name to the slot type (for this project, its langauge).
4. Add some langauges as Slot type values ssimilar to below picture. And click on Save slot type. Navigate to the Intents to use this slot type for this project's slot.
5. Click on Add slotand choose the type as 'langauge' which was previously made. Write down the prompt where the chatbot asks for userchouce for langauge translation. And click on Add.
6. Create another slot 'text' which takes the text that has to be translated as input. Choose 'AMAZON.FreeFormInput' as the type option and enter the promptthat has to be translated. And click Add. Als add an initial response to the initial intent as feedback message.

## Specify Fulfillemnt
1. Fulfillment runs the Lambda function to fulfill the intent and informs users about its status once it is complete.
2. Write suitable prompt on successful fulfillment and in case of failure.
3. Click 'Advanced Options' and check 'Use a Lambda function for fulfillment' and select Update Options. Also provide a Closing message after completion of the intent.
4. Click on Save Intent.

## Creating IAM Role
1. Navigate to 'IAM Role' from your AWS Console.
2. Click on 'Create Role' and this will be used for the Lambda function and access Amazon Translate.
3. Choose AWS service as trusted entity and Lambda as use case. Click Next.
4. Attach the following policy: 'TranslateFullAccess', 'AWSLambdaBasicExecutionRole' and click Next. Enter a suitable name and description for the role. This role will be used for the Lambda function permission.

## Creating Lambda Function
1. Look up 'Lambda Function' in the AWS Console and click on Create Function by providing a suitable name.
2. Select the runtime as 'Python 3.12' and choose the previously created role by selecting 'Default Execution Role' and keep the values as default and select Create Function.
3. The program is provided as 'index.py' and 'boto3' is used to interact with AWS services through code.
4. Click Deploy.

## Testing Lambda Function
1. Configure the Test Event.
2. Provide a suitable name for the test event and keep Event JSON as below.
```Python
{
  "sessionState": {
    "intent": {
      "name": "TranslateIntent",
      "slots": {
        "text": {
          "value": {
            "interpretedValue": "Hello",
            "originalValue": "Hello"
          }
        },
        "language": {
          "value": {
            "interpretedValue": "French",
            "originalValue": "French"
          }
        }
      }
    }
  }
}
```
The main reason for thi format is because Lambda function gets input from Amazon Lex as the exact format.
3. Save the test event and click on TEst again to invoke the event. The function gives an output in JSON format which is required format input for Amazon Lex.

## Testing the chatbot
1. Navigate to the Intent page of previously created Chatbot, before usin git specify the Lambda function ti be used by Lex.
2. Click on settings option and choose 'Source of Lambda function' as previous created function.
3. Test the chatbot. I have attached the screen shots from my chatbot.

## Key Highlights
* Integration of AWS Services: Amazon Lex, AWS Lambda and AWS IAM to create a cohesive solution.
* Chatbot Development: Gained knowledge of building a conversational interface with AWS services.
+ Learned how to configure intents, slots and utterences for specific use cases.
+ Implemented fulfillment logic using AWS Lambda to provide dynamic responses.
* Serverless Computing: Used AWS Lambda to run backend logic without managing servers by showcasing benefits of serverless architecture for scalability and cost efficiency.
* Secure Access Management: Implemented IAM policies for granting precise access to AWS services by ensuring security.
* Langauge Translation: Explored real time langauge translation and demonstrated how user can drive langauge specific processing and response. 
