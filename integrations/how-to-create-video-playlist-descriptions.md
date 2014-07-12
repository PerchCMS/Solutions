Created by: Marissa Cookson
Created date: 2014-07-12
Last updated: 2014-07-12
Authors: Marissa Cookson
Title: How do I create a video playlist with a description for each video?

# How do I create a video playlist with a description for each video?

## You want to create an editable playlist with a custom description for each video using jQuery. The video description should update when you click on a playlist item.

Tools:  
- jQuery 1.10.2+
- jQuery Responsive YouTube Vimeo Player  
http://codecanyon.net/item/responsive-youtube-vimeo-playlist/4748903

Live demo:  
http://www.thevisionhouse.com.au/gear-in-action

## Part 1: The video descriptions

Create an empty container for a list of video descriptions. These will be populated by Perch and only one list item will be visible based on the current video that’s playing. Default markup and css:

    <ul class="video-descriptions">
    	<?php perch_content('Videos'); ?>
    </ul>
    
    .video-descriptions li {
        display: none;
    }
    .video-descriptions li:first-child {
        display: block;
    }

Create a video_list.html template inside perch/templates/content.
This is a repeater block which will allow the editor to add multiple videos and reorder them. The video-url is used to  populate the playlist. These links are not visible on the page as they're empty. No need for a `p` tag around the description content because Perch adds one.

	<perch:repeater id="Videos" label="Videos">
		<li>
			<div>
				<a class="video-url" href="<perch:content id="video-url" type="text" label="Video URL" required="true" />"></a>
				<h3><perch:content id="video-title" type="text" label="Video Title" /></h3>
				<perch:content id="video-description" type="textarea" label="Video Description" textile="true" markdown="true" html="true"  />
			</div>
		</li>
	</perch:repeater>


## Part 2: The video playlist

Dynamically build a playlist based on the video links entered in Perch.

Video player markup:

    <div id="rp_plugin">
    	<div id="rp_videoContainer">
    		<div id="rp_video"></div>
    	</div>
    	<div id="rp_playlistContainer">
    		<!-- Playlist will be populated here —>
    	</div>
    </div>

Append a `ul` to the playlist container since an empty `ul` in the markup is invalid:
    
	$('#rp_playlistContainer').append('<ul id="rp_playlist" />');
	
For each video description item, get the video url and push it to a videoLinks array. Append an empty playlist item so there is an equal number of descriptions and videos:
    
	var videoLinks = [];
	$('.video-descriptions li').each(function(){
		var videoUrl = $('.video-url',this);
		videoLinks.push(videoUrl);
		$('#rp_playlist').append('<li />');
	});

For each empty playlist item, append the corresponding video link from the videoLinks array:

	$('#rp_playlist li').each(function(i){
		$(this).append(videoLinks[i]);
	});

Init video player (feel free to substitute your own. If yours doesn't have an onChange event, listen for a click on each playlist item instead).

onChange: Wait until the player has updated the current video, then get the index of the current video and show its corresponding video description. Hide the other descriptions.
	
	$("#rp_playlist").responsiveplaylist({
		onChange: function(){
	    		setTimeout(function(){
	    			var currIndex = $('#rp_playlist li.rp_currentVideo').index();
				$('.video-descriptions li:eq('+currIndex+')').show();
				$('.video-descriptions li:eq('+currIndex+')').siblings().hide();
		    	},1000);
		}
	});
