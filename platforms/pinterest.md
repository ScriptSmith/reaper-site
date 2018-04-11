# Pinterest
To download data from Pinterest, you should make use of the [PinterestAPI](https://developers.pinterest.com/docs/getting-started/introduction/)

Most public information on Pinterest can be accessed over the Data API.

To see a list of all possible endpoints on the Data API, visit the reference: [https://developers.google.com/youtube/v3/docs/](https://developers.pinterest.com/docs/api/overview/)

The reference will also explain what information you can get out of the *User*, *Board*, and *Pin* endpoints.

## Access token

To scrape data from the Pinterest API, you will need to create an app.

Start by navigating to [https://developers.pinterest.com/apps/](https://developers.pinterest.com/apps/) and creating an app

![](images/pinterest1.png)

On the next page, in the Redirect URIs textbox, put in *https://scriptsmith.github.io/reaper-site/redirect.html*, press enter, and then save your changes

![](images/pinterest2.png)

Now, scroll to the top of the page and copy the App ID and App secret into the fields below:

<p>
App id: <input type='text' id='appid'>
</p>
<p>
App secret: <input type='text' id='appsecret'>
</p>

Now click this button:

<script>
function auth() {
    client_id = document.getElementById('appid').value;
    window.open("https://api.pinterest.com/oauth/?response_type=code&client_id=" + client_id + "&state=reaper&scope=read_public,write_public,read_relationships,write_relationships&redirect_uri=https://scriptsmith.github.io/reaper-site/redirect")
}
</script>

<button onclick="auth()">Click me</button>