Created by: Drew McLellan
Created date: 2014-07-10
Last updated: 2014-07-10
Authors: Drew McLellan
Title: Can I use CDNify with Perch?
Tags: cdn, resources, performance

# Can I use CDNify with Perch?

## Sites with internation audiences can see performance benefits from moving images and static assets to a content delivery network (CDN). CDNify is one such service which is very easy to add to a Perch site.

The purpose of a content delivery network (CDN) is to make your site load faster by serving images and static assets from data centres that are physically closer to the site visitor. A CDN will automatically copy your assets to their data centres around the globe. When a visitor loads your site, they'll be sent assets from the closest data centre to their current location.

That all sounds pretty complicated to set up, right? Well yes, it can be, but it doesn't have to be. [CDNify](https://cdnify.com/) is a CDN service that does 80% of what you'd ever need, with only about 1% of the hassle. It's a bit like Perch (and that's why we like it).

CDNify works like this:

1. You create an account, and set your website up as a _resource_.
2. CDNify gives you a URL to put in front of any static asset paths on your site
3. The first time that asset is loaded, CDNify fetches it from your site, then serves its copy from that point on

One of the classic problems with using a CDN is making sure that updated assets get updated on the CDN too. That's not so much a problem with Perch, because everything is versioned, every updated image etc has a new file name.

## Getting started

Once you've signed up for CDNify and have set your site up as a resource, you'll be given a URL like this:

    mysite.a.cdnify.io

Open up your `perch/config/config.php` file and find this line:

    define('PERCH_RESPATH', PERCH_LOGINPATH . '/resources');

and update it to this:

    define('PERCH_RESPATH', 'http://mysite.a.cdnify.io' . PERCH_LOGINPATH . '/resources');

That's it. The explaination was longer than the instructions!

## Using with buckets

If you have a custom bucket list, you just need to prefix the `web_path` for any buckets you want to serve from the CDN. Open up `perch/config/buckets.php` and change your lines like this:

    'web_path'  => '/my/bucket/path',

to include the CDNify URL like this:

    'web_path'  => 'http://mysite.a.cdnify.io/my/bucket/path',

And you're done.