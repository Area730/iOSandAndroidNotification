.. _overview:

Installation
============

Import `this plugin`_ to your Unity project

Now you could build and run application to test. But please read all documentation!

.. image:: _static/images/screen_one.png
            :align: center 

Create IOSNotification With Code
================================

Schedule simple notification
----------------------------
The package contains code samples in Assets/Area730/Notifications/Examples/Scripts folder. Also you can build and run example scene *Assets/Area730/Notifications/IOS/Examples* to test notification.

The notifications are created using ``IOSNotificationBuilder`` class. Its constructor takes 3 arguments - ``id`` of the notification, ``title`` and ``notification text``.

Next example example shows how to schedule the notification that will be shown immediately:

.. code-block:: c#

    int id          = 1;
    string title    = "Notification titile";
    string body     = "Notification body";

    IOSNotificationBuilder builder = new IOSNotificationBuilder (id, title, body);
    IOSNotifications.scheduleNotification(builder.build());



Schedule delayed notifications
------------------------------
If you want to set delay - call ``builder.setDelay(int milliseconds)`` or ``builder.setDelay(System.TimeSpan delayTime)``. The next example shows how to create a notification that will be shown in one hour:

.. code-block:: c#

    int id          = 1;
    string title    = "Notification titile";
    string body     = "Notification body";

    // Show notification in one hour
    TimeSpan delay  = new TimeSpan(1, 0, 0); 

    IOSNotificationBuilder builder = new IOSNotificationBuilder (id, title, body);
    builder.setDelay(delay);

    IOSNotifications.scheduleNotification(builder.build());

Repeating notifications
-----------------------
To set repeating notification you should set notification as repeating and set the time interval.
According to `Apple documntaion`_  it is allowed to repeat notification every:

1. Minute

2. Hour

3. Day

4. Month

5. Year

.. code-block:: c#

    int id          = 1;
    string title    = "Notification titile";
    string body     = "Notification body";

    // Show notification in one hour
    IOSNotificationBuilder builder = new IOSNotificationBuilder (id, title, body);
    builder.setInterval(IntervalUnits.HOUR);

    IOSNotifications.scheduleNotification(builder.build());

Set Up Badge Number
-------------------
.. code-block:: c#

    int id          = 1;
    string title    = "Notification titile";
    string body     = "Notification body";

    // Show notification in one hour
    IOSNotificationBuilder builder = new IOSNotificationBuilder (id, title, body);
    builder.setNumber(3);

    IOSNotifications.scheduleNotification(builder.build());


Settings custom sound
---------------------
Now its supported only ``wav`` format sound notification.
Next section show how to use custom sound for notification

.. code-block:: c#

    IOSNotificationBuilder builder = new IOSNotificationBuilder (id, title, body);
    builder.setSound("notification_sound");//without wav extention

    IOSNotifications.scheduleNotification(builder.build());

**\*Important** *When you set up sound via script please add source file to the xCode project into *Data/Raw* folder manually.*
If you change audioclips via Editor please check *Assets/StreamingAssets* and *Assets/Plugins/IOS/Notifications* folders to delete old clips.


Cancel notification by id (both repeating and one-time)
-------------------------------------------------------
.. code-block:: c#

    //cancel notification with id 7
    IOSNotifications.cancelNotification(7);


Cancel all notification
-----------------------
.. code-block:: c#

    //cancel all notification
    IOSNotifications.cancelAll();


Clear shown notifications
-------------------------
.. code-block:: c#

    IOSNotifications.clearAll();


Updating notifications
----------------------
To update one-time or repeating notification, schedule a notification with updated data and with ID of the notification you want to update.

Show IOS toast notification
---------------------------
.. code-block:: c#

    IOSNotifications.showToast("Download completed");


Create IOSNotification With Visual Tool
======================================
.. image:: _static/images/notification.png
            :align: center 

To open visual tool to create notification go to *Window->IOS Local Notification*

Next example shows scheduling of the notification created in editor with name **notificationOne**

.. code-block:: c#

    string notificationName = "notificationOne";

    // Method returns builder so you can config your notification afterwards if you want
    IOSNotificationBuilder builder = IOSNotifications.GetNotificationBuilderByName(notificationName);

    // If notification with specified name doesn't exist builder will be null
    if (builder != null)
    {
        IOSNotification notif = builder.build();
        IOSNotifications.scheduleNotification(notif);
    }

Push Notification with OneSignal_ integration
=============================================
Add ``CrossPlatformPushNotificationController.cs`` to some object in your scene
and paste ``id`` from created application in onesignal. For more information go here_

Modifying plugin
================
All native source code is holding in *Assets/Plugins/IOS/Notifications*

Other
=====
All classes are located in **Area730.Notifications.IOS** namespace

Example scene with sample code is included in the package *(Assets/Area730/Notifications/Examples)*



.. _this plugin: http://u3d.as/pUc
.. _Apple documntaion: https://developer.apple.com/library/prerelease/watchos/documentation/iPhone/Reference/UILocalNotification_Class/index.html#//apple_ref/occ/instp/UILocalNotification/repeatInterval
.. _OneSignal: https://onesignal.com/
.. _here: https://documentation.onesignal.com/docs/generating-an-ios-push-certificate  

.. toctree::
   :glob:
   :maxdepth: 1

   overview/**