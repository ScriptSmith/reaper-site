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
// Only works after `FB.init` is called
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
	FB.api(page + '/posts', function(response) {
		document.getElementById('response').innerHTML = response;
	}
}
</script>

<div id='query' style='display: none'>
	Public Page to scrape: <input type='text'>
	<button onclick='scrapePage()'>Scrape</button>
	<div id='response'></div>
</div>


