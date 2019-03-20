---
title: "Geek Jokes API"
date: 2019-03-14
description: "Serve silly jokes"
---
<!-- 
https://twil-test.herokuapp.com/
 -->

<p>Here are a couple jokes while you wait:</p>
<div id="jokes">
</div>

<script async>
// Finally we will use the XHR open() method to setup our request with the URL and method
var makeRequestD = function (url, method) {

	// Create the XHR request
	var request = new XMLHttpRequest();

	// Return it as a Promise
	return new Promise(function (resolve, reject) {

		// Setup our listener to process compeleted requests
		request.onreadystatechange = function () {

			// Only run if the request is complete
			if (request.readyState !== 4) return;

			// Process the response
			if (request.status >= 200 && request.status < 300) {
				// If successful
				resolve(request);
			} else {
				// If failed
				reject({
					status: request.status,
					statusText: request.statusText
				});
			}

		};

		// Setup our HTTP request
		request.open(method || 'GET', url, true);

		// Send the request
		request.send();

	});
};


makeRequestD('https://geek-jokes.sameerkumar.website/api')
  .then(function(jokes){
    //   console.log('Success!', jokes);
    document.getElementById("jokes").innerText = jokes.response;
  })
  .catch(function (error){
      console.log('Something went wrong connecting with API', error);
  });

</script>