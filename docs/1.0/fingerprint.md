---
layout: page-classic-sidebar-left
title: Fingerprint Setup
featimg: MapAntifraud.png
previous: /docs/1.0/postnotification
next: /docs/1.0/autenticacao
---

Service that collects device fingerprints and real geolocation of the customer's IP  

-----------------------------------

## * ReDShield

## Integration with your checkout page (site)

## How it works?

![Fluxo]({{ site.url }}/img/fingerprint.png){: .centerimg }{:title="Fingerprint Collection Flow "}

1 - The store checkout page sends the attributes of the buyer's device to Iovation, thereby creating the *black box*  
2 - The store receives an Iovation encryption string and writes the same on the checkout page in a field of type *hidden*  
3 - The store sends to Braspag, together with the other data of the transaction to be analyzed, the *black box*  
4 - Braspag receives all data, validates and sends to ReD Shield  
5 - ReD Shield receives all data, sends the *black box* to the Iovation decrypt  
6 - Red Shield receives from Iovation the attributes of the buyer's device 

## How to configure?

1 - Include Iovation's javascript on your checkout page  
2 - Add configuration parameters in javascript  
3 - Create a field of type *hidden* on your page to write the *black box* in it and send it along with the transaction data to be analyzed  

**Note.:** Do not cache the script as it may occur that multiple devices are identified as being the same.

* Including javascript from Iovation  

    To include javascript, add the `<script>` element to your checkout page. This is the URL of the snare.js version of the Iovation production environment.  
    **Exemple:** `<script type="text/javascript" src="https://mpsnare.iesnare.com/snare.js"></script>`  

* Configuration parameters

    **io_install_flash**{:.custom-attrib} `optional`{:.custom-tag} `bool`{:.custom-tag} `DefaultValue=false`{:.custom-tag}  
    Determines whether the user is prompted to install or upgrade Flash if the required version of Flash is not installed. If the required version of Flash is installed, this setting has no effect.  

    **io_flash_needs_handler**{:.custom-attrib} `optional`{:.custom-tag}  
    If *io_install_flash* is set to false, this handler will not run.  
    Users may see an error if the required version of Flash is not installed to their systems. Use this variable to define your own JavaScript error handling for this condition.  
    For example, you can define your own error message: *var io_flash_needs_update_handler = "alert( 'Install Flash!' );";*  

    **io_install_stm**{:.custom-attrib} `optional`{:.custom-tag} `bool`{:.custom-tag} `DefaultValue=false`{:.custom-tag}  
    Determines whether the user is prompted to install the iovation Active X control. The Active X control helps collect hardware information. This control is only available for Internet Explorer.  
    If the Active X control is installed, this setting has no effect.  

    **io_exclude_stm**{:.custom-attrib} `optional`{:.custom-tag} `bitmask`{:.custom-tag}  `DefaultValue=15`{:.custom-tag}   
    Determines whether to use the iovation Active X control, if it is installed. When Active X is available in Internet Explorer (version 8+ and on Windows Vista), security warnings may appear when the control is installed but not yet run. You can opt to disable the control for specific platforms and therefore prevent the prompt from occurring.  
    This bitmask has the following set of values:  
        0 - default (run on all platforms)  
        1 - do not run on Windows 9x (including Windows 3.1, 95, 98 and Me)  
        2 - do not run on Windows CE  
        4 - do not run on Windows XP (including Windows NT, 2000, 2003, and 8)  
        8 - do not run on Vista or newer versions of Vista  
        
    Note.: The values are additive, so a value of 12 means do not run on either Vista (8) or Windows XP (4). 

    **io_bbout_element_id**{:.custom-attrib} `optional`{:.custom-tag}  
    The ID of the HTML element to populate with the blackbox. If *io_bb_callback* is specified, this parameter has no effect.  

    **io_enable_rip**{:.custom-attrib} `optional`{:.custom-tag} `bool`{:.custom-tag} `DefaultValue=true`{:.custom-tag}  
    Indicates whether iovation will attempt to collect information to determine the Real IP of the end user.  

    **io_bb_callback**{:.custom-attrib} `optional`{:.custom-tag}  
    This JavaScript function is an event handler that is called when a collection method has finished updating a blackbox.  
    Declare the function as follows:  
    *function io_callback( bb, complete)*  
    The variables store the following:  
        bb - the updated value of the blackbox  
        complete – a boolean value indicating whether all the collection methods have completed

    **IMPORTANT!**  
    The configuration parameters should be placed before the above tag is called. They determine how iovation's javascript will work, and errors can occur if they are placed before the javascript call.

