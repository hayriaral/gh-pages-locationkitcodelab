---
title: "Step 2: Add geofence"
description: 20
---

**Create pending intent**

You will create a `PendingIntent` in order to dynamically register to `BroadcastReceiver` through it.

1. In `MainFragment.kt`, above the `onViewCreated()` method, create a private type of `PendingIntent` variable which named `geofencePendingIntent` with lazy initialization. `getGeofenceAction()` returns action name as `String`, and `getGeofenceRequestCode()` returns request code as `Integer`. Both are implemented in `GeofenceHelper.kt`.

   <pre><div id="copy-button12" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.1:
   private val geofencePendingIntent: PendingIntent by lazy {
       val intent = Intent(context, LocationBroadcastReceiver::class.java)
       intent.action = getGeofenceAction()
       PendingIntent.getBroadcast(
           context,
           getGeofenceRequestCode(),
           intent,
           PendingIntent.FLAG_UPDATE_CURRENT
       )
   }
   <span class="pln">
   </span></code></pre>

**Create geofence service**

You will create a geofence service client to call geofence-related APIs.

1. In `MainFragment.kt`, above the `onViewCreated()` method, declare a private type of `GeofenceService` variable which named `geofenceService`.

   <pre><div id="copy-button13" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.2:
   private lateinit var geofenceService: GeofenceService
   <span class="pln">
   </span></code></pre>

2. In `MainFragment.kt`, in the `onViewCreated()` method, initialize `geofenceService` which is already declared above.

   <pre><div id="copy-button14" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.3:
   geofenceService = LocationServices.getGeofenceService(activity)
   <span class="pln">
   </span></code></pre>

**Build geofence and geofence request**

You will build a geofence object and a geofence request in order to add geofence.

1. In `MainFragment.kt`, in the `buildGeofence()` function, build a geofence using `Geofence.Builder()`. Set the followings: 

   - A request ID to identify the geofence.
   - The circular region of the geofence.
   - The transition types.
   - The expiration duration of the geofence.

   Finally, return the geofence.

   <pre><div id="copy-button15" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.4:
   return GeofenceRequest.Builder()
       .createGeofence(geofence)
       .setInitConversions(GeofenceRequest.ENTER_INIT_CONVERSION)
       .build()
   <span class="pln">
   </span></code></pre>

2. In `MainFragment.kt`, in the `buildGeofenceRequest()` function, build a geofence request using `GeofenceRequest.Builder()`. Create geofence to be monitored by geofence service, and set initial trigger callback for conversions. Then, return the request.

   <pre><div id="copy-button16" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.5:
   return Geofence.Builder()
       .setUniqueId(id)
       .setRoundArea(latLng.latitude, latLng.longitude, radius)
       .setConversions(transitionTypes)
       .setValidContinueTime(Geofence.GEOFENCE_NEVER_EXPIRE)
       .build()
   <span class="pln">
   </span></code></pre>

**Start Geofence**

Construct a request to add a geofence. After you send the request, the system will notify you of the request result through [Task](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References-V5/task_tresult-0000001050121148-V5).

1. In `MainFragment.kt`, in `startGeofence()` function, instantiate a variable type of `Geofence` by call `buildGeofence()` method which is created above.

   <pre><div id="copy-button17" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.6:
   val geofence: Geofence = buildGeofence(
       landmark.geofenceUniqueId, landmark.latLng, landmark.radius,
       Geofence.ENTER_GEOFENCE_CONVERSION
   )
   <span class="pln">
   </span></code></pre>

2. In `MainFragment.kt`, in `startGeofence()` function, instantiate a variable type of `GeofenceRequest` by call `buildGeofenceRequest()` method which is created above.

   <pre><div id="copy-button18" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.7:
   val geofenceRequest: GeofenceRequest = buildGeofenceRequest(geofence)
   <span class="pln">
   </span></code></pre>

3. In `MainFragment.kt`, in `startGeofence()` function, use `geofenceService`  to add geofence. At the beginning, remove existing geofence that in use by calling `deleteGeofenceList()`. In any case of the removal, add new geofence by passing `geofencePendingIntent`, and `geofenceRequest` to `createGeofenceList()` method. If adding geofence succeed, inform user with `Toast`. Otherwise, put message into `Log` calling `getGeofenceErrorString()` function.

   <pre><div id="copy-button19" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.8:
   geofenceService.deleteGeofenceList(geofencePendingIntent)?.run {
       addOnCompleteListener {
           geofenceService.createGeofenceList(geofenceRequest, geofencePendingIntent)?.run {
               addOnSuccessListener {
                   val toast = Toast.makeText(
                       context,
                       "Geofence started for ${landmark.latLng}",
                       Toast.LENGTH_SHORT
                   )
                   toast.setGravity(Gravity.CENTER, 0, 0)
                   toast.show()
               }
               addOnFailureListener {
                   Log.e(
                       TAG,
                       "Failed to add geofence. Error code: " + getGeofenceErrorString(it)
                   )
                   val toast =
                       Toast.makeText(context, "Failed to add geofence.", Toast.LENGTH_SHORT)
                   toast.setGravity(Gravity.CENTER, 0, 0)
                   toast.show()
               }
           }
       }
   }
   <span class="pln">
   </span></code></pre>

4. In `GeofenceHelper.kt`, in `getGeofenceErrorString()` function, return `GeofenceErrorCodes` as `String`.

   <pre><div id="copy-button20" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 2.9:
   if (exception is ApiException) {
       when (exception.statusCode) {
           GeofenceErrorCodes.GEOFENCE_UNAVAILABLE -> return "GEOFENCE_UNAVAILABLE"
           GeofenceErrorCodes.GEOFENCE_NUMBER_OVER_LIMIT -> return "GEOFENCE_NUMBER_OVER_LIMIT"
           GeofenceErrorCodes.GEOFENCE_PENDINGINTENT_OVER_LIMIT -> return "GEOFENCE_PENDINGINTENT_OVER_LIMIT"
       }
   }
   return exception.localizedMessage
   <span class="pln">
   </span></code></pre>