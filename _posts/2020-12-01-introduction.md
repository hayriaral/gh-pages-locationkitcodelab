---
title: "Introduction"
description: 1
---

<huawei-codelab-about codelab-title="HMS Location Kit - Geofence and Activity Identification Codelab" last-updated="2020-12-09T13:20:13-07:00" authors="Huawei Codelab Team">

<div class="HMS Location Kit - Geofence and Activity Identification">
<div class="token">HMS Location Kit - Geofence and Activity Identification Codelab</div></div>
<div class="about-card">
<h2 class="title">About this codelab</h2>
<div class="last-updated"><i class="material-icons">subject</i>Last updated Dec 30, 2020</div>
<div class="authors"><i class="material-icons">account_circle</i>Written by Huawei Codelab Team</div></div>
</huawei-codelab-about>

## **Overview**

Location Kit combines the GNSS, Wi-Fi, and base station location functionalities into your app to build up global positioning capabilities, allowing you to provide flexible location-based services for global users. Currently, it provides three main capabilities: fused location, activity identification, and geofence.

1. Fused location: Provides a set of easy-to-use APIs for your app to quickly obtain the device location based on the GNSS, Wi-Fi, and base station location data.

2. Geofence: Allows you to set an interested area through an API so that your app can receive a notification when a specified action (such as leaving, entering, or staying in the area) occurs.

   - Enter: Informs that the device has entered the geofence.

   - Dwell: Informs that the device has entered and is being inside the geofence for a given period of time.

   - Exit: Informs that the device has exited the geofence.

3. Activity identification: Identifies user motion status through the acceleration sensor, cellular network information, and magnetometer, helping you adapt your app to user behavior.

   - Activity Identification Updates: Proactively obtains the current device activity status.
   - Activity Conversion Updates: Detects activity conversion updates of the current device.
<aside class="special">
	<p><strong>Note:</strong> In this codelab, fused location will not covered.</p>
</aside>


**What you will do**
------------------------

In this codelab, you will use the demo project that has been created for you to experience with Huawei Mobile Services Location Kit’s Geofence and Activity Identification features. Through the demo project, you will get experience developing a geofence and physical activity identification to the user.

<div>
    <div style="padding: 5px">
        <img src="https://raw.githubusercontent.com/hayricaral/gh-pages-locationkitcodelab/main/assets/LocationKit1.jpg" style="width: 375.00px" ; padding:5px" />
        <img src="https://raw.githubusercontent.com/hayricaral/gh-pages-locationkitcodelab/main/assets/LocationKit2.jpg" style="width: 375.00px" ; padding:5px" />
    </div>
    <div style="padding: 5px">
        <img src="https://raw.githubusercontent.com/hayricaral/gh-pages-locationkitcodelab/main/assets/LocationKit3.jpg" style="width: 375.00px" ; padding:5px" />
        <img src="https://raw.githubusercontent.com/hayricaral/gh-pages-locationkitcodelab/main/assets/LocationKit4.jpg" style="width: 375.00px" ; padding:5px" />
    </div>
</div>




**What you will learn** 
-----------------------

In this codelab, you will learn how to:

<ul class="checklist">
	<li>Handle broadcast receivers.</li>
    <li>Add geofences.</li>
    <li>Remove geofence.</li>
    <li>Handle geofence transitions.</li>
    <li>Add activity identifications.</li>
    <li>Remove activity identifications.</li>
    <li>Register activity conversions.</li>
    <li>Unregister activity conversions.</li>
</ul>