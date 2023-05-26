## How to Dumbify Your Android Smartphone (Very Technical)

### Interlude

At some point in my late years of college, I was fed up with the amount of time that was wasted on my phone and could have been dedicated to doing something more useful. I've decided that I've had enough and that I have to find a solution to my phone problem, and so I sat down and opened my laptop and came up with the ideas described in this post.

### Why not just use a dumb phone?

1- What I want to do is to reduce the amount of time that I'm wasting on my phone, while keeping some of the more useful features that smartphones have to offer. Using an actual dumb phone would be undesirable as they cannot do all the things that smartphones can do.

2- It has been a common problem in recent years that whoever attempts to switch to a dumb phone gets made fun of and ridiculed. This setup makes it not so obvious that your phone's capabilities are limited, so things are going to be a little more bearable.

### Some Theory

#### Infinite Content vs Non-infinite Content
When we say *infinite content* we are referring to platforms that offer such a gigantic amount of content that it's not feasible for any single individual to consume all of that content. 

1- Social media sites have users constantly posting new content on these sites, hence they can be considered to be providing infinite content to consume.

2- Streaming apps also have huge libraries, and as such, could be considered infinite content.

3- Video games have limited content but they allow for so much variation in play, hence they are closer to infinite content.

In the last decade, we have largely moved to platforms/mediums that offer infinite content such as streaming services, hence we find it defficult to regulate our usage. On the other hand, Mediums that offer non-infinite content are less harmful and less wasteful.

How is this relevant to this post? Well, **we want to eliminate most apps that offer infinite content from our phones.**

#### The Lever

*The Lever* refers to the switch or button that could be used to turn off or disable software or tools designed to help the user reduce or block addictive content in their devices. Often times we find that blocking software is made very easy to disable or easy to circumvent. That is, the *the lever* is easy to pull.

Good software tools that are intended to reduce time spent on the screen should at the least make it difficult to pull the lever, otherwise they are not effective.

### The Plan

There are three primary things that we want to eliminate:

1- Anything involving infinite content/scrolling

   - I'm primarily thinking of social media here.
   
   - Streaming apps can also be a problem, so we want to eliminate those as well.

2- The Browser

The web browser gives you access to the whole internet, which means wasting a lot of time, so we don't want to have access to web browser in our phones.

3- App Stores

The app store allows you to install both 1 and 2, hence we don't want to have any app stores in our phones.

-----

### Prerequisites and Warnings

