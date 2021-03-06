## 8.4.1

### Fixed

* Fixed a crash when done drawing a stroke in the brush tool.

## 8.4.0

### Added

* Added a linear focus mode to the focus tool.
* Added a gaussian focus mode to the focus tool.
* Added temperature adjustments to the adjustment tool.
* Added blacks adjustments to the adjustment tool.
* Added whites adjustments to the adjustment tool.

### Changed

* The text tool now uses the same text settings of the last selected text when creating new texts.
* The `FocusType` type has been deprecated because it used incorrect namings. It is replaced by the `FocusMode` type, which uses the same namings as the PhotoEditor SDK on HTML5 and Android. More specifically `FocusType.linear` is now `FocusMode.mirrored` and `FocusType.gradient` is now `FocusMode.linear`, `.radial` and `.gaussian` remain the same.
* The SDK can now be used for testing purposes without unlocking it with a license. A watermark image will be displayed above the edited photo in such cases.

## 8.3.10

### Added

* Added the option to adjust the gamma in the adjustments tool.

### Fixed

* Fixed a crash when instantiating a `PESDKPhotoEditMenuItem` with Objective-C for a tool that is not licensed.

## 8.3.9

### Added

* Added `PhotoEditViewController.serializedSettings(withImageData:)` which enables you to specify whether or not to include image data in the generated JSON. It is recommended that the image is not included in the JSON but saved as a separate file.
* Added `PhotoEditViewControllerOptions.useParentNavigationItem`, allowing for the `PhotoEditViewController` to be embedded inside a custom container view controller inside a `UINavigationController`.
* Added accessibility support to the Text Design tool.

### Changed

* Changed serialization to require a `Photo` object instead of `UIImage`. This improves memory usage.
* Improved serialization performance when not including image data in the serialization.
* Changed the Text Design Tool icon.

### Fixed

* Fixed a bug where the edit screen would not be dismissed when changing the text of an already added text design from within the `TextDesignOptionsToolController`.

## 8.3.8

### Fixed

* Fixed multiple layout issues in the text design tool.

## 8.3.7

### Added

* Added support for gaussian and gradient focus to the renderer, to support cross-platform (de-)serialization.
* Added support for custom frame sizes to the renderer, to support cross-platform (de-)serialization.

### Fixed

* Fixed an issue with an incorrect deserialized focus gradient size.
* Fixed a layout issue in the `FontSelectorView`.

## 8.3.6

### Fixed

* Fixed a retain cycle in the serialization test suite.
* Fixed a bug when deserializing an unknown type of focus.
* Fixed a bug that added a little rotation to stickers and text when the image is flipped, the state is serialized and then again deserialized.
* Fixed a memory issues with labels that have a huge height by limiting the maximum allowed height.
* Fixed a bug where the UI would become unresponsive when the editor is embedded in an `UINavigationController` and the user very quickly closes a tool after opening it.
* Fixed a bug in the filter and focus shaders that prevented the iOS 12 shader compiler from compiling the shaders.

## 8.3.5

### Fixed

* Fixed a race condition when setting `StickerCategory.all`.
* Fixed a race condition in `PaintingFragment`.
* Fixed a layout bug when embedding `PhotoEditViewController` in a `UINavigationController` with an opaque navigation bar.
* Fixed an issue where drawing a new path in the brush tool would flicker.

## 8.3.4

### Fixed

* Fixed an issue where deserializing a brush would not load its first point.
* Fixed an issue where drawing a dot in the brush tool was not possible.
* Fixed an issue where `renderPipelineBlock` was not called during the high resolution rendering.
* When embedding the `PhotoEditViewController` in an `UINavigationController`, the `tintColor`, `imageEdgeInsets` and `backgroundImage` properties of the toolbar buttons are copied to the buttons in the navigation bar.

## 8.3.3

### Fixed

* Fixed an issue with iTunes Connect not accepting the build when integrating the SDK via CocoaPods.

## 8.3.2

### Fixed

* Fixed a bug where setting a title on a discard or apply button would not work when embedding the `PhotoEditViewController` in a `UINavigationController`.
* Fixed a crash when setting `StickerCategory.all` to an array of sticker categories with duplicate titles while the `StickerToolController` was visible.

## 8.3.1

### Fixed

