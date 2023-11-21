<!-- need to cast request.url to a string to be used later -->
<!-- use http for localhost and https for deployed app -->
<!-- works around bug with x-forwarded-proto -->
{% set request_url = request.url | string() %}
{% if ( '0.0' in request_url or 'localhost' in request_url )  %}
{% set full_url = request.url | string() %}
{% else %}
{% set full_url = request.url | replace("http:", "https:") | string() %}
{% endif %}
<!doctype html>
<html lang=en>
<head>
<meta charset=utf-8>
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="icon" href="{{ full_url ~ 'static/favicon.svg' }}">
<meta property="og:url" content="{{ full_url }}" />
<meta property="og:image" content="{{ full_url ~ 'static/social.png' }}" />
<meta property="og:title" content="Hello AWS App Runner"/>
<meta property="og:description" content="Example container to quickly run a service on AWS." />

<meta property="twitter:card" content="summary_large_image" />
<meta property="twitter:image" content="{{ full_url ~ 'static/social.png' }}" />
<meta property="twitter:title" content="Hello AWS App Runner" />
<meta property="twitter:domain" content="{{ full_url }}" />
<meta property="twitter:description" content="Example container to quickly run a service on AWS." />
<meta property="og:image:width" content="1200"/>
<meta property="og:image:height" content="630"/>

<title>Hello AWS App Runner</title>
<style>

/* open-sans-regular - latin */
@font-face {
  font-family: 'Open Sans';
  font-style: normal;
  font-weight: 400;
  src: url('../static/fonts/open-sans-v18-latin-regular.eot'); /* IE9 Compat Modes */
  src: local(''),
       url('../static/fonts/open-sans-v18-latin-regular.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('../static/fonts/open-sans-v18-latin-regular.woff2') format('woff2'), /* Super Modern Browsers */
       url('../static/fonts/open-sans-v18-latin-regular.woff') format('woff'), /* Modern Browsers */
       url('../static/fonts/open-sans-v18-latin-regular.ttf') format('truetype'), /* Safari, Android, iOS */
       url('../static/fonts/open-sans-v18-latin-regular.svg#OpenSans') format('svg'); /* Legacy iOS */
}

body {
  height: 100%;
  width: 100%;
  background-color: #161E2D;
  text-align: center;
  color: #FFFFFF;
  background: url("{{ full_url ~ 'static/background.svg' }}") #161E2D no-repeat;
}

h3 {
  font-size: 16px;
  font-weight: bold;
  letter-spacing: 0;
  line-height: 20px;
  color: #FFFFFF;
  /* margin-bottom: 5%; */
}

h2 {
  font-size: 18px;
  font-weight: bold;
  letter-spacing: 0;
  line-height: 22px;
  margin-bottom: 2%;
  margin-top: 3%;
}

h1 {
  height: 5%;
  font-size: 44px;
  font-weight: bold;
  letter-spacing: 0;
  margin-top: -2%;
  line-height: 56px;
}

.flex-container {
  position: relative;
  justify-content: center;
  width: 80%;
  margin: 0 auto;
  margin-top: 7%;
  margin-bottom: 10%;
}

.row {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  width: 100%;
}

.column {
  flex-direction: column;
  flex-basis: 100%;
  flex: 1;
  margin: 2%;
  margin-top: 0;
  margin-bottom: 0;
}

.icon {
  height: 80%;
  margin: 1%;
}

.subtext {
  color: #FFFFFF;
  font-size: 14px;
  letter-spacing: 0;
  line-height: 17px;
  margin-left: 2%;
  margin-right: 2%;
}

a {
  color: #527FFF;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 0;
  line-height: 22px;
}
a:link {
	text-decoration: none;
}
a:visited {
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
a:active {
  text-decoration: underline;
}

html, body {
  font-family: "Open Sans";
  margin:0;
  padding:0;
}

.banner {
	left:0;
	width:100%;
	height: 100%;
	display: inline-block;
	position: relative;
}

.apprunner_icon {
	width: 15%;
	margin-top: 19%;
	margin-bottom: 6%;
	max-height: 200px;
	min-width: 150px;
}

@media only screen and (max-width: 875px) {
  body { background: url("{{ full_url ~ 'static/background-mobile.svg' }}") #161E2D no-repeat;}
  .apprunner_icon {	min-width: 100px; }
  .icon { height: 60%; margin: 3%;}
  .flex-container {margin-top: 20%; margin-bottom: 30%;}
}

@media only screen and (min-width: 2000px) {
  .apprunner_icon {	margin-top: 13%; }
}

</style>
</head>

<body>
	<div class="container">
		<div class="banner">
			<img class="apprunner_icon" src="{{ full_url ~ 'static/apprunner_icon.svg' }}" />
		</div>

		<h1>And we're live from Raju sathish Computer!</h1>
		<div class="metadata">
			<p>
        {% if ( '0.0' in full_url or 'localhost' in full_url )  %}
          <h2>Contratulations, you deployed the container locally.</h2>
          <p class="subtext">If you would like to run this container publicly check out the links below to get started.</p>
        {% else %}
					<h2>Congratulations, your service has successfully deployed on AWS App Runner.</h2>
        {% endif %}
			</p>
		</div>
		<div class=flex-container>
			<div class='row'>
				<div class='column'>
          {% if ( '0.0' in full_url or 'localhost' in full_url )  %}
          <img class='icon' src="{{ full_url ~ 'static/git_icon.svg' }}" />
          {% else %}
					<img class='icon' src="{{ full_url ~ 'static/twitter_icon.svg' }}" />
          {% endif %}
				</div>
				<div class='column'>
					<img class='icon' src="{{ full_url ~ 'static/workshop_icon.svg' }}" />
				</div>
				<div class='column'>
					<img class='icon' src="{{ full_url ~ 'static/docs_icon.svg' }}" />
				</div>
			</div>
			<div class='row'>
				<div class='column'>
          {% if ( '0.0' in full_url or 'localhost' in full_url )  %}
          <h3>See the code</h3>
          <p class='subtext'>Check out the code to run this site in</br>AWS App Runner.</p>
					<a target="_blank" href="https://github.com/aws-containers/hello-app-runner">Github <img src="{{ full_url ~ 'static/external_link_icon.svg' }}" /></a>
          {% else %}
					<h3>Share on Twitter</h3>
					<p class='subtext'>A unique image has been generated for your service. <br>Share to see yours!</p>
					<a target="_blank" href="https://twitter.com/intent/tweet?text=I%20just%20deployed%20my%20first%20app%20using%20AWS%20App%20Runner%21%20https://apprunnerworkshop.com%20🚀&hashtags=AWSAppRunner&url={{ full_url }}">Share <img src="{{ full_url ~ 'static/external_link_icon.svg' }}" /></a>
          {% endif %}
				</div>
				<div class='column'>
					<h3>Learn more in the workshop</h3>
					<p class='subtext'>Deploy with automated CI/CD and additional examples.</p>
					<a target="_blank" href="https://apprunnerworkshop.com">Learn more <img src="{{ full_url ~ 'static/external_link_icon.svg' }}" /></a>
				</div>
				<div class='column'>
					<h3>Explore App Runner docs</h3>
					<p class='subtext'>Leverage App Runner for production services.</p>
					<a target="_blank" href="https://docs.aws.amazon.com/apprunner">Visit docs <img src="{{ full_url ~ 'static/external_link_icon.svg' }}" /></a>
				</div>
			</div>
		</div>
	</div>
</body>
</html>