**Exemple**  

```html
<html>
<head>
<script>
    var io_install_flash = false;
    var io_install_stm = false;
    var io_bbout_element_id = 'gatewayFingerprint';
</script>
</head>
<script type="text/javascript" src="https://mpsnare.iesnare.com/snare.js"></script>

<body>
    <form>
        <input type="hidden" name="gatewayFingerprint" id="gatewayFingerprint">
    </form>
</body>
</html>
```

## Integrating into Mobile Apps

**Overview**  
This topic explains how to integrate the iovation Mobile SDKs into your iOS and Android apps.  

**Downloading iovation Mobile SDK for iOS and Android**
If you have not already downloaded the iOS or Android SDKs, you must do so before proceeding. Log into the iovation Help Center via the Administration Console, and download the files from here:  
[Download Mobile SDK](http://help.iovation.com/Downloads)  

**About Mobile Integration**
Add the iovation Mobile SDK to your apps to collect information about your end-users' devices. The client generates a blackbox that contains all available device information.  
![Fluxo]({{ site.url }}/img/fingerprintmobile.png){: .centerimg }{:title="Fingerprint Colletion Flow"}  

* Integrating with iOS Apps  

iOS Integration Files and Requirements
![Detalhes]({{ site.url }}/img/fingerprintios1.png){: .left }{:title="iOS Integration Details"}  

Version 3.1.0 of the iovation iOS SDK supports iOS 5.1.1 or higher on the following devices:  
        iPhone 3GS and later  
        iPod Touch 3rd generation and later  
        All iPads  

* Installing the iovation Mobile SDK for iOS  
    1 - Download and unzip the SDK. See  
    2 - In Xcode, drag iovation.framework into your project's navigation area.  
    3 - Select Copy items if needed to copy the framework file into your project's directory.  
![Detalhes]({{ site.url }}/img/fingerprintios2.png){: .left }{:title="iOS Integration Details"}  
    4 - In the dialog that appears:  
        Select Copy items if needed to copy the framework file into your project's directory.
        Check the checkbox for the targets in which you plan to use the framework.
![Detalhes]({{ site.url }}/img/fingerprintios3.png){: .left }{:title="iOS Integration Details"}  
    5 - Click Finish.  
    6 - Add the following frameworks to your application's target in XCode:  
        - *ExternalAccessory.framework*. If you find that the Wireless Accessory Configuration capability is turned on in Xcode 6 or higher and you don't need it, turn it off and add ExternalAccessory.framework again.
        - *CoreTelephony.framework*
![Detalhes]({{ site.url }}/img/fingerprintios4.png){: .left }{:title="iOS Integration Details"}  
    7 - Optionally add these frameworks if your app makes use of them:  
        - *AdSupport.framework*. If your app displays ads. Do not include if your app does not use the ad framework. The App Store rejects apps that include the framework but don't use it.  
        - *CoreLocation.framework*. If your app uses location monitoring. Do not include this framework unless your application requests geolocation permission from the user.  

* Using the +ioBegin Function  
The +ioBegin function collects information about the device and generates a blackbox that contains this information. Submit this string in an HTTP request to your service. See the iovSample Xcode project included in the download for a sample implementation.  

* Syntax
> NSSstring *bbox = [iovation ioBegin];

* Return values
> bbox - a string that contains a blackbox.

**IMPORTANT**
The blackbox returned from *+ioBegin* should never be empty. An empty blackbox indicates that the protection offered by the system may have been compromised.  

* Example  

```html
#import "sampleViewController.h"
#import <iovation/iovation.h>
@implementation SampleViewController
@property (strong, nonatomic) UILabel *blackbox;
// Button press updates text field with blackbox value
- (IBAction)changeMessage:(id)sender
{
    self.blackbox.text = [iovation ioBegin];
}
@end
```

* Integrating with Android Apps

Android Integration Files and Requirements
![Detalhes]({{ site.url }}/img/fingerprintandroid.png){: .left }{:title="Android Integration Details"}  

**NOTA**
If the permissions listed are not required by the application, the values collected using those permissions will be ignored. The permissions are not required to obtain a usable blackbox, but they do help obtain some unique device information.  

Version 1.2.0 of the iovation Mobile SDK for Android supports Android 2.1 or higher.  

* Installing the SDK for Android  

1 - Download and unzip deviceprint-lib-1.2.0.aar.
2 - Launch your IDE of choice.
3 - In Eclipse and Maven, deploy the .aar file to your local Maven repository, using maven-deploy.  
    More details: [Maven Guide](http://maven.apache.org/guides/mini/guide-3rd-party-jars-local.html)  
4 - In Android Studio, select File -> New Module. Expand More Modules and choose Import existing .jar or .aar package.
5 - Select the deviceprint-lib-1.2.0.aar file, and press Finish.  
6 - Ensure that the deviceprint-lib is a compile-time dependency in the build.gradle file.
![Detalhes]({{ site.url }}/img/fingerprintandroid1.png){: .left }{:title="Android Integration Details"}  

* Using the ioBegin Function  

The *ioBegin* function collects information about the device and generates an encrypted string containing this information.  

* Syntax  

> public static String ioBegin(Context context)

* Parameters  

> context – An instance of the android.content.Context class used to access information about the device.  

* Return values  

A string that contains a blackbox.  

**IMPORTANT**  
The blackbox returned from *ioBegin* should never be empty. An empty blackbox or a blackbox that contains only *0500* indicates that the protection offered by the system may have been compromised.  

**IMPORTANT**  
You must package the deviceprint-lib-1.2.0.aar file with the application.  

* Compiling the Sample App in Android Studio  

**IMPORTANT**  
If the option to run the module does not appear, select FILE -> PROJECT STRUCTURE and open the Modules panel. From there, set the Module SDK drop-down to your target Android SDK version.  

1 - Download and unzip deviceprint-lib-1.2.0.aar  
2 - In Android Studio, select File | Open or click Open Project from the quick-start screen.  
3 - From the directory where you unzipped deviceprint-lib-1.2.0.aar, open the android-studio-sample-app directory.  
4 - Open the DevicePrintSampleActivity file.  
5 - With some configurations, Android Studio may detect an Android Framework in the project and not configure it. In this case, open the Event Log and click Configure.  
6 - A pop-up prompts you to select the Android framework. Click OK to fix the framework errors.  
7 - In Android Studio, select File -> New Module. Expand More Modules and choose Import existing .jar or .aar package.  
8 - Select the deviceprint-lib-1.2.0.aar file, and press Finish.  
9 - Ensure that the deviceprint-lib is a compile-time dependency in the build.gradle file.  
![Detalhes]({{ site.url }}/img/fingerprintandroid1.png){: .left }{:title="Android Integration Details"}  
10 - Open the DevicePrintSampleActivity folder.  
11 - In the project navigation view, open src/main/java/com/iovation/mobile/android/sample/DevicePrintSampleActivity.java  
12 - Right-click the file editing view and select Run DevicePrintSampleAct.  
13 - Select either an attached physical device, or an Android virtual device to run the app on.  
14 - The app should now compile and launch  

* Exemple  

The following example app assumes a simple view-based application where a button click populates a label containing the value of the blackbox.  

For a much richer example, see the Android Studio sample app included with the SDK  

```html
package com.iovation.mobile.android.sample;
import android.app.Activity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.TextView;
import com.iovation.mobile.android.DevicePrint;
public class DevicePrintSampleActivity extends Activity
{
    /**
    * Called when the activity is first created.
    * @param savedInstanceState If the activity is being re-initialized after
    * previously being shut down then this Bundle contains the data it most
    * recently supplied in onSaveInstanceState(Bundle). <b>Note: Otherwise it is null.</b>
    */
    
    @Override
    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
    }
    
    public void printDevice(View target)
    {
        String bb = DevicePrint.ioBegin(getApplicationContext());
        TextView bbResult = (TextView) findViewById(R.id.bbResult);
        bbResult.setText(bb);
        bbResult.setVisibility(View.VISIBLE);
    }
}

```

## * Cybersource

You need to add a 1-pixel image, which is not shown on the screen, and two segments of code to the tag *<body>* on your checkout page, making sure that it will take 10 seconds between the submission and execution of the code page to the server.  

**IMPORTANT!**  
If the 3 code segments are not placed on the checkout page, the results may not be accurate.  

**Putting the Code Segments and Substituting Variables**  
Place the code segments immediately above the *<body>* tag to ensure that the web page will render correctly. Never add code segments to visible HTML elements. Code segments need to be loaded before the buyer completes the purchase order, otherwise an error will be generated.  

In each segment below, replace the variables with the values ​​for the merchant and order number.  

* Domain:
    Testing - Use h.online-metrix.net, which is the DNS server's fingerprint, as outlined in Example HTML below;  
    Production - Change the domain to a local URL, and configure your webserver to redirect this URL to h.online-metrix.net.  

**ProviderOrgId**: To get it, contact Braspag.  
**ProviderMerchantId**: To get it, contact Braspag.  
**ProviderSessionId**: Use the same value passed in the parameter **MrchantOrderId** service request fraud analysis.  

* PNG Image  

```html

<html>
<head></head>
<body>
    <form>
        <p style="background:url(https://h.online-metrix.net/fp/clear.png?org_id=ProviderOrgId&amp;session_id=ProviderMerchantIdProviderSessionId&amp;m=1)"></p>  
        <img src="https://h.online-metrix.net/fp/clear.png?org_id=ProviderOrgId&amp;session_id=ProviderMerchantIdProviderSessionId&amp;m=2" alt="">  
    </form>
</body>
</html>

```

* Flash Code  

```html

<html>
<head></head>
<body>
    <form>
        <object type="application/x-shockwave-flash" data="https://h.online-metrix.net/fp/fp.swf?org_id=ProviderOrgId&amp;session_id=ProviderMerchantIdProviderSessionId" width="1" height="1" id="thm_fp">
            <param name="movie" value="https://h.online-metrix.net/fp/fp.swf?org_id=ProviderOrgId&amp;session_id=ProviderMerchantIdProviderSessionId" />
            <div></div>
        </object>
    </form>
</body>
</html>

```

* Javascript Code

```html

<html>
<head></head>
<script src="https://h.online-metrix.net/fp/check.js?org_id=ProviderOrgId&amp;session_id=ProviderMerchantIdProviderSessionId" type="text/javascript"></script>
<body></body>
</html>

```

**IMPORTANT!**  
Be sure to copy all data correctly and have replaced the variables correctly by their values.  

**Setting Your Web Server**  
If you do not complete this section, you will not get correct results, and the domain (url) of the supplier will be visible, it is more likely that your customer block it.  

In the section *Putting the Code Segments and Substituting Variables (Domain)*, all objects refer to h.online-metrix.net, the DNS server's fingerprint. When you are ready for deployment, you must change the server name to a local URL and configure your Web server in a URL redirect for h.online-metrix.net.  