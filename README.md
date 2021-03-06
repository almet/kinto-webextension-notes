# Webnotes

This is a small Firefox extension to publish selection of text with its context
(date and URL for now) when `Ctrl+Shift+U` is pressed or with a link in the
context menu.

<img src="/webnotes.gif?raw=true"/>

If you want, [have a look at the presentation
video](https://alexis.notmyidea.org/webnotes.mp4) (in french), or [my personal
webnotes](https://notes.notmyidea.org).

*Disclaimer: I've done this for myself. I'm happy to share it so other can
use it as well, but I'll probably not commit a lot of time maintaining this!*

## How does it work?

When you hit `Ctrl+Shift+U`, the content of the selection is sent to an
external service (that you have set, which can be under your control, the
service is [a Kinto server](https://kinto-storage.org)).

You can then configure any other application to access the data you saved. With
the current implementation, the stored data is available to everyone (it's my
use case) but it can easily be changed to something else if needed.

In the `app` folder, there is a webpage able to display the notes you've
published. You will just need to change the *server*, *bucket* and *collection*
to match yours.

## How do I install it?

First, go to [the addons.mozilla.org
page](https://addons.mozilla.org/en-US/firefox/addon/wwebnotes/) and click
"install", then head to `about:addons` and select "Install addon from file".

Once installed, click on "more" or "preferences" next to the addon name. There,
enter your kinto instance, bucket and collection name and then hit save.

Once the values saved, you can initialize the storage by clicking the link.

## Where can I see my notes?

In the `app` folder, there is a webpage able to display the notes you've
published. You will just need to change the *server*, *bucket* and *collection*
to match yours.

The `make serve` command will serve the content of this folder on
http://localhost:8000.

## Using a different Kinto server

If you want to use a different Kinto server, you might want to create a bucket to store all webnotes-related collections.

Here is an [httpie](https://httpie.org) command to do so (replace `notsecret` with the admin password you want to use):

> echo '{"data": {"id": "webnotesapp"}, "permissions": {"collection:create": ["system.Authenticated"]}}' | http post https://yourkintoinstance.tld/v1/buckets --auth="admin:notsecret" --verbose

## Why doing yet another tool for this?

The short answer is that I actually haven't found one that suits my need *and*
that is open-source.

[Wallabag](http://doc.wallabag.org/) plays a kind of similar role but
doesn't currently allow me to save selections of text nor to publish them to
somewhere public.