1- The catch is that you would need to have a phone that has a working official build of [LineageOS](https://download.lineage.microg.org/), otherwise you won't be able to follow this guide.

2- You are expected to have technical knowledge with regards to modifying Android phones, installing custom roms, and such. **THERE IS A RISK OF BRICKING YOUR PHONE OR LOSING YOUR PERSONAL DATA HERE.**

3- You are willing to tolerate some of inevitable problems associated with this setup (More on this later).

4- **THIS GUIDE IS NOT INTENDED FOR THE AVERAGE SMARTPHONE USER.** There is far too many hiccups and challenges associated with getting this setup up and running.

5- The Android ecosystem could change in the future in a way that would break the tools used in this guide, so I don't know if this will guide will continue working in the long term.

-----

### Execution

Now that we are past the introduction, theory, and warnings. We can start explaining how to actually dumbify your android smartphone.

**Step 1:** Install LineageOS with MicroG

1- Backup any data or media that you want to keep from your phone.

2- Download [ADB and Fastboot](https://developer.android.com/tools/releases/platform-tools) on your PC.

3- Download and install your phone's drivers.

4- Unlock your phone's bootloader. This will wipe all of your phone's data.

5- Install the version of [LineageOS with MicroG](https://download.lineage.microg.org/) for your respective smartphone. For the steps, you can [follow the guide for installing LineageOS](https://wiki.lineageos.org/) for the same phone.

After confirming that the ROM is working, you can move to the next step.

**Step 2:** Deleting unwanted apps that ship with the rom:

There are two system apps that ship with this ROM that we don't want because they violate our rules:

- The web browser

- The F-Droid store

To delete these two apps, do the following:

1- Enable Developer options

2- Enable USB debugging and Rooted debugging in Developer options.

3- Plug your phone into the computer.

4- In the computer, open the command line in the same directory as ADB and Fastboot.

5- Now you need to find where the apks for both the browser and the store are located:

Use the 'adb shell' command to open the shell. Then use the 'ls' command to list the files for a specific directory in the phone. Places that you could search are:

```
product/app
product/priv-app
system/app
system/priv-app
system/product/app
system/product/priv-app
```

The web browser that LineageOS is currently using is named *Jelly*.

6- Once you have found where both the browser and app store are located exit the shell and run the following commands:

```
adb root
adb remount
adb shell
rm -f app_location/app.apk
```

Note: avoid using the -r argument in the rm command, unless you want to accidently delete a portion of the ROM.

Once you've confirmed that both the web browser and app store apks have been deleted, restart your phone. The two apps should no longer show up in your phone's apps list.

### The Apps

This section is intended to address problems related to getting apps to work with this setup.

#### Installing apps

1- You can download and install apps by getting the [Aurura Store](https://f-droid.org/packages/com.aurora.store/) then putting and installing it on your phone. You would install any apps that you need, and then uninstall the store.

2- The Aurora Store can be buggy, so as an alternative you would need to find a well-reputed mirror site to download apks from. Some options that I know (but can't fully endorse) are:

- F-Droid (For free open-source software)

- APKMirror

- Uptodown

- APKPure

#### Problems

There are several problems that we are going to encounter here:

1- Some apps will simply refuse to work in phones with an unlocked bootloader or a custom ROM.
in recent years, Google has made it very difficult to bypass the detection. Some people have managed to use Magisk to get certain apps to work, but I personally could not get it to work.

2- Google Apps and Apps that depend on the Play Store:

You must have already noticed that there are no instructions to install Gapps in this guide. This is mainly because we are trying to avoid getting the Play Store in the phone. However, for many people Google apps are essential. This is why we are using a special build of LineageOS that includes MicroG, which provides an alternative to some of the important APIs that ship with the Play Store, allowing us to run the apps that depend on these APIs. As such, it should be possible to run some Google apps in this build without installing Gapps.

#### Enabling MicroG

To get MicroG working, go to the microG Settings app on your phone and do the following:

1- Enable device registration.

2- Go to Cloud Messaging and enable Receive push notifications. This should speed up the delivery of messages for apps that originally depended on Google's push notifications API, including WhatsApp’s messages, without this setting your messages will arrive late.

3- Enable both of the options found in Location modules. These will get Non-GPS based location to work on your phone.

To check if MicroG is working, you can look at the Self-Check page in the app.

It's possible to log in to your Google account from MicroG's settings. Note that this is against Google's terms of service, although so far no one has reported being banned for using it, but you don't want to lose your account by getting banned, so I advise against it.

4- The quality of photos taken with your phone camera will be sacrificed with this setup. There isn't any good fix for this. You might get some improvement in photo quality if you download the apk for your phone's original camera app and install it.

#### What to do if an app won't work

Despite all what we've done, some apps still won't work with our setup. In that case we have the following options:

1- Live without the app: If it's not essential then we could just not use it.

2- Find an alternative: In some cases, you will find that the next most popular app works fine, and so you could just use it.

### Advantages and Disadvantages

#### Advantages

1- I find myself wasting significantly less time on my phone when using this setup, compared to the regular setup that everyone uses.

2- There is less of an urge to check my phone every minute.

#### Disadvantages

Now, this setup comes with a lot of disadvantages that you should be aware of:

1- The main disadvantage of this setup is that it's still possible to download the apk for the browser or for any app on the computer and then install it on your phone, and then end up wasting a lot of time. Hence, an easy to pull *lever*.

2- You will inevitably come across situations where you need to install an app, open the browser, or do something with your phone that this setup can't do.

3- If you really need certain apps that don't work with this setup then you might not be able to stick with it.

4- This setup exposes you to more security risks when compared to a regular Android user (Bootloader is unlocked + downloading apps from places other than the Play Store + Trying out new apps as alternatives).

5- Good luck trying to explain to people why your phone doesn't have all the features and capabilities that people expect it to have.

6- People might call you crazy.

### Finale

Despite all of the problems, I still chose to stick with this setup. It made me waste significantly less time on my phone and made the amount time spent on my phone much more reasonable. Unless Google and Apple decide to develop better time management solutions, I shall continue to follow my own messy solutions.
