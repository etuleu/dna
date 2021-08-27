- https://developer.android.com/topic/performance/vitals/launch-time
    - "Users expect apps to be responsive and fast to load. An app with a slow start
time doesn’t meet this expectation, and can be disappointing to users. This
sort of poor experience may cause a user to rate your app poorly on the Play
store, or even abandon your app altogether."
- https://reactnative.dev/docs/ram-bundles-inline-requires
    - "You should now be ready to build your app using the RAM format and 
inline requires. Make sure you measure the before and after startup 
times."
- How do you measure?
    - You can launch the app manually and try to get a feel for how fast or slow it opens, but there are many things happening at the same time so the time to open might vary quite a bit. Also some improvements might not be very noticeable with the naked eye but might still add up over time. For example a 100ms improvement might be really good but difficult to notice with a few manual attempts.
    - For this reason we need a more robust way to measure this type of changes as well as keep track of them over time (for each commit in git).
    - Without proper measurements over time any commit can impact the app performance without anyone noticing until the app gets shipped to actual users. Reverting these changes is also time consuming and can badly affect app state for some users. It is better to detect these as soon as possible.
    - Some examples of changes that can impact app performance: 
        - new library added which can depend on many other libraries and therefore bloat the runtime or slow down app launch
        - new library has a higher minimum supported version for android or ios OS and can make the app unusable for a set of users
        - new module added that loads thing from disk or network on the main thread and therefore blocking the UI from rendering
        - too much work done on the main thread which can cause jankiness
- "A cold start refers to an app’s starting from scratch: the system’s process
has not, until this start, created the app’s process. Cold starts happen in
cases such as your app’s being launched for the first time since the device
booted, or since the system killed the app. This type of start presents the
greatest challenge in terms of minimizing startup time, because the system
and app have more work to do than in the other launch states."
    - As soon as the system creates the app process, the app process is responsible for the next stages:
        - Creating the app object.
        - Launching the main thread.
        - Creating the main activity.
        - Inflating views.
        - Laying out the screen.
        - Performing the initial draw.
- How fast is an empty app? What is an empty app? It's an app that doesn't do anything. It just displays a blank screen. So we can use this as a sort of baseline performance number.
    - Link to a github repo containing an empty android app: 
- Now a lot of companies build apps using react native which is a popular framework made by facebook that allows developers to build once and have an app that (mostly) works on both android and ios. Apps are writter using Typescript. These apps usually rely on a bridge that communicates between the native side of the OS and the Typescript code. More info here: https://reactnative.dev/docs/communication-ios
-  Android platform architecture: https://developer.android.com/guide/platform
- TODO: iphone platform architecture: 
- Android application fundamentals: https://developer.android.com/guide/components/fundamentals
- TODO: iphone application fundamentals
- Android vitals: https://developer.android.com/topic/performance/vitals
- Useful tools:
    - Android system tracing: https://developer.android.com/topic/performance/tracing
    - dumpsys is a tool that runs on Android devices and provides information about
system services: https://developer.android.com/studio/command-line/dumpsys.html
- Shrink, obfuscate, and optimize your app: https://developer.android.com/studio/build/shrink-code
- Two different states to test:
    - first time open, not onboarded
    - after onboarding, the feed has a bunch of different items, can scroll etc.
- Other things to measure: react native modules, bundle size, memory, network usage, battery usage, disk usage, cpu, gpu
- Things to try:
    - https://reactnative.dev/docs/ram-bundles-inline-requires
    - Analyze what is taking the most time and try to eliminate, optimize or move to async (off the main thread if possible)
    - Avoid blocking I/O operations on main thread
    - Measure app performance under different network conditions
    - 
