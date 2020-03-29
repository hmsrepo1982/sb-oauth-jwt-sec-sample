# sb-oauth-jwt-sec-sample

Before building this sample interaction, it is very importatnt to understand all different terminology Oauth uses.

1. OAuth - Open Authorization ( Internet Protocol ) 
2. Acts like framework.
3. Where - Token based Authorization on the internet.
4. What token contains - Header | Payload (User id | Roles | Expiration Data | Some other information) | Digital Signature
5. It would never contains password and also please note this is not used for Authentication.


Terminology - 

1. Actors - Applications participating in OAuth Framework.
2. Resource - Any secure item which needs access.
3. Resource Owner - Owner who has authority to grant permission on that Resource.
4. Client - An Application making protected resource request on behalf of the resource Owner and with its Authorization.

5. Authorization Server - Mostly work with Resource Server. Works hand in hand. If any server says that it has implemented Auth, then they need to implement --> Authorization Server. If it is embedded inside Resource Server or just coupled with that does not matter. This server would be responsible for issuing ACCESS TOKENS to client.

6. Workflows - many different ways to implement.

Authorization Code Flow : 

1. Logged on Photo print Service.

2. Want to print photo.

3. Photo printing Service --> calls - Authorization Server.

4. Now Authorization server unless Resource Owner Agrees, will not proceed further. So he sends a request to # Resource Owner.

NOTE  : If Resource Owner - agrees, then Resource Host can move forward since security ownership is on HOST.

5.Now Authorization Server gives a Authorization Token Back to Photo printing Service. This is short lived token.

6. Now Photo printing internally makes second call to Authorization Server - get Me Access - here is your # Authorization Token.

7. Now if Authorization server received valid Token, it would prepare and return Access Token back to PPService.

8. Now this would call Resource Host Server --> with Access Code.

9. Resource will be returned if Access Code is valid since Resource host has access to Access Code generated.

10. Photo will be allowed to download or print.

Authorization Code Flow - Implicit Style  - ( Less Secure compared to Other one ) : 

1. Logged on Photo print Service.

2. Want to print photo.

3. Photo printing Service --> calls - Authorization Server.

4. Now Authorization server unless Resource Owner Agrees, will not proceed further. So he sends a request to # Resource Owner.

NOTE  : If Resource Owner - agrees, then Resource Host can move forward since security ownership is on HOST.

5. Now Authorization server sends Access Token back to PPService.

6. Now this would call Resource Host Server --> with Access Code.

7. Resource will be returned if Access Code is valid since Resource host has access to Access Code generated.

8. Photo will be allowed to download or print.

BIG FLOW : 

Authorization between services - ( Micro Services ) - Good fit 

MS 1 - MS 2 calls 

MS2 - has access to DB.

Now burden of security on MS2 so that it wont give access to MS1 in some cases.

How data needs to flow.

MS1 -------1. calls Auth Server------- Auth Server

2. Gets the Access Token.

3. Calls MS2 with access token. 

4. If Access is allowed, then serves the MS1. Else Rejects the access for Data ( Eg : Payroll information ) 

Use case to understand this : Diagram is below.
