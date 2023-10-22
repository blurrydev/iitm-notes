# Live Session

## Frontend Implementation

- **Frontend** is the user facing part of the app consisting of UI and UX.
- A good user interface doesn't necessarily mean fancy user interface.

### Requirements

- Avoid complex logic. Keep it for the backend.
- Should not store data in frontend.
- Should work with stateless protocol. 

### Desirable

- Aesthetically Pleasing.
- Responsive: There should not be any lag. 
- Adaptive: It should be adaptive to different screens.

## Programming Styles

- **Imperative Programming:** We give the exact steps to achieve the final result.
- **Declarative:** Just specify what result we want and it'll do.

## State

- **User Interface** is the result when we apply a function to the state.
- State is the *current configuration or the condition* of an application or the component.

### Different types of States:

1. **System State:** 
	1. It represents the data and settings that affect the entire application. 
	2. This is crucial for the overall functionality of the application.
	3. Typically maintained on the server.
	4. Examples: 
		1. Complete database of amazon.in
			1. Stocks of available items
			2. Prices
			3. Logged in users
			4. Registered users
		2. All news articles ever published on toi.com, bbc.com.
		3. All students, courses, marks, certificates etc. for NPTEL.
	5. Typically huge, but comprehensive.
	6. Completely independent of UI / Frontend.
2. **Application State:**
	1. It focuses more on the localized data.
	2. You can think of it as system as seen by an user / session.
	3. It includes interactivity and session management.
	4. Examples:
		1. Shopping Cart, user preferences, theme
		2. Recommendations, read news articles, followed news items.
		3. Dashboard displays.
	5. This is relevant for designing the UI.
3. **UI State:**
	1. This is also called Ephemeral State. Ephemeral means *lasting for a short time*.
	2. This is the part of the UI that is actually seen and interacted with.
	3. Examples:
		1. Loading icons
		2. Currently selected tab in multi-tab document / page.

> Application state and UI state are the most crucial states in terms of designing an application and it's frontend.

