#oauth #cybersecurity #computer-science #applied-science

Main sources: 
* [Hem's OAuth 2.0 Flows Dev.to post](https://dev.to/hem/oauth-2-0-flows-explained-in-gifs-2o7a)
	* Truly an amazing post, kindly throw him some ❤️‍🔥.
	* Most of the notes below are from his post.
* "[The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749)" document published by the IETF.
	* This is probably the most comprehensive resource to understand OAuth from.
	* Even though it's very long, it is actually easy to read (i.e., no complicated terminologies are used).
	* I suggest reading it if you want to understand OAuth from a single source of truth, instead of jumping between websites/videos.
		* Side note: you may still jump to other websites, but that will happen less often.

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

| Term                   | Description                                                                                                                                                                                  |
|:---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Client 📦              | The application ("app") that seeks access to resources. Usually the third-party.                                                                                                                     |
| Resource Owner 👤      | The user who owns the resources. It can also be a machine 🤖 (E.g. Enterprise scenarios).                                                                                                    |
| Resource 🖼             | Could be images, data exposed via APIs, and so on.                                                                                                                                           |
| Resource Server 📚     | Server that hosts protected resources. Usually, an API server that serves resources if a proper token is supplied.                                                                          |
| Authorization Server 🛡 | Server responsible for authorizing the client and issuing access tokens.                                                                                                                     |
| User-Agent 🌐          | The browser or mobile application through which the resource owner communicates with the authorization server.                                                                               |
| Access Token 🔑        | A token which is issued as a result of successful authorization. An access token can be obtained for a set of permissions (scopes) and has a pre-determined lifetime after which it expires. |
| Refresh Token 🔄       | A special type of token that can be used to renew the access token.                                                                                                                      |

