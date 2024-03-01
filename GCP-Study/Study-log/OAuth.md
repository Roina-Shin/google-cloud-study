### [Source of this study material : GCP Professional Cloud Architect by Ranga Karanam](https://www.udemy.com/course/google-cloud-professional-cloud-architect-certification/)


## Getting started with OAuth

- OAuth is an **Authorization Framework**.


- Allows users to grant access to **server resources** to another entity WITHOUT sharing credentials.


- Example: Give access to your Google Drive to your photo editing application.

  - Resource owner: You

  - Resource: Google Drive

  - Client: Photo Editing application

  - Authorization server: Google OAuth service

  - **Client IDs and Client secrets**: How does your photo editing applicaiton authenticate itself to Google?

  - Scopes: What access is allowed? (READ/WRITE)



## Playing with OAuth 2.0

- **OAuth 2.0** is the latest and most popular version of OAuth.


- **https://developers.google.com/oauthplayground/** 


- Go to the OAuth playground. Here, you can think of OAuth Playground as your application making a call to the Google APIs. And you can search here for the Google API that you want to access.


- For this demo, we will make a call to the **Google Drive API**. Scroll down to find it and click the specific API you want.


![OAuth-playground](/GCP_pictures/Study-logs/OAuth/OAuth-playground.PNG "OAuth Playground")


- Then click Authorize APIs.


![click-authorize-apis](/GCP_pictures/Study-logs/OAuth/click-authorize-apis.PNG "Click Authorize APIs")


- You will see this permission screen. Allow the access to your Google service.


![allow-access](/GCP_pictures/Study-logs/OAuth/allow-access.PNG "Allow access")


- Then, you will need to **exchange authorization code for tokens**. Click the blue button.


![exchange-authorization-code-for-tokens](/GCP_pictures/Study-logs/OAuth/exchange-authorization-code-for-tokens.PNG "Exchange autorization code for tokens")


- Authorization code is sent as a part of the request and we need to select our request. The HTTP method is POST and click **List possible operations** to see the list of operations. Go with create presentations as your request.


![create-presentation-request](/GCP_pictures/Study-logs/OAuth/create-presentation-request.PNG "Create presentation request")


- If you click Send the request, you will see that the request is sent with the authorization code and the response comes back.


![oauth-acess-token](/GCP_pictures/Study-logs/OAuth/oauth-access-token.PNG "OAuth Access Token")


- When I did this, there was an error because of resources quota issue. So I tried with another Google account and it worked this time. When I go and check the slide in Google Slide, a new untitled presentation was made.


![untitled-presentation](/GCP_pictures/Study-logs/OAuth/untitled-presentation.PNG "Untitled presentation")

