# Live Example

Try the Quick Start script right from your browser! Simply replace the `appEUI` and `accessKey` values with those you have found for your application in [Quick Start / Connect](#connect) and hit the green **Run** button.

<script src="https://embed.tonicdev.com" data-element-id="live-code"></script>

<div id="live-code"><pre class="highlight"><code>var ttn = require('ttn@2.0.0-4');

var region = 'eu';
var appId = 'hello-world';
var accessKey = '2Z+MU0T5xZCaqsD0bPqOhzA6iygGFoi4FAgMFgBfXSo=';

var client = new ttn.Client(region, appId, accessKey);

client.on('connect', function(connack) {
	console.log('[DEBUG]', 'Connect:', connack);
});

client.on('error', function(err) {
	console.error('[ERROR]', err.message);
});

client.on('activation', function(data, devId) {
	console.log('[INFO] ', 'Activation:', devId, data);
});

client.on('message', function(data, devId) {
	console.info('[INFO] ', 'Message:', devId, JSON.stringify(data, null, 2));
});

client.on('message', function(data) {

	// respond to every third message
	if (data.counter % 3 === 0) {
	
        // Toggle the LED
        var payload = {
          led: !message.led
        };
        
        // If you don't have an encoder payload function:
        // var payload = [message.led ? 0 : 1];

        console.log('[DEBUG]', 'Sending:', JSON.stringify(payload));
        client.send(data.dev_id, payload, data.port);
	}
});</code></pre></div>