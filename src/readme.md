https://www.codementor.io/twitter530/i-ve-seen-heaven-and-it-s-written-in-javascript-dcc443lu4

## I've seen heaven. And it's written in JavaScript.

Published Oct 29, 2017Last updated Oct 30, 2017
I've seen heaven. And it's written in JavaScript.
Why React Native is the Future

I have a weird way of describing software. And you’ll either know what I mean, or you won’t. It’s sort of strange, but software interfaces feel like they have a weight. When I use an interface, it can feel heavy, or it can feel light. Neither is better than the other. It just sort of depends. Chrome is very light. Safari feels heavier. And Firefox feels the heaviest. It’s probably bullshit, but that’s the feeling I get.

One of the heaviest feeling experiences in my software development career has been using Swift in Xcode. Oh the pain. The delay. The Kanye-West compiler that never lets you finish. I’ve lived in this unwieldy world for the last several years, building applications the only way I knew how: raw, manual, single-platform code. Go native! Right?

When I learned about React Native, I was skeptic. Write code in JavaScript once and deploy native apps on both iOS and Android?—this has to suck. So I ignored it. And instead ended up writing two separate native apps, one in Swift for iOS, and the other in Java/Kotlin for Android. This was in addition to a web app written in JavaScript, and an Electron-based desktop app. (The app is an encrypted cross-platform notes app, so availability on every platform was key.)

This worked well enough for some time, but had its difficulties. I could manage writing the web app and iOS app, but I had no experience with Android whatsoever. In fact, I had never used an Android device my entire life for more than an hour. Luckily, a community contributor was happy to help in building the fundamentals, which allowed me to forego writing an app from scratch, and instead just maintaining it with incremental changes.

Any time a change needed to be made, or a feature added, I would need to journey into three separate code bases and write the same code, in three different languages. Being one person, this wasn’t always very efficient. It could take a week to make even the simplest cross-platform change. The result were apps that could never have nice things. For example, several users were asking for the ability to add a passcode and fingerprint lock to the application—a very reasonable request for a security-minded notes app. But the implementation of this was no triviality: first, a passcode setup interface in addition to an input interface was required. Then, encrypting offline user data with the passcode. Then, on mobile, specifying when the passcode or fingerprint should be requested (immediately or on app quit). The thought of writing all of that code in Swift, then Java, then JavaScript, was a nightmare. I couldn’t bring myself to do it.

There has to be a better way.

## Enter React Native

I had to describe the context and emotion behind what it felt to have to maintain separate codebases for an application, so that you know the elation I felt when I began using React Native. For the first week of writing native applications in Atom (!), my mouth was agape. I could not believe how easy it was. No Xcode, no Swift, instant reloading of changes, writing in the ever-easy to use JavaScript—I was in heaven. I would put the iOS simulator and Android emulator side-by-side as I was writing code, and spent half the time in utter disbelief that everything just worked. I never had to wonder, well, this looks good on iOS, I wonder if it’ll work well on Android? For the most part, if it works on one platform, it’ll work on both, with little adjustment.

The most beautiful part? I WAS REUSING ENTIRE CLASSES FROM MY WEB APP! I was able to copy complex classes involving models, controllers, and encryption logic wholesale with very little change. The entire sync engine of the app? Copied right from the web app. Encryption and decryption? From the web app. Models and relationships? From the web app.

I was so, so happy not to be writing all this stuff from scratch. Sync is hard, and encrypted sync is no easier. The web/desktop codebase was our flagship, tested product, and the confidence of being able to reuse those components was magnificent.

One of the hardest parts of building native applications using native IDEs is the user interface. On iOS, it is so painstakingly time-consuming to develop interfaces. You can do it through code, but it will involve a lot of code. And managing dynamic layout constraints with code is more hellish than most tasks. You could use the interface builder, but, you lose the fine-grained control and flexibility code gives you. And good luck committing and collaborating on Interface Builder changes in git.

In React Native, dynamic interfaces are a breeze. You use CSS-like syntax to build the the design of your dreams:

let containerStyles = {
  backgroundColor: “red”,
  display: “flex”,
  alignItems: “center”,
  width: “100%"
}

let childStyles = {
  fontSize: 14,
  color: “black”,
  fontWeight: “bold"
}

<View style={containerStyles}>
   <Text style={childStyles}>Hello, future.</Text>
</View>
This is the basis for building all interfaces in React Native. And it’s really as simple as it looks. And the bast part?

## THEMING.

Essentially, your entire interface is a bunch of JSON properties. You’ve probably already noticed it wouldn’t be very hard to pull a JSON style blob from a server or file and completely change the appearance of the app. So that’s exactly what I did:



Do you know how hard this would have been in native code? My mind aches just thinking about it.

## What's the catch?

During my journey through heaven, as I looked in every direction in utter amazement and wonder, I kept thinking, what’s the catch? It can’t be this easy to build native applications. It felt almost sinful.

Now, this is software, and a software development tool at that, so there is no such thing as perfect. React Native is still under active development, so you’ll experience some gotchas. My first few gotchas felt existential. “Shit! This is the end! I knew it. I knew it was too good to be true. This issue is going to completely blow up my project.” Luckily, there was no issue that couldn’t be solved.

For example, one of the more annoying issues I experienced was that the TextInput component of React Native just didn’t work well enough on Android for a notes app. The scrolling was laggy, and anytime you scrolled to read the note, it would automatically bring up the keyboard. Extremely frustrating. I tried for several days to hack my way around the issue by somehow manipulating the JavaScript code to prevent both issues. But absolutely nothing worked. I learned however that this is not the end of your project. It is the beginning.

React Native allows you to easily build native components for anything your heart desires. A native component or module means you can write interface and business logic using native Swift/Objective-C or Java/Kotlin and easily create a JavaScript interface for controlling those modules. In my case, I wrote a custom textview module in Java that made scrolling much smoother, and wouldn’t focus the input on scroll. This was straight up Java written in Android Studio. I imported it in JavaScript, added it to the view hierarchy, and boom, a beautifully scrolling text input in React Native. Problem solved.

I used native modules for other things too, including the encryption module (separate modules for iOS and Android) and the fingerprint authentication module.

## Should you use React Native?

Yes, yes, 100% yes. Even if you’re building a single-platform app, I would use React Native. It just feels like the better way to write apps. As new as Swift is, it feels ridiculously outdated and heavy compared to the nimbleness of writing apps in JavaScript. I really wish Apple focused on making it more accessible to write great applications, rather than introducing the most esoteric programming language I’ve encountered in some time. Xcode was built around Objective-C, and Swift still feels out of place inside.

I was able to re-use about 70-80% of the code from our web app in building the native mobile app. The rest is interface code that could not be re-used. I was even able to target lower versions of iOS and Android. Our original Swift Standard Notes app used the newest implementation of Core Data, so iOS 10 was required. The new React Native implementation works out of the box on iOS 8 and Android 5.

Want to see how a React Native app feels? You can download the finished product for iOS and Android. You can also check out the entire source code. If you have any questions on the React Native development process, please don’t hesitate to reach out on Twitter.

HN Submission/Discussion
react-native
mobile-development
mobile
JavaScript
Report
Enjoy this post? Give Mo Bitar a like if it's helpful.
3

1
SHARE
Mo Bitar
