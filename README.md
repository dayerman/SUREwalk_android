<p align="center">
  <img src="https://raw.github.com/pandanomic/SUREwalk_android/master/surewalk/src/main/res/drawable/surewalk_logo.png" alt="SUREwalk Logo" height="200" width="530"/>
</p>

<p align="center">
  This is the source code for the SUREwalk Android App.
</p>
=================

### [CHANGELOG](https://github.com/pandanomic/SUREwalk_android/blob/master/CHANGELOG.md)

### Members of the Android team include the following:
* [Guy Hawkins](https://github.com/GHawk1ns)
* [Chris Roberts](https://github.com/NASAgeek)
* [Henri Sweers](http://pandanomic.github.io)
* [Sam Thompson](https://github.com/st028)

### About
In the summer of 2013, a member of UT Student Government approached the Computer Science majors' Facebook group asking if anyone would be interested in helping them develop mobile apps for SUREwalk. SUREwalk is student-run, volunteer service where students can call at late hours of the night to have two volunteers come out and walk with them to wherever they need to go. SUREwalk wanted to increase improve their accessibility to students (before you just had to call them). We were more than happy to help with this cause.

Along with the Android side, other students also developed an iOS app and a website built with Rails, with all three platforms sharing a unified back end via Parse. If they opt to release that source code, we will post links here. 

We wanted to share this for the benefit of anyone else interested in developing an app for this purpose, or just developing an app itself.

### Basic Structure
* There is a main Dashboard Fragment that we use for the home screen, and displayed with a Twitter fragment (at their request) under a ViewPager
* The meat of the app is in the Request Activity. This is where we handled a paged request flow (we considered using WizardPager, but opted to roll our own instead). The steps of the flow are as follow:
  - Information: Name, EID, Phone, and E-Mail
  - Location: This is their start location, found either with the GPS or by entering an address to [Google's Geocoding API](https://developers.google.com/maps/documentation/geocoding/)
  - Destination: This is their destination, selected on a map displaying SUREwalk's boundaries
  - Review: This is the last step, allowing them to review their information and add any comments before submission.
* Throughout the Request flow, a ParseObject that mirrors one set up in our Parse database is constructed and fleshed out. Upon submission, this object is then saved to the Parse database, which is then polled by the Rails server to check for new requests.
* After SUREwalk receives the request and assigns it, a push notification is sent back using Parse+GCM to alert the user than the volunteers are on their way.

### Other stuff
If you want to build this locally, you'll need two strings.xml values files which we currently don't track. One called `private_strings.xml` and another called `com_crashlytics_export_strings.xml`. If you don't have these, your build will fail fast. We are considering dropping a couple of dummy files in there instead though.

`private_strings.xml` Looks like this:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources xmlns:tools="http://schemas.android.com/tools" tools:ignore="TypographyDashes">

    <string name="maps_api_key">key_goes_here</string>
    <string name="parse_app_key">key_goes_here</string>
    <string name="parse_client_key">key_goes_here</string>
    <string name="ga_tracking_id">UA-xxxxxxxx-x</string>
    <string name="crashlytics_api_key">key_goes_here</string>

</resources>
```

The crashlytics xml is auto-generated if you use it. If you'd rather not, simply comment out all the Crashlytics code (in `MainActivity.java` and `build.gradle`)

(Private accounts information is in an untracked private.md file)

### License
===========

        The MIT License (MIT)

        Copyright (c) 2014 SUREwalk

        Permission is hereby granted, free of charge, to any person obtaining a copy
        of this software and associated documentation files (the "Software"), to deal
        in the Software without restriction, including without limitation the rights
        to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
        copies of the Software, and to permit persons to whom the Software is
        furnished to do so, subject to the following conditions:

        The above copyright notice and this permission notice shall be included in all
        copies or substantial portions of the Software.

        THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
        IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
        FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
        AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
        LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
        OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
        SOFTWARE.
