---

layout: default

title: PhotoSwipe FAQ and Known Issues

h1_title: FAQ & Known Issues

description: Frequently asked questions and known issues about PhotoSwipe image gallery.

addjs: true

canonical_url: http://photoswipe.com/documentation/faq.html

buildtool: true

markdownpage: true

---

### <a name="keep-updated"></a> Where is changelog, how to do I get notified about updates?

Each time PhotoSwipe gets an update - [GitHub releases](https://github.com/dimsemenov/PhotoSwipe/releases) page is updated with details. 
Releases page has an [Atom feed](https://github.com/dimsemenov/PhotoSwipe/releases.atom), you may setup email notifications when feed is updated [using IFTTT](https://ifttt.com/recipes/230902-photoswipe-update-notification).

Also you may join my [email newsletter](http://dimsemenov.com/subscribe.html) (sent 3-4 times a year), follow [@PhotoSwipe on Twitter](http://twitter.com/photoswipe), and star/watch [PhotoSwipe on GitHub](https://github.com/dimsemenov/PhotoSwipe/).

It's very important to keep PhotoSwipe updated, especially during the beta period.


### When WordPress plugin will be released?

Plugin is under development and will be released in early-mid 2015. You may [subscribe here](http://dimsemenov.com/subscribe.html) to get notified.


### <a name="image-size"></a> I'm unable to predefine image size, what to do?

Use another gallery script ([1](http://dimsemenov.com/plugins/magnific-popup/), [2](http://dimsemenov.com/plugins/royal-slider/gallery/)), or find a way:

- You can read size of an image by downloading only small part of it ([PHP version](http://stackoverflow.com/questions/4635936/super-fast-getimagesize-in-php), [Ruby](https://github.com/sdsykes/fastimage), [Node.js](http://stackoverflow.com/a/20111234/331460)).
- You can store size of image directly in its filename and parse it on frontend during PhotoSwipe initialization. 
- Most CMS store size of an image in database and have API to retrieve it.
- Most web API (Facebook, 500px, Instagram, Flickr, Twitter, YouTube, Vimeo etc.) return size of images.

Dimensions are used for progressive loading, stretched placeholder, initial zoom-in transition, paning, zooming, caption positioning.


### <a name="different-thumbnail-dimensions"></a> My thumbnails are square but large images have different dimensions, what to do with opening/closing transition?

- Option 1: set option `showHideOpacity:true`, and opacity will be applied to main image, not just to background.
- Option 2: disable transition entirely (options `showAnimationDuration` and `hideAnimationDuration`).

I'll try to explain why this is not implemented yet. There are two ways to make expanding area animation:

1. Animate `clip` property. But [it forces Paint](http://csstriggers.com/#clip) each time, which makes animations jerky.
2. Wrap image that expands with two divs that have `overflow:hidden` and reposition them via `transform:translate` during the animation so they clip it at right parts. This method does not force Paint or Layout, but requires two additional elements in markup of each slide. Test prototype showed that it works smooth only on high-end mobile devices (like Nexus 5 with Chrome). Maybe some day I'll implement it.


## Known issues

### GIF images sometimes freeze on iOS8

iOS Safari has a bug that freezes GIF images that are shifted outside of the window (or outside of element with `overflow:hidden`). My recommendatiuon is to avoid using animated GIFs in PhotoSwipe at all, as they slow down animation performance in any mobile browser. But if you really need to use it, refer to [this hack](https://github.com/dimsemenov/PhotoSwipe/issues/662#issuecomment-66420874).


### Mobile browser crashes when opening PhotoSwipe

In most of cases, it can happen in iPhone or in old Android phones (before KitKat) with low memory limit. The #1 reason of crash is too big images (usually >2000px), avoid images larger than 1200px for an average 800x600 phone. Crash can also occur if you open PhotoSwipe during some process on your page (this can be initial page load/render, or some complex animation on page), try to delay PhotoSwipe initialization until page is rendered (18-300ms after document.ready), especially if you're opening large images.






Know how this page can be improved? [Suggest an edit!](https://github.com/dimsemenov/PhotoSwipe/blob/master/website/documentation/responsive-images.md)
