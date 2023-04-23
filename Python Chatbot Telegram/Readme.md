## Table of Content
- [Architecture](#rchitecture)

### Architecture
![](https://i.imgur.com/qOJPAQP.jpg)
We are using Dialogflow which is a chatbot building framework
1. In Architecture we make a chatbot using Dialogflow
2. Our user will talk to this chatbot
3. What ever the user will give command, it will be called `intent`
4. From `intent` we will extract `Entity`
 - Difference between intent and entity
 - Suppose use ask can you provide me phone no. so this is an intent the `phone no` is entity.
 - Suppose the user say to convert 500USD into INR. so 500 USD and INR both are entity
6. So our chatbot basically extract entity from intents
7. After Entity the next stage is `fulfillment`
8. In fullfilment, we make Flask API
9. That Flask API will do the conversion (currency conversion)
10. This flast api will give the conversion to chatbot 
11. The chatbot can be anywhere whats app, telegram, fb messenger