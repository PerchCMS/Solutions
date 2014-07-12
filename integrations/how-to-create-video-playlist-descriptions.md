Created by: Marissa Cookson
Created date: 2014-07-12
Last updated: 2014-07-12
Authors: Marissa Cookson
Title: How do I create a video playlist with a description for each video?

# How do I create a video playlist with a description for each video?

## You want to create an editable playlist with a custom description for each video using jQuery. The video description should update each time you click on a playlist item.

Tools
- jQuery 1.10.2+
- jQuery Responsive YouTube Vimeo Player
http://codecanyon.net/item/responsive-youtube-vimeo-playlist/4748903

Live demo
http://www.thevisionhouse.com.au/gear-in-action

## Part 1: The video descriptions

Create an empty container for a list of video descriptions. These will be populated by Perch and only one list item will be visible based on the current video that’s playing. A video-url is also added in Perch which is used to dynamically populate the playlist.

    <ul class="video-descriptions">
    	<?php perch_content('Videos'); ?>
    </ul>
    .video-descriptions li {
        display: none;
    }
    .video-descriptions li:first-child {
        display: block;
    }

Create a video_list.html template in perch/templates/content.
This is a repeater block which will allow the editor to add multiple videos and reorder them.

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

Video player markup

    <div id="rp_plugin">
    	<div id="rp_videoContainer">
    		<div id="rp_video"></div>
    	</div>
    	<div id="rp_playlistContainer">
    		<!-- Playlist will be populated here —>
    	</div>
    </div>

Append ul to playlist container since an empty ul in the markup is invalid
    
    $('#rp_playlistContainer').append('<ul id="rp_playlist" />');
	
For each video description item, get the video url and push it to a videoLinks array
    
    var videoLinks = [];
	$('.video-descriptions li').each(function(){
		var videoUrl = $('.video-url',this);
		videoLinks.push(videoUrl);
		// for each video description item, create an empty playlist item
		// so there is an equal number of descriptions and videos
		$('#rp_playlist').append('<li />');
	});

For each empty playlist item, append corresponding video link from videoLinks array

	$('#rp_playlist li').each(function(i){
		$(this).append(videoLinks[i]);
	});

Init video player (feel free to substitute your own)
	
	$("#rp_playlist").responsiveplaylist({
	    onChange: function(){
	    	// wait until video has changed before getting index of current video
	    	// show the corresponding video description
	    	setTimeout(function(){
	    		var currIndex = $('#rp_playlist li.rp_currentVideo').index();
				$('.video-descriptions li:eq('+currIndex+')').show();
				$('.video-descriptions li:eq('+currIndex+')').siblings().hide();
	    	},1000);
		}
	});
