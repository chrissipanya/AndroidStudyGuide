# Core Android

#### Tell all the Android application components

###### Activites
-	entry point of the app
-	keeps track of what user cares about (what is on the screeen)	
-	knowing prevously used process so it can go back to it
-	helpping app kill process so user can return to prevous state
-	provide a way for apps to implement user flow between each other

###### Services
-	general-purpose entry point for keeping a app running in the background
-	allow process to run in the background
-	example: music player
-	can be killed and restarted later

###### Broadcast receivers
-	enable the system to deliver event to the app outside of a regular user flow
-	allow the app to respond to system-wide broadcast even to app that isnt currently running
-	Example: 
-	an app can schedule an alarm to post a notification to tell the user about an upcoming event... and by delivering that alarm to a BroadcastReceiver of the app, there is no need for the app to remain running until the alarm goes off
-	broadcast receiver is just a gateway to other components and is intended to do a very minimal amount of work 

###### Content providers (used to talk to database?)
-	manages a shared set of app data that you can store in the file system
-	can use different ways to store its data and the data can be stored in a database, in files, or even over a network.
-	Shared Preferences V.S. Content Provider
-	shared preferences are the location where you can store the secret information for your app, like setting cookies in the browser, this can be used for login credentials and other
	-	used key vaule pairs
	-	easy to store and retrieve data, but only small data
	-	issues with big strcture data
		-	need to define key for every single data, furthermore you cannot really search within the data except you have a certain concept for naming the keys
-	content provider stores and retrieves the data and make it available to other applications also. like suppose you want to access the contacts available in the android phone, they can be accessed by content providers
	-	manage structure data
	-	encapsulate the data, and provide mechanisms for defining data security
	-	standard interface that connects data in one process with code running in another process.

#### What is the project structure of an Android Application? 
-	AndroidManifest.xml - stored in the root directory of its project hierarchy and it defines the structure and metadata of our application, its components, and its requirements
-	Java - where the source  code lives
-	drawable - resource files like png, vector, ect.
-	layout - screen/user interface
-	mipmap - image asset like android icons
-	color.xml - color resource
-	string.xml - string resrouce
-	styles.xml - theme style resource
-	build.gradle(Module:app) - define build configurations and add dependencies 


#### What is Context? How is it used?
-	It is the context of the current state of the application.
-	It can be used to get information regarding the activity and application.
-	It can be used to get access to resources, databases, and shared preferences, and etc.
-	Both the Activity and Application classes extend the Context class.
-	Application Context - It is the application and we are present in Application. For example - MyApplication(which extends Application class). It is an instance of MyApplication only.
-	You only use getApplicationContext() when you know you need a Context for something that may live longer than any other likely Context you have at your disposal.
-	Activity Context - It is the activity and we are present in Activity. For example - MainActivity. It is an instance of MainActivity only.
-	Always try to use the nearest context which is available to you. When you are in Activity, the nearest context is Activity context. When you are in Application, the nearest context is the Application context. If Singleton, use the Application Context.


#### What is Application class?
-	The Application class in Android is the base class within an Android app that contains all other components such as activities and services. The Application class, or any subclass of the Application class, is instantiated before any other class when the process for your application/package is created.



# Activity and Fragment

#### What is Activity and its lifecycle?
-	UI over the screen is called activity
-	provide a window to draw the UI of your app
-	Lifecycle
-	**onCreate()** : It is called when an activity is first created. When a user opens the app then some Activity is created. You have to implement this method in every activity because, inside this method, all the necessary components of your activity will be initialized. Here the initialization of your application's UI is done.
-	**onStart()**: This method is called when an activity becomes visible to the user. When all the initialization is done by the onCreate() method, then this method is called.
-	**onResume()**: It is called just before the user starts interacting with the application. Most of the core functionalities of the app are implemented in this method.
-	**onPause()**:  It is called when the activity is paused i.e. it is mostly called when you press the back or home button of your Android device. It is an indication that the user is leaving the activity and starting some other activity.
-	**onStop()**: It is called when the activity is no longer visible to the user. If you are starting a new activity, or some existing activity is entering into onResume() state, then the current activity will not be visible to the user and is stopped.
-	**onRestart()**: It is called when the activity in the stopped state is about to start again. By doing so, the state of the activity from the time it was stopped will be restored.
-	**onDestroy()**: It is  called when the activity is totally destroyed i.e. when you clear the application stack then onDestroy() will be called and all the states of the activity will be destroyed.

