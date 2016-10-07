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
* [Barbara Bermes: Cheat Sheet to a Lean website](#barbara)
* [Zell Liew: Building Responsive CSS Components](#zell)
* [Scott Helme: CSP STS PKP SRI ETC OMG WTF BBQ (Modern web security standards)](#scott)
* [Sarah Drasner: Functional Animation](#sarah)
* [Bruce Lawson: World-Wide Web, not Wealthy Western Web](#bruce)
* [Léonie Watson: Technologic (Human Afterall): Accessibility Mix](#leonie)


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

If the team's not contributing to meaningful experiences for the end-user, it's not very useful to talk about standards. Don't optimize for the perfect codebase, optimize for making an impact (for the end-user). If growing is something you want to do, understanding what you're trying to scale is the most important question. Think critically about your craft, standards, and culture. Embrace the crazy chaotic work that is frontending!

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

=========================================================================================================================================================================
<a name="barbara"></a>
# Barbara Bermes: Cheat Sheet to a Lean website

## Intro
Fast and scalable wins the race. Why should we care about performance? It's not so much about writing beautiful fast code, it's about the business and the end user. No one likes to wait. Waiting for slow pages to load is the biggest frustration users have. In general, websites have grown in the last several years, but they've also gotten faster. But still, data is expensive, and latency continues to exist. If users are disappointed in your website's performance, chances are they won't return.

One second delay = 11% fewer page views, 7% loss in conversion, 16% decrease in customer satisfaction.

## Shape a performance culture
It starts with the people who make decisions within your company. Make them aware about performance, and make them care about it. It's everyone's business, not just the developers. Don't be scared to say "no" when marketing wants to use terribly slow ads, and let them know why you're saying no. Celebrate success (website smaller and loading faster? Party!). See Etsy's performance hero idea, and their quarterly public performance report.

https://twitter.com/lara_hogan/status/578295642302316546

https://codeascraft.com/category/performance/

## Performance = perception and respect
The greater respect you show your users, the better it makes them feel. How long does it take your user to start interacting with your page? Treat speed as a feature. Optimize from the user's perspective: get some real user numbers, figure out what their ISP speeds are like. Your company's internet is not representative.

Measure first, then optimize. Establish a performance budget - set a baseline on how fast a website should be. Compare with competitors. Barbara recommends several things to look at: speed index (the average time at which visible parts of the page are displayed), Google's Page Speed (85+ is good), Speedcurve, how the browser renders a page. Determine your critical rendering path. It's very important to know how the browser renders, in what order, so you can decide what you should display first and how you should display it.

Reduce HTTP requests: every request costs money. Concatenate where applicable, don't blindly use JS libraries/frameworks, use image sprites and for small images, consider using the data URI technique to remove additional HTTP requests.

https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/

Summary: measure and monitor constantly. Automate all the things. "Browsing should be as simple and fast as turning a page in a magazine" - Larry Page.

=========================================================================================================================================================================
<a name="zell"></a>
# Zell Liew: Building Responsive CSS Components

## Intro
How do we make responsive components without hacky, ugly code? The moment things get messy, we're doing something wrong. We want modular and scalable components. What do these two buzzwords mean? The dictionary definition of modularity: composed of standardized units for easy construction. Kind of like Lego blocks. In web terms, a component can be a grid item, a sidebar, a header, content. We look at the following when we look at modularity:
- Markup structure
- CSS selectors
- Naming convention
- DRY

Think BEM, SMACSS, Atomic Design. It's all about communicating with your team and deciding on standards and a modular structure.

Scalability: we're not really talking about this on the web. Dictionary definition: to adjust in amount according to a fixed scale or proportion. It's quite easy to build a scalable component. But how much do we need to actually scale? To infinity and beyond? Do we need giant buttons? No, it's all proportional: upwards and downwards.

Components are not in a vacuum: you have to take into account the rest of the page.

## Design principles
Principe of repetition: repetition breeds familiarity. One dot attracts attention, with a pattern of dots you don't know where to look at, you've shifted the focus.
- Limit your number of font sizes, and repeat them. We don't need an infinite amount of scale - using the same component in three different scales is better.
- Keep whitespace consistent.

Keep visual consistency.
Keep margin and padding consistent.

Why `rem` and not `em`? An `em` is a unit of typography equal to the currently specified point-size. It's kind of hard to wrap our heads around. `rem` is equal to the unit typography size. `em` is like a local variable, `rem` is like a global variable. Global variables are usually seen as bad, but for consistent padding/margin and typography, it's very much acceptable. Size in `em` if the property scales according to its font-size. Size everything else in `rem`.

The real problem comes in with breakpoints, media queries and scaling. We tend to write a lot of media queries, which is where things get complicated. We're repeating ourselves. Abstract as much as possible. A solution is element queries.

https://www.sitepoint.com/beyond-media-queries-time-get-elemental/

https://www.smashingmagazine.com/2016/07/how-i-ended-up-with-element-queries-and-how-you-can-use-them-today/

http://elementqueries.com/

> Element queries are a new way of thinking about responsive web design where the responsive conditions apply to elements on the page instead of the width or height of the browser. Unlike CSS `@media` queries, `@element` Queries are aware of more than just the width and height of the browser, you can write responsive conditions for a number of different situations like how many characters of text or child elements an element contains. Another concept that element queries brings to CSS is the idea of ‘scoping’ your styles to one element in the same way that JavaScript functions define a new scope for the variables they contain. - http://elementqueries.com/

However, this isn't valid CSS (yet) and you'll need JS polyfills for this.

https://zellwk.com/blog/changing-modular-scale/

## Scaling summary
- Determine component area maps
- Determine breakpoints and changes in styles
- Determine units for CSS properties
- Communication is key: scaling isn't so hard when you talk about it with your team
- Handle complex variations with mixins or element queries, depending on the stack you're using
- Don't over-engineer for the sake of over-engineering

=========================================================================================================================================================================
<a name="scott"></a>
# Scott Helme: CSP STS PKP SRI ETC OMG WTF BBQ (Modern web security standards)

## Intro
We don't educate people enough on security standards. We're good at creating security standards, but not good at promoting them. Security is a hard sell. How do we incentivize security?

HTTP/2 comes with performance improvements (which people love), but only works over HTTPS. Other cool features, like Geolocation, getUserMedia(), AppCache, Brotli compression, can only be used over HTTPS. If you want to do all these cool things, you need to use HTTPS. You also get an SEO boost if you serve your site over a secure connection.

Historically, we only focused on securing our servers. But the browser has also taken on responsibilities. We're bringing the browser on our team as well, so we can secure all the things! Browser support is pretty good - plus, if it doesn't support them, it'll just ignore them, so people with older browsers can still use your website.

## Security headers
We've got tons of security headers. CSP, PKP, STS are the most important right now.

## Content security policy
Built and created to stop content injection (XSS). Meaning someone has managed to get a malicious script tag in our page. CSP gives us the power to stop this. CSP is just a HTTP ID. The value of the header is the policy enforcing on that particular page. It has several fetch directives. A basic policy:

`Content-Security-Policy: default-src 'self' example.com`

It's quite a bit strong though - what about external CDNs? You can also specify `script-src` for say, Cloudflare and Google. This whitelists those domains.

A nice thing about CSPs comes with mixed-content warnings. If you serve your site over HTTPS but load a font over HTTP, your browser will warn you or even refuse to load insecure content unless you explicitly allow it. This gives a pretty bad user experience.

Cool examples of mixed content errors:

https://mixed-script.badssl.com

https://mixed.badssl.com

An interesting directive is `block-all-mixed-content`. It blocks anything loaded over http without notice. The user won't get any warnings, but you'll lose the mixed content. Another interesting directive is `upgrade-insecure-requests`, because it won't block http, it'll change http to https. So you're avoiding the mixed content warning. Potential issue is that the source doesn't have https enabled.

https://report-uri.io/ 

http://securityheaders.io/

CSP is available in report only mode, so you can test without breaking anything.

## Strict transport security
Fixes one of the big problems on the web. We default to insecure protocols (i.e. you type in http://twitter.com). This header tells you "no, we're using https" and sends you to https://twitter.com. Three directive: `max-age`, `includeSubDomains` and `preload`. Max-age is the only required directive (how long to cache policy). If the user types in http, the browser will override it with https for the max-age you set. This adds to performance, less redirects = more better!

## Public key pinning
Quite a difficult topic, used for ecommerce and finance websites. It fixes rogue certificates. The browsers checks three things of a certificate: the name of the site, the validity period, and if the CA is trusted. Unfortunately any CA can issue a cert. If the CA has been compromised, someone could get a hold of your cert and impersonate your website. HPKP helps resolve this.

> The Public Key Pinning Extension for HTTP (HPKP) is a security feature that tells a web client to associate a specific cryptographic public key with a certain web server to prevent MITM attacks with forged certificates. - https://developer.mozilla.org/en-US/docs/Web/Security/Public_Key_Pinning

Directives: pin-sha256, max-age. You must have a minimum of two pins, one is your current key, the other is an offline backup you can keep safe.

https://scotthelme.co.uk/guidance-on-setting-up-hpkp/

What if you're using CDNs? They can get hacked or tampered with. SRI to the rescue:

> Subresource Integrity (SRI) is a security feature that enables browsers to verify that files they fetch (for example, from a CDN) are delivered without unexpected manipulation. It works by allowing you to provide a cryptographic hash that a fetched file must match. - https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity

=========================================================================================================================================================================
<a name="sarah"></a>
# Sarah Drasner: Functional Animation

## Intro
When visiting a website, your eyes are never static. People try to make a mental map of what's around them. Why is that important regarding animation? Animation tends to get a bad rap - you're biologically trained to notice things in motion. If something's moving on the page, your eye is drawn to that. So when animation as a tool is used improperly, it's very distracting. Animation as a tool can be used in different ways: invisible animation versus immersive animation.


## Invisible Animation aka UX Choreography
If state changes on your website, it's nice to join the previous and the new state. Animation can help here. The space between doing one task and another must not be disruptive. By understanding spacial awareness we can avoid cognitive leaks for users. We want to give users a sense of space.

- Modals break context (brute force UX: I want you to pay attention to this, so I'm going to shove it in your face)
- Adhering to your branding means motion solves the problem for your users. Good animation branding means being consistent.
- You might want to think about toggling animation on and off, especially when they're large and immersive.
- Empower the user with animation.
- Animation needs to be built in the core of the application - you wouldn't add colors later in the development stage, you need to take animation in account sooner.
- Users like custom loaders, because it shows you care about them.
- Opacity and transforms are very performant.

## Immersive animation: when you want people to pay attention to your animation.
You can use the (virtual) DOM, or HTML5 Canvas. The first is great for SVG that is resolution independent, and it's easier to debug. However, it tanks with a lot of objects. HTML5 Canvas does not have this drawback. It's great for impressive 3D work. The cons are it's harder to make accesible. Neither is is resolution independent out of the box.

People don't realize how good SVGs are. They're very well supported, plus you can always use fallbacks if you have to. They're crispon display, and there are less HTTP requests to handle. It's easily scalable for responsive, and it has a small filesize if you design for performance. SVG is good for a lot of things we used to use Flash for: it's interactive, immersive, narrative. Greensock is a powerful animation API. It solves cross-browser inconsistencies.

=========================================================================================================================================================================

<a name="bruce"></a>
# Bruce Lawson: World-Wide Web, not Wealthy Western Web

![](https://media.giphy.com/media/LXONhtCmN32YU/giphy.gif)

You can't predict the unpredictable, but Asia and Africa are huge upcoming markets. It's quite likely your new customers will be from these markets. These people are usually on older devices, experiencing lots of network problems. Nevertheless, SEA is the fastest growing internet market in the world. It's a young population too, very internet savvy. And when they come online, they use a mobile device and they're mobile only. These mobile devices are not the newest devices such as the iPhone 7 - they're mostly lower end. However, they want to consume the same goods and services as people in the western world.

In browser-land, developers are working on making the web work on lower-spec devices. People in emerging markets have cheaper phones with not a lot of storage, so native apps aren't very handy -- hence why browser vendors are pushing PWAs. People are unlikely to make room for native apps by deleting videos/photos. Besides storage, people in emerging markets are very data sensitive. PWAs do not have to be downloaded, which saves a lot of data. All a user downloads is a manifest file. On flaky networks, a PWA is a lot more reliable than a native app. They live on the server, so there is no update distribution lag. They require no app store, and are normal websites. They are searchable, indexable and work offline.

https://pwa.rocks

The technology of how things work offline is the service worker. Until now, if your web browser is disconnected from the internet there's no functionality, but with a service worker sitting in between you can give a meaningful offline experience. They also give push notifications and background sync.

Using responsive images well you can save on average bytes per page. Not everyone's got great internet. If bloated images are using up people's data plan, they'll lose money.

A lot of people choose to use proxy browsers: Opera Mini, Silk, Puffin, UCWEB, Chrome (Data Reduced), Opera Turbo. Opera Mini is made for feature phones because they do not have the power to render mobile web pages. It's quite a thin client, and all the hard work happens on the server (it's called Thor and is in Iceland). Thor has a hammer, and squishes down (i.e. compress) your website. This decreases average load time and page size. Mini uses less battery and data. Battery matters too - power is in short supply.

Funnily enough, the servers are located outside these emerging markets. That's because the local networks are very much overloaded and flaky. Requesting a site in Cape Town will send your request all the way to the US, because that's more reliable than SA's networks.

## Designing for emerging markets
- Don't write somebody's name in red in Thailand - it means they're dead!
- Millions of people in Indonesia have only one name. Requiring a surname disrespects them. https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/
- Dealing with a proxy browser means everything happens on a server. Everything needs user interaction, everything needs a server roundtrip, and JS on page load runs for 5 seconds max.
- JS only APIs don't work.
- No fancy rounded CSS corners and gradients. Design will not always be preserved. Which is fine: people want the content.
- No animations: they only show the first frame. Animations take up CPU cycles and drain battery.
- No web fonts: they can be huge downloads and on small monochrome screens, they don't look very well.

Thus: progressive enhancement is key! Make sure your site works without CSS and JS.

## Demand side problems
**Bruce's Law of Smartness™: It doesn't matter how smart your phone is if your network is dumb**

The market for smartphones is declining. The average entry level smartphone is still too expensive, even if they're only 60 dollars. It's not just about affordability and networks though: a lack of awareness, digital illiteracy, and lack of locally relevant content is considered the most important barrier to internet adoption.

**Windows XP is used by 9% of global computer users. To ignore these people is to ignore an entire market. Making the internet globally accessible should be a major priority.**

The web empowers women by enabling them to work from home. However, internet usage of women in emerging markets is still quite low.

## What can we do?
- Progressive enhancement! Clunky is fine.
- Feature detection
- Compress images, use responsive images
- Consider PWAs

=========================================================================================================================================================================

<a name="leonie"></a>
# Léonie Watson: Technologic (Human Afterall): Accessibility mix

## Intro
"Buy it, use it, break it, fix it" encapsulates accessibility. You can get it "for free" by using good semantics. For example, with a link, you can include a role, an accessible name, and a state. The same is true for an image: a role (image) and an accessible name (alt tag).

## Semantics
Divs and spans are neutral, they have no role, purpose or state. Another thing you get for free with HTML is keyboard focus: it has interactive elements that receive focus by using the tab key, including: link, button, form fields. The tab order follows the DOM order of interactive elements. You also get interactive elements when using HTML in its native sense.

Besides a DOM tree, there's also an accessibility tree. This is hierarchical as well. They're separate, but closely related. Assistive technologies listen for changes in the accessibility tree and respond accordingly.

ARIA: accessible rich internet applications. 30+ roles including dialog, slider, toolbar, tree, tablist, all fairly typical software UI components. Allows you to add accessible names and descriptions. An ARIA element can have 9 states (checked, pressed, hidden, et cetera). ARIA is very useful when it comes to screen readers, but you'll still need to think about other assistive technologies.

Add focus by using the `tabindex` attribute and JS.

What was very helpful for accessibility was the separation of document structure and design - when CSS was introduced, things got a little better. Flexbox poses some problems, though:

> CSS Flexbox can create a disconnect between the DOM order and visual presentation of content, causing keyboard navigation to break. For this reason, the CSS Flexible Box Layout module warns against resequencing content logic, but asking authors not to use flexbox in this way seems illogical in itself. - http://tink.uk/flexbox-the-keyboard-navigation-disconnect/.

`tabindex` can partially fix this, by taking control of the keyboard sequence, but this is really hard because you'll have to resequence everything on your page. The `aria-flowto` attribute looks like another solution, but it's not viable:

> The first reason aria-flowto does not solve the flexbox disconnect, is because it complicates rather than simplifies the problem. It introduces a third mode of navigation, and one that is only applicable to screen reader users (who must use specific keyboard commands to benefit from it). The second problem is that aria-flowto has extremely poor accessibility support. Of the various popular browser and screen reader combinations, only Jaws with Firefox, or Narrator with Edge and IE, has support for aria-flowto. http://tink.uk/flexbox-the-keyboard-navigation-disconnect/.

There is however, a Firefox bug that realigns the tab order to match the visual order.

## Tools, resources
http://tink.uk/using-the-aria-controls-attribute/

https://tenon.io/ for use with build tools

https://github.com/reactjs/react-a11y

https://facebook.github.io/react-native/docs/accessibility.html

https://docs.angularjs.org/api/ngAria

http://www.ssbbartgroup.com/blog/how-the-w3c-text-alternative-computation-works/

**Test it yourself! Abandon your mouse, turn on a screen reader, zoom in and out.**
**It doesn't have to be perfect, it has to be just a little bit better than yesterday.**
