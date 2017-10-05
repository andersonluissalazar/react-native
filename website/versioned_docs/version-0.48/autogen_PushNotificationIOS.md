---
id: version-0.48-pushnotificationios
title: PushNotificationIOS
category: APIs
permalink: docs/pushnotificationios.html
original_id: pushnotificationios
---
<div><div><span><div class="banner-crna-ejected">
  <h3>Projects with Native Code Only</h3>
  <p>
    This section only applies to projects made with <code>react-native init</code>
    or to those made with Create React Native App which have since ejected. For
    more information about ejecting, please see
    the <a href="https://github.com/react-community/create-react-native-app/blob/master/EJECTING.md" target="_blank">guide</a> on
    the Create React Native App repository.
  </p>
</div>

</span><p>Handle push notifications for your app, including permission handling and
icon badge number.</p><p>To get up and running, <a href="https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6" target="_blank">configure your notifications with Apple</a>
and your server-side system.</p><p><a href="docs/linking-libraries-ios.html#manual-linking" target="_blank">Manually link</a> the PushNotificationIOS library</p><ul><li>Add the following to your Project: <code>node_modules/react-native/Libraries/PushNotificationIOS/RCTPushNotification.xcodeproj</code></li><li>Add the following to <code>Link Binary With Libraries</code>: <code>libRCTPushNotification.a</code></li></ul><p>Finally, to enable support for <code>notification</code> and <code>register</code> events you need to augment your AppDelegate.</p><p>At the top of your <code>AppDelegate.m</code>:</p><p>  <code>#import &lt;React/RCTPushNotificationManager.h&gt;</code></p><p>And then in your AppDelegate implementation add the following:</p><div class="prism language-javascript">  <span class="token comment" spellcheck="true"> // Required to register for notifications
</span>   <span class="token operator">-</span> <span class="token punctuation">(</span><span class="token keyword">void</span><span class="token punctuation">)</span>application<span class="token punctuation">:</span><span class="token punctuation">(</span>UIApplication <span class="token operator">*</span><span class="token punctuation">)</span>application didRegisterUserNotificationSettings<span class="token punctuation">:</span><span class="token punctuation">(</span>UIUserNotificationSettings <span class="token operator">*</span><span class="token punctuation">)</span>notificationSettings
   <span class="token punctuation">{</span>
    <span class="token punctuation">[</span>RCTPushNotificationManager didRegisterUserNotificationSettings<span class="token punctuation">:</span>notificationSettings<span class="token punctuation">]</span><span class="token punctuation">;</span>
   <span class="token punctuation">}</span>
  <span class="token comment" spellcheck="true"> // Required for the register event.
</span>   <span class="token operator">-</span> <span class="token punctuation">(</span><span class="token keyword">void</span><span class="token punctuation">)</span>application<span class="token punctuation">:</span><span class="token punctuation">(</span>UIApplication <span class="token operator">*</span><span class="token punctuation">)</span>application didRegisterForRemoteNotificationsWithDeviceToken<span class="token punctuation">:</span><span class="token punctuation">(</span>NSData <span class="token operator">*</span><span class="token punctuation">)</span>deviceToken
   <span class="token punctuation">{</span>
    <span class="token punctuation">[</span>RCTPushNotificationManager didRegisterForRemoteNotificationsWithDeviceToken<span class="token punctuation">:</span>deviceToken<span class="token punctuation">]</span><span class="token punctuation">;</span>
   <span class="token punctuation">}</span>
  <span class="token comment" spellcheck="true"> // Required for the notification event. You must call the completion handler after handling the remote notification.
