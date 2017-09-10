# AlexaROS
sent data between Alexa and ROS topic.

roslaunch rosbridge_server rosbridge_websocket.launch
rostopic echo /speech_recognition

1.Make AlexaROS.zip
-index.js
APP_ID = 'amzn1.ask.skill.927bcbb3-ff87-4bed-954d-d6a1c13c7f0b' from https://developer.amazon.com/
url : 'ws://PubilicIP:9090'
or url : 'ws://phawit.ddns.net:9090'
**whatmyip for find PubilicIP
-Generate AlexaROS.zip (node_modules,index.js,AlexaSkill.ja)

2.Set router http://192.168.1.1
-forword port 9090 to IP_localROS

3.Make own ddns https://www.noip.com/
-set in router
-set Dynamic Update Detected ip in ubuntu

4.AWS --> Lambda >> N.virginia
https://aws.amazon.com/
code : AlexaROS.zip
Configuration : Runtime-Node.js 4.3
                Handler : index.handler
                Role : Choose an existing role
                Existing role : Lambda_basic_execution
Action >> configs > config test event > start session            

4.Amazon Developer Services --> Alexa skill kit
https://developer.amazon.com/
Intent Schema :
{
  "intents": [
    {
      "slots": [
        {
          "name": "Message",
          "type": "AMAZON.LITERAL"
        }
      ],
      "intent": "MessageIntent"
    },
    {
      "intent": "AMAZON.HelpIntent"
    },
    {
      "intent": "AMAZON.StopIntent"
    },
    {
      "intent": "AMAZON.CancelIntent"
    }
  ]
}

Sample Utterances :
MessageIntent {i want a plastic bowl|Message} using LITERAL
MessageIntent {give me the metal spoon|Message} using LITERAL
MessageIntent {pass me the spoon|Message} using LITERAL
MessageIntent {can i have a bowl|Message} using LITERAL
MessageIntent {hand me the plastic spoon|Message} using LITERAL
MessageIntent {give me that|Message} using LITERAL

Configuration ::
North America, Default : arn:aws:lambda:us-east-1:475736037737:function:robot


