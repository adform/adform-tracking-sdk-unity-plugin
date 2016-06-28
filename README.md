# Adform Tracking SDK Unity Plugin

Adform Tracking SDK Unity Plugin provides a way to integrate Adform tracking in Unity applications easily. This plugin applies for Android and iOS unity applications.

## Importing the Plugin

Our plugin is available on [GitHub](https://github.com/adform-tracking-sdk-unity-plugin).

To add the downloaded plugin:

1. Open your Unity project.
2. Go to `Assets -> Import Package -> Custom Package` and select the
`AdformTrackingSDK.unitypackage` to import. Import everything that is included in the pakage for your desired platform (iOS and/or Android).
3. In your GameObject, click `Add Component -> New Script`.
4. Integrate tracking in that script. An example of this script could be found in `Assets/Adform/Tracking/Sample/Sample.cs`.

## Basic integration

To initiate Adform Tracking SDK, execute `init()` method. 

`AdformTrackingSDK.init();`

To start tracking, you need to run `startTracking` method. Note that Tracking_ID should be replaced with your tracking id.

`AdformTrackingSdk.startTracking(this, Tracking_ID);`

Also, AdformTrackingSdk needs methods that would indicate of application activity resume and pause. In Unity you could override `OnApplicationPause(bool pauseStatus)` method to execute AdformTrackingSdk `onPause` and `OnResume`.

```c#
void OnApplicationPause (bool pauseStatus) 
{
if (pauseStatus) {
AdformTrackingSDK.onPause ();
} else {
AdformTrackingSDK.onResume ();
}
}
```

Optionally, you can set custom application name and order before calling startTracking:

```c#
Order order = new Order ();
order.country = "Australia";
AdformTrackingSDK.setOrder (order);
AdformTrackingSDK.setAppName ("app name");
```

## Sending custom app events

To create an event, first you need to create a TrackPoint with Tracking_ID. Note that startTracking should occur before event sending.

```c#
TrackPoint trackPoint = new TrackPoint();
trackPoint.trackPointId	 = Tracking_ID;
```

Also some advanced integrations are available, like custom parameter or using custom application name setting.

Setting custom application name:

```c#
trackPoint.appName = "custom application name";
```

Adding custom parameters (key values should be the same as it is in Adform data exports, for example sv1, sv2..sv89, var1, var2...var10, sales, orderid, etc.):

```c#
Order order = new Order ();
order.country = "Australia";    
trackPoint.order = order;
```

Setting custom tracking point name:

```c#
trackPoint.sectionName = "Tracking point name";
```

To send prepared track point, just use sendTrackPoint.

```c#
AdformTrackingSDK.sendTrackPoint(trackPoint);
```

Also it is posible to send additional product variables information with tracking points. To do so you need to create 'Product' object and set your product values. Then add that object to the trackpoint.

```c#
Product product = new Product ();
product.productId = "Product ID";
product.productName = "Product name";
product.categoryId = "Category ID";
product.categoryName = "Category name";
product.productSales = 545f;
product.productCount = 11;
product.weight = 5;

Product[] products = new Product[] {
product
};
trackpoint.products = products;
```

Do not forget to call `sendTrackPoint(trackPoint)` method to send your trackpoint with product items. 

## Custom Adform Tracking SDK implementations

### Enable/Disable tracking

You can enable/disable tracking by calling `setEnabled(boolean)` method.

```c#
AdformTrackingSDK.setEnabled(true);
```

### Enable/Disable HTTPS

You can enable/disable HTTPS protocol by calling `setHttpsEnabled(boolean)` method. By default HTTPS is enabled.

```c#
AdformTrackingSDK.setHttpsEnabled(true);
```

### Enable/Disable SIM card state tracking

You can enable/disable tracking by calling `setSendSimCardStateEnabled(boolean)` method. By default SIM card state tracking is disabled.

```c#
AdformTrackingSDK.setSendSimCardStateEnabled(true);
```


## Configuration for Android

The `Assets/Plugins/Android` folder includes a working example of `AndroidManifest.xml`. This example contains the necessary components, simply modify it to suit your needs. 

If you already have `AndroidManifest.xml` file in you android directory, modify it according to [Adform Tracking SDK documentation](https://github.com/adform/adform-tracking-android-sdk-dev#3-update-androidmanifestxml).

Adform Tracking SDK Unity Plugin also requires the [Google Play Services](http://developer.android.com/google/play-services/setup.html). Google Play Services are located at `{ANDROID_SDK_LOCATION}/extras/google/google_play_services/libproject`, please import `google-play-services_lib` folder into `Assets/Plugins/Android` directory.

Adform Tracking SDK Unity Plugin also requires Google Protocol Buffers library, this library is already included in the Unity package, so you don't need to download and import it seperately.

## Configuration for iOS

You must make sure that these frameworks are included to unity generated xCode project for the sdk to work properly:

* AdSupport.framework
* CoreData.framework
* SystemConfiguration.framework
* CoreTelephony.framework
* SafariServices.framework

Adform Tracking SDK Unity Plugin also requires Google Protocol Buffers library, this library is already included in the Unity package, so you don't need to download and import it seperately.
