# Appium Server Side Java Sample

The project uses the Bitbar Sample App, installs it on the device, and then goes through the application.

The project uses:

- [BitBar Cloud](https://cloud.bitbar.com) - Web service for automated testing on
  real mobile devices. You'll need to have an active account for launching the tests in cloud.

- [Maven](https://maven.apache.org/) - Compiles and launches the test code.

### Test apps

The project uses Bitbar Sample apps, which are available in this
repository [test-samples/apps](https://github.com/bitbar/bitbar-samples/tree/master/apps/).

Test samples are designed to run with:

* Android: https://github.com/bitbar/test-samples/blob/master/apps/android/bitbar-sample-app.apk
* iOS: https://github.com/bitbar/test-samples/blob/master/apps/ios/bitbar-ios-sample.ipa

### Run tests locally from Command Line with Maven

To run tests locally, follow these steps:

1. **Prepare the Application File**
    - Place your tested application at the root of the project.
        - For Android: `application.apk`
        - For iOS: `application.ipa`
    - For iOS: The `bitbar-ios-sample.ipa` file must be re-signed for your test devices if you want to run tests
      locally.

2. **Start Appium Server**
    - Ensure an Appium server is running before executing tests.
    - For iOS: The UDID of your device must be pre-set in the Appium server settings.

3. **Run Tests with Maven**
   To run a specific test method (e.g., `mainPageTest` in `AndroidSample`):
     ```sh
     mvn -Dtest=AndroidSample#mainPageTest clean test
     ```

4. **Using an IDE**

   You can also run tests from your IDE. Make sure the project is imported as a Maven project and that `pom.xml` is
   recognized for dependency management.

5. **Reports**

   Test reports, screenshots, and other artifacts will be available under: `./target/reports/`

### Run tests as Server Side Appium in [BitBar Cloud](https://cloud.bitbar.com)

Use the following scripts to create the test zip for your project:

    ./createAndroidZip.sh

or

    ./createiOSZip.sh

Once you have your test zip and application file ready, follow these steps to run your tests
in [BitBar Cloud](https://cloud.bitbar.com):

1. **Upload Files**
    - Go to the Files Library in BitBar Cloud and upload both your application file and the test zip.

2. **Create a Test Run**
    - Open the [Test Run Creator](https://cloud.bitbar.com/#testing/test-run-creator).
    - Select the appropriate OS type (Android or iOS).
    - Choose the "Server Side" test framework.
    - Select your uploaded files and pick the devices you want to test on.
    - Start the test execution.

**Note:**
If you change the name of your Android or iOS test class, update the following variables in `run-tests_android.sh` or
`run-tests_ios.sh` as needed:

```sh
# Name of the desired test class and optionally a specific test case, e.g., AndroidSample#mainPageTest
TEST=${TEST:="AndroidSample"}
# OPTIONAL: Specify the test case name to use with the `mvn test` command
# Leave blank to test the whole class!
TEST_CASE="#mainPageTest"
```
