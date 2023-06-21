---
title: "Using iCalendar for semi-predictable but oddball events"
datePublished: Sat Nov 06 2021 07:47:59 GMT+0000 (Coordinated Universal Time)
cuid: ckvniu2y800mi4as1hq0w8j3s
slug: using-icalendar-for-semi-predictable-but-oddball-events
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1636185637483/G2NgyD--F.png
tags: productivity, programming-blogs, developer, programming-tips

---

## Background
My girlfriend is a nurse, and around these parts that means she works shift work. Her schedule is a block of shifts (sometimes day shifts, sometimes evening shifts) followed by a block of days off (which also varies as to the number of days), and the entire schedule itself repeats every so many weeks. Basically, picture something like this:

![https _bucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com_public_images_9fdca9ec-9ad8-4df3-8cb5-bbdde5f5cce0_1260x426.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636183660092/pJ1POvinl.png)

...and repeat.

While there *is* a pattern to it, it essentially means that without access to a copy of her schedule readily at hand, it is *literally impossible* to know if we are free on some random day next month. So obviously, I want an electronic version at the ready for these types of inquiries.

Unfortunately, it is also *incredibly tedious* to enter all of these shifts one by one, by hand, into something like Google Calendar, because it requires manually creating dozens of events (“repeats every other Monday” unfortunately does not cut it here :P), and on each of them, manually selecting “Repeats,” manually selecting “Custom…”, manually selecting “every X weeks”, all without introducing any errors. *Ugh.*

Fortunately, here to save the day… the iCalendar specification!

## What is the iCalendar specification?

