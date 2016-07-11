---
title: ios-reading-cocoa-and-core-services
date: 2016-07-10 17:53:15
tags: iOS
---


# Cocoa Touch Layer


Cocoa Touch is a collection of frameworks which are providing appearance (UI) for our app and multi-tasking, touch-based input, push notifications.





## Standard system view controllers

- Display or edit contact information: pick a ctrl from Address Book UI framework.

- Compose an email or SMS: pick a ctrl from message ui fk.

- Open or preview the contents of a file: Use the UIDocumentInteractionController class


## Handoff

- Handoff is a feature to enable user can migrate their tasks from one device(iPhone) to another device(maybe Mac).

Handoff makes this experience as seamless as possible.

Of course, to use it you need to study its official API.

## Document picker

Enable user can access files outside from the current app.

Simple mechanism for sharing documents within apps.

## AirDrop

Share photos, documents, URLs with nearby devices.

## Textkit

Textkit a full-featured to organize paragraphs, columns, ...

- comments: well, I prefer to keep content as simple as possible. Too much fexlibility will harm the reading experience. eg. I like the philosophy of Medium

## Multitasking

If you want to do some tasks after the app is switched to the backgorund. You need to use it to enable your app can work in the backgorund.


# Auto layout

Help you build dynamic interfaces with little code.

Comment: I hate to layout components with storyboard. It should be done with some css-similar syntax 

# Storyboards

A way to defin `segues` which are transitions from one view CTRL to another. These transitions allow you to captire the flow of UI in addition to the content.

# UI State preservation

It can restore the last time App's state. Provide a good user experience.


# Apple push notification services

To alert user notifications.

- The app muse request the delivery of notifications and process the notification content once it's delivered.
- Provide a server-side process to generate the notifications in the first place.

Comment: I've done thise before, but only on Rubymotion toolchain.


# Local notification.

The notifications coming from the app itself. you can schedule it.

# Gesture Recognizers


TL;DR



# Framworks

- Address Book UI Framework:  contacts-related events
- EventKit : calendar-related events
- MapKit
- Message UI 
- GameKit, iAD, 