</span>   <span class="token operator">-</span> <span class="token punctuation">(</span><span class="token keyword">void</span><span class="token punctuation">)</span>application<span class="token punctuation">:</span><span class="token punctuation">(</span>UIApplication <span class="token operator">*</span><span class="token punctuation">)</span>application didReceiveRemoteNotification<span class="token punctuation">:</span><span class="token punctuation">(</span>NSDictionary <span class="token operator">*</span><span class="token punctuation">)</span>userInfo
                                                          fetchCompletionHandler<span class="token punctuation">:</span><span class="token punctuation">(</span><span class="token keyword">void</span> <span class="token punctuation">(</span><span class="token operator">^</span><span class="token punctuation">)</span><span class="token punctuation">(</span>UIBackgroundFetchResult<span class="token punctuation">)</span><span class="token punctuation">)</span>completionHandler
   <span class="token punctuation">{</span>
     <span class="token punctuation">[</span>RCTPushNotificationManager didReceiveRemoteNotification<span class="token punctuation">:</span>userInfo fetchCompletionHandler<span class="token punctuation">:</span>completionHandler<span class="token punctuation">]</span><span class="token punctuation">;</span>
   <span class="token punctuation">}</span>
  <span class="token comment" spellcheck="true"> // Required for the registrationError event.
</span>   <span class="token operator">-</span> <span class="token punctuation">(</span><span class="token keyword">void</span><span class="token punctuation">)</span>application<span class="token punctuation">:</span><span class="token punctuation">(</span>UIApplication <span class="token operator">*</span><span class="token punctuation">)</span>application didFailToRegisterForRemoteNotificationsWithError<span class="token punctuation">:</span><span class="token punctuation">(</span>NSError <span class="token operator">*</span><span class="token punctuation">)</span>error
   <span class="token punctuation">{</span>
    <span class="token punctuation">[</span>RCTPushNotificationManager didFailToRegisterForRemoteNotificationsWithError<span class="token punctuation">:</span>error<span class="token punctuation">]</span><span class="token punctuation">;</span>
   <span class="token punctuation">}</span>
  <span class="token comment" spellcheck="true"> // Required for the localNotification event.
</span>   <span class="token operator">-</span> <span class="token punctuation">(</span><span class="token keyword">void</span><span class="token punctuation">)</span>application<span class="token punctuation">:</span><span class="token punctuation">(</span>UIApplication <span class="token operator">*</span><span class="token punctuation">)</span>application didReceiveLocalNotification<span class="token punctuation">:</span><span class="token punctuation">(</span>UILocalNotification <span class="token operator">*</span><span class="token punctuation">)</span>notification
   <span class="token punctuation">{</span>
    <span class="token punctuation">[</span>RCTPushNotificationManager didReceiveLocalNotification<span class="token punctuation">:</span>notification<span class="token punctuation">]</span><span class="token punctuation">;</span>
   <span class="token punctuation">}</span></div></div><span><h3><a class="anchor" name="methods"></a>Methods <a class="hash-link" href="docs/pushnotificationios.html#methods">#</a></h3><div class="props"><div class="prop"><h4 class="methodTitle"><a class="anchor" name=""></a>=<span class="methodType">(NewData, NoData, ResultFailed, }, static, (, :)</span> <a class="hash-link" href="docs/pushnotificationios.html#">#</a></h4></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="schedulelocalnotification"></a><span class="methodType">static </span>scheduleLocalNotification<span class="methodType">(details)</span> <a class="hash-link" href="docs/pushnotificationios.html#schedulelocalnotification">#</a></h4><div><p>Schedules the localNotification for future presentation.</p><p>details is an object containing:</p><ul><li><code>fireDate</code> : The date and time when the system should deliver the notification.</li><li><code>alertBody</code> : The message displayed in the notification alert.</li><li><code>alertAction</code> : The "action" displayed beneath an actionable notification. Defaults to "view";</li><li><code>soundName</code> : The sound played when the notification is fired (optional).</li><li><code>isSilent</code>  : If true, the notification will appear without sound (optional).</li><li><code>category</code>  : The category of this notification, required for actionable notifications (optional).</li><li><code>userInfo</code> : An optional object containing additional notification data.</li><li><code>applicationIconBadgeNumber</code> (optional) : The number to display as the app's icon badge. Setting the number to 0 removes the icon badge.</li><li><code>repeatInterval</code> : The interval to repeat as a string.  Possible values: <code>minute</code>, <code>hour</code>, <code>day</code>, <code>week</code>, <code>month</code>, <code>year</code>.</li></ul></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="cancelalllocalnotifications"></a><span class="methodType">static </span>cancelAllLocalNotifications<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#cancelalllocalnotifications">#</a></h4><div><p>Cancels all scheduled localNotifications</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="removealldeliverednotifications"></a><span class="methodType">static </span>removeAllDeliveredNotifications<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#removealldeliverednotifications">#</a></h4><div><p>Remove all delivered notifications from Notification Center</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getdeliverednotifications"></a><span class="methodType">static </span>getDeliveredNotifications<span class="methodType">(callback)</span> <a class="hash-link" href="docs/pushnotificationios.html#getdeliverednotifications">#</a></h4><div><p>Provides you with a list of the appâ€™s notifications that are still displayed in Notification Center</p><p>@param callback Function which receive an array of delivered notifications</p><p> A delivered notification is an object containing:</p><ul><li><code>identifier</code>  : The identifier of this notification.</li><li><code>title</code>  : The title of this notification.</li><li><code>body</code>  : The body of this notification.</li><li><code>category</code>  : The category of this notification, if has one.</li><li><code>userInfo</code>  : An optional object containing additional notification data.</li><li><code>thread-id</code>  : The thread identifier of this notification, if has one.</li></ul></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="removedeliverednotifications"></a><span class="methodType">static </span>removeDeliveredNotifications<span class="methodType">(identifiers)</span> <a class="hash-link" href="docs/pushnotificationios.html#removedeliverednotifications">#</a></h4><div><p>Removes the specified notifications from Notification Center</p><p>@param identifiers Array of notification identifiers</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="setapplicationiconbadgenumber"></a><span class="methodType">static </span>setApplicationIconBadgeNumber<span class="methodType">(number)</span> <a class="hash-link" href="docs/pushnotificationios.html#setapplicationiconbadgenumber">#</a></h4><div><p>Sets the badge number for the app icon on the home screen</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getapplicationiconbadgenumber"></a><span class="methodType">static </span>getApplicationIconBadgeNumber<span class="methodType">(callback)</span> <a class="hash-link" href="docs/pushnotificationios.html#getapplicationiconbadgenumber">#</a></h4><div><p>Gets the current badge number for the app icon on the home screen</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="cancellocalnotifications"></a><span class="methodType">static </span>cancelLocalNotifications<span class="methodType">(userInfo)</span> <a class="hash-link" href="docs/pushnotificationios.html#cancellocalnotifications">#</a></h4><div><p>Cancel local notifications.</p><p>Optionally restricts the set of canceled notifications to those
