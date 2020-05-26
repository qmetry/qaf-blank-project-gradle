# qtm-QAF-GRADLE-example

This is automation project skeleton to start with using Gradle. Please refer [documentaion](https://qmetry.github.io/qaf/) for more help.

This is sample project with Gradle directory structure:
```
.
+-- config
|	+-- testrun_config.xml (configuration files)
+-- resources (required resources including properties files and data files, and is a place holder for other resources.)
|   +-- application.properties
|   +-- log4j.properties
|	+-- log4jtestng.properties
+-- src (java files and is a place holder for other java files.)
+-- scenarios (contains bdd files)
|   +-- suite1.bdd
+-- build.gradle
+-- test-results (contains result files.)
|   +-- RESULT_FOLDER
```
Please refer https://qmetry.github.io/qaf/

Note: This sample project uses chrome driver and it requires chrome driver binary.
You need to download and set **webdriver.chrome.driver** property in **application.properties** file with driver binary path.
## How to set chromdriver path?

Open 'application.properties' from 'resources' directory.
add chromedriver path.
```
webdriver.chrome.driver = <CHROMDRIVER_PATH>
```
## How to integrate QTMGradlePlugin?
Add QTMGradlePlugin to upload test-result files to QMetry Test Management.
1. Add following code in `build.gradle`
```
plugins
{
    id 'com.qmetry.QTMGradlePlugin' version '1.3'
}
 
qtmConfig 
{ 
	qtmUrl = 'https://testmanagement.qmetry.com' 
	qtmAutomationApiKey = 'cwmtmB6WYXo7Sj0YEchpJYiZgt3nd8TZCmtsDwD' 
	automationFramework='QAS' 
	testResultFilePath='../test-results'
	project='Demo Project'
	testSuiteId='STR-TS-01'
	platform='Chrome' 
	release='Demo Release'
	cycle='Demo Cycle'
	build='Demo Build' 
	
}
```
Please refer https://github.com/qmetry/qmetry-test-management-gradle-plugin for more information

2. To run the project, from command prompt go to project home and run 
```
gradle test qtmUploadResults
```

3. Response
```
----------------------------------------------------------------
QMetry Test Management Gradle Plugin : Starting Post Build Action
-----------------------------------------------------------------
QMetry Test Management Gradle Plugin : Reading result files from Directory 'D:/Gradle Plugin/qtm-QAF-GRADLE-example/build/../test-results'
QMetry Test Management Gradle Plugin : Creating zip file...
QMetry Test Management Gradle Plugin : Reading result file 'D:/Gradle Plugin/qtm-QAF-GRADLE-example/build/../test-results/01_Nov_2018_12_46_PM/testresult.zip'
QMetry Test Management Gradle Plugin : Uploading result file...
QMetry Test Management Gradle Plugin : TestSuiteId : STR-TS-01
QMetry Test Management Gradle Plugin : Project : Demo project
QMetry Test Management Gradle Plugin : Release : Demo Release
QMetry Test Management Gradle Plugin : Cycle : Demo Cycle
QMetry Test Management Gradle Plugin : Build : Demo Build
QMetry Test Management Gradle Plugin : Platform : Chrome
QMetry Test Management Gradle Plugin : Response : {"success":true,"code":"CO.IMPORT_SCHEDULED","data":[{"id":27670,"buildID":7150,"platformID":4808,"dropID":1407,"testsuiteId":"STR-TS-01","entityURL":"https://testmanagement.qmetry.com/#/test-suite/92558"}]}
QMetry Test Management Gradle Plugin : Result file successfully uploaded!
QMetry Test Management Gradle Plugin : Finished Post Build Action!
```

4. View results in QMetry Test Management
To view result login to QMetry Test Management, copy value of **entityURL** and open URL in browser.
![Test Results](img/qtm-result.png?raw=true "Testsuite")
