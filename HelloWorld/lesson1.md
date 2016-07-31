# Android Hello World

## Setup
In Android Studio, create a new project:
- If you don't have a project opened, in the Welcome screen, click New Project.
- If you have a project opened, from the File menu, select New Project. The Create New Project screen appears.

Fill out the fields on the screen.
- For Application Name use "My First App". For Company Domain, use "livewires.dev". For the other fields, use the default values and click Next

Here's a brief explanation of each field:
- Application Name is the app name that appears to users.
- Company domain provides a qualifier that will be appended to the package name; Android Studio will remember this qualifier for each new project you create.
- Package name is the fully qualified name for the project (following the same rules as those for naming packages in the Java programming language). Your package name must be unique across all packages installed on the Android system. You can Edit this value independently from the application name or the company domain.
- Project location is the directory on your system that holds the project files.

Under Target Android Devices, accept the default values and click Next.

The Minimum Required SDK is the earliest version of Android that your app supports, indicated using the API level. To support as many devices as possible, you should set this to the lowest version available that allows your app to provide its core feature set. If any feature of your app is possible only on newer versions of Android and it's not critical to the app's core feature set, you can enable the feature only when running on the versions that support it (as discussed in Supporting Different Platform Versions).

Under Add an Activity to Mobile, select Empty Activity and click Next.

Activities

An activity is one of the distinguishing features of the Android framework. Activities provide the user with access to your app, and there may be many activities. An application will usually have a main activity for when the user launches the application, another activity for when she selects some content to view, for example, and other activities for when she performs other tasks within the app. See Activities for more information.

Under Customize the Activity, accept the default values and click Finish.
Your Android project is now a basic "Hello World" app that contains some default files. Take a moment to review the most important of these:

`app/src/main/java/com.example.myfirstapp/MainActivity.java`
This file appears in Android Studio after the New Project wizard finishes. It contains the class definition for the activity you created earlier. When you build and run the app, the Activity starts and loads the layout file that says "Hello World!"

`app/src/main/res/layout/activity_main.xml`
This XML file defines the layout of the activity. It contains a TextView element with the text "Hello world!".

`app/src/main/AndroidManifest.xml`
The manifest file describes the fundamental characteristics of the app and defines each of its components. You'll revisit this file as you follow these lessons and add more components to your app.

`app/build.gradle`
Android Studio uses Gradle to compile and build your app. There is a build.gradle file for each module of your project, as well as a build.gradle file for the entire project. Usually, you're only interested in the build.gradle file for the module, in this case the app or application module. This is where your app's build dependencies are set, including the `defaultConfig` settings:

`compiledSdkVersion` is the platform version against which you will compile your app. By default, this is set to the latest version of Android available in your SDK. By default, this is set to the latest version of Android SDK installed on your development machine. You can still build your app to support older versions, but setting this to the latest version allows you to enable new features and optimize your app for a great user experience on the latest devices.

`applicationId` is the fully qualified package name for your application that you specified in the New Project wizard.

`minSdkVersion` is the Minimum SDK version you specified during the New Project wizard. This is the earliest version of the Android SDK that your app supports.

`targetSdkVersion` indicates the highest version of Android with which you have tested your application. As new versions of Android become available, you should test your app on the new version and update this value to match the latest API level and thereby take advantage of new platform features.

Note also the `/res` subdirectories that contain the resources for your application:

`drawable-<density>/`
Directories for drawable resources, other than launcher icons, designed for various densities.

`layout/`
Directory for files that define your app's user interface like activity_main.xml, discussed above, which describes a basic layout for the MainActivity class.

`menu/`
Directory for files that define your app's menu items.

`mipmap/`
Launcher icons reside in the `mipmap/` folder rather than the `drawable/` folders. This folder contains the ic_launcher.png image that appears when you run the default app.

`values/`
Directory for other XML files that contain a collection of resources, such as string and color definitions.

## Running the app

Set up your device as follows:

Connect your device to your development machine with a USB cable. If you're developing on Windows, you might need to install the appropriate USB driver for your device. For help installing drivers, see the OEM USB Drivers document.
Enable USB debugging on your device by going to Settings > Developer options.

> Note: On Android 4.2 and newer, Developer options is hidden by default. To make it available, go to Settings > About phone and tap Build number seven times. Return to the previous screen to find Developer options.

Run the app from Android Studio as follows:

1. In Android Studio, select your project and click Run  from the toolbar.
2. In the Select Deployment Target window, select your device, and click OK.

Android Studio installs the app on your connected device and starts it.

## Building a Simple User Interface

