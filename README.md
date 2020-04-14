
# Android Coding Standards 

Coding standards are a set of guidelines, best practices, programming styles and conventions that developers follow when writing code for a project. A coding standard makes sure that all the developers working on the project are following certain specified guidelines. The code can be easily understood and proper consistency is maintained. Some of the coding standards are given below:

# Coding Guidelines

## 1.  Project Structure :

 **1.1.  Code Structure :**
 Structure depends on project size and architectural  pattern.

- **Package by Component :** 
  Organising folders on the basis of components and integrations
        
      com.example.myapp.activities - Contains all activities
      com.example.myapp.fcm - Contains all firebase messaging integration
      com.example.myapp.adapters - Contains all custom adapters
      com.example.myapp.models - Contains all our data models
      com.example.myapp.network - Contains all networking code
      com.example.myapp.fragments - Contains all fragments
      com.example.myapp.utils - Contains all helpers supporting code
      com.example.myapp.interfaces - Contains all interfaces
    
- **Package by Functionality :** 
   Organising folders on the basis of app Functionality
   
      com.example.myapp.utils - Contains all helpers supporting code.
      com.example.myapp.ui.* - Contains all UI-related packages/classes
      
      com.example.myapp.ui.login - Contains classes related to some app's Main Screen, like in MVP architecture 	   				      activity/fragment, presenters, adapter etc. and 
      for MVVM activity/fragment, viewmodels etc.
      
      com.example.myapp.ui.orderdetail - Contains classes related to some app's Item Details Screen
      

 **1.2. Resources Structure:**

	res/layout/ - contain all layout files
	res/drawable/ - contain all Bitmap files (.png,.9.png,.jpg,.gif)
	res/color/ - contain all custom color definitions
	res/menu/  - contain all menu bar
	res/values - contain all XML files that contain simple values, 
	             such as strings, integers, and colors.

## 2. Naming Conventions:

 **2.1.  Code naming rules:**

- The name of a class is usually a noun or a noun phrase explaining what the class is: List, PersonReader. 
-  The name of a method is usually a verb or a verb phrase saying what the method does: close, readPersons. 
- The name should also suggest if the method is mutating the object or returning a new one. For instance sort is sorting a collection in place, while sorted is returning a sorted copy of the collection. 
- The names should make it clear what the purpose of the entity is, so it's best to avoid using meaningless words (Manager, Wrapper etc.) in names. 
- When using an acronym as part of a declaration name, Capitalize it if it consists of two letters (IOStream); Capitalize only the first letter if it is longer (XmlFormatter, HttpInputStream). 
- Non-public, non-static field names start with m. 
- Static field names start with s.


| **Type** | **Rule** | **Example** |
|--|---|--|
| Package | Start with an lowercase letter and use the camel case | org.example.myProject|
| Class | Start with an uppercase letter and use the camel case | LoginFragment, LoginActivity, LoginPresenter, LoginViewModel |
| Variable/Property | Start with an lowercase letter and use the camel case  | isProcessing |
| Constants |Use all uppercase letter separated by “_”  | RESPONSE_STATUS|
| Function/Method | Start with an lowercase letter and use the camel case | hideTouchKeyPad() |

**2.2.  Resources naming rules:**
All Resources names should use all lowercase and separated by “_”. Follow the convention of prefixing the type, as in type_foo_bar.xml.

 **Example:** fragment_order_details.xml, view_primary_button_pressed.xml, activity_signup.xml.

**2.3.  Id naming rules:**
 Use Component name as prefix
 **Example :** image_profile, textView_name, menu_done


**2.3.  String naming rules:**
String names start with a prefix that identifies the section they belong to.

**Example :** error_not_valid, success_login etc.

## 3.  Code Formatting :

> Android studio provides easy code indentation and Formatting by using "Command + Alt +L" .

- We use four (4) space indents for blocks and never tabs. When in doubt, be consistent with the surrounding code.

		if (values != null) {
		  for (val in values) {
		    // ...
		  }
		}
-   We use eight (8) space indents for line wraps, including function calls and 
assignments.
	      
	    Instrument i = 
	            someLongExpression(that, wouldNotFit, on, one, line);

