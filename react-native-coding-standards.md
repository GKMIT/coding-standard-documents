# What is React-Native?
[React Native](https://reactjs.org/docs/getting-started.html) is an open-source framework for developing Android, iOS, web and UWP applications, originally released by Facebook in 2015.The React Native framework is built on top of the React library in JavaScript for building user interfaces.

React Native is a new technology and Best practices are still evolving However, we have summarised some of them in this document. Let’s Look at them briefly:


## Project Structure 

Defining a proper structure for a project is essential for growth, efficiency and easier maintenance.

Our first step will be to define the directory structure within `src` (Source). This directory will contain all major project files.

	|— src
		|— screens
			|— login
				|— Login.js
				|— styles.js
			|— home
				|— Home.js
				|— styles.js
			|— profile
				|— Profile.js
				|- styles.js
		|— actions
			|— users.js
			|— products.js
		|— assets
			|— images
			|— components
				|— button
					|— styles.js
					|— index.js
					|— Button.js
				|— inputs
					|— datetime
						|— index.js
						|- styles.js
						|- Datetime.js
					|— text
						|— Text.js
						|- styles.js
						|- index.js
		|— utils
			|-constants.js
			|— utils.js
			|— validations.js
		|— reducers
			|— users.js
			|— products.js
		|— network
			|— URLs.js
			|— NetworkManager.js
		|— resources
			|— strings.js
			|— colors.js
			|— fonts.js
		|- config
			|- routes.js
			|- saga.js
			|- environment.js
			|- store.js


## **Naming Conventions**

-   A folder and sub folder name should always start with small letters and the files belong the folders is always in pascal case.
-   Component Name should follow the pascal case
    
-   Class names should be declared as file names that will be easy during importing and to maintain the standard declaration.
    
-   The object and variable declaration should always be in camel case statement.



## Code Formatting 

- Create aliases using [babel-plugin-module-resolver](https://github.com/tleunen/babel-plugin-module-resolver) to avoid nested imports such as import Product from						
`../../../Components/Product`	Aliases created using babel-plugin-module-resolver look something like this.

		alias: {
		  actions: './app/actions',
			api: './app/api',
			assets: './app/assets',
			components: './app/components',
			containers: './app/containers',
			constants: './app/constants',
			sagas: './app/sagas',
			selectors: './app/selectors',
			types: './app/types',
			utils: './app/utils',
		}
		

-   Including all the controls in a single import belong to the same module end with semicolon. There should be no space between two imports.
    
		Ex. : - import { View, Platform, StatusBar, FlatList, Share, Text } from "react-native";

-   Not allowing setState() to be invoked on Render() of a React Component.
    
-   If continuation lines are not indented automatically, indent them one tab stop (four spaces).
    
-   Add at least one blank line between method and property definitions.
    
-   There should be no line space between a similar looking statement or similar bunch of code applied for the same activity.
    
-   Always end a statement with a semicolon.


##  Best Practices

**1.** Split the components into presentational and containers.

-  ### **Presentational components**
	Presentational components are those components whose only job is to render a view according to the styling and data passed to them. This means that they don't have direct access to Redux or other data stores. Data is passed to them via props.

 -  ###  **Container components**

	Container components are those React components which have access to the store. These components make API calls, do processing and contain the business logic of the app. Container components shouldn't have the view logic or presentational logic. The job of container components is to compute the values and pass them as props to the presentational components.

  
  


**2.** Choose wisely between 4 types on react component according to the functionality and requirement,

    
-   ### **Functional Components**
    Functional components are functions that take in props and return JSX. They don’t have state or lifecycle methods, but this functionality can be added by implementing React Hooks.
    

-   ### **Class Components**
   
	Class components can utilize the main functions of React, state, props, and lifecycle methods. Unlike functional components, class components consist of a class extending with React.Component.

-   ### **Pure Components**
    

	Pure components do not depend or modify the state of variables outside its scope, pure components perform shallow comparisons on state change. Pure components take care of shouldComponentUpdate(), If the previous state and/or props are the same as the next, the component is not re-rendered.

	React Components are usually re-rendered when:

	-   props values are updated
	-   forceUpdate() is called 
	-   setState() is called
 
-   ### **Higher-Order Components**
    
	Higher-order components(HOC) are functions that return a component(s). They are used to share logic with other components. The basic usage of Hoc are :

	- Get array data from state or props.
	-	Map over that array and return a React component for each element.
    

**For Example :**
`this.props.myArray.map((element) => (<MyComponent />))
`
	
This is a function that returns one or multiple components, depending on the number of elements in the array, also known as HOC.

**3.**  Bind custom component using constructor, There is a Babel plugin called [Class properties transform](https://babeljs.io/docs/plugins/transform-class-properties/) . You can write an auto-bound function using the fat-arrow syntax.
    
**4.** Use Redux for managing States and Business Logic, Try to avoid using setState in your component when you are using state management libraries like redux.
    
**5.** For Redux’s event dispatching actions use bindActionCreators.
    
**6**.  Use a library like redux-saga. redux-saga helps you handle the App side effects (asynchronous logic such as API calls, Navigation to another screen, etc.) and makes them easier to code and manage.
    
**7.** Code reusability is essential for every project for Example:
    

- Create small reusable components with minimum functionality.
    
- Write similar logical functions in separate file like validation, calculation functions.
    

**8.** To Prevent The Breaking functionality, use fixed versions of dependencies
		
	"react-native-modal": "^11.3.1" → "react-native-modal": "11.3.1",

**9.**  Do not use inline styling. Import JavaScript files with styles defined and reuse in multiple files.
    
**10.**  Define styles separately from your React components.
    
**11.**  Use Platform specific code and styles:
    

	ios: {
		fontFamily: 'Arial',
	},
	android: {
		fontFamily: 'Roboto',
	},

  

**12.**  Do not use logs in the release build.
    
**13.**  Prefer using [react-native-fast-image](https://github.com/DylanVann/react-native-fast-image) for image caching solution, This will help you boost the app even if that is minimal.
    
**14.** For better UI experience use SafeAreaView which provides automatic padding when a view intersects with a safe area for IOS devices.
    
**15.**  Write test cases to ensure that any new code added to your project integrates well with existing code and does not break existing functionality. App should implement at least the Snapshot tests and Redux tests (actions, reducers, sagas, and selectors), For the former, you can use a JavaScript test runner,