* Fixed a crash when increasing the width of text too much.
* Fixed an issue with color spaces. Colors are now always displayed correctly and the exported image will have the Display P3 color space on supported devices. Some filters still do not support wide color gamuts and clamp to the sRGB gamut. This will be fixed in a future update.
* Fixed a crash when updating stickers or sticker categories from a thread different than the main thread while the sticker tool was visible.
* Removed the new -Osize Swift optimization mode for now, because iTunes Connect rejects binaries built with it.

## 8.3.0

### Added

* Added support for HEIF image exports. See `PhotoEditViewControllerOptions.outputImageFileFormat` for more details.
* Added backend support for gamma correction.

### Changed

* Built with Swift 4.1 / Xcode 9.3.
* Switched from `Float` to `Double` in all photo edit and serialization models, because converting an `NSNumber` implicitly to `Float` (e.g. `NSNumber(0.26) as? Float`) returns `nil` with Swift 4.1 if it can't be represented exactly by a float. 
* When updating `StickerCategory.all` while the sticker selection tool is visible, it now automatically reloads the available categories and stickers.

### Fixed

* Fixed some minor layout bugs on iPhone X.
* Fixed an issue where the dSYM file would not be integrated into the final app when using CocoaPods.
* Fixed an issue with the SoftLight blend mode not looking as expected.
* Fixed an issue with the brush not respecting the hardness when deserializing.
* Fixed an issue with the first path of a brush not being drawn when deserializing.
* Fixed an issue with the radial blur being misplaced when deserializing.
* Fixed an issue with overlays being misaligned.

## 8.2.4

### Added

* Added an option to show a close button in the `CameraViewController`. See `CameraViewControllerOptions. showCancelButton`, `CameraViewControllerOptions.cancelButtonConfigurationClosure` and `CameraViewController.cancelBlock` for more details.
* Added full support for right-to-left languages.

### Fixed

* Fixed an issue where the flash icon would not be visible while the camera was in video mode.
* Fixed an issue where all Objective-C bridged `SpriteModel`s were of type `PESDKSpriteModel` instead of their concrete subclasses.
* Fixed an issue with the toolbar having the wrong size while the keyboard was active on an iPhone X.
* Fixed an issue where focus would not work in the camera after switching from back to front camera. 

## 8.2.3

### Fixed

* Fixes an issue with the transform tool not rotating correctly.
* Fixes an issue where an overlay would not be applied when selecting the 'Normal' blend mode.

## 8.2.2

### Fixed

* Fixes an issue with the size of rotated stickers on iOS 10.

## 8.2.1

### Fixed

* Overlays and blur handle transparency correctly now.
* `TextFontToolControllerOptions.fontSelectorViewConfigurationClosure` and `TextFontToolControllerOptions.handleButtonConfigurationClosure` work as expected now.
* Fixes an issue with undoing brush strokes.
* Fixes an issue where the undo or redo buttons would be active although there was nothing to undo/redo.
* Fixes a bug where video recording would take a long time to stop on older devices.
* Fixes a rare crash with the license checker on iOS 9.

## 8.2.0

### Added

* Added a check that verifies that no two assets have the same identifier.
* Added a `Photo` class that wraps different types of image data. Added `PhotoEditViewController(photoAsset:configuration:menuItems:photoEditModel:)` and `PhotoEditPreviewController(photoAsset:photoEditModel:)` and deprecated all previous initializers of both classes in favor of those. Please take a look at the API documentation for the `Photo` class, as using it correctly can have a huge impact on the memory footprint of the SDK.
* Added `accessibilityIgnoresInvertColors` where needed.
* PNG support, see `PhotoEditViewControllerOptions.outputImageFileFormat` for more details.
* Added `PESDK.renderPipelineBlock` which can be used to modify each stage of the render pipeline.

### Fixed

* The top screen edge system gesture is now deferred to avoid conflicts with the transform tool.
* The touchable area for `leftButton` and `rightButton` in the toolbar is wider now.
* Removed all server calls for enterprise licenses.
* Fixed invalid license check in `BrushColorToolController` and `TextOptionsToolController`.
* Improved performance and memory usage.

## 8.1.3

### Fixed

* Fixed a bug where `FrameToolControllerOptions.cellConfigurationClosure` would not be called.

## 8.1.2

### Fixed

* Fixed a crash when narrowing the text bounding box while zoomed in on the image.

## 8.1.1

### Added

* Added haptic feedback for supported devices.
* Added class replacement support for `StickerImageView`, `FrameImageView`, `SpriteLabel`, `Painting` and `CanvasView`.

### Changed

* Made the `BrushSpriteModel` initializers public.

### Fixed

