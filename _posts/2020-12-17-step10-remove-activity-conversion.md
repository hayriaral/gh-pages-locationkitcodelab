---
title: "Step 10: Remove activity conversion"
description: 3
---

When you no longer need to receive activity conversion, you can remove it through `PendingIntent`.

1. In `MainFragment.kt`, in `removeActivityConversion()` function, remove current activity conversion through `activityConversionPendingIntent`.

   <pre><div id="copy-button39" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 10.1:
   activityIdentificationService.deleteActivityConversionUpdates(
       activityConversionPendingIntent
   )?.run {
       addOnSuccessListener {
           //Activity Identification removed successfully.
           Log.i(TAG, "Activity Conversion updates has been stopped.")
       }
       addOnFailureListener {
           //Removing Activity Conversion process failed.
           Log.i(TAG, "Failed to stop Activity Conversion updates.")
       }
   }
   <span class="pln">
   </span></code></pre>