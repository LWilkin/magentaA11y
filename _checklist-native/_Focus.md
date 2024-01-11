---
layout: entry
title:  "Focus" 
categories: common patterns


keyboard:
  tab, arrow keys or Ctl+tab: |
    Focus visibly moves to all controls
  visible focus indicator: |
    Is clearly shown around controls in a logical order

          
mobile gestures:
  swipe: |
    Initial focus moves to a logical place on screen, then to all meaningful images, text and controls
  Doubletap: |
    Activates controls
    
screenreader: 
  initial focus: |
    Starts in a logical place (ex: back button, close button, top of screen)
  navigate: |
    Focus moves left to right, top to bottom in a logical order
  visible focus indicator: |
    Is clearly shown around content when tapped or with navigation gestures

---


## iOS

### Developer notes
- On most devices, the focus indicator color can be changed to pass color contrast ratios against its background
- Keep focused components from being obscured by other content, like Cookies and Chat buttons
- Focus should move into a picker, modal or alert when it appears
- When a modal or alert is closed, focus should go back to triggering element, or to a logical place
- Focus should be contained in a modal when content underneath is hidden
- Let the device manage focus, for the most part
- Do not move focus automatically when on a user-input component (radio button, text field, etc)
  
<!-- 
  
### Name
- Programmatic name describes the purpose of the control.
- If visible text label exists, the programmatic name should match the visible text label
    - **Note:** Setting a programmatic name while a visible text label exists may cause VoiceOver to duplicate the announcement of the name. If this happens, hide the visible text label from VoiceOver recognition.

Enter information for iOS Name using UIKIT, update below with appropriate details, replace _component with new component name or appropriate description
-->
- **UIKit**
  - You can programmatically set the visible label with `setTitle()`.
    - The _component title will overwrite the _component `accessibilityLabel`.
  - If a visible label is not applicable in this case, set the _component `accessibilityLabel` to the label of your choice.
    - To do this in Interface Builder, set the label using the Identity Inspector
  - To hide labels from VoiceOver programmatically, set the label's `isAccessibilityElement` property to `false`
  - To hide labels from VoiceOver using Interface Builder, uncheck `Accessibility Enabled` in the Identity Inspector.

<!-- 
Enter information for iOS Name using SwiftUI, update below with appropriate details

- **SwiftUI**
  - If no visible label, use view modifier `accessibilityLabel(_:)`.


Enter information for iOS Role, update information below with appropriate details, or remove details not needed

### Role
- When using non-native controls (custom controls), roles will need to be manually coded.

Enter information for iOS Name using UIKIT, update below with appropriate details, replace _component with new component name or appropriate description

- **UIKit**
  - 
  - 

Enter information for iOS Name using SwiftUI, update below with appropriate details

- **SwiftUI**
  - 
  - 

Enter information for iOS Groupings, update below with appropriate details, replace _component with new component name or appropriate description

### Groupings
- Group visible label or icon with the input field, if applicable, to provide a programmatic name for the search field.

Enter information for iOS Groupings using UIKit, update below with appropriate details

- **UIKit**
  - 
  - 
Enter information for iOS Groupings using SwiftUI, update below with appropriate details

- **SwiftUI**
  - Use view modifier `accessibilityElement(children: .combine)` to merge the child accessibility element’s properties into the new accessibilityElement.

Enter information for iOS State, update below with appropriate details, replace control with new component name or appropriate description

### State 


Enter information for iOS State for UIKit, update below with appropriate details, replace control with new component name or appropriate description

- **UIKit**  
  - For enabled: Set `isEnabled` to `true`.
  - For disabled: Set `isEnabled` to `false`. Announcement for disabled is "Dimmed".
    - If necessary, you may change the accessibility trait of the _component to `notEnabled`, but this may overwrite the current accessibility role of the control.

Enter information for iOS State for SwiftUI, update below with appropriate details, replace control with new component name or appropriate description

- **SwiftUI**
  - For selected, use `accessibilityAddTraits(.isSelected)`.
  - For disabled, use view modifier `disabled()`.


Enter information for iOS Focus, update below with appropriate details
-->

### Focus
- Use the device's default focus functionality. 
- Consider how focus should be managed between child elements and their parent views.
- External keyboard tab order often follows the screen reader focus, but sometimes this functionality requires additional development to manage focus.

<!-- 
Enter information for iOS Focus using UIKit, update below with appropriate details
-->

- **UIKit**
  - If VoiceOver is not reaching a particular element, set the element's `isAccessibilityElement` to `true`
    - **Note:** You may need to adjust the programmatic name, role, state, and/or value after doing this, as this action may overwrite previously configured accessibility.
  - Use `accessibilityViewIsModal` to contain the screen reader focus inside the modal.
  - To move screen reader focus to newly revealed content, use `UIAccessibility.post(notification:argument:)` that takes in `.screenChanged` and the newly revealed content as the parameter arguments.
  - To NOT move focus, but dynamically announce new content: use `UIAccessibility.post(notification:argument:)` that takes in `.announcement` and the announcement text as the parameter arguments.
  - `UIAccessibilityContainer` protocol: Have a table of elements that defines the reading order of the elements. 

<!-- 
Enter information for iOS Focus using SwiftUI, update below with appropriate details
-->
 
- **SwiftUI**
  - For general focus management that impacts both screen readers and non-screen readers, use the property wrapper `@FocusState` to assign an identity of a focus state.
    - Use the property wrapper `@FocusState` in conjunction with the view modifier `focused(_:)` to assign focus on a view with `@FocusState` as the source of truth.
    - Use the property wrapper `@FocusState`in conjunction with the view modifier `focused(_:equals:)` to assign focus on a view, when the view is equal to a specific value.
  - If necessary, use property wrapper `@AccessibilityFocusState` to assign identifiers to specific views to manually shift focus from one view to another as the user interacts with the screen with VoiceOver on.


