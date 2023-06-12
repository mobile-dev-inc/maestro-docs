---
description: A guide to implementing Page Object Model within Maestro
---

# Page Object Model


## Content

* Introduction
* Login Page example
  * login.js
* Nested example
  * cards.js
* How to structure and tips
  * Folder structure example
  * Ensuring all elements are loaded
    * loadElements.yaml
    * flow.yaml
* Cross-platform example


## Introduction

Implementating a Page Object Model has many benefits:
* Improved readability, abstraction and grouping
* Reducing unnecessary duplication
* Improving test/flow maintenance

It allows you to update an element in one place which will then cascade throughout all of your tests/flows. This can save a lot of time when elements are modified and also assist in easier debugging of issues.



## Login Page example

### login.js
```
// login.js
output.login = {
	email: 'email_text',
	password: 'password_text',
	loginBtn: 'loginButton',
	registerBtn: 'registerButton'
}
```

You can then use these variables to reference element IDs, text or even other test data:

```
- runScript: login.js
- tapOn:
	id: ${output.login.email}
- inputText: "simon@maestro.com"
- tapOn:
	id: ${output.login.password}
- inputText: ${PASSWORD}
- tapOn:
	id: ${output.login.loginBtn}
```



## Nested example

### cards.js
```
// cards.js
output.cards = {
	cardName: 'card_title',
	cardImage: 'card',

	// All Cards Screen
	allCards: {
		createNewBtn: 'btn_create',
		cardImage: 'card_image',
		cardName: 'card_title'
	},

	// Virtual Cards
	virtualCards: {
		createNewBtn: 'btn_create',

		cardDetails: {
			cardNumber: 'card_number',
			expiryDate: 'card_expiry'
		}
	}
}
```

You can create nested element structures to better separate/organise screens and flows. Using the example below, it's easy to define a separate structure for Virtual Cards within the overall Cards object. You could then use them in your flows as follows:

```
- runScript: cards.js
- tapOn:
	id: ${output.cards.virtualCards.createNewBtn}
- assertVisible:
	id: ${output.cards.virtualCards.cardDetails.cardNumber}
```



## How to structure and tips

### Folder structure example

Creating an elements folder is good practice as it allows you to keep all of your element files together. 

```
android/
	cards/
	elements/
		cards.js
		help.js
		home.js
		loadElements.yaml
		login.js
		nav.js
	home/
	login/
iOS/
	cards/
	elements/
		cards.js
		help.js
		home.js
		loadElements.yaml
		login.js
		nav.js
	home/
	login/
```


### Ensuring all elements are loaded

Once you begin creating numerous js files to cover all of your app screens and elements, it can become tricky to remember if you've included the right ones at the start of your test, especially if your flow is crossing multiple areas. A nice trick is to simply add your `runScript` command once to a single common flow, and then you can run that parent flow once at the start of all your other flows to ensure all of your screens and elements are loaded in correctly.

#### loadElements.yaml
```
# loadElements.yaml
appId: com.appid
---
- runScript: cards.js
- runScript: home.js
- runScript: login.js
- runScript: nav.js
- runScript: tabBar.js
```

Usage:

#### flow.yaml
```
appId: com.appID
---
- runFlow: elements/loadElements.yaml
- launchApp
// Test Steps
```



## Cross-platform example

If you have the same app across both Android and iOS but the elements have different IDs, you can employ `runFlow` with a platform conditional to load in the correct elements.

```
- runFlow:
    when:
	    platform: Android
    commands:
	    - runScript:
	        file: android_elements/login.js
- runFlow:
    when:
	    platform: iOS
    commands:
	    - runScript:
	        file: iOS_elements/login.js
```