#### What is the difference between onCreate() and onStart() 
-	**onCreate()** is called when the Activity is created; that is, it is launched or started.
-	**onStart()** is called following onCreate() at startup. Additionally, it is also called when the app is navigated back to after onStop() (and following onRestart()), which occurs after the Activity is no longer visible 

#### When only onDestroy is called for an activity without onPause() and onStop()? 
-	Call **finish()**
-	destorys activity, used when user doesnt want the activity to load again

#### Why do we need to call setContentView() in onCreate() of Activity class? 
-	Reason why is because onCreate() only gets called once. Only need to call setContentView() once

#### What is onSavedInstanceState() and onRestoreInstanceState() in activity?
-	**onSavedInstanceState()** - This method is used to store data before pausing the activity.
-	**onRestoreInstanceState()** - This method is used to recover the saved state of an activity when the activity is recreated after destruction. So, the onRestoreInstanceState() receive the bundle that contains the instance state information.

#### What is Fragment and its lifecycle?
-	A Fragment is a piece of an activity which enable more modular activity design. Kind of like a sub-activity
-	Life Cycle
	-	When fragment come up on the screen:
		-	**onAttach()** — This method called first, To know that our fragment has been attached to an activity. We are passing the Activity that will host our fragment.
		-	**onCreate()** —  This method called when a fragment instance initializes, just after the onAttach where fragment attaches to the host activity.
		-	**onCreateView()** —  The method called when it’s time for the fragment to draw its user interface for the first time. To draw a UI for your fragment, you must return a View component from this method that is the root of your fragment’s layout. You can return null if the fragment does not provide a UI.
		-	**onActivityCreated()** — This method called when Activity completes its onCreate() method
		-	**onStart()** — This method called when a fragment is visible
		-	**onResume()** — This method called when a fragment is visible and allowing the user to interact with it. Fragment resumes only after activity resumes.

	-	When fragment goes out off the screen:
		-	**onPause()** — This method called when a fragment is not allowing the user to interact; the fragment will get change with other fragment or it gets removed from activity or fragment’s activity called a pause.
		-	**onStop()** — This method called when the fragment is no longer visible; the fragment will get change with other fragment or it gets removed from activity or fragment’s activity called stop.
		-	**onDestroyView()** —  This method called when the view and related resources created in onCreateView() are removed from the activity’s view hierarchy and destroyed.
		-	**onDestroy()** —  This method called when the fragment does its final clean up.
		-	**onDetach()** —  This method called when the fragment is detached from its host activity.

#### What are "launch modes"?
-	Controls how to stack of the activity works
	-	singleTop
		-	if not top of the task, new instance will be created
	-	singleTask
		-	will destory top of stack to get to bottom task
	-	singleInstance
	-	standard
		-	if new activity starts, if not on top of stack, create new instance
-	Flags
	-	FLAG_NEW_TASK
	-	FLAG_CLEAR_TASK
	-	FLAG_SINGLE_TOP
	-	FLAG_CLEAR_TOP

#### What is the difference between a Fragment and an Activity? Explain the relationship between the two.
-	Fragment are solution for reuseable interface
	1. You can add or remove fragments in an activity while the activity is running.
	2. You can combine multiple fragments in a single activity to build a multi-pane UI.
	3. A fragment can be used in multiple activities.
	4. The fragment life cycle is closely related to the lifecycle of its host activity.
	5. When the activity is paused, all the fragments available in the acivity will also be stopped.
	6. A fragment can implement a behavior that has no user interface component.
	7. Fragments were added to the Android API in Android 3 (Honeycomb) with API version 11.	 
	8. A fragment has its own layout and its own behavior with its own lifecycle callbacks.

