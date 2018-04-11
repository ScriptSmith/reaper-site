# LinkedIn
To download data from LinkedIn, you should make use of the [LinkedIn API](https://developers.pinterest.com/docs/getting-started/introduction/)

Your own information and some public information is accessible through their API. If you obtain approval from LinkedIn, job listings can be accessed through their API.

To see a list of all possible endpoints on the API, visit the reference: [https://developer.linkedin.com/docs/guide/v2](https://developer.linkedin.com/docs/guide/v2)

The reference will also explain what information you can get out of the available endpoints.

## Access token

To scrape data from the LinkedIn API, you will need to create an app.

Start by signing in to LinkedIn, navigating to [https://www.linkedin.com/developer/apps](https://www.linkedin.com/developer/apps) and creating an app

Once the app has been set up, in the Authorized Redirect URLs textbox, put in *https://scriptsmith.github.io/reaper-site/redirect.html*  and tick all the application permissions

![](images/linkedin1.png)

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
    window.open("https://www.linkedin.com/oauth/v2/authorization?response_type=code&client_id=" + client_id + "&state=reaper&scope=r_basicprofile,r_fullprofile,r_emailaddress,rw_company_admin,w_share&redirect_uri=https://scriptsmith.github.io/reaper-site/redirect.html")
}

function post() {
    console.log('posted')
    client_id = document.getElementById('appid').value;
    client_secret = document.getElementById('appsecret').value;
    code = document.getElementById('code').value;
    var http = new XMLHttpRequest();
    var url = "https://cors-anywhere.herokuapp.com/https://www.linkedin.com/oauth/v2/accessToken";
    var params = "redirect_uri=https://scriptsmith.github.io/reaper-site/redirect.html&grant_type=authorization_code&client_id=" + client_id + "&client_secret=" + client_secret + "&code=" + code;
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

<div id="accesstoken" style="background-color: grey; word-wrap: break-word"></div>

![](images/linkedin2.png)