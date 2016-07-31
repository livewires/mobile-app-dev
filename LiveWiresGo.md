# LiveWiresGo

## Get a map on screen

Open up Android Studio and create a new project called 'Go'. Add an `Empty activity` to the project.

In `build.gradle` in the `dependancies` node add this:

```
compile 'com.google.android.gms:play-services-maps:7.8.0'
compile 'com.google.android.gms:play-services-location:7.8.0'
```

Open up `AndroidManifest.xml`. Before the `application` starts add:

```
<uses-feature
    android:glEsVersion="0x00020000"
    android:required="true"/>
 
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

Then within the `application` node add:

```
<meta-data
    android:name="com.google.android.gms.version"
    android:value="@integer/google_play_services_version" />
 
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="@string/google_api_key"/>
```

In `res/values/strings.xml` add the following in the `resources` node

    <string name="google_api_key">{{ ASK JAMES FOR THIS }}</string>

Next, create a new Java class called `MapFragment`:

```
package dev.livewires.map;
import com.google.android.gms.maps.SupportMapFragment;
public class MapFragment extends SupportMapFragment {
    // Coming soon...
}
```

Once you have the initial fragment built, you need to let `MainActivity` know that it should use this fragment. Open `activity_main.xml` from your resources folder and change it so that it includes the fragment as a view.

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="dev.livewires.map.MainActivity">
    
    <fragment
        android:id="@+id/map"
        android:name="dev.livewires.map.MapFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</RelativeLayout>
```

Hit `play`, you should get a map appearing in the centre of your phone.

## Get a blue dot to show your location

## Place pins in random locations around current location

##Replace pin with data behind then - {name: 'David', image: 'david_face.jpg'}

## When user is within pin radius show pin. Else hide pin

## On pin click "A wild David appeared screen"

## Capture David (rand) if true then success else escape and respawn elsewhere on the map

