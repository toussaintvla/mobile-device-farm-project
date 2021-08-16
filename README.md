# mobile-device-farm-project

## Getting Started

*To get started, you’ll need 3 things:*

- An AWS Account
- An Appium Node.js test
- An application .apk or .ipa file

If you `do not` have a test already written or an application to test, I provide them for you in the following section.

If you do have a test already written and an .ipa or .apk file, skip to the section `“Packaging the Test Files for Device Farm”`. If not, continue to the next step of creating the demo test.

The first thing we’ll do is create a basic test for our application. To do this, we’ll need to create a test file (I’ll call mine `test_native_android.js`):

In this test we’re doing two things:

- We first test to see that the application loads
- Next, we’re running a loop that will check to see if a button exists, click on the button, & then go back. The loop runs 5 times.

- The code provided is targeting the example .apk we will be providing you for the tutorial. If you bring you own .apk you will need to write your own test.

- Next, we’ll create a package.json file for the dependencies that we’ll need for this test:

- In our package.json, we’ve included the mocha (a JavaScript testing framework) & chai (an assertion library for node and the browser) frameworks which we’ll need for our test to run, as well as the wd library (A node.js client for webdriver).

- Next, we’ll need to install the dependencies we’ll need for this test to run:

```node
npm install
```

```node
npm install -g npm-bundle
```

- Next, we’ll run the npm bundle command from within root of our test:

```node
npm-bundle
```

Now, we’ll zip the .tgz file:

```node
zip -r MyTest.zip *.tgz
```

- Our test is now written, bundled & ready to go.
Finally, export your .apk file if you have an existing application, or download the example Android .apk file for the above test

```node

```

## Running your Test on AWS Device Farm

- Now that we have a test written & an .apk to run the test on, we can navigate to the Device Farm console.
- Click Create New Project & give the project a name
- Click Create a New Run
- Click on the Android / iOS Button (to specify a Native application)
- Upload the .apk file.
- Give the Run a name & click Next Step.

Next, in the dropdown menu for the type of test to run, you’ll see the option for Appium Node.js. Choose this option & upload the zipped folder we created in the previous steps:

Next, we’ll be given a default TestSpec YAML file that will describe some configuration for our test.
In the test: phase, we’ll need to update the command: property to be the command we need to use to execute our mocha test.

Here, we’ll replace:
node YOUR_TEST_FILENAME.js
with:
./node_modules/mocha/bin/mocha test_native_android.js

Then, click Save TestSpec.

In this YAML file you can also set other configuration for your test environment, including things like the node environment you’d like to be running in, post test commands, & ADB device commands (like turning animations off).

After the test has been saved, click Next step.

In the next screen, we’ll be given the option to choose a custom set of devices (a Device Pool) or choose a default Device Pool. Here, either choose the default Device Pool or create your own using the devices you’d like to test on.

After you’ve chosen your Device Pool, click Next step.

In the next screen, we’re given some options to specify device state. Here, you can set custom device settings that you’d like to configure on each device (things like geolocation, wifi status, etc..).

Here, either leave the defaults or configure your custom device state & click Next step.

Now, the test is ready to run & we can click Confirm & start run.
Once the test is complete, you should see the test results overview in the dashboard.