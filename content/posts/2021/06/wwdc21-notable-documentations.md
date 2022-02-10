---
title: "WWDC’21: Notable Documentations"
date: "2021-06-08"
categories: 
  - "post"
---

* * *

Most users don’t follow the WWDC beyond the Keynote session. The trove of recorded sessions are thought to be relevant to only coders, not to mention the developer documentations. However, there are actually many summary articles that are easy to follow and full of tasteful tidbits, and even the rest of us can find interesting to read. If you have ever wondered how sites like MacStories and Ars Techinica can dig out so many details in their reviews of the annual OS releases, here lies the answer.

The following is an inconclusive list of such approachable documentations updated during WWDC’21 that I’ve discovered. I may (or may not, dependent on my time available) update the list with further readings. For an official list of new technologies across the Apple platforms, see [New Technologies WWDC 2021](https://developer.apple.com/documentation/New-Technologies-WWDC-2021).

* * *

### [ManagedSettings](https://developer.apple.com/documentation/ManagedSettings)

Managed Settings provides a privacy-preserving way for users to restrict access to certain settings and features on their devices. With the user’s permission, your app can limit media showings, restrict app purchases, lock passcode settings, and configure other device behavior.

![A web diagram consisting of three arrows to the left, below and right with a settings icon in the center. On the left side is a yield sign toward 18+ content. To the right is a restrict sign toward app store content, and below is a lock sign toward iPhone passcode.](https://docs-assets.developer.apple.com/published/acc1e9abeed55948d8f76d19856eac54/10200/managed-settings-overview@2x.png)

Managed Settings works together with [ManagedSettingsUI](https://developer.apple.com/documentation/ManagedSettingsUI), [DeviceActivity](https://developer.apple.com/documentation/DeviceActivity), and [FamilyControls](https://developer.apple.com/documentation/FamilyControls) to allow your app to restrict, authorize, and monitor device usage.

### [Audio Graphs](https://developer.apple.com/documentation/accessibility/audio_graphs)

Use the Audio Graphs API to provide all the information that VoiceOver needs to construct an audible representation of the data in your charts and graphs, giving people who are blind or have low vision access to valuable data insights.

![Conceptual illustration of an audio graph that shows data points modulating in pitch along the Y-axis as a slider moves in time along the X-axis. ](https://docs-assets.developer.apple.com/published/b1012142b1/rendered2x-1621039087.png)

An _audio graph_ turns the data in your chart into an audible representation by encoding the data on each axis as audio. Typically, the audio graph represents the X-axis as time, and the Y-axis as pitch. For example, an audible representation of a scatter plot that shows a linear downward trend might be a series of individual tones descending in pitch over time. An audible representation of a stock chart might be a single continuous tone with a pitch that modulates up or down with the stock price (Y-axis) as the audio plays over time (X-axis).

### [Sound Analysis](https://developer.apple.com/documentation/soundanalysis)

- Identify specific sounds, such as laughter or applause, in your app by creating an `SNClassifySoundRequest` to analyze an audio file or stream. Sound requests can identify over 300 sounds.
- Alternatively, you identify a custom set of sounds by providing the sound request with a custom Core ML model. You train a custom sound classification model by creating an `MLSoundClassifier` with audio data in Create ML.

#### [Discover built-in sound classification in SoundAnalysis](https://developer.apple.com/videos/play/wwdc2021/10036/)

Mentioned in [WWDC 2021: More cowbell](https://sixcolors.com/post/2021/06/wwdc-2021-more-cowbell/) by Jason Snell

- Presenter Jon Huang of Apple’s audio team demonstrates a built-in audio recognition model
    - that allows his Mac to dynamically recognize different sounds as they occur around it:
    - talking, music, elements of the music like vocals and guitars
- Kevin Durand \[then\] uses Shortcuts on a Mac running macOS Monterey to process a folder full of movies,
    - looking for any that contain the sound of a cowbell—and then clipping out that movie and saving it to a new location.
    - Shortcuts doesn’t have audio classification built into it (yet?),
    - but Durand has built a simple app using Apple’s new SoundAnalysis APIs
        - that identifies whether a particular sound is found inside a particular file.
    - a good example of what Shortcuts enables on the Mac

### [ShazamKit](https://developer.apple.com/documentation/shazamkit)

- The process
    - ShazamKit uses the unique acoustic _signature_ of an audio recording to find a match.
    - ShazamKit generates a _reference signature_ for each searchable full audio recording.
    - A _catalog_ stores the reference signatures and their associated metadata, or media items.
    - Searching for a match compares a _query signature_, which ShazamKit generates for captured audio, with the reference signatures in the catalog.
- You can create a custom catalog with your own reference signatures and their associated metadata.
    - a virtual learning app
        - reference signatures = teaching videos
        - associated metadata = the timecodes for questions
        - offer choices for a possible answer for a matched question; updates with fwd. and bwd.

### [Nearby Interaction](https://developer.apple.com/documentation/nearbyinteraction)

#### [Nearby Interactions with U1 - Apple Developer](https://developer.apple.com/nearby-interaction/)

- Accessory manufacturers: Use the Nearby Interaction accessory protocol and an Apple-approved UWB solution to manufacture accessories that interact with U1 in supported Apple products. Get started by previewing the [specifications](https://developer.apple.com/nearby-interaction/specification/).
- Chipset manufacturers: Provide Apple U1 interoperability with your UWB solution. Chipset manufacturers who are interested should join the MFi Program to access the necessary [technical specifications and resources](https://mfi.apple.com/).

#### Interact with Apple Watch

The U1 chip-capable Apple Watch running watchOS 8 supports Nearby Interaction sessions. Apps share discovery tokens to begin an interaction session. The [Multipeer Connectivity](https://developer.apple.com/documentation/multipeerconnectivity) framework provides a way for apps to share discovery tokens over a local network on iOS; on watchOS, apps share discovery tokens using a custom server, [Core Bluetooth](https://developer.apple.com/documentation/corebluetooth), LAN (TCP/UDP), or [Watch Connectivity](https://developer.apple.com/documentation/watchconnectivity).

The system backgrounds the foreground Watch app **after two minutes**; when the system backgrounds an app, Nearby Interaction sessions suspend.

Nearby Interaction on iOS provides a peer device’s distance and direction, whereas Nearby Interaction **on watchOS provides only a peer device's distance**.

#### Interact with Third-Party Devices

In iOS 15, iPhones can interact with third-party accessories that you partner with or develop with a U1-compatible UWB chip.

### [Increasing the Visibility of Widgets in Smart Stacks](https://developer.apple.com/documentation/WidgetKit/Widget-Suggestions-In-Smart-Stacks)

When users configure Smart Stacks, they have two options for surfacing widgets:

1. Smart Rotate **automatically rotates widgets** to the top of the stack when they have timely, relevant information to show.
2. Widget Suggestions **automatically suggest widgets** that the user doesn’t already have in their stack, perhaps exposing them to widgets they don’t even know exist.

- Your app **donates intents** and **identifies relevant shortcuts** to provide a _signal_ about **how** the user uses your app, **when** they use it, and **what** is most relevant to them.
- While intent donations using `INInteraction` give Smart Stacks insight into the past user behavior, `INRelevantShortcut` informs future suggestions.
    - The app conveys this information by specifying a _relevance provider_ as part of the INRelevantShortcut.
    - Relevance providers determine when a shortcut is relevant, such as at a specific time of day: `INDateRelevanceProvider`

### [Delivering an Enhanced Privacy Experience in Your Photos App](https://developer.apple.com/documentation/photokit/delivering_an_enhanced_privacy_experience_in_your_photos_app)

- In iOS 15.0 and later, you can present the limited-library picker with a _callback_.
    - The callback provides a list of local identifiers that reflect the user’s new selections.
    - This method only works when the user enables limited-library mode.
- To monitor changes to the user’s limited-library selection, use the standard change observer API as described in Observing Changes in the Photo Library.
- Register your app to receive notifications and update your user interface as the system notifies it of state changes.

### [About Continuous Integration and Delivery with Xcode Cloud](https://developer.apple.com/documentation/Xcode/About-Continuous-Integration-and-Delivery-with-Xcode-Cloud)

- Xcode Cloud is a CI/CD system that
    - uses Git for source control and
    - provides you with an integrated system that
        - ensures the quality and stability of your codebase.
        - It also helps you publish apps efficiently.
- Xcode supports source control with Git.
    - By using source control, you improve your project’s quality by tracking and reviewing code changes.
- The Importance of Automated Building and Testing
    - A typical development process starts with making changes to your code, building the project, and running your app in the Simulator or on a test device.
        - take a significant amount of your time.
        - especially true for complex apps or frameworks
    - With Xcode Cloud, however, you can build, run, and test your project on multiple simulated devices in less time than you can traditionally
    - After verifying a change, Xcode Cloud automatically notifies you about the result via email.
- Continuous Delivery
    - The flip side to continuous integration (CI) is continuous delivery (CD).
    - When Xcode Cloud verifies a change to your code (CI), it can
        - automatically deliver (CD) a new version of your app to testers with TestFlight, or
        - make a new version available for release in the App Store.
        - upload the exported app archive or a framework to your own server.
- Collaborative Software Development with Xcode Cloud
    - support for pull requests (PRs): When you create a PR, you inform your team that a change is ready for review, and you and your team can take a look at each other’s code changes, and provide and address feedback before merging branches.
    - In Xcode 13 and later, you can create, view, and comment on PRs, and merge changes into your codebase if you host your Git repository with Bitbucket Server, GitHub, or GitHub Enterprise.
    - You can also configure Xcode Cloud to detect new PRs, or changes to an existing PR.

### [Safari Web Extensions](https://developer.apple.com/documentation/safariservices/safari_web_extensions)

Safari web extensions are available in macOS 11 and later, macOS 10.14.6 or 10.15.6 with Safari 14 installed, and iOS 15 and later.

### [Designing Your App for the Always On State](https://developer.apple.com/documentation/watchkit/designing_your_app_for_the_always_on_state)

- watchOS 8 expands Always On to include your apps.
- Even though your app is inactive or running in the background,
    - the system continues to update and monitor many of the user interface elements.
    - any controls in the user interface remain interactive.
- Apps compiled for watchOS 8 and later have Always On enabled by default.
    - Always On isn’t available on Apple Watch SE or Apple Watch Series 4 and earlier; the screen turns off when the app transitions to the background or inactive states.
- Understand Frontmost App Behavior
    - By default, when the user lowers their wrist or stops interacting with their watch, your app transitions to the **inactive state**.
    - The system continues to display your app’s user interface as long as your app remains **the frontmost app** (usually **two minutes**) before transitioning to the background and becoming **suspended**.
    - If the user **dismisses** the app (for example, by pressing the crown or by covering the screen), the app transitions immediately to the background and doesn’t become the frontmost app.
    - Users can set the amount of time that apps remains the frontmost app by changing the settings at Settings > General > Wake Screen > Return to Clock.
        - They can also specify a **custom time** for individual apps from the Wake Screen.
        - In WatchOS 8 and later, apps can remain in the frontmost app state for a **maximum of 1 hour**.
    - When the app is inactive, the user interface doesn’t update by default. However, you can use a `TimelineView` to schedule periodic updates.
- Update the Display During Background Sessions
    - Unlike frontmost apps, apps running a background session can continue to update their user interface;
        - however, to save battery life, the system reduces the update frequency.
    - For the best UX,
        - pause any animation and show the final state (or a good static image), and
        - remove any subsecond updates.
- Hide Sensitive Information
    - Add the `privacySensitive(_:)` **view modifier** to blur out specific user interface elements during Always On.
    - Or access the `redactionReasons` environment variable.
        - If \[this variable contains the `privacy` value.\], eliminate or obscure any sensitive data.
    - Always hide any highly sensitive information, such as financial information or health data.
        - If the user has any concerns, they can disable Always On on a per-app basis.
- Customize the Reduced Luminance Appearance
    - The system determines the screen’s overall luminance by comparing the ratio of lit pixels to dark pixels.
    - It then reduces the overall brightness to an appropriate level.
    - Many system controls also automatically update their appearance during Always On.
    - You can customize the appearance during Always On to highlight glanceable, important information in your user interface.
    - To customize your interface, use the `isLuminanceReduced` environment variable.

### [Accessing the Camera While Multitasking](https://developer.apple.com/documentation/avfoundation/cameras_and_media_capture/accessing_the_camera_while_multitasking)

- **Starting with iOS 13.5**, you can use the new Multitasking Camera Access Entitlement to let your app continue using the camera when Multitasking.
    - This scenario occurs in both Split View and Slide Over modes.
- In **iOS 15.0 or later**, this behavior **extends to Picture in Picture** mode using AVKit’s new API.
- Respond to System Pressure
    - Multitasking introduces the possibility of performance degradation; Increased device temperature and power usage can lead to frame drops or poor capture quality.
    - Monitor\[\] the `systemPressureState` property on `AVCaptureDevice`
        - When the pressure reaches excessive levels, the capture system shuts down and emits an `AVCaptureSessionWasInterrupted` notification.
        - Apps reduce their footprint on the system by lowering the frame rate or requesting lower-resolution, binned, or non-HDR formats.
- Observe Capture Session Notifications
    - The system only allows **one** app to use the device’s camera at a given time.
    - Prepare your app to respond when another app starts using the camera
        - observe two notifications: `AVCaptureSessionWasInterrupted` and `AVCaptureSessionInterruptionEnded`.
        - The notification object’s user information dictionary contains **the reason for an interruption**, \[which\] lets you configure your user interface as your camera access changes.

### [StoreKit - Apple Developer](https://developer.apple.com/storekit/)

StoreKit 2 introduces modern Swift-based APIs that make it easier than ever to deliver high-quality in-app purchase experiences.

- Simple and secure transactions: In StoreKit 2, transactions are cryptographically signed by the App Store in JSON Web Signature format for increased security and easier parsing of transaction information. And StoreKit 2 automatically makes up-to-date transactions available to your app, whether a user launches it for the first time or downloads it on another device.
- Customer support: let users request refunds and manage their subscriptions from within your app; confirming a user’s purchase details during a customer support call and extending the renewal date

#### [Choosing a StoreKit API for In-App Purchase](https://developer.apple.com/documentation/storekit/choosing_a_storekit_api_for_in-app_purchase)

The StoreKit framework provides two APIs for implementing a store in your app and offering in-app purchases:

- [In-App Purchase](https://developer.apple.com/documentation/storekit/in-app_purchase), a Swift-based API that provides Apple-signed transactions in JSON Web Signature (JWS) format, available starting in iOS 15, macOS 12, tvOS 15, and watchOS 8.
- [Original API for In-App Purchase](https://developer.apple.com/documentation/storekit/original_api_for_in-app_purchase), an API that provides transaction information using App Store receipts, available starting in iOS 3, macOS 10.7, tvOS 9, and watchOS 6.2.

Both APIs provide access to your data in the App Store, such as your configured in-app purchases and transaction information for your customers. They also provide the same user experience with the App Store for your customers. In-app purchases that users make using either API are fully available to both APIs.

#### [beginRefundRequest(in:)](https://developer.apple.com/documentation/storekit/transaction/3803220-beginrefundrequest)

\[Revealing that the Refund API doesn't let you programmatically issue a refund to your customers. It merely lets you show a sheet to customers, so they can request a refund from Apple. They hear back within 48 hrs. See @jakemor’s [tweet](https://twitter.com/jakemor/status/1402047383882637314)\]

- When you call this function, the system displays a refund sheet with the customer’s purchase details and list of reason codes for the customer to choose from.
- The App Store takes up to 48 hours to either approve or deny a refund.

### [SF Symbols - Apple Developer](https://developer.apple.com/sf-symbols/)

- \[Notable features\]
    - 600+ new symbols
    - Enhanced color customization
        - Hierarchical rendering adds depth and emphasis to symbols using a single tint color with multiple levels of opacity.
        - Palette rendering allows symbols to be customized with multiple contrasting colors.
        - And Multicolor rendering provides intrinsic color across hundreds of symbols.
    - Configure, preview, copy, paste
        - Symbols can be previewed using adaptive Apple platform colors and custom colors on Light and Dark backgrounds.
        - symbols can now be copied as images with color annotations and pasted in design tools.
    - Improved support for custom symbols: Custom symbols can now be imported, organized, and annotated with layers to support Hierarchical, Palette, and Multicolor rendering.

See also:

[WWDC 2021: For SF Symbols, Cyan is the new Teal – Six Colors](https://sixcolors.com/post/2021/06/wwdc-2021-for-sf-symbols-cyan-is-the-new-teal/)

#### [SF Symbols - SF Symbols - Human Interface Guidelines - Apple Developer](https://developer.apple.com/design/human-interface-guidelines/sf-symbols/overview/)

- Colors
- SF Symbols 3 provides four rendering modes that enable multiple options when applying color to symbols.
- SF Symbols 3 organizes a symbol’s paths into distinct layers
    - e.g.: cloud.sun.rain.fill = cloud + sun & rays + raindrop
    - annotating: assign a specific color/level to each layer in a symbol
- Rendering modes: monochrome, hierarchical (1 color with varying opacity), palette (2+ contrasting colors), and multicolor
- Weights and Scales: small, medium (the default), and large.
- Variants
- outline, fill, slash, and enclosed
    - variants for specific languages
- Creating Custom Symbols
- export a symbol that’s similar to the design you want, then use a vector-editing tool like Sketch or Illustrator to modify it.
- When you export a 3.0 template to create a custom symbol, you can choose between _static_ or _variable_ (i.e., a master template) setups
- When rendering a symbol, the system **adheres to the Z order of its layers**, so paths in the top layer may occlude paths in the bottom layers where they overlap.

### [Secure login with iCloud Keychain verification codes - WWDC 2021 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2021/10105/)

- New in iOS 15 and macOS Monterey, we've built time-based verification code generators into iCloud Keychain Password Manager
- the basics: looking up and copying codes to use on this device or another device
    - When you add a special link or a button to your TOTP setup pages, someone using iOS 15 or macOS Monterey will be able to set up a new verification code on the same device with just a couple taps
    - verification codes are synced and securely backed up with iCloud Keychain.
- iCloud Keychain uses `otpauth:` URLs to suggest an account to add the verification code to.
    - These URLs contain all of the information required to set up a code generator, including
        - the base32-encoded secret key,
        - the number of digits in each code,
        - the period of time that each code is valid for, and
        - an issuer field that you should set to your domain name.
    - You can link directly to the iCloud Keychain Password Manager by prefixing the URL with "apple-".
- How to implement a link
    - On web pages: take this apple- otpauth: URL and put it in an anchor tag
    - In apps: create a link by adding the "link" attribute to an NSAttributedString that you assign to a textView's attributedString property, or open the URL in response to a button tap
- If Safari determines that the QR code contains an otpauth: URL, it will offer to set up the code generator in the context menu for the QR code image.
    - Annotate username, password, verification code fields with content types
- A step beyond any of these is to get rid of passwords altogether.
    - The WebAuthentication standard, or "WebAuthn," does exactly this by using public key cryptography
    - iOS 15 and macOS Monterey contain a preview of this technology that offers a usable replacement for passwords.
- verification codes delivered over SMS

### [Meet TestFlight on Mac - WWDC 2021 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2021/10170/)

- To make it easy to recognize it as a beta app, we show a yellow dot next to the app name in the Dock, in Launchpad, and as a Beta Application in Finder.
- Native Mac apps require a provisioning profile to be distributed with TestFlight on Mac.
    - You can create groups to manage testers and distribute each one, very similar to iOS or tvOS.
- iOS apps on Apple Silicon Macs
    - For each tester group, you can control the TestFlight availability. When this is disabled, all iOS builds from that group will stop being available on Mac
- You can now create multiple internal groups similar to external groups. You can also configure distribution of builds and collection of feedback per internal group.
- Xcode Cloud integrates with TestFlight and provides a seamless experience to automatically build, test, and distribute your apps.

### [Build Mail app extensions - WWDC 2021 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2021/10168/)

- Like other app extensions, \[Mail app exts.\]
    - can be in any properly signed Mac app,
    - can be bundled in your existing apps, and
    - can also be distributed in the App Store
- Plug-ins will stop functioning in a future macOS release.
- 4 new ways you can extend Mail's user experience
    - Compose
    - Action ext
    - Content blocking
    - Message security
- Eg. Big Secrecy Extension
    - A button on toolbar
    - an icon indicating that an extension performed an action on a message
- Compose ext.
    - Capabilities
        - Annotate recipient email addresses
        - Present view controller
        - Set additional headers
        - Validate message before sending
    - Steps to create
        - Select the new Mail Extension template
        - Choose a type and capabilities
        - In the Info.plist, specify an icon and a descriptive tooltip in the MEComposeSession dictionary.
    - How does the API works
        - Mail creates a unique MEComposeSession instance for every Mail compose window.
        - It has a MEMessage property that exposes various details of the message being edited
- Action ext
    - Capabilities
        - modify read status and flags of incoming messages,
        - move messages to system mailboxes such as Junk, Trash or Archive, or
        - apply colors to messages
    - Mechanism
        - Mail calls your handler's decideAction for message for every new message that it downloads before it is even visible in the inbox.
            - But your decideAction for message method can return an invokeAgainWithBody decision, which will cause Mail to fetch the complete message body and headers before invoking your handler's decideAction for message method again.
        - You can provide a decision such as coloring the message based on the available headers (a subset of all).
- Content blocker extension
    - hook into Mail's WebKit configuration for its message view to allow extensions to block loading content based on triggers in the message's HTML.
    - The content rule lists are specified using the same syntax as Safari content blockers.
        - Provided to Mail by returning it in the contentRulesJSON method.
- Message security extensions
    - Capabilities
        - encode and decode encrypted messages
        - view certificates of signed messages
    - Encoding a message is broken down into two parts.
        - UI indications: lets the extension show if it has the ability to sign and encrypt the current message
        - actually encrypt and sign the message as it is being sent
    - Mechanism
        - As a message is composed, Mail will send the message, including the sender and current list of recipients to the extension, which will .
        - when the message is sent, Mail will take the RFC822 message data and pass it to the extension. The extension will sign and encrypt the message as needed, and return
        - When a message is viewed
            - the signer certificate can be clicked next to the signer label to view the sender's certificate information.
            - Mail allows extensions to provide its own view controller to render this certificate information

### [GroupActivities](https://developer.apple.com/documentation/GroupActivities)

- Create app-specific activities your users can share and experience together.
- Implementation
    - This framework leverages the FaceTime infrastructure to synchronize your app’s activities and to invite other participants to join those activities.
    - When your app’s UI contains shareable activities, adopt the GroupActivity protocol in the objects you use to represent those activities.
    - When a group activity begins, use the GroupSession object to synchronize your app’s behavior with other participating devices.
- end-to-end encryption on all session data
    - Apple doesn’t have the keys to decrypt this data.
    - Occasionally, Apple may ask a small number of users to help troubleshoot issues
    - which may incidentally result in Apple collecting some information related to content shared in your app.

#### [Inviting Participants to Share an Activity](https://developer.apple.com/documentation/groupactivities/inviting-participants-to-share-an-activity)

- Separate activity types makes it easier to customize the experience for each activity.
- your app must have the com.apple.developer.group-session entitlement
- Activity instances provide descriptive information about a specific activity your app makes available to participants.
    - The activity instance might actually be an existing data type in your app.
    - For example, an activity instance for a movie-watching app might contain
        - the name of the movie,
        - a poster image, and
        - app-specific information about how to play the movie.

#### [Joining and Managing a Shared Activity](https://developer.apple.com/documentation/groupactivities/joining-your-app-to-a-shared-activity)

- When a participant accepts an invitation, the system:
    - Launches your app, as needed.
    - Creates a GroupSession object for the selected activity.
    - Delivers the session asynchronously to your app.
- Perform any required validation of the activity and session before you present any UI for that activity.
    - If your app requires participants to pay for content, provide login credentials, download content, or perform other tasks, display UI for those tasks first.
- A new GroupSession object doesn’t synchronize data with the group right away.
    - the object starts in the GroupSession.State.waiting state, and
    - you must explicitly call its join() method to let the system know that your app is ready to begin the associated activity.

#### [Meet Group Activities - WWDC 2021 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2021/10183/)

- we built an entirely new playback-sync protocol with deep integration into the AVFoundation stack on the device.
    - That means someone hits play, and everyone in the group immediately starts playback at the same time.
- Jump to a favorite scene and everyone else sees it too,
    - allowing people to experience moments together in perfect sync
- The magic behind this playback synchronization means we won’t retransmit your media in any way.
    - Everyone will get your full-fidelity video because it’s playing right from your app and streaming from your servers as it always does.
- With smart volume, when people speak up during playback, we’ll automatically duck the audio of the content and bring it back up when appropriate.
- works with Picture in Picture