* Fixed a bug where custom fonts would not be loaded.
* Fixed an issue where sticker and sticker category thumbnails would sometimes have lower resolution.

## 8.1.0

### Added

* Added the possibility to change a sticker's brightness, contrast and saturation. Take a look at `Sticker.allowBrightnessAdjustment`, `Sticker.allowContrastAdjustment`, `Sticker.allowSaturationAdjustment` and `StickerAction.brightness`, `StickerAction.contrast`, `StickerAction.saturation` for more details.
* iPhone X support for `CameraViewController`.
* Added `TextToolControllerOptions.dimmingViewConfigurationClosure`.

### Changed

* `Font` expects an `URL` instead of a `String` now.

### Fixed

* Fixed a misplaced title view on iOS 9 when embedding the `PhotoEditViewController` inside a `UINavigationController`.
* `StickerToolController` displays the currently selected sticker category as its title again.
* The color picker's saturation and brightness picker updates as expected now when saturation is set to 0 and the user drags the hue picker.
* `ColorPickerViewController` and `FontSelectorViewController` didn't call `addChildViewController(_:)` and `didMove(toParentViewController:)` for their contained `SpriteEditController`, resulting in layout issues.

## 8.0.1

### Fixed

* Fixed a bug where static frames would not be shown.
* Made `PhotoEditViewController.init(photo:data:configuration:menuItems:photoEditModel:)` public to enable subclassing `PhotoEditViewController`.
* Fixed new warnings generated by Xcode 9.1 beta.
* Fixed a bug where undo and redo would not work correctly when drawing out of bounds within the brush tool.

## 8.0.0

### Added

* Full support for iOS 11 and Swift 4.
* Added rotation gesture support to `FrameToolController` (disabled by default).
* Added serialization format v3.0.0, which can be used to serialize and deserialize edits across all platforms.
* Added support for the iPhone X to `PhotoEditViewController`.

### Changed

* Completely refactored the sprite handling code. Sprites (stickers, text, brush and frames) are now directly rendered on top of the image instead of rendering a view snapshot. This results in better looking images, better performance and more robust code.
* Completely refactored `PhotoEditViewController` and all `PhotoEditToolController` subclasses. We make heavy use of composition and container view controllers now, leading to better support for customizations and custom user interfaces.
* All view controllers and views can be replaced by a custom subclass using `PESDK.replaceClass(_:with:)` for even better customization options.
* Undo and redo is now supported by all tools. The sticker, text and brush tools continue to have a local undo/redo stack in addition to the global undo/redo stack.

### Fixed

* Fixed an issue where the selected crop rectangle would change after tapping the apply button in the transform tool.
* Fixed an issue where focus would change its appearance and position after transform.
* Fixed an issue where the color saturation and brightness picker would sometimes not update while dragging the hue picker.
* The `PhotoEditViewController` can now be pushed onto a navigation controller that uses a translucent navigation bar.
* Fixed various layout issues with the transform and frame tools.
* Fixed a crash when quickly switching between a sticker and text.

### Removed

* Removed the transparent color from the default color palette for text color and brush color.
* The `ToolbarController` class has been removed. An instance of `PhotoEditViewController` can now be used directly.

## 7.3.0

### Fixed

* Fixed a layout issue in tool controllers when zooming is disabled.
* Fixed a memory issue while deserializing.
* Fixed an issue in the transform tool where the selected crop rectangle would sometimes not match the actual crop rectangle.
* Fixed an issue with the image renderer emitting a warning.

### Deprecated

* Serialization version 2.0.0 has been deprecated in this release and will not be supported by future versions of the SDK. Please use PhotoEditor SDK 8.0 with serialization version 3.0.0 instead.

## 7.2.0

### Added

* `PhotoEditViewController` has a new property called `hasChanges`, which is `true` if a user applied any changes to a photo.
* `StickerToolControllerOptions` has a new property called `defaultStickerCategoryIndex` that can be used to specify the index of the initially selected sticker category.
* All `UICollectionViewCell` subclasses can be replaced with custom subclasses using `Configuration`'s `replaceClass(_:replacingClass:moduleName:)` method.

### Changed

