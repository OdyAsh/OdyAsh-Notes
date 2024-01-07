#oauth #cybersecurity #computer-science #applied-science

# Main Sources

* [Hem's OAuth 2.0 Flows Dev.to post](https://dev.to/hem/oauth-2-0-flows-explained-in-gifs-2o7a)
	* Truly an amazing post, kindly throw him some ❤️‍🔥.
	* Most of the notes below are from his post.
* ["How OAuth Authentication Works", by goteleport.com](https://goteleport.com/blog/how-oauth-authentication-works/)
	* Talks about scopes and tokens.
		* Specifically refresh tokens, which is briefly mentioned in the previous source.
	* Talks about grants and flows.
	* Mentions a detailed case study on how [Teleport](https://goteleport.com/how-it-works), an open-source remote access tool, uses OAuth to allow users to log in through GitHub single sign-on (SSO).
* [OAuth.com](https://www.oauth.com/)
	* A simplified guide to building an OAuth 2.0 server.
	* For learning how to take advantage of the OAuth 2.0 framework while building a secure API through high-level overviews, step-by-step instructions, and real-world examples.
	* Pro-tip 1: click the "Table of Contents" button at the website's top-right section to view detailed chapters of each topic. 
	* Pro-tip 2: Whenever you finish (or start , or both!) a grant flow, cement your knowledge with hands-on experience found in the website's [playground page](https://www.oauth.com/playground/index.html). 
	* Some of the chapters I've personally read:
		* [8.2: "The Client ID and Secret"](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)
			* Self-explanatory :]
* "[The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749)" document published by the IETF.
	* This is probably the most comprehensive resource to understand OAuth from.
	* Even though it's very long, it is actually easy to read (i.e., no complicated terminologies are used).
	* I suggest reading it if you want to understand OAuth from a single source of truth, instead of jumping between websites/videos.
		* Side note: you may still jump to other websites, but that will happen less often.
* Credit to [this](https://www.reddit.com/r/webdev/comments/isx7fg/oauth_20_resources_you_can_actually_understand/) sub reddit post from which I found some of the resources above.

# OAuth Definition

* OAuth stands for Open Authorization.
* It is an open-standard authorization protocol or framework ([source: Varonis](https://www.varonis.com/blog/what-is-oauth#:~:text=OAuth%20is%20an%20open%2Dstandard,give%20ESPN%20your%20Facebook%20password.)).
	* A "protocol" is a standardized set of rules for formatting and processing data ([source: Cloudflare](https://www.cloudflare.com/learning/network-layer/what-is-a-protocol/#:~:text=In%20networking%2C%20a%20protocol%20is,to%20communicate%20with%20one%20another.)).
	* This set of rules is often explained in flow diagrams, which are shown later.
* It enables third-party apps (e.g., websites) to access user's data without requiring them to share their credentials.
	* The user uses this protocol to _authorize_ which resources an app can access and limits the *scope* of access accordingly.
	* In other words, the protocol makes *access delegation* possible.
		* "Access delegation" is when a person authorizes another to serve as his or her representative for a particular task ([source: Oracle](https://docs.oracle.com/cd/E56917_01/cs9pbr4/eng/cs/lscc/concept_UnderstandingDelegatedAccess-888000.html#:~:text=Delegation%20is%20when%20a%20person,access%20to%20perform%20a%20transaction.)).

# Terminologies Related to OAuth

| Term                     | Description                                                                                                                                                                                  |
|:------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Client 📦                | The application ("app") that seeks access to resources. Usually the third-party.                                                                                                             |
| Client ID 🪪             | The `client_id` is a public identifier for the app. Even though it’s public, it’s best that it isn’t guessable by third parties. Example: from [Google Cloud](https://cloud.google.com/docs/overview), which supports OAuth 2.0: `292085223830.apps.googleusercontent.com`                                                                                                                                                                                               |
| Client Secret 🤫         | The `client_secret` is a secret known only to the app and the authorization server.                                                                                                                                                                                               |
| Confidential Client 📦🔒 | Confidential clients are apps that can guarantee the secrecy of `client_secret`.                                                                                                             |
| Resource Owner 👤        | The user who owns the resources. It can also be a machine 🤖 (E.g. Enterprise scenarios).                                                                                                    |
| Resource 🖼               | Could be images, data exposed via APIs, and so on.                                                                                                                                           |
| Resource Server 📚       | Server that hosts protected resources. Usually, an API server that serves resources if a proper token is supplied.                                                                           |
| Authorization Server 🛡   | Server responsible for authorizing the client and issuing access tokens.                                                                                                                     |
| User-Agent (device) 🌐   | The browser or mobile application through which the resource owner communicates with the authorization server.                                                                               |
| Access Token 🔑          | A token which is issued as a result of successful authorization. An access token can be obtained for a set of permissions (scopes) and has a pre-determined lifetime after which it expires. |
| Refresh Token 🔄         | A special type of token that can be used to renew the access token.                                                                                                                          |

# Grant Types and Flows

* An analogy of two (real-world) grant types and their flows is shown [here](https://goteleport.com/blog/how-oauth-authentication-works/#:~:text=Going%20back%20to%20our,is%20to%20be%20used.). 
	* Grant types:
		* Physical ticket
		* Digital ticket
	* Flows:
		* Steps 1 to 7 (in case of physical ticket)
		* Steps 1 to 5 (in case of digital ticket)
* Authorization grant is a credential. ([source: RFC](https://www.rfc-editor.org/rfc/rfc6749#section-1.3))
	* It is created/issued by the resource owner (RO).
		* It represents the RO's authorization and approval for a client to use its resources within a certain scope.
	* It is used by the client to obtain an access token issued by the authorization server.
	*  There are 4 main grant types (i.e., This "credential" can be one of four things):
		* Authorization code
			* Authorization code with PKCE
		* Client credentials
		* Resource owner password credentials
		* Implicit credentials
* A "flow" refers to the whole protocol that allows the access token issuance. ([source: SO](https://stackoverflow.com/questions/46134223/in-oauth-2-0-what-is-the-difference-between-a-grant-and-a-flow#:~:text=refers%20to%20the%20whole%20protocol%20that%20allows%20the%20access%20token%20issuance))
	* "Protocol" in this context means the sequential and ordered steps done between the user, client, authentication server, and resource server.
	*  Examples of "flows" are shown in the sub-sections below, which explain each grant type.

## Authorization Code Grant (ACG)

* It is a popular browser-based authorization flow for Web and mobile apps.
* This flow is optimized for _confidential clients_.
	* Confidential clients are apps that can guarantee the secrecy of `client_secret`.
* Steps are beautifully illustrated in the [videos sub-section](#ACG%20Illustrations%20using%20Videos%20and%20Images), and in the [sequence diagrams sub-section](#ACG%20Sequence%20Diagrams).
* Playground (recommended): try an interactive demo [here](https://www.oauth.com/playground/authorization-code.html). 
* Note it is not commonly abbreviated to ACG; this is just me :].

### ACG Illustrations using Videos and Images

As a video ***(personal favorite)***. Tip: I suggest pausing the video at each step, to see the data (i.e., emojis) sent. ([source: dev.to](https://dev.to/hem/oauth-2-0-flows-explained-in-gifs-2o7a#:~:text=1.-,Authorization%20Code%20Grant%20flow,-It%20is%20a)):

![Authorization Code Grant flow video](Attachments%20-%20OAuth/Authorization%20Code%20Grant%20flow%20video.mp4)

As a gif:

![Authorization Code Grant flow gif](Attachments%20-%20OAuth/Authorization%20Code%20Grant%20flow%20gif.gif)

Another detailed video ([source: RFC YT video](https://www.youtube.com/watch?v=7D-OU4hZW70)):

<iframe width="690" height="415" src="https://www.youtube.com/embed/7D-OU4hZW70" title="OAuth 2.0 Authorization Code Grant Flow" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Its image:

![](Attachments%20-%20OAuth/Pasted%20image%2020231215090617.png)


A less-detailed (i.e., simpler) video:

<iframe width="690" height="415" src="https://www.youtube.com/embed/ZV5yTm4pT8g" title="OAuth 2.0 Authorization Code Grant Flow" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Important note: if you read the first comment of the video above, you'll see that the inaccuracy issue mentioned in the [ACG Sequence Diagrams](#ACG%20Sequence%20Diagrams) section is also present here.

Finally, very in-depth videos are [this](https://www.youtube.com/watch?v=GyCL8AJUhww) and [this](https://www.youtube.com/watch?v=996OiexHze0).
### ACG Sequence Diagrams

<mark style="background: #FF5582A6;">Important note</mark>: 
* The 3 diagrams below are almost equivalent; 
	* each one is just a further abstraction of the previous diagram. 
* **However**, the first (i.e., most detailed) diagram is the most accurate in some details.
	* For example, the "authorization code" should be sent to the resource owner (i.e., in their "user agent", i.e., browser). That code is then redirected to the client.
		* This is shown properly in the most detailed diagram, but not in the others.

A detailed sequence diagram of authorization code grant (ACG) flow ([source: page 18 in "Authorization server with OAuth support and recommended usage patterns" pdf](https://s3.eu-central-1.amazonaws.com/ucu.edu.ua/wp-content/uploads/sites/8/2021/07/Kovalchuk-Bogdan_188594_assignsubmission_file_Bohdan_Kovalchuk.pdf)):

![](Attachments%20-%20OAuth/Pasted%20image%2020231215100143.png)

A less detailed sequence diagram of ACG flow ([source: c-sharpcorner.com](https://www.c-sharpcorner.com/article/understanding-workflow-of-oauth2-0-authorization-grant-types/#:~:text=for%20user%20resources.-,Below%20workflow%20diagram,-of%20authorization%20code))

![](Attachments%20-%20OAuth/Pasted%20image%2020231215093333.png)

A much less detailed sequence diagram of ACG flow ([source: Sarasa's medium post](<https://sarasagunawardhana.medium.com/oauth-2-0-framework-dfe1cffc2e4b#:~:text=This%20is%20the%20ideal%20scenario%20and%20the%20safer%20one%20because%20the%20access%20token%20is%20not%20passed%20on%20the%20client%20side%20(web%20browser%20in%20our%20example).>)):

![](Attachments%20-%20OAuth/Pasted%20image%2020231215093937.png)
