# Bootcamp - Intro to Android, git, and testing
## CS305 Bootcamp
**The bootcamp is due on Friday 29-Sep-2017 at 18:00**
This homework will show you how to get started with the tools you will need for this course. You will learn about Android development, git, and unit testing.

The lab session is a great opportunity to ask the teaching assistants about any problems you have with the homework. Thus, we encourage you to start it today, and ask your questions at the lab.

Now let's dive right in.
### Homework tasks
#### Setup Android Studio
Download and install Android Studio from [https://developer.android.com](https://developer.android.com). If you need any help, follow the [instructions](https://developer.android.com/studio/install.html).

You should choose the default options (we will do more tool configuration later).

Once you reach the welcome screen, please click on **Configure** at the bottom right of the window, and select **SDK Manager**. Then, in the **SDK Platforms** tab, please intall **Android 7.1.1** (API Level 25).
After that, in the **SDK Tools** tab, first select **Show Package Details** (at the bottom right) , then choose **Android SDK Build Tool 25.0.3** and install it.
#### Create a new project
Launch the Start a new *Android Studio project* wizard. Name your project **Bootcamp** and choose **sweng.epfl.ch** as the domain. Leave the other settings at their default (i.e. choose API 15: Android 4.0.3 (Ice Cream Sandwich) as minimum SDK and add an Empty Activity). After a bit of time, you should see Android Studio open up with a number of files created for this project.

This is a good time to open a file explorer and look at all the files that have been created. The Android developer documentation on [managing projects](https://developer.android.com/studio/projects/index.html) provides a good overview of what all these files do.

Before running your app, please set the correct version of Android. To do it, open the **app/build.gradle** file. In this file, please update the following settings:
* `compileSdkVersion 25`
* `buildToolsVersion "25.0.3"`
* `targetSdkVersion 25`
* In the *dependencies*, update `compile 'com.android.support:appcompat-v7:26.+'` to `compile 'com.android.support:appcompat-v7:25.3.1'`

To run your app, use *Run* > *Run 'app'*. You will see a dialog asking about which emulator you want to use. The default (Nexus 5X API 25 x86) is fine. It will take a few seconds to start up the emulator and then you will see Android itself start up, followed by your app. If this emulator is not installed, please create it by selecting **create a new virtual device**.
#### Set up git, and create a repository
Let's save a snapshot of the project, so that we can get back to this stage if we make a mistake. We will use git throughout the course for source control (and also to collaborate with your team mates).

Setting up Git is easy: First, you need an account on [GitHub](https://github.com) (the site that will host our code during this course). If you don't already have a GitHub account, create one by [following their instructions](https://github.com/join). Please make sure that your profile shows your real name. Next, follow their [setup instructions](https://help.github.com/articles/set-up-git/) to install git on your computer.

To track your project using git, open a command line or git shell. cd to where your project is; this folder should have a file named Bootcamp.iml, among others. From there, execute the following commands:
```sh
git init   # Initialize a new repository
git add .  # Add all the files to the repository
git commit # Create a first commit
```
If that sounded scary to you, this is a good moment to browse some Git documentation. We recommend this [interactive tutorial](https://try.github.io/levels/1/challenges/1), [the documentation at GitHub](https://help.github.com/articles/set-up-git/), or [the git book](https://git-scm.com/book/en/v2).
#### Publish your repository on GitHub
Once you have set up git, please [fill out this form](https://docs.google.com/forms/d/e/1FAIpQLSc6xu45l_943LuL4GOJKi_-2qBLlXM2q0x20kYgzSuNxleimw/viewform). We will need this information to associate your GitHub account with your GASPAR identity. Once you have filled out the form, we will create a repository for you where you can push this homework. You will need this repository to complete the next steps (but you can also do the next step later).

To get this homework graded, you need to publish your commits on GitHub since that is where we look for submitted homework. This requires two steps:
1. Add GitHub as a "remote" to your repository, using the following command: `git remote add origin https://github.com/sweng-epfl/bootcamp-gaspar.git` (Replace gaspar with your with your GASPAR user name.)
2. Push your commits to GitHub: `git push -u origin master`

Android Studio will recognize that you've just added your code to git (**Unregistered VCS root detected**). If you click on **Add root**, you can use Android Studio to manage your git commits instead of the command line. On Windows and Mac OS, you can also use the desktop GitHub client, but we will continue to explain in terms of git shell commands.

From now on, the commands to create a commit and push it are:

```sh
git add . # Add all the changes
git commit # Commit; you can also add -m "put your commit message here..."
git push # The "-u origin master" parameters are only needed the first time.
```
#### Create an Android app
We will kickstart your career as Android software engineer by creating a friendly greeting application.

Below is a list of steps we suggest to build this app. In addition, you will find below some hints, and the grading criteria that we will use to check whether you understood git, unit testing, and Android basics.
Try to follow the steps as well as you can. If you get stuck, there are several options:
* Check the hints below.
* Follow the Android documentation links.
* Google your question or search on [stackoverflow](https://stackoverflow.com/questions/tagged/android)
* Ask a question in the course forum.
* Ask a TA or AE at the lab session.
#### Create the main screen
Edit the **app/res/layout/activity_main.xml** file and add a "Plain Text" text field and a button to your activity by dragging them from the Palette of components and setting the appropriate properties. In the Properties of the component, enter some text in the "Plain Text" text field as a hint, then style the text field and button as you like.

One part is important though: set the id property of both the field and the button to a meaningful value, such as mainName and mainGoButton. You will use this ID to access the elements from your source code. To do it, scroll down the Properties and select "View all properties", then you can update the id property of the component by clicking on it.

Launch your app. This will start an emulator and show the awesome activity you just created. If it works well, this is a good time for another git commit. Do this before continuing.

#### Test your app
Let's make the app do something! In this course, you will learn how to develop high quality software, in other words, make the app do the right thing. One effective way to achieve this is testing, so we will start by writing a test. It goes in a new file (**MainActivityTest.java**) in the **ch.epfl.sweng.swengbootcamp** (androidTest) folder and contains the following code:
```java
@RunWith(AndroidJUnit4.class)
public class MainActivityTest {
    @Rule
    public final ActivityTestRule<MainActivity> mActivityRule =
            new ActivityTestRule<>(MainActivity.class);
    @Test
    public void testCanGreetUsers() {
        onView(withId(R.id.mainName)).perform(typeText("from my unit test"));
        onView(withId(R.id.mainGoButton)).perform(click());
        // onView(withId(R.id.greetingMessage)).check(matches(withText("Hello from my unit test!")));
    }
}
```

If you want to know more about this test, have a look at the [Android testing guides](https://developer.android.com/training/testing/index.html). This test relies on a library called [Espresso](https://developer.android.com/training/testing/ui-testing/espresso-testing.html). You need to add Espresso as a dependency to the project. To do so:
* Add these lines to the *dependencies* section of your **app/build.gradle** (under "Gradle Scripts" in the project explorer): 
    ```Gradle
        androidTestCompile 'com.android.support:support-annotations:25.3.1'
        androidTestCompile 'com.android.support.test:runner:0.5'
        androidTestCompile 'com.android.support.test:rules:0.5'
        androidTestCompile 'com.android.support.test.espresso:espresso-core:2.2.2'
    ```
* Set your test runner to **android.support.test.runner.AndroidJUnitRunner** (File > Project Structure, select 'app' in the module list, Flavors > Test Instrumentation Runner). 
* Disable animations in your emulator (Inside the emulator, click the round **Apps** button, then choose **Settings**. If you do not see an entry named Developer options, then go to Settings > About emulated device and click on the Build number entry 5 times. A message should normally tell you that you are x steps away from becoming a developer. Then set Settings > Developer options > Window animation scale to Animation off; same for Transition animation scale and Animator duration scale).

Now, you have all the prerequisites to make your test compile. You still need to complete the test file by adding import statements. Android Studio can do this for you: select the places with compile errors, press Alt+Enter, and choose **import ...**.

Once all compile errors are fixed, run your test by right-clicking on the **MainActivityTest** class and selecting Run 'MainActivityTest', then watch it pass. Works? Great! Don't forget to git add and git commit.

#### Add behavior to your app
Uncomment the last statement in your test, the one that is commented out in the example code that we provided. The test will no longer compile, since you do not yet have a view with the name greetingMessage.

So, add a second activity called **GreetingActivity** to your app, with a TextView that has ID "greetingMessage". This will make your test compile again. However, the test fails because your app doesn't do anything when the button is clicked.

Now, you can add the code that starts the GreetingActivity when you click the button and sets the greeting message to "Hello <name>!", where <name> is whatever the user entered in the text field. The [Android documentation on starting an activity](https://developer.android.com/training/basics/firstapp/starting-activity.html) contains all you need to know to do this.


One hint: the Android documentation talks about editing the XML files directly. You can do this, but you don't need to since you can set all of these properties for Views using the interface designer in Android Studio.

#### Clean up
Once your test passes, you're almost done. Congrats!

This is a good time to clean up your code. Make sure there are no compiler warnings. Remove unneeded code such as the **onCreateOptionsMenu** and **onOptionsItemSelected** methods. Run Code > Optimize imports and Analyze > Inspect code to improve the quality of your code. As final steps, git add, git commit your work, and git push it to your bootcamp-gaspar repository.

### About some common warnings
* **Add backup properties** and **Google Search indexation**: These would be useful in a real app, but not here. Ignore the warnings.
* **Missing return value** in the Gradle script: This appears to be an Android Studio bug. Ignore the warning.
* **Unused property** in gradle.properties: Ignore the warning.
* **Typos** in words like sweng or epfl: Ignore them. (but fix real typos!)
* **Unused parameter** in the *onClick* handler: Android requires that parameter, even if you're not using it. Suppress the warning (for the method only!)
* **Obsolete stuff** in the tests: Suppress the warnings.

If you encounter some other warning, and believe it to either be a false positive, or something that cannot be fixed without too much effort compared to the app's complexity, please ask the staff by creating a thread on this forum.

### Hints
If you don't want to enter a password every time you connect to GitHub, you can [set up authentication via SSH](https://help.github.com/articles/connecting-to-github-with-ssh/).

The emulator should boot and launch your app in 60 seconds or less. If not, there is probably a problem with your configuration, and you might want to revisit hardware acceleration settings.

You can set the ID of a View element by double-clicking on it in the graphical editor. Alternatively, look for a property called id in the list of properties, or add **android:id="..."** to the XML code of the element.

Android Studio is quite helpful. Did you know that many errors can be resolved by pressing Alt+Enter? That Shift+F6 renames a variable? We recommend getting familiar with Android Studio now, because you will use it throughout the semester.

If Espresso tests fail with **java.lang.SecurityException**: Injecting to another application requires INJECT_EVENTS permission, the most likely reason is that the soft keyboard is hiding your button. You can disable the soft keyboard (Tools > Android > AVD Manager > Edit > Show Advanced Settings > Enable keyboard input).

If you are stuck and cannot get something to work, see if you can't find the answer in the documentation or online. But if that does not work, do not waste a lot of your time randomly trying alternatives. Ask a TA or AE or post on the course forum.

### Grading
This homework is worth 100 points. To grade it, we will look at the code that is pushed to your bootcamp-gaspar repository on the submission deadline. You will receive points for the following:
* 10 points if your project compiles and runs.
* 25 points if it has a text input field and a button, and clicking the button opens an activity with a greeting as described above.
* 30 points if you have a test that verifies this behavior, and the test passes.
* 20 points for high-quality code. We will look at code layout, the names of your methods, variables, and IDs. We will remove points if we see bad coding practices.
* 15 more points for high-quality code if you don't have any compiler warnings or severe issues detected by Android Studio. The Android Studio analyzer does have some false positives, which are OK, but you should resolve all the real issues.

Note that code quality matters. The actual implementation is only worth one third of the points; the rest you receive for testing and for writing nice code.
