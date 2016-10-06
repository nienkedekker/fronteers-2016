My notes on [https://fronteers.nl/congres/2016](Fronteers 2016). Don't mind any spelling mistakes, and any potential misinterpretations are all mine :)

# Ire Aderinokun: What About CSS? Progressive enhancement and CSS.

## Intro
What happens when there is no CSS enabled in the browser? How do we apply progressive enhancements techniques to CSS? The prevailing practice in 2003 was graceful degradation: the practice of building your web functionality so that it provides a certain level of user experience in more modern browsers, but it will also degrade gracefully to a lower level of user experience in older browsers.

Ex:
`<noscript> You don't have JS, go change your browser! </noscript>`

This has its problems:
- Doesn't straddle technology inflection points well
- Many designers only test one version back: we're not making sure the site degrades gracefully for everyone
- It does not address the different needs of different audiences. It's good for people with modern browsers, but not for edge cases.
- It's expensive to retrofit to new alternative devices.
- Whatever is 'good enough' usually rules, we do not go the extra mile for those who aren't using the most up to date browsers.

So...progressive enhancement!
Web design must mature and accept the developments of the past several years. We need to look at the past. The goal of web design is not merely to dazzle, but to deliver information to the widest audience. So what does this mean in practice?

5 guidelines:
- Basic content and functionality should be accessible to all web browsers.
- Sparse, semantic markup should contain all the content. We need to use to correct elements in the correct oder. Use header, main, footer.
- Content should be defined in plain text in the markup.
- Enhanded layout can be provided by CSS stylesheets. Keyword: enhanced! The site must be useful if CSS is not used in the browser. It doesn't have to look great, but it has to be functional.
- Enhanced behavior can be provided by unobtrusive JS. It is not required for the site to function, it is only for enhancement.
- End-user web browser preferences should be respected. The user should ultimately be in control of their experience. Don't take control away from the user.

In 2016, we have a lot more browsers. In addition, we have many more versions of these browsers. We also have a lot of new technologies and things that may work in some browsers, and not in others. Finally, we have a lot more users. More users = more variation in needs.

Besides all of this: the web is open and inclusive. We need to manage all these things and graceful degradation is just not a viable option anymore.

## Progressive enhancement in JS
Possible problems:
- JS is not enabled in the browser
- The browser does not support a particular JS feature

So, how to fix this? First, make sure the website is functional with JS. JS is enhancement, not a requirement. Next, we can do feature detection. Before using service workers, check if they're available! If we really need a feature, we can use polyfills. Pretty simple.

## Progressive enhancement in HTML
- The browser does not understand the semantic meaning of an HTML tag. Like `<header`. Some browsers do not understand this and interpret it as `<div`. The page still loads and everything is fine (graceful degredation approach), with progressive enhancement we can add some `role=` so older browsers understand the semantic meaning too.

## Progressive enhancement and CSS
We have the selector, the property, and the value of the property. What happens if something goes wrong? Let's say we wanna flip an image by 180 degrees:

image {
  transform: rotate(90deg)
}

Lots of things can go wrong with selector, property and value (misspellings). Plus, a user's browser may not even support rotate. And unlike JS, we can't prepare for unsupportd features. Unlike HTML, there is no built-in fallback. This makes debugging CSS hard.

What are the solutions?
- Start with sensible HTML. Make sure your site is functional with only mark-up.
- Progressive enhancement M&M: the content is the core, the presentation and client-side scripting is 'extra'.
- Take advantage of the cascade. Write rules and build them on top of eachother, and each rule can enhance the other. Example:

div {
  background-color: green; // legacy
  background-image: cool gradient stuff; // cool new browser
}

- Adopt a mobile first strategy. Min-width based media queries > max-width. Graceful degradation things 'desktop first', whereas progressiv enhancement assumes mobile first. Start the least retricted as possible.
- Use flexbox. It is designed to be a progressive enhancement. It's well supported.
- Separate stylesheets. This is a last resort. Separate stylesheets for different browsers.

## The future
-  Feature queries: `@supports`. Supported by most browsers, but not all. See blog post by Jen Simmons.
- Problem: browser does not support feature queries, but it does support the feature in question! How to solve this? Progressive enhancement! Use feature queries as a progressive enhancement rather than a requirement. Take advantage of the cascade.
- There will be more browsers and devices (VR headsets, smartwatches).
- There will be more technologies. We don't know what works in which browsers.
- There will be more people online and there is no guarantee they'll be using iPhones 7s.

Lastly: LEAVE NO ONE BEHIND. The web is meant to be open and for everyone.
Look at your userbase, your location - where is the project built? Don't just look at global statistics.
Progressive enhancement should be thought of at all stages: not just frontend, but also backend and design. Let go of the pixel perfect things. Either make things more simple overall, or accept different experiences on different browsers.
It's all about your userbase. If only 0.1 percent uses Opera Mini, it's a difficult business case to make. But if a lot of people use it, it's obvious. However, if you build your sites in a way that's progressive, you kind of make it automatically accessible for everyone, including low-end browser users.
New feature? Always check availability first. Don't get tempted to use all new features until it's not going to break too many things.

=========================================================================================================================================================================

# Nadieh Remer: Data Visualization
This was supercool! Note to self: look into D3.js.

=========================================================================================================================================================================

# G Scott Olson: How You Do What You Do Is Who You Are

## Intro
Leveraging React to improve the user experience. Paper uses several devices, but all the clients use the same API. When talking about React you need to consider which parts need to be seamless. There are some pages you don't want pageload on. But it's okay to do a full-page refresh for other pages (like infrequently used page such as Settings). Other pages could be static and not a part of the React app at all.

## Using React to improve (pre)loading images
The source attribute is dynamically set based on the state. If there is an error, you use a handler to assign a broken image (load up a pretty image). If the image has successfully loaded, set the source. When you have images in a grid you want to lay them out responsively (3x2 = 33.3 percent per image). The component loads, the image is mounted, but what if image 1, 4 and 6 come in first? You want things to load in order to avoid page reflow. Is there a way we can improve the way our preloader works?

- Transparent spacer images (three divs, but creates an extra http request)
- Dynamic spacers
- SVG

http://daverupert.com/2012/04/uncle-daves-ol-padded-box/

=========================================================================================================================================================================

# Nolan Lawson: Offline, progressive, and multithreaded: a peek at the web apps of the future
Back then, we used Flash to make rich web experiences. HTML5 was a response to that, and it won. However, we won just in time for mobile to eat the world. On mobile, we use native apps, not websites. If you want to build a rich experience on mobile, you write a native app. In the same way HTML5 was a response to Flash, progressive web apps are a response to native mobile apps.

There are three major features commonly talked about about web apps:
- Do they work offline (available on native apps, not so much on web apps)
- Are they progressive (unavailable on native apps - lots of downloads/mbs). Webapps are really good at this.
- Are they multithreaded (i.e. they take advantage of mobile hardware). Native apps are very good at this. Web apps, not so much.

However, PWAs can do exceedingly well on all three of these points.

## Offline
IndexedDB allows you to store data offline in a structural way, data that is accessible when the user is offline. "Offline first" is a bit of a red herring - a site being unavailable on the subway is not a huge deal. It's about speed. Memory is superfast, disk is a bit slower, network is real slow. The reason you're doing offline first is that it forces you to think about people on slower networks. So how do we do offline? We're not quite there yet. The old way for storing static data is AppCache (pretty inflexible). The new way is Cache API/Service Workers. Service Workers are kind of a build of your own AppCache, but tons more flexible.

The old sorta deprecated way for dynamic/query data we used LocalStorage (and WebSQL). Local Storage has a lot of drawbacks. The new way is IndexedDB (asynchronous so no DOM blocking). It's also transaction-based.

## Progressive
A bit of a loaded term. Web apps progressively become apps - they start as a website, but then slowly turn into an app. That's one sense of the word. The other sense is progressive enhancement -- upgrade per capabilities, progressively add features (weak version) and your site should work without JS (strong version). PWAs don't work without JS. However, in 2016, it is perfectly okay to build a website that doesn't work without JS. The web isn't uniform. Even Facebook doesn't use JS, so that's a bit of a relief, even if they can't then it's okay to require JS.

People have reliable JS, but not reliable internet connections. So we need to build stuff that works offline, and let go of the "JS should not be required" idea.

## Multithreaded
Why do we want to think about this? Ultimately, the DOM is single-threaded, so is JS. Using huge JS apps makes things 'janky' i.e. slow, because it competes with the DOM on one single thread. This is avoidable when we look at the hardware out there. Even low-range Android phones have at least 4 cores. Yes, they are slow, but they can do 4 things slowly at once. We need to harness this power. Browser vendors can solve this issue. But web developers are responsible as well: web workers! This is a way to explicitly take a bit of JS and run it in a separate thread. It's simple, but very much underused. Lawson promotes one thread for web workers, and one for UI. The web worker takes care of the vast majority of app logic, the UI thread takes care of the UI effects.

So why aren't we using web workers? According to some, the gain is pretty marginal and it adds a lot of development complexity.

## Webapps of the future
Offline-first (it's always faster to go to the local cache), progressive, multithreading (no jankiness). It's all about the user, that is who we're building for. And if we can build fast, responsive and robust apps that's in everyone's best interest.

=========================================================================================================================================================================

# Martin Splitt: Multi-user WebVR or: wait, who are these people?

## WebVR is pretty neat.

# Lodewijk Nauta: Big Data, Big Impact

## KPMG sales pitch.

=========================================================================================================================================================================

# Monika Piotrowicz: Scaling Frontend Development 
