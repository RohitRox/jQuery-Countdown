# jQuery Countdown [Enhanced]

This is a fork of jquery countdown published at [Tutorialzine](http://tutorialzine.com/2011/12/countdown-jquery/).

This enhanced version contains abilty reset countdown at any instant programmatically,
and hookable expire after feature as explained below:

```js

// Original feature and example

$(function(){
	
	var note = $('#note'),
		ts = new Date(2012, 0, 1),
		newYear = true;
	
	if((new Date()) > ts){
		// The new year is here! Count towards something else.
		// Notice the *1000 at the end - time must be in milliseconds
		ts = (new Date()).getTime() + 10*24*60*60*1000;
		newYear = false;
	}
		
	$('#countdown').countdown({
		timestamp	: ts,
		callback	: function(days, hours, minutes, seconds, total_sec_left){
			
			// the callback now has one more parameter,
			// total_sec_left, which is total seconds remaining left 

			var message = "";
			
			message += days + " day" + ( days==1 ? '':'s' ) + ", ";
			message += hours + " hour" + ( hours==1 ? '':'s' ) + ", ";
			message += minutes + " minute" + ( minutes==1 ? '':'s' ) + " and ";
			message += seconds + " second" + ( seconds==1 ? '':'s' ) + " <br />";
			
			if(newYear){
				message += "left until the new year!";
			}
			else {
				message += "left to 10 days from now!";
			}
			
			note.html(message);
		}
	});
	
});
```
#### Now the countdown can be reset any time by calling
```js
	$.countdown.reset();
	// also a callback function can be passed
	$.countdown.reset( function(elapsed){ alert('Resetted in '+elapsed+'seconds.'); } );
```
#### After reset, calling the plugin creates new instance of countdown
```js
		$('#countdown').countdown({ ... });
```

#### The plugin now can be initialized in a completely new way, via hookable expire_after
```js
	// let's set our timer for 6 sec and after 6 sec timer should automatically stop and alert 'timeover baby !'
	$('#countdown').countdown({ 
		expire_after : 6 // put your time here in sec
	},
		function()
		{
			alert('timeover baby !'); // do after expire
		}
	});
```

