## Go OAuth example

Read the blog post [here](https://www.sohamkamani.com/blog/golang/2018-06-24-oauth-with-golang/)

This is an example node application that implements Githubs OAuth2 API.

In order to run the application:

1. Register your new application on Github : https://github.com/settings/applications/new. In the "callback URL" field, enter "http://localhost:8080/oauth/redirect". Once you register, you will get a client ID and client secret.
2. Replace the values of the `clientID` and `clientSecret` variables in the [main.go](/main.go) file and also the [index.html](https://github.com/sohamkamani/go-oauth-example/blob/master/public/index.html#L14) file 
4. Start the server by executing `go run main.go`
5. Navigate to http://localhost:8080 on your browser.

github process flow https://stackoverflow.com/questions/43046097/post-request-to-github-api


Register your app.

On your github account, go to settings -> OAuth Applications

This is the image when you register your application

Get the Client ID and Client Secret.

This is the image after you receive Client ID and Client Secret

Ask for Github Code

Now you have Client ID. Go to this url.

https://github.com/login/oauth/authorize?client_id=b420627027b59e773f4f&scope=user:email,repo

Please define your own client_id and scope.

Get the Github Code

Remember the Authorization callback URL you input when register? After you go to the link above, you should have redirected to your callback URL with the code as the parameter.

For example http://localhost:8080/github/callback?code=ada5003057740988d8b1

Ask and Get the Access Token

Now you need to do http request post with Client ID, Client Secret, and Code you have got as the parameter.

Request

POST https://github.com/login/oauth/access_token?client_id=a989cd9e8f0137ca6c29&client_secret=307d18600457b8d9eec1efeccee79e34c603c54b&code=ada5003057740988d8b1

Response

access_token=e72e16c7e42f292c6912e7710c838347ae178b4a&token_type=bearer

Post Issue to Github

Now you have access token you can use it to access Github API.

fetch('https://api.github.com/repos/organization/repo/issues?access_token=e72e16c7e42f292c6912e7710c838347ae178b4a', {
      method: 'post',
      body: {
        title: 'Title',
        body: {body: "body", title: "title"}
      }
    })