#### When should you use a Fragment rather than an Activity?
-	When you have some UI components to be used across various activities
-	When multiple view can be displayed side by side just like viewPager

#### What is the difference between FragmentPagerAdapter vs FragmentStatePagerAdapter?
-	**FragmentPagerAdapter**: Each fragment visited by the user will be stored in the memory but the view will be destroyed. When the page is revisited, then the view will be created not the instance of the fragment.
-	**FragmentStatePagerAdapter**: Here, the fragment instance will be destroyed when it is not visible to the user, except the saved state of the fragment.

#### What is the difference between adding/replacing fragment in backstack?
-	**replace** removes the existing fragment and adds a new fragment..
-	**add** retains the existing fragments and adds a new fragment that means existing fragment will be active and they wont be in 'paused' state hence when a back button is pressed onCreateView() is not called for the existing fragment(the fragment which was there before new fragment was added).

#### Why is it recommended to use only the default constructor to create a Fragment?
-	Android has no idea what constructor is created
-	Fragments need to have a no-args constructor for the Android system to instantiate them
-	Your Fragment subclasses need a public empty constructor as this is what's being called by the framework.

#### How would you communicate between two Fragments?
1.	With the help of ViewModel
2.	With the help of Interface
	1.	Make an Interface in your FragmentA
	2.	Implement the Interface of the FragmentA in your Activity
	3.	Call the Interface method from your Activity
	4.	In your Activity, call your FragmentB to do the required changes

#### What is retained Fragment?
-	By default, Fragments are destroyed and recreated along with their parent Activity’s when a configuration change occurs. Calling setRetainInstance(true) allows us to bypass this destroy-and-recreate cycle, signaling the system to retain the current instance of the fragment when the activity is recreated.

# Views and ViewGroups

#### What is View in Android?
-	component which Android provides us to design the layouts of the app

#### Difference between View.GONE and View.INVISIBLE?
-	View.GONE This view is invisible, and it doesn't take any space for layout purposes.
-	View.INVISIBLE This view is invisible, but it still takes up space for layout purposes.

#### Can you a create custom view? How?
-	Yes
	1.	By Extending an Existing Widget Class (eg. Button, TextView)
	2.	By Extending the View Class (eg. View)

#### What are ViewGroups and how they are different from the Views?
-	**View**: View objects are the basic building blocks of User Interface(UI) elements in Android. View is a simple rectangle box which responds to the user’s actions. Examples are EditText, Button, CheckBox etc. View refers to the android.view.View class, which is the base class of all UI classes.
-	**ViewGroup**: ViewGroup is the invisible container. It holds View and ViewGroup. For example, LinearLayout is the ViewGroup that contains Button(View), and other Layouts also. ViewGroup is the base class for Layouts.

#### What is a Canvas?
-	Canvas API in Android is a drawing framework which helps us to draw custom design like line, circle or even a rectangle. Using these we can make any shape whichever we want according to design.
-	The drawing of canvas happens in Bitmap, where we draw the outline and then the Paint API helps to fill color and whatever style we need.

#### What is a SurfaceView? 
-	SurfaceViews contain a nice rendering mechanism that allows threads to update the surface's content without using a handler (good for animation).
-	Surfaceviews cannot be transparent, they can only appear behind other elements in the view hierarchy.
-	faster for animation than rendering onto a View.
-	surfaceView can be updated on the background thread

#### Relative Layout vs Linear Layout.
- Relative means concerning another, or we can understand this as a relative to one another. In this layout, all the components are arranged concerning with each other.
-	Linear means in a line, either horizontal or vertical. We can understand here as all the elements inside the linear layout get arranged linearly, one after the other. If you are using horizontal orientation, then all the views inside the LinearLayout will be arranged horizontally one after the other.

