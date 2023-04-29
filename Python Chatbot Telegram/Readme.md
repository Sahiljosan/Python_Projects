## Table of Content
- [Architecture](#architecture)
- [Dialogflow](#dialogflow)
- [Flask Syntax](#flask-syntax)
- [ngrok](#ngrok)
- [Fulfillment](#fulfillment)
- [Updated Flask app code](#updated-flask-app-code)
- [API For Conversion Factor](#api-for-conversion-factor)

Start from here after receiving API - https://youtu.be/Nb21OhaW8GY?t=3586

### Architecture
![](https://i.imgur.com/vWbMl5j.png) <br>
We are using `Dialogflow` which is a chatbot building framework
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
12. `Integration` means on which platform you want to publish your chatbot


### Dialogflow
- Dialogflow provides NLU (Natural Language Understanding) platform, using which we can create chatbots. We donot have to train the model from scratch
- Service like dialogflow are : 
     - `AWS lex` make chatbots using AWS
     - `wit.ai` make chatbots with facebook 
     - `watson` IBM
     - `AL chatbot` Microsoft Azure
- Give personality to chatbot using `small talk`
- Now we send these parameters to python flask API
- if Flask API doesnot work, then we have to assign default response 
- Go to `responses` and write default response
- Now we wil send `Diagnostic Info` to flask API 

[Back To Top](#table-of-content)

### Flask Syntax
```
from flask import Flask

app = Flask(__name__)  # app : object Flask : Class

@app.route('/')  # decorator to create a route

def index():
    return "Hello"

if __name__ == "__main__":
    app.run(debug = True)
```
Now the problem is dialogflow is running on google cloud and flask app is running on our machine so how can we establish communication between both, for that we will use ngrok

### ngrok
`ngrok` is the fastest way to put your app on the internet. Test mobile apps against your development backend. in simple word ngrok makes one port of our machine online for 2 hours.
- at development time we will use `ngrok`
- at production time we can use heroku or AWS
-----------------------------------------------------------
So download and open ngrok and write ngrok http "Port name that u want to make online"

![](https://i.imgur.com/f5oXoXv.png)

Now we have to copy forwarding URL and copy in our browser



[Back To Top](#table-of-content)

![](https://i.imgur.com/YB2ObTh.png)

If Flask API doesn't run throught agrok the we have authenticate our ngrok agent <br>
For that write below text in command promt
```
ngrok config add-authtoken 2P6JvrndnRTt4m4m12hBnOE9tUQ_5pyeNhbY8uoaEwErcC47q
```

Now our flask code is working in web 
![](https://i.imgur.com/DOaK5es.png)

### Fulfillment
Enter the URL generated from agrok and click save


![](https://i.imgur.com/JxkBIH3.png)

Now go to intents and enable webhook call for this intent 


![](https://i.imgur.com/N2yffm4.png)

Now whatever response we get, we can receive it in flask app 


[Back To Top](#table-of-content)

### Updated Flask app code
```
from flask import Flask, request

app = Flask(__name__)  # app : object Flask : Class

@app.route('/', methods = ['POST'])  # decorator to create a route

def index():
    data = request.get_json()
    source_currency = data['queryResult']['parameters']['unit-currency']['currency']
    amount = data['queryResult']['parameters']['unit-currency']['amount']
    target_currency = data['queryResult']['parameters']['currency-name']
    print(source_currency)
    print(amount)
    print(target_currency)
    return "<h1> Hello </h1>"

if __name__ == "__main__":
    app.run(debug = True)
```

### API For Conversion Factor


![](https://i.imgur.com/Apr6A8O.png)

Free Api key
```
9aa0c54f5ad4c460c36d
```

Full Link
```
https://free.currconv.com/api/v7/convert?q=USD_PHP&compact=ultra&apiKey=9aa0c54f5ad4c460c36d
```






