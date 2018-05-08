# Facebook scraping of public pages

<script>
  window.fbAsyncInit = function() {
    FB.init({
      appId            : '948109978690942',
      autoLogAppEvents : true,
      xfbml            : true,
      version          : 'v3.0'
    });
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "https://connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
</script>

<script>
function myFacebookLogin() {
  FB.login(function(){
	document.getElementById('query').style.display = 'block';
}, {scope: ''});
}
</script>

This tool uses the Facebook Graph API to look at the posts on public facebook pages. After signing in below, enter the name or id of the page that you would like to scrape.

<button onclick="myFacebookLogin()">Sign in with Facebook</button>

<script>
function scrapePage() {
	var page = document.getElementById('page').value;
	var args = document.getElementById('args').value;
	FB.api(page + '/posts?' + args, function(response) {
		console.log(response);
		var text = "";
		if ('error' in response) {
			text = '<h3>Error occurred</h3>' + response['error']['message'];
		} else {
			text = '<h3>Data</h3>' + JSON.stringify(response['data']);
		}
		document.getElementById('response').innerHTML = text;
	})
}
</script>

<div id='query' style='display: none'>
	Public Page to scrape: <input type='text' id='page' value='mcdonaldsau'><br>
	Query Arguments: <input type='text' id='args'><br>
	<button onclick='scrapePage()'>Scrape</button>
	<div id='response'></div>
</div>


