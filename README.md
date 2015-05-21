Question App


Demo
=====
https://jboss7-undersun.rhcloud.com/question/welcome

How It Should Work
======

1. Create a default page i.e. start.html
2. Create the angular script on start.html 

The first angular ajax script should be calling "getFirstQuestion"

Below is the POST call to this url.

https://qa1-mindelements.rhcloud.com/question-web/rest/questions/getFirstQuestion/{memberNumber}/inputFile

There are two inputs to be passed on this ajax call

a. memberNumber should be passed with random number (8 numbers)
b. mulipart/encoded file upload. The field name is "file"

Below is the sample json response

```
{
  "question": "Which of the following is an example of a vulnerability?",
  "selection": {
    "d": "Unauthorized access to confidential resources",
    "b": "Misconfigured server",
    "c": "Virus infection",
    "a": "Denial of service attack"
  },
  "questionNumber": 8,
  "sessionId": "4a030e93-504f-4ff8-9e2c-420fccd5dff9",
  "answer": null,
  "explanation": null,
  "questionBucketDetails": {
    "questionNumber": 8,
    "totalQuestionRunningValue": 0,
    "totalQuestion": 12,
    "numberOfSetsDone": 1,
    "questionSetRunningValue": 0,
    "questionSetTotalValue": 8
  },
  "status": "QUESTION_AVAILABLE",
  "questionType": "single"
}
```
Based on quesiton type, you will create the answer selection as radio button or checkbox. If question type value is single, then it is a radio button. If multi-select, it should be checkbox.

You should layout the json response above like shown below:

Question: sample question
() Potato
() Apple
() Guava

For multi-select, it should be a check box


Question: sample question
[] Potato
[] Apple
[] Guava


On the bottom of the question and answer selection, you will have two button.

[Check Answer] [Next Question]








Main page

* https://qa1-mindelements.rhcloud.com/question-web/

Initial REST POST call with file attachement

POST getFirstQuestion

* https://qa1-mindelements.rhcloud.com/question-web/rest/questions/getFirstQuestion/{memberNumber}/inputFile

Sample
* https://qa1-mindelements.rhcloud.com/question-web/rest/questions/getFirstQuestion/1111/inputFile

```
{"question":"What is ABC related for?","selection":{"d":"TV","b":"Space","c":"Travel","a":"Food"},"questionNumber":2,"sessionId":"d26fc144-0468-4f43-bfd5-8c19617e0bfb","answer":null,"explanation":null,"questionBucketDetails":{"questionNumber":2,"totalQuestionRunningValue":0,"totalQuestion":10,"numberOfSetsDone":1,"questionSetRunningValue":0,"questionSetTotalValue":8},"status":"QUESTION_AVAILABLE"}
```

Get remaining question one by one
GET getNextQuestion
*https://qa1-mindelements.rhcloud.com/question-web/rest/questions/getNextQuestion/{memberNumber}/{sessionId}

Sample
*https://qa1-mindelements.rhcloud.com/question-web/rest/questions/getNextQuestion/1111/d26fc144-0468-4f43-bfd5-8c19617e0bfb

```
{"question":"other question 7","selection":{"d":"other answer d 7","b":"other answer b 7","c":"other answer c 7","a":"other answer 7"},"questionNumber":10,"sessionId":"d26fc144-0468-4f43-bfd5-8c19617e0bfb","answer":null,"explanation":null,"questionBucketDetails":{"questionNumber":10,"totalQuestionRunningValue":0,"totalQuestion":10,"numberOfSetsDone":1,"questionSetRunningValue":1,"questionSetTotalValue":8},"status":"QUESTION_AVAILABLE"}
```

Check the answer for every question

GET checkAnswer

* https://qa1-mindelements.rhcloud.com/question-web/rest/questions/checkAnswer/{answer}/{sessionId}/{questionNumber}

Sample

* https://qa1-mindelements.rhcloud.com/question-web/rest/questions/checkAnswer/a/1111/d26fc144-0468-4f43-bfd5-8c19617e0bfb/1

```
{"answer":"Answer is correct"}
```

Get the list of wrong answer one by one

https://qa1-mindelements.rhcloud.com/question-web/rest/questions/getWrongAnswer/{memberNumber}/{sessionId}

Sample:

https://qa1-mindelements.rhcloud.com/question-web/rest/questions/getWrongAnswer/1111/d26fc144-0468-4f43-bfd5-8c19617e0bfb

```
{"question":"","selection":{},"questionNumber":10,"sessionId":"d26fc144-0468-4f43-bfd5-8c19617e0bfb","answer":"NA","explanation":"NA","questionBucketDetails":{"questionNumber":10,"totalQuestionRunningValue":0,"totalQuestion":10,"numberOfSetsDone":1,"questionSetRunningValue":1,"questionSetTotalValue":8},"status":"STATUS_NULL_QUESTIONS_NOT_ANSWERED"}
```

Swagger Documentation
==================

Check for QuestionBucket and AnswerBucket response json

* https://portal-mindelements.rhcloud.com/question-rest/apidocs/#!/questions
 

Real-time Development
======================

Once code is committed or changed on github. The code is build automatically. The output application will show on link below:

* https://qa1-mindelements.rhcloud.com/question-web/


 