#### Tell about Constraint Layout
-	ConstraintLayout is a view group which allows you to position and size widget in a flexible way.
-	ConstraintLayout provides a level of flexibility that allows many of the features of older layouts to be achieved with a single layout instance. Before, you needed to nest multiple layouts.

#### Do you know what is the view tree? How can you optimize its depth?
-	A view tree observer is used to register listeners that can be notified of global changes in the view tree.
-	not sure how to optimized its depth

#### How does the Touch Control and Events work in Android?
- Using touch gesture will trigger a callback event


# Displaying Lists of Content

#### What is the difference between ListView and RecyclerView?
-	RecyclerView is a improved version of ListView
-	The view are reusable, so overall doesn't use more resources than needed

#### How does RecyclerView work internally? 
-	Data Source -> Adapter(ViewHolder) -> RecyclerView(LayoutManager)

#### What is the ViewHolder pattern? Why should we use it?
-	Able access a element without needing to look it up everytime
-	It helps put with the performace.

#### What is SnapHelper?
-	SnapHelper is a helper class that helps in snapping any child view of the RecyclerView.


# Dialogs and Toasts

#### What is Dialog in Android?
-	It is a alert pop up
-	A dialog is a small window that prompts the user to make a decision or enter additional information. A dialog does not fill the screen and is normally used for modal events that require users to take an action before they can proceed.

#### What is Toast in Android? 
-	A toast provides simple feedback about an operation in a small popup. It only fills the amount of space required for the message and the current activity remains visible and interactive. Toasts automatically disappear after a timeout.

#### What the difference between Dialog and Dialog Fragment? 
-	Dialog is best used when doing simple alert or yes/no questions
	-	Dependent on actvivty life cycle
-	Dialog Fragment is best use for more complex events and/or views

# Intents and Broadcasting
#### What is Intent? 
-	An Intent is a messaging object you can use to request an action from another app component.
-	Types
	- Explicit Intents: If you want communication between the components of your application only then you can use the Explicit Intents
		-	communication in your own application
	-	Implicit Intents: Here, you don’t need to specify the fully-qualified address. All you need to do is just specify the action that is to be performed by an Intent
		-	you can communicate between various applications present in the mobile device
-	Use Cases
	-	Starting an Activity, Service and delivering a broadcast
-	Information present in Intent
	-	Action
		-	An action is a string that specifies the action to be performed by a particular Activity
		-	For example, you can use the ACTION_VIEW with startActivity() when your application contains some information like images that can be shown to the user
	-	Data 
		-	you can pass the data and the type of data on which the action is to be performed by the Android System with the help of Intents
		-	For example, if you want to edit some data then you have to pass the URI of the data in your ACTION_EDIT action.
	-	Category
		-	Category is used in case of Explicit Intents where you need to specify the type of application that will be used to perform a particular action. 
		-	For example, if you want to send some data then only data sending applications should be made available for choice to the users. 
	-	Component Name
		-	 the name of the component that is to be started. You can set the component name by using setComponent() or setClass() or with the Intent Constructor.
	-	Extras
		-	You can add extra data to an Intent in the form of key-value pairs and this extra information can be passed from one Activity to the other

#### What is a BroadcastReceiver?
-	android component which let an app to listen for system or application events.

#### What is a LocalBroadcastManager?
-	to register and send a broadcast of intents to local objects in your process
-	**deprecated**

#### What is a intent filter?
-	is an expression in an app's manifest file that specifies the type of intents that the component would like to receive.

#### What is a Sticky Intent?
-	Sticky Intents allows communication between a function and a service. sendStickyBroadcast() performs a sendBroadcast(Intent) known as sticky
-	i.e. the Intent you are sending stays around after the broadcast is complete, so that others can quickly retrieve that data through the return value of registerReceiver(BroadcastReceiver, IntentFilter). For example, if you take an intent for ACTION_BATTERY_CHANGED to get battery change events: When you call registerReceiver() for that action — even with a null BroadcastReceiver — you get the Intent that was last Broadcast for that action. Hence, you can use this to find the state of the battery without necessarily registering for all future state changes in the battery.