* `TransformToolController` now sends a `.transformStraightenAngleChange` analytics event for changes of the straighten angle.
* `TransformToolController` now includes `.cropRect`, `.straightenAngle` and `.aspectRatio` attributes in its `.applyChanges` analytics event.
* When adding or removing a sticker a `.stickerAdd` or `.stickerRemove` analytics event is sent with the associated sticker as a `.sticker` attribute. Those events are also sent when adding or removing a sticker by tapping the undo/redo buttons.
* When adding or removing text a `.textAdd` or `.textRemove` analytics event is sent with the associated text as a `.text` attribute. Those events are also sent when adding or removing text by tapping the undo/redo buttons.
* `TextOptionsToolController` now includes `.text`, `.font`, `.textColor`, `.backgroundColor` and `.alignment` attributes in its `.applyChanges` analytics event.

## 7.1.1

### Added

* `CameraViewControllerOptions` includes a `includeUserLocation` property now that is `true` by default. It can be used to stop the camera from asking for the user's location.

### Changed

* `LoggerProtocol` is now a `class` protocol because loggers are required to be reference types in the current implementation.

### Fixed

* Fixed several smaller bugs regarding deserialization.
* Sometimes the cropping area would be resized while modifying the straighten angle.
* Memory is not copied twice anymore during painting fragment restoration.
* The project compiles with Xcode 9 now.

## 7.1.0

### Added

* The camera tags photos with their location now. This only works when using `Data` instances instead of `UIImage` instances to pass the photo around because those strip EXIF data. See `CameraViewController.dataCompletionBlock` for more details.
* We added a default confirmation dialog when dismissing the editor with changes pending. This can be changed or disabled by setting `PhotoEditViewControllerOptions.discardConfirmationClosure`.

### Changed

* The preview image is now automatically resized when a slider overlays the preview at the bottom, so that is always completely visible.
* We replaced the gaussian blur used in the focus tool with a lens blur like effect for much better looking photos. This does not work on the following older devices where we continue to use a gaussian blur due to performance issues:
	* iPad mini 1st, 2nd and 3rd gen
	* iPad 2nd and 3rd gen
	* iPhone 4S
	* iPod touch

### Fixed

* Fixed various issues with the serialization and deserialization features.
* Fixed an issue with different color spaces used for the preview and the thumbnails in the filter tool.
* Stickers now use anti-aliasing.
* The icon of the 'No Frame' cell in the frame tool is now tinted with the cell's `tintColor` to better match other cells.
* The label of the 'Magic' cell in the main menu is now tinted with the cell's `tintColor` when highlighted to better match other cells.
* The `Slider` now sends a `.touchUpInside` event after a `.touchDown` event has been sent without dragging in between.
* When adding a frame to a photo it would sometimes not completely cover the preview image (by about 1 px).
* When selecting a sticker with its `tintMode` set to `.none` and then dismissing the `StickerOptionsToolController`, the color option would be visible for a split second during the dismissal animation.
* The `BoxGradientView` and `CircleGradientView` now only draw themselves while visible, resulting in a minor performance improvement.
* Sprites didn't have the correct position for a split second when opening the frame tool.
* Sprites would be rotated in the wrong direction when the photo has been flipped.
* Text bounding box resizing would be inverted if the image has been flipped and rotated.

## 7.0.1

### Added

* Added the ability to zoom using a pinch gesture within the `CameraViewController`.

### Fixed

* The icon of the 'No Overlay' option in the overlay tool was not using its @2x and @3x variants.
* Fixed a bug with the new filters and adjustments.
* Fixed interface rotation support.

## 7.0

### Changed