The  [iCalendar specification](https://tools.ietf.org/html/rfc5545) (as in  [RFC 5545](https://tools.ietf.org/html/rfc5545), not to be confused with good ol’  [iCal](http://www.apple.com/ical/), now known as Apple’s  [Calendar](https://support.apple.com/en-ca/guide/calendar/welcome/mac) app) is a “data format for representing and exchanging calendaring and scheduling information such as events, to-dos, journal entries, and free/busy information, independent of any particular calendar service or protocol.”

Basically, it’s a list of rules about how to describe events in computer-friendly language, and if you follow those rules, users can import your events consistently in whatever various calendaring programs they might be using. Glancing through the specification, you’ll see it talks about how to specify all kinds of features you may have seen in various calendaring apps, such as:

- Specify a location
- Specify a time zone
- Repeat an event with a certain frequency
- Note whether someone’s an optional or required attendee
- Denote whether it shows up as busy or free time on someone’s calendar
- Send an alert a few minutes before an event happens

...and much, much more.

If you’ve ever received an email with a .ics file attached, and when you click it you’re prompted to add an event to your calendar, such as below… Congratulations! You officially have experience with iCalendar! :D

![https _bucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com_public_images_7fc915a4-a284-405f-8f0c-3ef32e207213_926x368.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636183864658/ziqjHsdhb.png)

Let’s talk about what iCalendar looks like under the hood.

## The Basics of iCalendar

The “simplest thing that can possibly work” in terms of iCalendar is a text file, with an .ics extension, that contains the following properties:

- **`BEGIN:VCALENDAR … END:VCALENDAR`**: (required) Marks the beginning and end of the iCalendar object as a whole (similar to how `<html> … </html>` wraps around a web page).

- **`VERSION`**: (required) The version number of the specification required (generally, “2.0” unless you’re feeling super retro).

- **`PRODID`**: (required) A unique identifier for the product that created the iCalendar object. Some real-world examples are `“-//Google Inc//Google Calendar 70.9054//EN”` for Google Calendar and `“-//Apple Inc.//Mac OS X 10.14.6//EN”` for Apple Calendar.

- **`BEGIN:VEVENT … BEGIN:VEVENT`**: One or more of these pairings mark the beginning and end of an event definition.

- **`UID`**: (required) A unique identifier for the event. `[buncha-random-chars]` and `[buncha-random-chars]@[yourdomain.com]` are both common patterns.

- **`DTSTAMP`**: (required) The date/time that the event was created (not to be confused with when it starts, which is the next one). 

- **`DTSTART … DTEND`**: When the event starts and ends.

Here’s a simple example tying all of that together:

```
BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//Example Corp//Example Calendar App 1.0//EN
BEGIN:VEVENT
UID:20210310T001345Z-0242ac130003@example.com
DTSTAMP:20210310T001345Z
DTSTART:19991231T235959
DTEND:20000101T000000
SUMMARY:Party like it’s 1999!
END:VEVENT
END:VCALENDAR
```

If you save this as “y2k.ics” and import it, you should see a new event appear at the very tail end 1999 that lasts from 11:59:59PM on December 31, 1999 until midnight on January 1, 2020!

## How to specify a date/time?

The RFC gets into this at length, but the basic gist is:

-  If it’s a date only, it’s specified in the format of `YYYYMMDD`.
-  If it’s a date *and* time, it’s specified in the format of `YYYYMMDDTHHMMSS` (with `HH` in 24-hour time). If it’s a UTC time (see below) it also has a `Z` at the end.

There are  [three different ways to specify a date and time](https://tools.ietf.org/html/rfc5545#section-3.3.5) such as 11:59:59PM on December 31, 1999:


1.  Date with local time: Used when you want an event to be at the same time, regardless of a person’s location.
```
        DTSTART:19991231T235959
```

2. Date with UTC time:  Used when you want an event to be at an absolute time across all geographic locations, and disregarding Daylight Savings Time. (Note: DTSTAMP is always in this format.)
```
        DTSTART:19991231T235959Z
```
3. Date with local time and timezone reference: A combination of both; it pegs to a specific time, but within a given time zone, so it takes into consideration things like Daylight Savings Time.
```
        DTSTART;TZID=America/Vancouver:19991231T235959
```

In the above example, we went with the “date with local time” format so that the event would be at the same time regardless of location, since exactly when the “last minute of 1999” is differs across the globe. But for tracking shift schedules, “Date with local time and timezone reference” makes more sense, because if I fly to Europe for work, I don’t want the start times to shift by several hours.

*Nope, that semi-colon after DTSTART in the third example is not a typo. “Property parameters” such as TZID are passed in with a semicolon rather than a colon. (See List and Field Separators) This will also come into play with...*

## Repeating Events

Ok, so we already have enough information to create each shift schedule the *first* time, but note that it repeats every X weeks. How do we handle *that*?

Enter  [Recurrence Rules (RRULE)](https://tools.ietf.org/html/rfc5545#section-3.8.5.3)! This property defines a rule or repeating pattern for recurring events. Here are just a few of the  [options](https://tools.ietf.org/html/rfc5545#section-3.3.10) that it supports:

- **`FREQ`**: How often the event occurs. Some examples are `WEEKLY`, `DAILY`, and even `SECONDLY`.

- **`INTERVAL`**: How many `FREQ`s should there be in between events?

- **`COUNT`**: Repeat the event X times. (Useful if you have a class that runs for 4 weeks, for example)

- **`UNTIL`**: Alternatively, this will repeat the event until a certain date.

- **`BYDAY`**: Allows you to say something only happens on certain days of the week.

The RFC has  [all sorts of examples](https://tools.ietf.org/html/rfc5545#section-3.8.5.3).

## Putting it All Together

For our purposes, we need events that:

1. Use a **Date with local time and timezone reference** because I travel frequently (in non-COVID times) and I want the events to be shown at the proper start/end times regardless of where I am in the world.

1. Have a `FREQ` of `WEEKLY` and an `INTERVAL` of `8` since the schedule repeats every 8 weeks.

1. And an `UNTIL` date of `12/31/2021` because the schedule gets reset every calendar year, and next year will be something different! (Hance my very strong desire to write this process down. ;))

Put it all together, and you get:

```
BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//Webchick Inc//Webchick’s Crappy Bash Script 1.0//EN
BEGIN:VEVENT
UID:3231CB09-1E10-4910-BB24-B358629890B7
DTSTAMP:20210314T090733Z
SUMMARY:Day Shift
DTSTART;TZID=America/Vancouver:20210111T080000
DTEND;TZID=America/Vancouver:20210111T180000
RRULE:FREQ=WEEKLY;INTERVAL=8;UNTIL=20211231
END:VEVENT

... (repeat x many more events) ...

BEGIN:VEVENT
UID:F20376E5-FA0F-429D-AB1F-3F0155EE10BA
DTSTAMP:20210314T090734Z
SUMMARY:Evening Shift
DTSTART;TZID=America/Vancouver:20210208T173000
DTEND;TZID=America/Vancouver:20210208T233000
RRULE:FREQ=WEEKLY;INTERVAL=8;UNTIL=20211231
END:VEVENT

... (repeat x many more events) ...

END:VCALENDAR
```
And when imported into Apple Calendar:

![https _bucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com_public_images_9d99d098-3f0a-4e16-b4b7-27cabf5ec3d4_1522x322.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636184766693/m8vxEWXqF.png)

And there you have it!

So. The next time you get one of those .ics files, try popping it open in a text editor and see how much of it makes sense now!

PS: If you want to see the bash script I used to generate this, it’s at https://github.com/webchick/shiftycal. If you want to go it alone,  [this handy validator](https://icalendar.org/validator.html) is your friend!

*(Cover image: "[iCal icon replacement](https://www.flickr.com/photos/64503524@N00/2319463826)" by  [bertop](https://www.flickr.com/photos/64503524@N00) is licensed under CC  [BY-NC-SA 2.0](https://creativecommons.org/licenses/by-nc-sa/2.0/?ref=ccsearch&atype=rich))*