#### Describe how broadcasts and intents work to be able to pass messages around your app? 
-	https://stackoverflow.com/questions/7276537/using-a-broadcast-intent-broadcast-receiver-to-send-messages-from-a-service-to-a

#### What is a PendingIntent?
-	If you want someone to perform any Intent operation at future point of time on behalf of you, then we will use Pending Intent.

#### What are the different types of Broadcasts?
1.	Normal Broadcasts:
	-	These are asynchronous broadcasts.
	-	Receivers of this type of broadcasts may run in any order, sometimes altogether.
	-	This is efficient.
	-	Receivers cannot use the result.
	-	They cannot abort the included APIs.
	-	These broadcasts are sent with Context.sendBroadcast
2. Ordered Broadcasts
	-	These are synchronous broadcasts.
	-	One broadcast is delivered to one receiver at a time.
	-	Receivers can use the result. In fact as each receiver executes, result is passed to next receiver.
	-	Receiver can abort the broadcast and hence no broadcast is received by other receivers.
	-	The order of receivers is managed and controlled by the attribute android:priority in corresponding intent-filter.
	-	If receivers will have same priority then they may run in any order.

# Services

#### What is a service?
-	A Service is an application component that can perform long-running operations in the background.

####  Service vs IntentService.
1.	**Usage**: If you want some background task to be performed for a very long period of time, then you should use the IntentService. But at the same time, you should take care that there is no or very less communication with the main thread. If the communication is required then you can use main thread handler or broadcast intents. You can use Service for the tasks that don’t require any UI and also it is not a very long running task.
2.	**How to start?**: To start a Service you need to call the onStartService() method while in order to start a start IntentService you have to use Intent i.e. start the IntentService by calling Context.startService(Intent).
3.	**Running Thread**: Service always runs on the Main thread while the IntentService runs on a separate Worker thread that is triggered from the Main thread.
4.	**Triggering Thread**: Service can be triggered from any thread while the IntentService can be triggered only from the Main thread i.e. firstly, the Intent is received on the Main thread and after that, the Worker thread will be executed.
5.	**Main Thread blocking**: If you are using Service then there are chances that your Main thread will be blocked because Service runs on the Main thread. But, in case of IntentService, there is no involvement of the Main thread. Here, the tasks are performed in the form of Queue i.e. on the First Come First Serve basis.
6.	**Stop Service**: If you are using Service, then you have to stop the Service after using it otherwise the Service will be there for an infinite period of time i.e. until your phone is in normal state. So, to stop a Service you have to use stopService() or stopSelf(). But in the case of IntentService, there is no need of stopping the Service because the Service will be automatically stopped once the work is done.
7.	**Interaction with the UI**: If you are using IntentService, then you will find it difficult to interact with the UI of the application. If you want to out some result of the IntentService in your UI, then you have to take help of some Activity.

#### What is a JobScheduler?
-	An API for scheduling various types of jobs against the framework that will be executed in your application's own process

# Inter-process Communication

#### How can two distinct Android apps interact?
-	The app must use intents to send to send data bundles back and forth

#### Is it possible to run an Android app in multiple processes? How?
-	Yes, You can specify android:process=":remote" in your manifest to have an activity/service run in a seperate process. The "remote" is just the name of the remote process, and you can call it whatever you want. If you want several activities/services to run in the same process, just give it the same name.
		-	<activity android:name=".RemoteActivity" android:label="@string/app_name" android:process=":RemoteActivityProcess"/>

#### What is AIDL? Enumerate the steps in creating a bounded service through AIDL.
-	AIDL = Android Interface Definition Language
-	 It allows you to define the programming interface that both the client and service agree upon in order to communicate with each other using interprocess communication (IPC)
-	To create a bounded service using AIDL, follow these steps:
		1. Create the .aidl file
			-	This file defines the programming interface with method signatures.
		2.	Implement the interface
			-	The Android SDK tools generate an interface in the Java programming language, based on your .aidl file. This interface has an inner abstract class named Stub that extends Binder and implements methods from your AIDL interface. You must extend the Stub class and implement the methods.
		3.	Expose the interface to clients
			-	Implement a Service and override onBind() to return your implementation of the Stub class.

