# Presentr

[![Version](https://img.shields.io/cocoapods/v/Presentr.svg?style=flat)](http://cocoapods.org/pods/Presentr)
[![Platform](https://img.shields.io/cocoapods/p/Presentr.svg?style=flat)](http://cocoapods.org/pods/Presentr)
[![License](https://img.shields.io/cocoapods/l/Presentr.svg?style=flat)](http://cocoapods.org/pods/Presentr)

*Presentr is a simple wrapper for the Custom View Controller Presentation API introduced in iOS 8.*

## About

It is very common in an app to want to modally present a view on top of the current screen without covering it completely. It can be for presenting an alert, a menu, or any kind of popup with some other functionality.

Before iOS 8 this was done by adding a subiew on top of your content, but that is not the recommended way since a modal should ideally have its own view controller for handling all of the logic. View controller containment was also used, and was a better alternative, but still not ideal for this use case.

iOS 8 fixed all of this by introducing Custom View Controller Presentations, which allowed us to modally present view controllers in new ways. But in order to use this API it is up to us to implement a couple of classes and delegates that could be confusing for some.

**Presentr** is made to simplify this process by hiding all of that and providing a couple of custom presentations and transitions that I think you will find useful. If you want to contribute and add more presentations or transitions please send me a pull request!

## Installation

#### [Cocoapods](http://cocoapods.org)

```ruby
use_frameworks!

pod 'Presentr'
```

## Usage

### Main Types

#### Presentation Type

```swift
public enum PresentationType {
  case Alert
  case Popup
  case TopHalf
  case BottomHalf
}
```

#### Transition Type

```swift
public enum TransitionType{
  // System provided
  case CoverVertical
  case CrossDissolve
  case FlipHorizontal
  // Custom
  case CoverVerticalFromTop
  case CoverHorizontalFromRight
  case CoverHorizontalFromLeft
}
```

### Getting Started

#### Create a Presentr object

It is **important to hold on to the Presentr object as an instance variable(property)** since internally it will be used as a delegate for the custom presentation.
```swift
let presenter = Presentr(presentationType: .Alert)
presenter.transitionType = .CoverHorizontalFromRight // Optional
```
The presentation type is required for initialization. The transition type is optional.

```swift
presenter.presentationType = .Popup
presenter.transitionType = .CoverVerticalFromTop
```
Both types can be changed later on in order to reuse the Presentr object for other presentations.

#### Present the view controller.
```swift
customPresentViewController(presenter, viewController: alertController, animated: true, completion: nil)
```
This is a helper method provided for you as an extension on UIViewController. It handles setting up the view controller's delegates and other boilerplate. 

#### Presentr also comes with a cool AlertViewController baked in if you want something different. API is very similar to Apple's alert controller.
```swift
let alertController = Presentr.alertViewController(title: "Warning", body: "Are you sure?")

let cancelAction = AlertAction(title: "Cancel", style: .Cancel) {
  print("CANCEL!")
}
        
let okAction = AlertAction(title: "Ok", style: .Destructive) {
  print("OK!")
}
        
alertController.addAction(cancelAction)
alertController.addAction(okAction)
```

## Requirements
* Xcode 7.3+
* iOS 8.0+
* Swift 2.2+

## Documentation

Read the [docs](http://danielozano.com/PresentrDocs/). Generated with [jazzy](https://github.com/realm/jazzy).

## Author
[Daniel Lozano](http://danielozano.com) <br>
iOS Developer @ [Icalia Labs](http://www.icalialabs.com)

## License
Presentr is released under the MIT license.  
See LICENSE for details.
