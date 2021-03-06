# Pinterest
To download data from Pinterest, you should make use of the [Pinterest API](https://developers.pinterest.com/docs/getting-started/introduction/)

Your own information is accessible through their API. If you obtain approval from pinterest, most public information can be accessed through their API.

To see a list of all possible endpoints on the API, visit the reference: [https://developers.pinterest.com/docs/api/overview/](https://developers.pinterest.com/docs/api/overview/)

The reference will also explain what information you can get out of the *User*, *Board*, and *Pin* endpoints.

## Access token

To scrape data from the Pinterest API, you will need to create an app.

Start by signing in to Pinterest, navigating to [https://developers.pinterest.com/apps/](https://developers.pinterest.com/apps/) and creating an app

![](images/pinterest1.png)

On the next page, in the Redirect URIs textbox, put in:

`https://scriptsmith.github.io/reaper-site/redirect.html`

Then press enter and save your changes

![](images/pinterest2.png)

Now, scroll to the top of the page and copy the App ID and App secret into the fields below:

<p>
App id: <input type='text' id='appid'>
</p>
<p>
App secret: <input type='text' id='appsecret'>
</p>

Now click this button and accept the request permissions:

<script>
function auth() {
    client_id = document.getElementById('appid').value;
    window.open("https://api.pinterest.com/oauth/?response_type=code&client_id=" + client_id + "&state=reaper&scope=read_public,write_public,read_relationships,write_relationships&redirect_uri=https://scriptsmith.github.io/reaper-site/redirect.html")
}

function post() {
    console.log('posted')
    client_id = document.getElementById('appid').value;
    client_secret = document.getElementById('appsecret').value;
    code = document.getElementById('code').value;
    var http = new XMLHttpRequest();
    var url = "https://api.pinterest.com/v1/oauth/token";
    var params = "grant_type=authorization_code&client_id=" + client_id + "&client_secret=" + client_secret + "&code=" + code;
    console.log(params)
    http.open("POST", url, true);
    
    //Send the proper header information along with the request
    http.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
    
    http.onreadystatechange = function() {//Call a function when the state changes.
        document.getElementById('accesstoken').innerHTML = http.responseText;
    }
    http.send(params);
}
</script>

<button onclick="auth()">Click me</button>

Copy the code from the page you are redirected to into the field below:

<p>
Code: <input type='text' id='code'>
</p>

Now click this button:

<button onclick="post()">Click me</button>

When it appears, copy the access token below into Reaper:

*If an error occurs, try request the code again*

<div id="accesstoken" style="background-color: grey"></div>

![](images/pinterest3.png)

## A note on access to profile information

To request a list of boards belonging to a user, you can use the **User -> Boards** node. This will only work with your own user (`me` or `your.username`), you can't request a list of boards from other users.

However, if you want to scrape the information about or the pins belonging to a known board (as in, you know the name of the board) then you can download it for any user that has made that board public.