-   Each line of text in your code should be at most 100 characters long.
-   Import statements should be in order.
       -   Android imports
       - Imports from third parties (com, junit, net, org)
       -  java and javax
       -  Same project imports
       
-   Keep spaces between words and special characters.
-   Never put a space after (, [, or before ], ).
-   Class member ordering :
       - Constants
       -  Fields
       - Constructors
       - Override methods and callbacks (public or private)
       - Public methods
       - Private methods 
       - Inner classes or interfaces
        
**3.1 Xml formatting :**

-   One attribute per line, indented by 4 spaces.
-   android:id as the first attribute always.
-   android:layout_**** attributes at the top.
-   Style attribute at the bottom.
-   Tag closer /> on its own line, to facilitate ordering and adding attributes.
-   Rather than hard coding android:text, consider using string.xml.

## 4.  Test style rules:

Follow test method naming conventions and use an underscore to separate what's being tested from the specific case being tested. This style makes it easier to see which cases are being tested. 
**Example:**

	testMethod_specificCase1 testMethod_specificCase2

	void testIsDistinguishable_protanopia() {
	  ColorMatcher colorMatcher = new ColorMatcher(PROTANOPIA)
	  assertFalse(colorMatcher.isDistinguishable(Color.RED, 						
	  Color.BLACK))
	  assertTrue(colorMatcher.isDistinguishable(Color.X, Color.Y))
	}


# Best Practices

## 1. Use Gradle configurations

Use Android build system to perform custom build configurations without modifying your app's core source files. our default option should be [Gradle](https://gradle.org/) using the [Android Gradle plugin](https://developer.android.com/studio/build/index.html).

**1.1. Use Property file:**
Create  "gradle.properties"  file to define all the sensitive information about the application. Like signing Configs, server url etc.

**Example :** Define base-url for different environment.


	**Build.gradle file :-**

	productFlavors {
	  Production {
		buildConfigField "String", "BASE_URL", BASE_URL
	  }
	  Staging {
		buildConfigField "String", "BASE_URL", BASE_URL_STAGING
	  }
	}
	
	**gradle.properties file :-**
	
	BASE_URL=www.abcd.com
	BASE_URL_STAGING=stage.abcd.com

**1.2. Use Build types and Flavours :**
Define different server configuration in different build type and flavours for easy and fast development and debugging.

  - Use different package name for non-release builds :

		android {
		    buildTypes {
		        debug {
		            applicationIdSuffix '.debug'
		            versionNameSuffix '-DEBUG'
		        }
		        release {
		           // ...
		        }
		   }
		}

**1.3. Use signingConfigs :**
Define Signing configuration in gradle for fast and easy build generation.

	signingConfigs {
	  release {
		storeFile file("myapp.keystore")
		storePassword KEYSTORE_PASSWORD
		keyAlias "thekey"
		keyPassword KEY_PASSWORD
	  }
    }
    
**1.4** Avoid Maven dynamic dependency resolution such as 2.1.+ as this may result in different and unstable builds or subtle, untracked differences in Behaviour between builds.

**1.5 Use [Proguard](https://developer.android.com/studio/build/shrink-code.html):** 
This will remove all your unused code, which will reduce APK size.

	buildTypes {
	  debug {
		minifyEnabled false
	  }
	  release {
	    signingConfig signingConfigs.release
	    minifyEnabled true
		proguardFiles getDefaultProguardFile('proguard-android.txt'), 			   'proguard-rules.pro'
	  }
	}


## 2.  Maintain code quality :

-   Use software Design Patterns and architectural patterns like MVP/MVVM/MVC/etc.
-   Use code reusability principles
-   Use Android Lint utility to ensure your code has no structural problem by running the code through lint.
-   Detecting and fixing memory leaks in android.
-   Use the Parcelable class instead of Serializable when passing data in Intents or Bundles.
- Always remember to unsubscribe listener.

**2.1.  Resources Usage :**

-   Use .xml files values to define strings, dimension, themes.
-   Use .xml file for shapes and states instead of using images.
-   Use vector drawables as much as you can.
   
**2.2.  Logging guidelines :**
 Always disable logging with production builds.