#### What can you use for background processing in Android?
-	Immedidate task
	-	We recommend **Kotlin coroutines** for tasks that should end when the user leaves a certain scope or finishes an interaction. Many Android KTX libraries contain ready-to-use coroutine scopes for common app components like ViewModel and common application lifecycles.
	-	For Java programming language users, see **Threading on Android** for recommended options.
	-	For tasks that should be executed immediately and need continued processing, even if the user puts the application in background or the device restarts, we recommend using **WorkManager** and its support for long-running tasks.
-	Deferred task
	-	Every task that is not directly connected to a user interaction and can run at any time in the future can be deferred. The recommended solution for deferred tasks is **WorkManager**.
-	Exact task
	-	A task that needs to be executed at an exact point in time can use **AlarmManager**.


#### What is a ContentProvider and what is it typically used for?
-	A content provider manages access to a central repository of data. A provider is part of an Android application, which often provides its own UI for working with the data.
-	Content providers can help an application manage access to data stored by itself, stored by other apps, and provide a way to share data with other apps. They encapsulate the data, and provide mechanisms for defining data security.

#Long-running Operations

#### How to run parallel tasks in Java or Android, and get callback when all complete?
- Create Thread/runable class then build programing model 
	- Program Components
		-	**Task**: It is a Runnable that will contains the code to be executed in a separate thread.
		-	**Worker**: It will be responsible for creating a thread and running the supplied task.
		-	**Executor**: It will create workers to handle the tasks. It will also be responsible for broadcasting the completion of all the tasks.
-	https://blog.mindorks.com/run-parallel-tasks-in-java-or-android-and-get-callback-when-all-complete-video

#### Why should you avoid to run non-ui code on the main thread?
-	The code can hang the UI for the user
-	Main thread is mostly busy doing UI realted stuff like rendering/drawing the view

#### What is ANR? How can the ANR be prevented?
-	ANR = Application Not Responding
-	App’s main thread, which is responsible for updating the UI, can’t process user input events or draw, causing frustration to the user
-	Only run UI realted code on main thread and non ui code on background thread

#### What is an AsyncTask? 
-	It is a helper/wrapper class that helps with threading in android
-	It provides following methods :
		1.	**onPreExecute()**: It is invoked on the UI (one with onCreate that sets the activity layout) thread before the task is executed. It is generally used to create dialog box or progress bar and carry out initialization.
		2.	**doInBackground()** : (This is similar to run() method in thread )Invoked on the background thread immediately after onPreExecute() finishes executing. Generally used to perform background computation that can take a long time (Download for instance). The parameters of the asynchronous task are passed to this step.
		3.	**onProgressUpdate(Progress)** : ( Replacement for sendMessage() method in Handler ) invoked on the UI thread after a call to publishProgress(). The timing of the execution is undefined. This method is used to display any form of progress in the user interface while the background computation is still executing. For instance, it can be used to animate a progress bar or show logs in a text field.
		4.	**onPostExecute(Result)** : ( To process final data returned by doInBackground ) Invoked on the UI thread after the background computation finishes. The result of the background computation is passed to this step as a parameter.
-	Before you go on to code AsyncTask in your project you should know the
		1. Input Data Type
		2. Intermediate Data Type 
		3. Final Output type.
-	Note : The doInBackground() method is mandatory to be over written . Other methods can be ignored or implemented as per need

#### What are the problems in AsyncTask? 
1.	Memory leaks
2.	Cancellation of background work
3.	Computational cost

#### When would you use java thread instead of an AsyncTask?
1.	Network operations which involve moderate to large amounts of data (either uploading or downloading)
2.	High-CPU tasks which need to be run in the background
3.	Any task where you want to control the CPU usage relative to the GUI thread