## Android

### Developer notes
- On most devices, the focus indicator color can be changed to pass color contrast ratios against its background
- Keep focused components from being obscured by other content, like Cookies and Chat buttons
- Focus should move into a picker, modal or alert when it appears
- When a modal or alert is closed, focus should go back to triggering element, or to a logical place
- Focus should be contained in a modal when content underneath is hidden
- Let the device manage focus, for the most part
- Do not move focus automatically when on a user-input component (radio button, text field, etc)
  
<!-- 
### Name
- Name describes the purpose of the control
- Programmatic name matches the visible text label or search icon meaning

- **Android Views**
  - `android:text` XML attribute
  - Optional: use `contentDescription` for a more descriptive name, depending on type of view and for elements (icons) without a visible label
  - `contentDescription` overrides `android:text`
  - Use `labelFor` attribute to associate the visible label with the control

Enter information for Android Name for Jetpack Compose, update information below with appropriate details, or remove details not needed

- **Jetpack Compose**
  - Compose uses semantics properties to pass information to accessibility services.
  - Example specification of contentDescription in compose: `modifier = Modifier.semantics { contentDescription = "" }`

Enter information for Android Role, update information below with appropriate details, or remove details not needed

### Role
- When not using native controls (custom controls), roles will need to be manually coded.

Enter information for Android Role for Android Views, update information below with appropriate details

- **Android Views**
  - 

Enter information for Android Role for Jetpack Compose, update information below with appropriate details

- **Jetpack Compose**
  - 

Enter information for Android Groupings, update information below with appropriate details, or remove details not needed

### Groupings
- Group visible label or icon with the input field, if applicable, to provide a programmatic name for the search field.


Enter information for Android Groupings using Android Views, update information below with appropriate details, or remove details not needed

- **Android Views**
  - `ViewGroup`
  - Set the container object's `android:screenReaderFocusable` attribute to true, and each inner object's `android:focusable` attribute to false. In doing so, accessibility services can present the inner elements' `contentDescription` or names, one after the other, in a single announcement.

Enter information for Android Groupings using Jetpack Compose, update information below with appropriate details, or remove details not needed

- **Jetpack Compose**
  - `Modifier.semantics(mergeDescendants = true) {}` is equivalent to `importantForAccessibility` when compared to android views
  - `FocusRequester.createRefs()` helps to request focus to inner elements with in the group


Enter information for Android State, update information below with appropriate details, or remove details not needed

### State

Enter information for Android State for Android Views, update information below with appropriate details, or remove details not needed

- **Android Views**
  - Active: `android:enabled=true`
  - Disabled: `android:enabled=false`. Announcement: disabled

Enter information for Android State for Jetpack Compose, update information below with appropriate details, or remove details not needed

- **Jetpack Compose**

Enter information for Android Focus, update information below with appropriate details, or remove details not needed
-->

### Focus
- Only manage focus when needed. Primarily, let the device manage default focus
- Consider how focus should be managed between child elements and their parent views
- External keyboard tab order often follows the screen reader focus, but sometimes needs focus management


Enter information for Android Focus for Android Views, update information below with appropriate details, or remove details not needed

- **Android Views**
  - `importantForAccessibility` makes the element visible to the Accessibility API
  - `android:focusable`
  - `android=clickable`
  - Implement an `onClick( )` event handler for keyboard, as well as `onTouch( )`
  - `nextFocusDown`
  - `nextFocusUp`
  - `nextFocusRight`
  - `nextFocusLeft`
  - `accessibilityTraversalBefore` (or after)
  - To move screen reader focus to newly revealed content: `Type_View_Focused`
  - To NOT move focus, but dynamically announce new content: `accessibilityLiveRegion`(set to polite or assertive)
  - To hide controls: `importantForAccessibility=false`
  - For a `ViewGroup`, set `screenReaderFocusable=true` and each inner object’s attribute to keyboard focus (`focusable=false`)

<!-- 
Enter information for Android Focus for Jetpack Compose, update information below with appropriate details, or remove details not needed
-->
- **Jetpack Compose**
  - `Modifier.focusTarget()` makes the component focusable
  - `Modifier.focusOrder()` needs to be used in combination with FocusRequesters to define focus order
  - `Modifier.onFocusEvent()`, `Modifier.onFocusChanged()` can be used to observe the changes to focus state
  - `FocusRequester` allows to request focus to individual elements with in a group of merged descendant views
  - Example: To customize the focus events
    - step 1: define the focus requester prior. `val (first, second) = FocusRequester.createRefs()`
    - step 2: update the modifier to set the order. `modifier = Modifier.focusOrder(first) { this.down = second }`
    - focus order accepts following values: up, down, left, right, previous, next, start, end
    - step 3: use `second.requestFocus()` to gain focus

<!-- 
Enter information for Android Custom Accessibility Action, update information below with appropriate details, or remove details not needed
-->
### Custom Accessibility Action
- When UI elements are customized and coded to look like a specific component say button, to ensure that name, role, state and action are all intact might need to update accessibility service and semantics.
- Disclaimer: This customization would not be needed unless it is required to modify/add gestures or actions.

<!-- 
Enter information for Android Custom Accessibility Action for Android Views, update information below with appropriate details, or remove details not needed
-->
- **Android Views**
- 

<!-- 
Enter information for Android Custom Accessibility Action for Jetpack Compose, update information below with appropriate details, or remove details not needed
-->
- **Jetpack Compose**
  - List of custom accessibility actions can be defined relatively easily in compose compared to Views using customActions. 
  - Example: `modifier = Modifier.semantics { customActions = listOf(CustomAccessibilityAction(label = "", action = { true }))}`