

# OAuth 2.0 Use Cases

## Using YouTube Data API V3 and Postman

Resources that can help (even though they could be about different APIs, but encapsulates the essential steps of the OAuth2 work flow):

[source 1: Google OAuth in Postman](https://quickstarts.postman.com/guide/google-oauth-in-postman/index.html), [source 2: YT video: How to OAuth 2.0 Authorization with Postman](https://www.youtube.com/watch?v=zHfR96IZECQ)

### Logical Overview

draft: 
![](Attachments%20-%20Postman/Pasted%20image%2020231209044137.png)

TODO: draw diagram of web app, inside it, some GCP services, inside it, YT API and OAuth client (and OCS in 2nd diagram)

The steps are outlined in the sub headers below.

### Create a GCP Project

Side note: GCP stands for Google Cloud Platform; it is a widely used cloud computing platform [along with AWS and Azure](https://www.digitalocean.com/resources/article/comparing-aws-azure-gcp). [Google apparently started calling it GC instead of GCP](https://www.reddit.com/r/googlecloud/comments/183bq2i/what_is_the_difference_between_google_cloud_and/?ref=readnext) to avoid confusion about its services, since it offers IaaS, PaaS, and SaaS cloud services.

* You'll simply need a Google account. With it, go to [console.cloud.google.com](https://console.cloud.google.com/)
	* If you need to deal with payments, follow [this](https://www.youtube.com/watch?v=hRXMuMQQ27c) video.
* Then, go to "APIs & Services" tab:
  
  ![|450](Attachments%20-%20Postman/Pasted%20image%2020231208101323.png)
  
* Create a project from here:
  
  ![](Attachments%20-%20Postman/Pasted%20image%2020231208101717.png)
  
	* Side note: when choosing a project name, try to make it unique, in order for its id to match its name. For example:
	  
	  ![](Attachments%20-%20Postman/Pasted%20image%2020231208101931.png)
	  
	  Apparently, the project name above has already been used by another user, so Google adds a number as a suffix. However, if we change it like this:
	  
	  ![](Attachments%20-%20Postman/Pasted%20image%2020231208102031.png)
	  
	  We see that it is unique, so the name matches the id. This isn't mandatory, but it's just an advice to easily use the id.

### Install YouTube Data API V3 Library to GCP Project

* In "APIs & Services" tab, choose Library:
  
  ![|243](Attachments%20-%20Postman/Pasted%20image%2020231208102333.png)
  
* Search for "YouTube Data API v3", choose the first option, then click "Enable":
  
  ![|500](Attachments%20-%20Postman/Pasted%20image%2020231208102431.png)

### Create OAuth Consent Screen

The OAuth Consent Screen (OCS) is a UI in which:
* The *resource owner* sees the access which the *client* wants to the *resource server*.
	* The resource owner can then accept/decline this access request.
* Assuming the resource owner accepts, the client will manage the data found on the resource server.

Note: the *client* isn't the one that wants this data access. Rather it is the **application (app)** which calls the client to access this data on its behalf. In other words, <mark style="background: #D2B3FFA6;">an application uses a client to manage data found on the resource server</mark>. The rest of this section considers this "app" to be the postman **web application**, i.e., `web.postman.co`. 

In general, the OAuth 2.0 process is summarized in steps 1 to 6 of the figure below:

![](Attachments%20-%20Postman/Pasted%20image%2020231208164005.png)

Where:

![](Attachments%20-%20Postman/Pasted%20image%2020231208155914.png)

Therefore, <mark style="background: #D2B3FFA6;">whenever the word "client", "app", or "client app" is mentioned below, I believe it refers to the web application (which internally uses the client)</mark>:

![](Attachments%20-%20Postman/Pasted%20image%2020231208191818.png)

Side note: 

Now, the following steps outline how to create OCS:
* Go to the OAuth Consent Screen (OCS) tab from here:
  
  ![](Attachments%20-%20Postman/Pasted%20image%2020231208102805.png)
  
* Choose user type based on your needs):
  
  ![](Attachments%20-%20Postman/Pasted%20image%2020231208160123.png)
  
* Fill the rest of the details in the "OAuth consent screen" tab (e.g., "App Information", "App Logo", etc.). Sample example:
  
  ![|500](Attachments%20-%20Postman/Pasted%20image%2020231208160533.png)
  
  ![](Attachments%20-%20Postman/Pasted%20image%2020231208160604.png)
  
  ![](Attachments%20-%20Postman/Pasted%20image%2020231208160812.png)
  
* Notes:
	* "App name" and "App logo" appear here in the OCS:
	  ![|300](Attachments%20-%20Postman/Pasted%20image%2020231208160652.png)
	* "Authorized domains" are domains that are authorized to make OAuth 2.0 requests on behalf of your application. For example:
		* Suppose you have a web application hosted at `https://myapp.example.com`. 
		* In this case, you would enter `example.com` in the "Authorized domains" field. 
		* This means that only requests coming from `myapp.example.com` are authorized to interact with your application. 
			* I.e., any other domain that tries to interact with your application would be denied.


TODO: update info above based on this Bing answer:

In the context of OAuth 2.0 and Google Cloud Platform (GCP), the “client” refers to your application that is using the YouTube Data API V3 library to access YouTube Data.

Here’s how it fits together:

- **Your Application**: This is the software you’re developing. It could be a web application, a mobile app, a desktop app, etc. This application wants to access YouTube Data on behalf of users.
    
- **YouTube Data API V3 Library**: This is a specific set of functions provided by Google that allows your application to interact with YouTube Data. Your application uses this library to make requests to the YouTube Data API.
    
- **OAuth 2.0 Client**: This is a component of your application that handles the OAuth 2.0 process. It’s responsible for redirecting users to the authorization server (Google), receiving the authorization code, and exchanging it for an access token.
    
- **OAuth Client ID**: This is a unique identifier for your OAuth 2.0 client. It’s generated when you create an OAuth 2.0 client in GCP and is used by Google to identify your application during the OAuth 2.0 process.
    
- **OAuth Consent Screen**: This is the screen that users see when your application requests access to their YouTube Data. It shows information about your application and the data it’s requesting access to.
    

So, in this context, the “client” is your application that’s using the YouTube Data API V3 library. The OAuth 2.0 process is a way for your application to get permission from users to access their YouTube Data on their behalf.

TODO: state that "authorized domains" are usually the domains automatically added from "web clients" (which are actually OAuth clients, so just name them that when screenshotting plz). A domain mentioned in an OAuth client is usually a redirect URL (e.g., `oauth.pstmn.io/../...` so the domain part only is added to the OCS) (possible reference: [so post](https://stackoverflow.com/questions/56436510/testing-google-oauth-2-0-with-localhost#:~:text=Notice%20the%20description%20%2D%2D%20%22When%20a%20domain%20is%20used%22.%20so%20it%27s%20not%20an%20obligation%20to%20add%20authorized%20domain%20for%20consent%20screen))

TODO: draw diagram of web app, inside it, some GCP services, inside it, YT API and OAuth client (and OCS in 2nd diagram)


