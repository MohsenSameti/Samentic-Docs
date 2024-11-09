---
hide:
  - navigation
---

## Introduction to MVI

## How Are Screens Organized?

Each Screen will be Composed of 3 main composable, each of which handle composable:
- First one handles navigation logic
- Second one handles state 
- Third one is PureUI composable.

These Composables are named as follows:
- &lt;ScreenName&gt;Route: the first one which controls navigation has a  **Route** suffix.
- &lt;ScreenName&gt;: the second one which controls the state has the same name as the screen.
- &lt;ScreenName&gt;Ui: the third one which is the pure ui has a **Ui** suffix.

## Sending Action From UI Composable

## Send Action to ViewModel

## ViewModel HandleActions

## ViewModel Update State

## References
- [How to Implement MVI with Delegates on Android](https://engineering.teknasyon.com/how-to-implement-mvi-with-delegates-on-android-f2aa1a842b73)
- [ViewModel One-Off event antipatterns](https://manuelvivo.dev/viewmodel-events-antipatterns)
- [YouTube: How to write your own MVI system and why you shouldn't](https://www.youtube.com/watch?v=E6obYmkkdko)