#### What is the relationship between the life cycle of an AsyncTask and an Activity? What problems can this result in? How can these problems be avoided?
-	An AsyncTask is not tied to the life cycle of the Activity that contains it. So, for example, if you start an AsyncTask inside an Activity and the user rotates the device, the Activity will be destroyed (and a new Activity instance will be created) but the AsyncTask will not die but instead goes on living until it completes.

-	Then, when the AsyncTask does complete, rather than updating the UI of the new Activity, it updates the former instance of the Activity (i.e., the one in which it was created but that is not displayed anymore!). This can lead to an Exception (of the type java.lang.IllegalArgumentException: View not attached to window manager if you use, for instance, findViewById to retrieve a view inside the Activity).

-	There’s also the potential for this to result in a memory leak since the AsyncTask maintains a reference to the Activity, which prevents the Activity from being garbage collected as long as the AsyncTask remains alive.

-	For these reasons, using AsyncTasks for long-running background tasks is generally a bad idea . Rather, for long-running background tasks, a different mechanism (such as a service) should be employed.

-	Note: AsyncTasks by default run on a single thread using a serial executor, meaning it has only 1 thread and each task runs one after the other.

#### Explain Looper, Handler and HandlerThread.
-	There are the classes provided bt the android os for managing a theread and the tasks it run.
-	Looper: Keeps the thread alive by running a infinite loop.
	-	Kills threads bt calling loopers qiut method.
-	Handler: Puts the messages into the looper
-	HandlerThread: Alternative way to create a looper and a handler for a thread.

#### How does the threading work in Android?
-	When an application is launched in Android, it creates the first thread of execution, known as the “main” thread. The main thread is responsible for dispatching events to the appropriate user interface widgets as well as communicating with components from the Android UI toolkit.
-	You also have background threads that is used when doing a long operation. So its doesnt interfer with the UI and cause ANR

#### Android Memory Leak and Garbage Collection
-	A **memory leak** happens when your code allocates memory for an object, but never deallocates it. This can happen for many reasons. You’ll learn these causes later.
No matter the cause, when a memory leak occurs the **Garbage Collector** thinks an object is still needed because it’s still referenced by other objects. But those references should have cleared.

# Working With Multimedia Content

#### How do you handle bitmaps in Android as it takes too much memory? 
-	You can decode inSampleSize
-	Scale the image before appying it because it will not always need to use the whole image resolution depending on the device
		-	Estimated memory usage of loading the full image in memory.
		-	Amount of memory you are willing to commit to loading this image given any other memory requirements of your application.
		-	Dimensions of the target ImageView or UI component that the image is to be loaded into.
		-	Screen size and density of the current device.

#### What is the difference between a regular Bitmap and a nine-patch image?
-	In general, a Nine-patch image allows resizing that can be used as background or other image size requirements for the target device. The Nine-patch refers to the way you can resize the image: 4 corners that are unscaled, 4 edges that are scaled in 1 axis, and the middle one that can be scaled into both axes.

#### Tell about the Bitmap pool. 
-	It avoid continuous allocation and deallocation of memory in your application, you reduce GC overhead, which results in a smooth-running application.

#### How to play sounds in Android?
-	To play audio or video files in Android, the Android multimedia framework includes the support of MediaPlayer APIs. So, by using MediaPlayer APIs, you can play audio/video files from your Android filesystem or play files from your Application's resource file or even you can stream audio/video files just like Spotify

#### How image compression is preformed?
- Image Types
	-	PNG
	-	Vector Drawable
	-	JPG
	-	WebP
-	2 Proccess
	-	**Filtering**: Here in this process, we will keep the value at each pixel and find the difference of value at one pixel with the value of the next or previous or up or down of a pixel.
	-	**Deflate**: The output of the filtering process is put into an encoding system called **deflate**. Here, we use two algorithms named **LZ77** and **Huffman encoder**.

# Data Saving

####	How to persist data in an Android app?
-	Use SharedPreferences 