In this lesson, you create a layout in XML that includes a text field and a button. In the next lesson, your app responds when the button is pressed by sending the content of the text field to another activity.

The graphical user interface for an Android app is built using a hierarchy of View and ViewGroup objects. View objects are usually UI widgets such as buttons or text fields. ViewGroup objects are invisible view containers that define how the child views are laid out, such as in a grid or a vertical list.

Android provides an XML vocabulary that corresponds to the subclasses of View and ViewGroup so you can define your UI in XML using a hierarchy of UI elements.

Layouts are subclasses of the ViewGroup. In this exercise, you'll work with a LinearLayout.

![Illustration of how ViewGroup objects form branches in the layout and contain other View objects.](https://developer.android.com/images/viewgroup.png)

## Linear Layout

1. From the res/layout/ directory, open the activity_main.xml file. This XML file defines the layout of your activity. It contains the default "Hello World" text view.
2. When you open a layout file, you’re first shown the design editor in the Layout Editor. For this lesson, you work directly with the XML, so click the Text tab to switch to the text editor.
Replace the contents of the file with the following XML:

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
</LinearLayout>
```

`LinearLayout` is a view group (a subclass of `ViewGroup`) that lays out child views in either a vertical or horizontal orientation, as specified by the `android:orientation` attribute. Each child of a `LinearLayout` appears on the screen in the order in which it appears in the XML.

Two other attributes, `android:layout_width` and `android:layout_height`, are required for all views in order to specify their size.

Because the `LinearLayout` is the root view in the layout, it should fill the entire screen area that's available to the app by setting the width and height to "`match_parent`". This value declares that the view should expand its width or height to match the width or height of the parent view.

For more information about layout properties, see the Layout guide.

## Adding a text field

In the `activity_main.xml` file, within the `<LinearLayout>` element, add the following `<EditText>` element:

```
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <EditText android:id="@+id/edit_message"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:hint="@string/edit_message" />
</LinearLayout>
```

## Add String Resources

By default, your Android project includes a string resource file at `res/values/strings.xml`. Here, you'll add two new strings.

From the `res/values/` directory, open `strings.xml`.
Add two strings so that your file looks like this:

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">My First App</string>
    <string name="edit_message">Enter a message</string>
    <string name="button_send">Send</string>
</resources>
```

For text in the user interface, always specify each string as a resource. String resources allow you to manage all UI text in a single location, which makes the text easier to find and update. Externalizing the strings also allows you to localize your app to different languages by providing alternative definitions for each string resource.

## Add a Button

Go back to the `activity_main.xml` file and add a button after the `<EditText>`. Your file should look like this:

```
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
        <EditText android:id="@+id/edit_message"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:hint="@string/edit_message" />
        <Button
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="@string/button_send" />
</LinearLayout>
```

The layout is currently designed so that both the `EditText` and `Button` widgets are only as big as necessary to fit their content, as figure 2 shows.

![The EditText and Button widgets have their widths set to "wrap_content".](https://developer.android.com/images/training/firstapp/edittext_wrap.png)

This works fine for the button, but not as well for the text field, because the user might type something longer. It would be nice to fill the unused screen width with the text field. You can do this inside a `LinearLayout` with the weight property, which you can specify using the `android:layout_weight` attribute.

The weight value is a number that specifies the amount of remaining space each view should consume, relative to the amount consumed by sibling views. This works kind of like the amount of ingredients in a drink recipe: "2 parts soda, 1 part syrup" means two-thirds of the drink is soda. For example, if you give one view a weight of 2 and another one a weight of 1, the sum is 3, so the first view fills 2/3 of the remaining space and the second view fills the rest. If you add a third view and give it a weight of 1, then the first view (with weight of 2) now gets 1/2 the remaining space, while the remaining two each get 1/4.

The default weight for all views is 0, so if you specify any weight value greater than 0 to only one view, then that view fills whatever space remains after all views are given the space they require.

## Make the Input Box Fill in the Screen Width

In `activity_main.xml`, modify the `<EditText>` so that the attributes look like this:

```
<EditText android:id="@+id/edit_message"
    android:layout_weight="1"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:hint="@string/edit_message" />
```

Setting the width to zero (0dp) improves layout performance because using "`wrap_content`" as the width requires the system to calculate a width that is ultimately irrelevant because the weight value requires another width calculation to fill the remaining space.

![The EditText widget is given all the layout weight, so it fills the remaining space in the LinearLayout.](https://developer.android.com/images/training/firstapp/edittext_gravity.png)

Here’s how your complete `activity_main.xml` layout file should now look:

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:orientation="horizontal"
   android:layout_width="match_parent"
   android:layout_height="match_parent">
    <EditText android:id="@+id/edit_message"
        android:layout_weight="1"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="@string/edit_message" />
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/button_send" />
</LinearLayout>
```

## Run Your App
This layout is applied by the default Activity class that the SDK tools generated when you created the project.

To run the app and see the results, click Run 'app' in the toolbar.

## Respond to the Send Button

In the file `res/layout/activity_main.xml`, add the `android:onClick` attribute to the `<Button>` element as shown below:

```
<Button
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:text="@string/button_send"
      android:onClick="sendMessage" />
```

This attribute tells the system to call the `sendMessage()` method in your activity whenever a user clicks on the button.

In the file `java/com.example.myfirstapp/MainActivity.java`, add the `sendMessage()` method stub as shown below:

```
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void sendMessage(View view) {
        // Do something in response to button
    }
}
```

In order for the system to match this method to the method name given to `android:onClick`, the signature must be exactly as shown. Specifically, the method must:

- Be public
- Have a void return value
- Have a View as the only parameter (this will be the View that was clicked)

Next, you’ll fill in this method to read the contents of the text field and deliver that text to another activity.

## Build an Intent

An Intent is an object that provides runtime binding between separate components (such as two activities). The Intent represents an app’s "intent to do something." You can use intents for a wide variety of tasks, but in this lesson, your intent starts another activity.

In `MainActivity.java`, add the code shown below to `sendMessage()`:

```
public class MainActivity extends AppCompatActivity {
    public final static String EXTRA_MESSAGE = "com.example.myfirstapp.MESSAGE";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void sendMessage(View view) {
        Intent intent = new Intent(this, DisplayMessageActivity.class);
        EditText editText = (EditText) findViewById(R.id.edit_message);
        String message = editText.getText().toString();
        intent.putExtra(EXTRA_MESSAGE, message);
        startActivity(intent);
    }
}
```

There’s a lot going on in `sendMessage()`, so let’s explain what's going on.

The Intent constructor takes two parameters:

- A Context as its first parameter (this is used because the Activity class is a subclass of Context)
- The Class of the app component to which the system should deliver the Intent (in this case, the activity that should be started).

The `putExtra()` method adds the EditText's value to the intent. An Intent can carry data types as key-value pairs called extras. Your key is a public constant `EXTRA_MESSAGE` because the next activity uses the key to retrive the text value. It's a good practice to define keys for intent extras using your app's package name as a prefix. This ensures the keys are unique, in case your app interacts with other apps.

The `startActivity()` method starts an instance of the `DisplayMessageActivity` specified by the Intent. Now you need to create the class.

## Create the Second Activity

1. In the Project window, right-click the app folder and select New > Activity > Empty Activity.
2. In the Configure Activity window, enter "`DisplayMessageActivity`" for Activity Name and click Finish

Android Studio automatically does three things:

- Creates the class `DisplayMessageActivity.java` with an implementation of the required `onCreate()` method.
- Creates the corresponding layout file activity_display_message.xml
- Adds the required <activity> element in AndroidManifest.xml.
- 
If you run the app and click the Send button on the first activity, the second activity starts but is empty. This is because the second activity uses the default empty layout provided by the template.

## Display the Message

Now you will modify the second activity to display the message that was passed by the first activity.

In `DisplayMessageActivity.java`, add the following code to the `onCreate()` 
method:

```
@Override
protected void onCreate(Bundle savedInstanceState) {
   super.onCreate(savedInstanceState);
   setContentView(R.layout.activity_display_message);

   Intent intent = getIntent();
   String message = intent.getStringExtra(MainActivity.EXTRA_MESSAGE);
   TextView textView = new TextView(this);
   textView.setTextSize(40);
   textView.setText(message);

   ViewGroup layout = (ViewGroup) findViewById(R.id.activity_display_message);
   layout.addView(textView);
}
```

Press Alt + Enter (option + return on Mac) to import missing classes.

There’s a lot going on here, so let’s explain:

1. The call `getIntent()` grabs the intent that started the activity. Every Activity is invoked by an Intent, regardless of how the user navigated there. The call `getStringExtra()` retrieves the data from the first activity.
2. You programmatically create a `TextView` and set its size and message.
3. You add the `TextView` to the layout identified by `R.id.activity_display_message`. You cast the layout to `ViewGroup` because it is the superclass of all layouts and contains the `addView()` method.

You can now run the app. When it opens, type a message in the text field, and click Send. The second activity replaces the first one on the screen, showing the message you entered in the first activity.

That's it, you've built your first Android app!


