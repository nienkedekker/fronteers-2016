My notes on [Fronteers 2016](https://fronteers.nl/congres/2016). Don't mind any spelling mistakes, and any potential misinterpretations are all mine :)

**DAY ONE**
* [Ire Aderinokun: What About CSS? Progressive enhancement and CSS.](#ire)
* [Nadieh Remer: Data Visualization](#nadieh)
* [G Scott Olson: How You Do What You Do Is Who You Are](#gscott)
* [Nolan Lawson: Offline, progressive, and multithreaded: a peek at the web apps of the future](#nolan)
* [Martin Splitt: Multi-user WebVR or: wait, who are these people?](#martin)
* [Lodewijk Nauta: Big Data, Big Impact](#lodewijk) 
* [Monika Piotrowicz: Scaling Frontend Development](#monika)
* [Jason Grigsby: Adapting to Input](#jason)

**DAY TWO**
* [Peter Gasston: Surveying the Landscape](#jason)

<a name="ire"></a>
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

`image {
  transform: rotate(90deg)
}`

Lots of things can go wrong with selector, property and value (misspellings). Plus, a user's browser may not even support rotate. And unlike JS, we can't prepare for unsupportd features. Unlike HTML, there is no built-in fallback. This makes debugging CSS hard.

What are the solutions?
- Start with sensible HTML. Make sure your site is functional with only mark-up.
- Progressive enhancement M&M: the content is the core, the presentation and client-side scripting is 'extra'.
- Take advantage of the cascade. Write rules and build them on top of eachother, and each rule can enhance the other. Example:

`div {
  background-color: green; // legacy
  background-image: cool gradient stuff; // cool new browser
}`

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
<a name="nadieh"></a>
# Nadieh Remer: Data Visualization
This was supercool! Note to self: look into D3.js.

=========================================================================================================================================================================
<a name="gscott"></a>
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
<a name="nolan"></a>
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
<a name="martin"></a>
# Martin Splitt: Multi-user WebVR or: wait, who are these people?

WebVR is pretty neat.
<a name="lodewijk"></a>
# Lodewijk Nauta: Big Data, Big Impact

KPMG sales pitch.

=========================================================================================================================================================================
<a name="monika"></a>
# Monika Piotrowicz: Scaling Frontend Development 

## Intro

Frontend does not live in a vacuum. How do you scale a team to work across multiple disciplines? At Shopify, frontend development means having a strong knowledge of HTML, CSS and JS. Frameworks come and go. The FED team sits in the middle of a spectrum: Design - FED - App Dev. This spectrum model is helpful because some people can fall inbetween (half design, half FED, or full-stack devs). What matters is that there's a group in the middle that is accountable for building the UI.

## Standardisation
So what does good frontend actually look like?
- **Language styleguides** for HTML, CSS and JS. This is to bring order in a codebase: work as a team, not as a collective of individuals. Consistency will allow you to work faster (BEM/SMACSS, etc). A styleguide also challenges your implicit assumptions on what's good code, and which comments are useful or not. A styleguide keeps things predictable and keeps you accountable. Creating a styleguide can actually be fun and engaging for a team.
- **Code reviews**. A lot of tools allow you to automate simple things like whitespaces and such, but every line of code should still be reviewed. If there's a rule that keeps getting broken, that's a signal that that rule is not doing what it's supposed to be doing. Review also helps you to define shared standards, share experiences, and enable discussion. Standards are impossible to apply retroactively, but new code can confirm to whatever your standards are. Some active parts of the codebase can be refactored. We're not looking for perfection, but for improvement. A wonderful side effect is that code review builds a culture of feedback and knowledge sharing: bounce ideas off people, and learn from eachother. Pair programming and whiteboarding is great for this tool.
- **Pattern libraries**. You want to build a great, consistent interface for your app. A library of consistent UI patterns makes it possible to share code and gives a starting point for new projects. It'll create standards and conventions. Don't reinvent the wheel! Other things to consider standardising is your stack, responsive guidelines, testing standards, performance standards, accessibility (color contrasts, bulletproof HTML for form fields by using helpers), and language tooling. Having standards also allows newbies to pick up things faster.
- **UI libraries**. For core application patterns, built in a resusable way. These are totally custom.

- Making a pattern is all about finding the commonalities in components and then coming up with guidelines.
- Sharing expertise is really important - no one knows everything but we can learn a lot from eachother.
- "Is something a pattern?" is a good question for the Design team.
- To actually build a pattern/create an API, and how it should be built, are questions for the dev team, with input given from FED.
- Use API to make FED available for everyone in the company. Using APIs also allows you to edit patterns later without having to rewrite code in different places.
- Doing all this is hard work, but it's rewarding: you solve problems at once, everyone can contribute (even if UI is not your area of expertise, you can still use a pattern), and you can use your frontend devs to build actual impactful features, not bug hunting. 
- Teach, build, review

## Building a culture
Individuals are going to have to make choices. How and when do we experiment with new tools? When is it time to change our standards? How do you compromise and prioritize? Do you want specialists, or generalists on your team? What are the hard requirements? What's the interview process look like? 

Pro-tip: have more conversations! Bounce ideas off of eachother, talk about standards, common problems, chat on Slack, get everyone together for short talks on new frontend techniques/discoveries. Use your co-workers as resources to get inspiration from. Don't forget the design and dev team here -- teach Ruby devs CSS to get appreciation for others' craft.

Within a large team, some people can 'own' specialties: interaction engineers, prototypers, CSS devs, performance analysts..you can have experts on certain topics, but what binds everyone is the appreciation of the HTML/CSS/JS foundation.

If the team's not contributing to meaningful experiences for the end-user, it's not very useful to talk about standards. Don't optimize for the perfect codebase, optimize for making an impact (for the end-user). If growing is something you want to do, understanding what you're trying to scale is the most important question. Think critically about your craft, standards, and culture. Embrace the cracy chaotic work that is frontending!

=========================================================================================================================================================================

<a name="peter"></a>
# Peter Gasston: Surveying the Landscape

## Intro
The web is at risk - it's not going to be wiped out, but there is a danger that it could become marginalized. What we're seeing is that a lot of new big popular apps don't really touch the web anymore. Twitter and Facebook were built on the web, but Instagram or Vine hardly touch the web. You can view things, but not upload them. Snapchat doesn't even acknowledge the web. Because of this a few businesses decided to go app-only. Even ChromeOS is now merging with Android.

## Moving to mobile
Selling apps is big business. Apple co-opted deeplinking to send people to apps. Even if you decide to use the website, you get told off for doing so (see: Medium). It's not a level playing field either: a story on the NYT app looks great, but terrible on web. A lot on the web page is just advertising and tracking too. Ads represent 9% of the space on a page, but account for 54% of the load time and 55% of the bandwidth. As a result, people use adblockers on the mobile web. The problem is that ads generate revenue and adblockers stop this revenue stream. Free, ad-supported webpages are no longer sustainable, as there is no money coming in.

Is the web going the way of the printing press? Is having a homepage worth the cost when your content is spread over 20 different platforms? Is having an individual website DOA? Is designing a website still a growth business? Mobile has fundamentally changed the dynamics of how information is distributed. Platforms that came of age on the web, are starting to leave it behind: Facebook, Twitter.

If we're all using apps and leaving the web behind, what does that mean for ownership and privacy? And what does it mean for people who are coming online just now, i.e. people from India? They're mostly on mobile, and visiting web pages costs a lot of data (= money). **1GB of data in Myanmar is 15% of the average person's monthly income!** Everyone uses prepaid, so users feel each megabyte. Facebook has a compelling advantage over other news apps: the content of many posts and news items live inside Facebok itself. And FB is very good at optimizing: FB does not waste MBs on tracking software and such. For some people in developing countries, **Facebook is the internet**. People don't see Facebook as "the internet". The amount of content that lives in FB will only increase. For us folks in developed countries that's terrifying, but it's great news for people paying a lot for data. FB's Instant Articles makes FB's attraction even bigger. FB's ads also load very fast. Result: FB in effect becomes the mobile internet. What's next: shopping and selling via FB. **Facebook has become the browser**.

http://www.theatlantic.com/technology/archive/2016/01/the-facebook-loving-farmers-of-myanmar/424812/

In Chine, a third of the time spent on mobile is spent on WeChat. It's unavoidable, just like the web once was. Slack is becoming a rich platform too -- allowing brands to contact you directly. There's no need to download anything or go to any URLs. Messaging apps are the new browsers. Bots are a new area that's become rather influential:

http://venturebeat.com/2016/06/13/the-conversational-economy-part-1-whats-causing-the-bot-craze/

Bots abstract away all the complex interfaces of the web. If apps are the new web, are bots the new web pages? And is a bot not just an API wrapper for an app?

Other new technologies are Alexa, Echo and Google Home: no browser or phone even required.

## It's not all bad news
A meta platform is a platform hosted on a platform: Facebook, WeChat, Kakao, and also the web. Many of the platforms on mobile are choosing to host content within their own app and this is a direct and compelling threat to the web. 

Google's business model relies on the web, so they're working on AMP. Still not 'open', but better than FB. The web is still alive and kicking - Chrome on mobile goes up in usage every year. Plus, people do use apps a lot, but only one single app, their favorite. The best way to reach new consumers is through the open web. Bots, apps, chat etc are all very popular, but most people still use a browser for say, shopping online on mobile. WeChat has supplanted the web, but it's using the web inside. It's just brought into the app and enhanced with platform features. In China, a mobile-first web page is of the utmost importance - it's just that people see these web pages through WeChat.

Progressive web apps are coming and so far, businesses have had great success with PWAs. PWAs are engaging, installable and most of all, fast. This is especially important in developing countries. So maybe the web's not as dead as we thought it was.

However, we can't just presume the web's going to win. We've been through this before, we have to fight to have the web survive. We can't just presume the web's going to always prosper. We always need to enhance and we're doing that in several ways: physical web/rich local discovery, fat beacons (could contain a whole web page), Flyweb, IoT, PWAs, AMP, Web VR, AR, web bluetooth API. So the web still has a role to play. But the web is not just the browser. We need to start transcending web browsers. Users don't care where they see stuff, they want to get things done. A new definition: the web is any user experience that's delivered across multiple channels and devices.

=========================================================================================================================================================================
<a name="jason"></a>
# Jason Grigsby: Adapting to input

## Intro    
Input is more complex than it used to be. The web was formless - to link between documents. It didn't require forms until we made the web commercial. Our canvas size (screen size we work with) has also changed - larger monitors, different devices, et cetera. We tricked ourselves into thinking the canvas we use is static. But if we're honest, the web never had a fixed canvas.

Responsive design has changed our mindset but we're still tricking ourselves: desktop equals mouse, and phone equals touch. Desktop UI is different from mobile UI - or that's what we think. We envision desktop users as different from mobile. However, it's time to break free of these assumptions. We're thinking too binary-like.

## Four truths about Input
1. Input is exploding. In a very short period of time, we've gone from keyboard and mouse to touch, gestures, camera, voice control, and tons of other new sensors and capabilities added to our devices as new types of input.  And there's more on the way, like the Hololens (mixed reality content). It's not slowing down at all.
2. Input is a continuum. We've always had phones that keyboards or styluses. Then there are laptops with touchscreens. We have a continuum we're designing for and that means we can no longer make any assumptions based on screen size or form factor.
3. Input is undetectable. Whatever you may think, it currently isn't possible to reliably detect whether or not a device has a touch screen from within the browser. You can't detect a mouse or keyboard reliably either. Input is like Schrodingers cat: until we observe the user, we can't detect their input.
4. Input is transient. It can be added or removed. Knowing what input is used one moment tells you nothing about what will be used next.

## Adapting to input (7 recommendations)
1. Design for the largest target by default. Minimum control sizes are different from keyboard/mouse and touch first. Fitt's Law: the time to acquire a target is a function of the distance to and size of the target. The larger the target, the easier it is to select. Design things touch first, because that, right now, is the largest target.
2. Design for modes of interaction instead of input. You're designing for a user need, not for a specific form factor or input.
3. Make things accessible. Building accessibly increases the likelihood of support for future, unknown inputs. Cortana/Alexa seems super new, but its voice control technology has been around for a lot longer.
4. Design for multiple concurrent inputs. There are devices that allow you to use both touch and keyboard/mouse. Don't assume if one input is present that the person doesn't have access to other types of input.
5. Abstract baseline input. Instead of talking about tap or click, we need to start thinking about point and select. Our language may unintentionally reinforce the ideas we have right now about input. The new pointer events spec that normalizes touch, mouse and stylus so you can just write pointer events one time.
6. Progressively enhance input. When we've got the baseline taken care of, we can actually do cool stuff with input. Examples: the Warby Parker gyroscope, Chrome's Lightsaber Escape, Webcam Toy, speech recognition API, bluetooth, web beacons.. Don't rely on it as a baseline, but use it for progressive enhancement.
7. Make input part of your test plans. Start looking at ways to bring input in as a criteria. A device testing lab is perfect for this.

https://cloudfour.com/thinks/autofill-what-web-devs-should-know-but-dont/

http://alistapart.com/article/adapting-to-input

https://www.sitepoint.com/pointer-events-will-make-cross-browsers-touch-support-easy/

https://dev.opera.com/articles/media-features/

Who are we to judge which input is better? For many people, typing on a virtual keyboard is faster than on a physical keyboard. We need to learn to adapt and let go of the illusions that comfort us, and face the web as it really is.
