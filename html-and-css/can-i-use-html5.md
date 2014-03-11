# Can I use HTML5 with Perch?

## Perch doesn’t insert anything into your website without you asking it to, this means that you can use any mark-up. So whether you prefer HTML4.01, XHTML or HTML5 or even want to edit an XML document, Perch will help you do that.

Perch doesn’t insert anything into your website without you asking it to, this means that you can use any mark-up. So whether you prefer HTML4.01, XHTML or HTML5 or even want to edit an XML document, Perch will help you do that. In this solution we’ll have a look at some of the new HTML5 elements and how you can create templates for these. The example files that ship with Perch and first party add-ons all use HTML5.

The information and examples in this article have been mainly taken from the HTML5 Doctor website, which is a great first port of call if you want to start using HTML5. I have linked to the appropriate pages on that site throughout.

To start using HTML5, you need to use the HTML5 doctype on your pages:

    <!DOCTYPE html>

This is backwards compatible and you are safe to use this instead of your current HTML or XHTML doctype. You’ll find that if you were already coding in HTML 4.01 or XHTML that your pages should validate as HTML5 and you can carry on working in the way you have done, this is because you can write HTML5 in an HTML or XHTML style. From this point on it is up to you whether to just use older elements – or to begin to introduce some of the new HTML5 elements – whichever path you choose Perch can help.

# HTML5 Boilerplate

For this tutorial I’m starting out with a page based on the HTML5 Boilerplate available from the HTML5 Doctor website. This includes some CSS and also a link to a JavaScript file that makes the new HTML5 elements stylable with CSS in versions of Internet Explorer earlier than IE9. You only need this if you are using the new structural elements and not for using HTML5 audio or video for example.

    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <title>HTML 5 complete</title>
      <!--[if IE]>
      <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
      <![endif]-->
      <style>
       article, aside, details, figcaption, figure, footer, header,
       hgroup, menu, nav, section { display: block; }
      </style>
    </head>
<body>
<p>Hello World</p>
</body>
</html>

## HTML5 Structural Elements

HTML5 gives us semantic, meaningful ways to mark-up our content and describe what it is. It includes new elements such as article, section, nav and aside. The `<article></article>` element is used to mark-up an independent piece of content – something that could be republished and make sense outside of the site. A blog post would be a good example of content you would put inside the article element. See HTML5 Doctor – article for more examples.

You might use section instead of article if the thing you are marking up is not something that could be independently syndicated, however is still a complete section of a document – including a heading.

The nav element is for marking up navigation. The aside element can be used within article, in which case it refers to information related to that article or outside of an article, in which case it refers to information relating to the current web page.

Perch, with its focus on structured content, is ideal as a CMS for managing content marked up using these HTML5 elements. For example, the following template would enable an editor to add an article, with an aside for further reading.

<article>
    <h1><perch:content id="heading" type="text" label="Heading" required="true" title="true" /></h1>
    <perch:content id="body" type="textarea" label="Article body" 
textile="true" editor="markitup" required="true" />
    <aside>
     
      <h1>Further reading</h1>
      <perch:content id="reading" type="textarea" label="Further reading" 
textile="true" editor="markitup" required="true" />
    </aside>
</article>

It is allowed to have multiple articles on the page – if that is the case in your site you could set this to allow multiples in Perch.

## HTML5 Audio and Video

HTML5 gives us a way to include video and audio in HTML documents without needing any plugins. For example to include audio on a page you can use the following.

<audio controls preload="auto" autobuffer> 
  <source src="elvis.mp3" />
  <source src="elvis.ogg" />
  Your browser does not support the <code>audio</code> element.
</audio>

As a Perch template including the ability for the admin to upload the various files.

<audio controls preload="auto" autobuffer> 
  <source src="<perch:content id="audiomp3" type="file" label="MP3 File" order="1" />" />
  <source src="<perch:content id="audioogg" type="file" label="Ogg File" order="2" />" />
  Your browser does not support the <code>audio</code> element.
</audio>

This will embed video.

<video controls>
  <source src="foo.ogg" type="video/ogg">
  <source src="foo.mp4">
  Your browser does not support the <code>video</code> element.
</video>

Here it is as a Perch template.

<video controls> 
  <source src="<perch:content id="videomp4" type="file" label="MP4 File" order="1" />" />
  <source src="<perch:content id="videoogg" type="file" label="Ogg File" order="2" />" type="video/ogg" />
  Your browser does not support the <code>video</code> element.
</video>

With both audio and video, if you replace the comment with your chosen Flash solution this will then kick in if the browser does not have support for the video and audio elements. For example for the videos on this website – which play as HTML5 video if you have a supporting browser – use Flowplayer if the video element is unsupported. So your Perch video template would look like the below, if you were to do the same in Perch.

<video width="502" height="376" controls="controls">
  <source src="<perch:content id="videomp4" type="file" label="MP4 File" order="1" />" />
  <source src="<perch:content id="videoogg" type="file" label="Ogg File" order="2" />" type="video/ogg" />
  <source src="<perch:content id="videowebm" type="file" label="webm File File" order="3" />" 
type="video/webm" />
  <a id="flashplayer" href="<perch:content id="videoflv" type="file" label="FLV File" order="4" />"></a>
  <script type="text/javascript" charset="utf-8">
            flowplayer("flashplayer", "/assets/swf/flowplayer-3.1.1.swf",  {
                clip: { autoPlay: false,  autoBuffering: true } 
            });
  </script>
</video>

The lists of formats for audio and video are due to the different browsers supporting different formats. You can read more about this on the HTML5 Doctor website – audio and video. For our Perch videos we use the online service encoding.com, uploading a .mov file and the service then returns the MP4, OGV, WEBM and FLV formats.
HTML5 Blog templates

*Happy HTML5-ing with Perch!*