notifications whose <code>userInfo</code> fields match the corresponding fields
in the <code>userInfo</code> argument.</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getscheduledlocalnotifications"></a><span class="methodType">static </span>getScheduledLocalNotifications<span class="methodType">(callback)</span> <a class="hash-link" href="docs/pushnotificationios.html#getscheduledlocalnotifications">#</a></h4><div><p>Gets the local notifications that are currently scheduled.</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="addeventlistener"></a><span class="methodType">static </span>addEventListener<span class="methodType">(type, handler)</span> <a class="hash-link" href="docs/pushnotificationios.html#addeventlistener">#</a></h4><div><p>Attaches a listener to remote or local notification events while the app is running
in the foreground or the background.</p><p>Valid events are:</p><ul><li><code>notification</code> : Fired when a remote notification is received. The
handler will be invoked with an instance of <code>PushNotificationIOS</code>.</li><li><code>localNotification</code> : Fired when a local notification is received. The
handler will be invoked with an instance of <code>PushNotificationIOS</code>.</li><li><code>register</code>: Fired when the user registers for remote notifications. The
handler will be invoked with a hex string representing the deviceToken.</li><li><code>registrationError</code>: Fired when the user fails to register for remote
notifications. Typically occurs when APNS is having issues, or the device
is a simulator. The handler will be invoked with
{message: string, code: number, details: any}.</li></ul></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="removeeventlistener"></a><span class="methodType">static </span>removeEventListener<span class="methodType">(type, handler)</span> <a class="hash-link" href="docs/pushnotificationios.html#removeeventlistener">#</a></h4><div><p>Removes the event listener. Do this in <code>componentWillUnmount</code> to prevent
memory leaks</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="requestpermissions"></a><span class="methodType">static </span>requestPermissions<span class="methodType">(permissions?)</span> <a class="hash-link" href="docs/pushnotificationios.html#requestpermissions">#</a></h4><div><p>Requests notification permissions from iOS, prompting the user's
dialog box. By default, it will request all notification permissions, but
a subset of these can be requested by passing a map of requested
permissions.
The following permissions are supported:</p><ul><li><code>alert</code></li><li><code>badge</code></li><li><code>sound</code></li></ul><p>If a map is provided to the method, only the permissions with truthy values
will be requested.</p><p>This method returns a promise that will resolve when the user accepts,
rejects, or if the permissions were previously rejected. The promise
resolves to the current state of the permission.</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="abandonpermissions"></a><span class="methodType">static </span>abandonPermissions<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#abandonpermissions">#</a></h4><div><p>Unregister for all remote notifications received via Apple Push Notification service.</p><p>You should call this method in rare circumstances only, such as when a new version of
the app removes support for all types of remote notifications. Users can temporarily
prevent apps from receiving remote notifications through the Notifications section of
the Settings app. Apps unregistered through this method can always re-register.</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="checkpermissions"></a><span class="methodType">static </span>checkPermissions<span class="methodType">(callback)</span> <a class="hash-link" href="docs/pushnotificationios.html#checkpermissions">#</a></h4><div><p>See what push permissions are currently enabled. <code>callback</code> will be
invoked with a <code>permissions</code> object:</p><ul><li><code>alert</code> :boolean</li><li><code>badge</code> :boolean</li><li><code>sound</code> :boolean</li></ul></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getinitialnotification"></a><span class="methodType">static </span>getInitialNotification<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#getinitialnotification">#</a></h4><div><p>This method returns a promise that resolves to either the notification
object if the app was launched by a push notification, or <code>null</code> otherwise.</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="constructor"></a>constructor<span class="methodType">(nativeNotif)</span> <a class="hash-link" href="docs/pushnotificationios.html#constructor">#</a></h4><div><p>You will never need to instantiate <code>PushNotificationIOS</code> yourself.
Listening to the <code>notification</code> event and invoking
<code>getInitialNotification</code> is sufficient</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="finish"></a>finish<span class="methodType">(fetchResult)</span> <a class="hash-link" href="docs/pushnotificationios.html#finish">#</a></h4><div><p>This method is available for remote notifications that have been received via:
<code>application:didReceiveRemoteNotification:fetchCompletionHandler:</code>
<a href="https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplicationDelegate_Protocol/#//apple_ref/occ/intfm/UIApplicationDelegate/application:didReceiveRemoteNotification:fetchCompletionHandler">https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplicationDelegate_Protocol/#//apple_ref/occ/intfm/UIApplicationDelegate/application:didReceiveRemoteNotification:fetchCompletionHandler</a>:</p><p>Call this to execute when the remote notification handling is complete. When
calling this block, pass in the fetch result value that best describes
the results of your operation. You <em>must</em> call this handler and should do so
as soon as possible. For a list of possible values, see <code>PushNotificationIOS.FetchResult</code>.</p><p>If you do not call this method your background remote notifications could
be throttled, to read more about it see the above documentation link.</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getmessage"></a>getMessage<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#getmessage">#</a></h4><div><p>An alias for <code>getAlert</code> to get the notification's main message string</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getsound"></a>getSound<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#getsound">#</a></h4><div><p>Gets the sound string from the <code>aps</code> object</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getcategory"></a>getCategory<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#getcategory">#</a></h4><div><p>Gets the category string from the <code>aps</code> object</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getalert"></a>getAlert<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#getalert">#</a></h4><div><p>Gets the notification's main message from the <code>aps</code> object</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getcontentavailable"></a>getContentAvailable<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#getcontentavailable">#</a></h4><div><p>Gets the content-available number from the <code>aps</code> object</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getbadgecount"></a>getBadgeCount<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#getbadgecount">#</a></h4><div><p>Gets the badge count number from the <code>aps</code> object</p></div></div><div class="prop"><h4 class="methodTitle"><a class="anchor" name="getdata"></a>getData<span class="methodType">()</span> <a class="hash-link" href="docs/pushnotificationios.html#getdata">#</a></h4><div><p>Gets the data object on the notif</p></div></div></div></span></div>