* **The SDK has been renamed from `imglyKit` to `PhotoEditorSDK` and all class prefixes have been renamed from `IMGLY` to `PESDK`. Likewise the CocoaPod has been renamed to `PhotoEditorSDK`.**
* We now ship the framework as a DMG file and include the dSYM file and bcsymbolmaps for better debugging. To integrate the dSYM into your final app, please follow the [updated manual integration guide](https://docs.photoeditorsdk.com/guides/ios/v7_1/introduction/getting_started).
* The `PESDK.shared` singleton has been removed. All of its properties are now static properties on the `PESDK` class.
* The default progress view must be set using the static `PESDK.progressView` property instead of the `Configuration` closure.
* The integrated fonts have been changed.
* The `AdjustToolController` has been improved for much better looking and faster adjustments.
* We were able to significantly decrease the size of our filter's lookup images while also improving the filter's performance.
* All asset names have been changed to a consistent naming scheme.
* The overall look and feel of the `FrameToolController` has been improved.
* Custom stickers are now added by setting `Sticker.all`, custom fonts are added by setting `FontImporter.all`, custom frames are added by setting `Frame.all` and custom overlays are added by setting `Overlay.all` instead of using the `Configuration` class.

### Added

* Serialization and deserialization has been added. Because of this many classes (e.g. `Sticker`, `Frame`) now require an `identifier`. For more information please see the documentation.
* The `OverlayToolController` tool has been added, which can be used to add overlays to a photo. Please see the documentation for more information.
* A custom logger with varying log levels was added. See documentation for more information.
* The `Sticker` class now supports `.colorized` as its `tintMode`. See the API documentation for more information.
* A 3:2 crop aspect has been added to `TransformToolController`'s defaults.
* An Emoticon and a Shapes sticker set has been added.
* `TextFontToolControllerOptions` now has a `fontSelectorViewConfigurationClosure` property and a `handleButtonConfigurationClosure` property for better customization.
* `StickerToolControllerOptions` now has a `stickerPreviewSize` property to adjust the size of the stickers in the preview.

### Removed

* The Toy sticker set has been removed.

### Fixed

* The button to show/hide the font selector view within the `TextFontToolController` now respects the view's `tintColor`.
* Full accessibility support has been restored.

## 6.5.4

### Changed

* With the color picker expanded you can now tap anywhere above it to dismiss the color picker.
* We restored iOS 8 compatibility in this release. Please note that this only means that the framework can be integrated into a target with iOS 8 as its deployment target. However most classes and especially all view controllers are *not* available on iOS 8. We strongly advise that you disable any editing functions for users running iOS 8.

## 6.5.3

### Changed

* We replaced the set of included fonts with much better looking fonts.

## 6.5.2

### Fixed

* Fixed a crash when adding text. This was introduced by the Swift 3.1 compiler, see [SR-4393](https://bugs.swift.org/browse/SR-4393) for more details.

## 6.5.1

### Fixed

* Fixed an issue with the `forceCropMode` setting.

## 6.5.0

### Changed

* This version is compiled with Swift 3.1 and can be used with Xcode 8.3. It does not contain any other changes.

## 6.4.2

### Fixed

* Fixed a scaling issue regarding backdrops.

## 6.4.1

### Changed

* Sticker and text overlays have a bigger touch area so that they are easier to grab.

### Fixed

* Fixed a rare crash in `CameraViewController` that occurred when disabling focus lock while deallocating the controller.

## 6.4.0

### Added

* Added a `discardConfirmationClosure` property to `PhotoEditViewControllerOptions` that is called when tapping the cancel button while changes are applied to the image.
* Zooming is now enabled in all tools except for the focus tool.

### Changed

* The overlay buttons (i.e. undo, redo, etc.) in the sticker, text and brush tool have been moved to the bottom.
* `StickerTintMode.tint` has been renamed to `StickerTintMode.solid`.
* `StickerTintMode.ink` has been renamed to `StickerTintMode.colorized`.
* When adding long text the created label breaks the text into multiple lines if the font size would be too small otherwise.
* `IMGLYSetLocalizationDictionary` has been replaced by `PESDK.localizationDirectory`.
* `IMGLYSetLocalizationBlock` has been replaced by `PESDK.localizationBlock`.
* `IMGLYSetBundleImageBlock` has been replaced by `PESDK.bundleImageBlock`.

### Fixed

* `DefaultProgressView` was not positioned correctly when used in an iPad Split View environment.
* The menu collection views were not positioned correctly when used in an iPad Split View environment.

## 6.3.1

### Fixed

* Fixed warnings that are generated by SwiftLint 0.16.1.
* Moved the overlay image generation to a background queue, so that the progress view appears immediately when the user taps the save button.
* Fixed an ambiguous constraints warning in `CameraViewController`.
* Fixed an issue where the loading progress view would disappear while presenting the editor.

## 6.3.0

### Added

* Added an option to change the default color of newly added text (see `TextToolControllerOptions.defaultTextColor`).
* A progress view is displayed while generating the preview image now.
* Tinting of stickers can be enabled on a per sticker basis (see `Sticker.tintMode`).
* Crop Aspect Ratios can be rotated by tapping on an already selected crop aspect (see `CropAspect.isRotatable`).

### Changed

* Changed the default icon of the transform tool.
* The magic tool displays a selected state when active.
* The `.straighten` option has been removed from the default options of `TextOptionsToolController` and `StickerOptionsToolController`.
* The `.flip` option has been removed from the default options of `TextOptionsToolController`.
* The alignment, bring to front, straighten and flip buttons within `TextOptionsToolController` were moved from an overlay into the menu.
* When resizing text the bounding box of the text becomes wider along with the font size.
* While the `BrushColorToolController` is active the user can continue to paint in the canvas.
* Editing text works by just single tapping on an already selected label instead of long pressing.
* The delete button within the brush tool was moved to the top, the bring to front button was moved from an overlay into the menu.
* The flip, straighten and bring to front buttons within `StickerOptionsToolController` were moved from an overlay into the menu.

### Fixed

* Fixed a crash that occurred when opening the transform tool very quickly after presenting the editor.
* Fixed an issue with the brush tool that occurred when opening the brush very quickly after presenting the editor.
* Fixed an issue where the progress view would not disappear when tapping the save button.
* Fixed an issue regarding the frame tool and rotated images.
* Fixed a bug where a crop would sometimes be applied although the user tapped the cancel button.
* When changing a text the changes are reflected in the label while typing.
* Fixed a crash in `CameraController`.

## 6.2.0

### Added

* Support for wide color images. More information is available [here](https://medium.com/imgly/bringing-wide-color-to-photoeditor-sdk-a6ce8bb19ef7#.1nw0egenf).
* Added redo support and optimized undo support. Each time the sticker, text or brush tool is openend, a new undo/redo stack is created and local changes within those tools can be un- and redone. The `PhotoEditViewController` also has support for undo and redo and performs all undo or redo operations of the tools mentioned above combined, either step by step or tool by tool (see `PhotoEditViewControllerOptions.undoStepByStep`).

### Changed

* `M_PI` has been replaced by `.pi`, `FLT_EPSILON` has been replaced by `.ulpOfOne`
* Adding a new sticker from within the `StickerOptionsToolController` now opens the already instantiated `StickerToolController` that was passed to `PhotoEditViewController` instead of creating a new instance.
* The blur radius specified in the `FocusToolController` is now relative to the smaller side of the image instead of an absolute value, which means that the final output image looks like the preview image.

### Fixed

* Fixed a crash that occurred when setting `CameraViewControllerOptions.showFilters` to `false`.

## 6.1.4

### Fixed

* Fixed a crash in `CameraViewController`.
* The `photoActionButtonConfigurationClosure` closure was not called initially.
* Changing the `tintColor` of the button to take a photo works now.

## 6.1.3

### Added

* Added default intensities for blend modes.

### Changed

* Changed some `enum`s to lower case to match Swift 3.0 naming conventions.

### Fixed

* Fixed a memory leak in `CameraViewController`.
* Fixed a memory leak in `FrameToolController`.
* Fixed a scaling issue for backdrop images.
* Fixed the Podspec so that the resource bundle is not added twice to projects that use CocoaPods to integrate the SDK.

## 6.1.2

### Added

* A new API to integrate the SDK into your analytics. See `AnalyticsClient` and `PESDK.shared.analytics` for more details.
* Added an option to set a backdrop image (`backdropImage`), a blend mode (`backdropBlendMode`) and an intensity (`backdropIntensity`) for it to `PhotoEditModel`.

## 6.1.1

### Fixed

* Fixed a bug regarding image orientation that occurred when saving an unedited image. The image that was passed to `PhotoEditViewController` is now passed back to the delegate untouched when saving and image without any modifications.

## 6.1.0

### Added

* Dynamic frames, which are generated during runtime and adjust to the image based on a given set of rules, similar to 9-patch images. See `CustomPatchFrameBuilder` for more information.

### Changed

* Frames participate in the bring-to-front behavior so that stickers, text and brush can be moved behind or in front of frames.
* Licensing has been improved to support multiple bundle identifiers within one license.

## 6.0.1

### Added

* Licensing

## 6.0

### Added

* Stickers can be grouped into individual categories and their color can be changed by the user.
* New initializers for `PhotoEditViewController`: `init(data: Data)`, `init(data: Data, configuration: Configuration)` and `init(data: Data, menuItems: [MenuItem], configuration: Configuration)` which allow passing an image as data in which case EXIF information can be preserved.
* `PhotoEditModel` is a Swift `struct` now. When using Objective-C you can use `IMGLYBoxedPhotoEditModel` instead where needed.

### Changed

* The crop UI has been completely revised and supports arbitrary rotations now.
* Updated the UI of the focus tool so that the user can change the width of the focus gradient.
* Updated the overall look and feel of the UI.
* Custom fonts can be added to the SDK.
* Many performance improvements.
* Asset datasources support remote sources out of the box now.
