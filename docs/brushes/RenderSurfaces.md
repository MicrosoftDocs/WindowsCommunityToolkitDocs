---
title: Render Surfaces
author: ratishphilip
description: Detailed description about creating custom shaped visuals using various render surfaces.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, Win2D, composition
---

# Render Surfaces

Windows Community Toolkit provides five types of rendering surface interfaces which can be used for rendering custom shapes and images or creating masks from geometric shapes or images.

- _`IRenderSurface`_ - This interface acts as the base interface for interfaces which render to the `ICompositionSurface`. It mainly contains references to an `ICompositionGenerator` object and an `ICompositionSurface` object which are the core objects required for rendering any geometry or image onto a `ICompositionSurface`.
- _`IGeometrySurface`_ - This interface is used for rendering custom shaped geometries onto `ICompositionSurface`.
- _`IGeometryMaskSurface`_ - This interface is used for rendering custom shaped geometries onto `ICompositionSurface` so that they can be useds as masks on Composition Visuals.
- _`IGaussianMaskSurface`_ - This interface derives from `IMaskSurface` and is used for rendering custom shaped geometries onto `ICompositionSurface` so that they can be useds as masks on Composition Visuals. You can apply a Gaussian Blur to the mask.
- _`IImageSurface`_ - This interface is used for rendering images onto `ICompositionSurface`.
- _`IImageMaskSurface`_ - This interface is used for creating a mask using the alpha values of the image pixels.

Here is the interface hierarchy

![Image Mask Surface brush](../resources/images/Surface/RenderSurfacesHierarchy.png 'Image Mask Surface Brush')

Most of the APIs to create custom shaped surfaces are provided by the `CompositionGenerator` class.

## Creating a custom shaped Visual

### Using IGeometrySurface

![Geometry Surface](../resources/images/Surface/GeometrySurface.jpg 'Rendering using Geometry Surface')

```cs
var compositor = Window.Current.Compositor;

// Get the Composition Generator
var generator = CompositionGenerator.Instance;

// Create the visual
var visual = compositor.CreateSpriteVisual();
visual.Size = new Vector2(400, 400);
visual.Offset = new Vector3(50, 50, 0);

// Create the combined geometry
var ellipse1 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 150, 75);
var ellipse2 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 75, 150);
var combinedGeometry = ellipse1.CombineWith(ellipse2, Matrix3x2.Identity, CanvasGeometryCombine.Union);

// Create the Geometry Surface filled with red color
var geometrySurface = generator.CreateGeometrySurface(visual.Size.ToSize(), combinedGeometry, Colors.Red);

// Create the brush from the geometry surface
var brush = compositor.CreateSurfaceBrush(geometrySurface);

// Apply the brush to the visual
visual.Brush = brush;

ElementCompositionPreview.SetElementChildVisual(RenderGrid, visual);
```

### Using Animated Geometry Surface

![Animated Geometry Surface](../resources/images/Surface/AnimatedGeometrySurface.gif 'Rendering using Animated Geometry Surface')

Event though the visuals can be animated using CompositionAnimation, to animate the geometry, we need to manually calculate the intermediate values and update them periodically. Calling the Redraw method of the IGeometrySurface instance will cause the brush to be refreshed. Therefore you need to create the brush only once. In order to get a smooth animation, here Win2d's CanvasAnimatedControl is used, whose Draw event is fired at 60 fps.

```cs
private CanvasGeometry _geometry;
private IGeometrySurface _animatedGeometrySurface;
private float _angle = 0;

private void CreateAnimatedGeometrySurface()
{
    var compositor = Window.Current.Compositor;

    // Get the Composition Generator
    var generator = CompositionGenerator.Instance;

    // Create the visual
    var visual = compositor.CreateSpriteVisual();
    visual.Size = new Vector2(400, 400);
    visual.Offset = new Vector3(50, 50, 0);

    // Create the combined geometry
    var ellipse1 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 150, 75);
    var ellipse2 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 75, 150);
    _geometry = ellipse1.CombineWith(ellipse2, Matrix3x2.Identity, CanvasGeometryCombine.Union);

    // Create the Geometry Surface filled with red color
    _animatedGeometrySurface = generator.CreateGeometrySurface(visual.Size.ToSize(), _geometry, Colors.Red);

    // Create the brush from the geometry surface
    var brush = compositor.CreateSurfaceBrush(_animatedGeometrySurface);

    // Apply the brush to the visual
    visual.Brush = brush;

    ElementCompositionPreview.SetElementChildVisual(AnimatedCanvas, visual);
}

/// <summary>
/// Handler for the Draw event of CanvasAnimatedControl.
/// </summary>
/// <param name="sender">CanvasAnimatedControl.</param>
/// <param name="args">CanvasAnimatedDrawEventArgs.</param>
private void OnDraw(ICanvasAnimatedControl sender, CanvasAnimatedDrawEventArgs args)
{
    _angle = (_angle + 0.5f) % 360f;
    var angleInRadians = _angle * (float)Math.PI / 180f;
    var transform = Matrix3x2.CreateRotation(angleInRadians, new Vector2(200, 200));
    var geometry = _geometry?.Transform(transform);
    _animatedGeometrySurface?.Redraw(geometry);
}
```

### Using IGeometryMaskSurface

![Geometry Mask Surface](../resources/images/Surface/GeometryMaskSurface.jpg 'Rendering using Geometry Mask Surface')

This example consists of a ContainerVisual which has two SpriteVisuals as children. The SpriteVisual in the background is filled with blue color. The brush applied to the foreground SpriteVisual is created using an IGeometryMaskSurface.

```cs
var compositor = Window.Current.Compositor;

// Get the Composition Generator
var generator = CompositionGenerator.Instance;

// Create the container visual to hold all visuals
var container = compositor.CreateContainerVisual();
container.Size = new Vector2(400, 400);
container.Offset = new Vector3(50, 50, 0);

// Create the background visual
var bgVisual = compositor.CreateSpriteVisual();
bgVisual.Size = new Vector2(200, 200);
bgVisual.Offset = new Vector3(100, 100, 0);
bgVisual.Brush = compositor.CreateColorBrush(Colors.Blue);

// Create the foreground visual
var visual = compositor.CreateSpriteVisual();
visual.Size = new Vector2(400, 400);

// Create the combined geometry
var ellipse1 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 150, 75);
var ellipse2 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 75, 150);
var combinedGeometry = ellipse1.CombineWith(ellipse2, Matrix3x2.Identity, CanvasGeometryCombine.Union);
var rectGeometry = CanvasGeometry.CreateRectangle(generator.Device, new Rect(0, 0, 400, 400));
var finalGeometry = rectGeometry.CombineWith(combinedGeometry, Matrix3x2.Identity, CanvasGeometryCombine.Exclude);

// Create the MaskSurface
var maskSurface = generator.CreateGeometryMaskSurface(visual.Size.ToSize(), finalGeometry);

// Create SurfaceBrush from MaskSurface
var mask = compositor.CreateSurfaceBrush(maskSurface);
var source = compositor.CreateColorBrush(Colors.Red);

// Create mask brush
var maskBrush = compositor.CreateMaskBrush();
maskBrush.Mask = mask;
maskBrush.Source = source;

// Apply the brush to the visual
visual.Brush = maskBrush;

// Add the visuals to the container
container.Children.InsertAtBottom(bgVisual);
container.Children.InsertAtTop(visual);

ElementCompositionPreview.SetElementChildVisual(RenderGrid, container);
```

### Using Animated Geometry Mask Surface

![Animated Geometry Mask Surface](../resources/images/Surface/AnimatedGeometryMaskSurface.gif 'Rendering using Animated Geometry Mask Surface')

Similar to the animated Geometry Surface example above, here also a CanvasAnimatedControl's Draw event is used to update the IGeometryMaskSurface to refresh the brush.

```cs
private CanvasGeometry _geometry;
private CanvasGeometry _rectGeometry;
private IGeometryMaskSurface _animatedGeometryMaskSurface;
private float _angle = 0;

private void CreateAnimatedGeometryMaskSurface()
{
    var compositor = Window.Current.Compositor;

    // Get the Composition Generator
    var generator = CompositionGenerator.Instance;

    // Create the container visual to hold all visuals
    var container = compositor.CreateContainerVisual();
    container.Size = new Vector2(400, 400);
    container.Offset = new Vector3(50, 50, 0);

    // Create the background visual
    var bgVisual = compositor.CreateSpriteVisual();
    bgVisual.Size = new Vector2(200, 200);
    bgVisual.Offset = new Vector3(100, 100, 0);
    bgVisual.Brush = compositor.CreateColorBrush(Colors.Blue);

    // Create the foreground visual
    var visual = compositor.CreateSpriteVisual();
    visual.Size = new Vector2(400, 400);

    // Create the combined geometry
    var ellipse1 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 150, 75);
    var ellipse2 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 75, 150);
    _geometry = ellipse1.CombineWith(ellipse2, Matrix3x2.Identity, CanvasGeometryCombine.Union);
    _rectGeometry = CanvasGeometry.CreateRectangle(generator.Device, new Rect(0, 0, 400, 400));
    var finalGeometry = _rectGeometry.CombineWith(_geometry, Matrix3x2.Identity, CanvasGeometryCombine.Exclude);

    // Create the MaskSurface
    _animatedGeometryMaskSurface = generator.CreateGeometryMaskSurface(visual.Size.ToSize(), finalGeometry);

    // Create SurfaceBrush from MaskSurface
    var mask = compositor.CreateSurfaceBrush(_animatedGeometryMaskSurface);
    var source = compositor.CreateColorBrush(Colors.Red);

    // Create mask brush
    var maskBrush = compositor.CreateMaskBrush();
    maskBrush.Mask = mask;
    maskBrush.Source = source;

    // Apply the brush to the visual
    visual.Brush = maskBrush;

    // Add the visuals to the container
    container.Children.InsertAtBottom(bgVisual);
    container.Children.InsertAtTop(visual);

    ElementCompositionPreview.SetElementChildVisual(AnimatedCanvas, container);
}

/// <summary>
/// Handler for the Draw event of CanvasAnimatedControl.
/// </summary>
/// <param name="sender">CanvasAnimatedControl.</param>
/// <param name="args">CanvasAnimatedDrawEventArgs.</param>
private void OnDraw(ICanvasAnimatedControl sender, CanvasAnimatedDrawEventArgs args)
{
    _angle = (_angle + 0.5f) % 360f;
    var angleInRadians = _angle * (float)Math.PI / 180f;
    var transform = Matrix3x2.CreateRotation(angleInRadians, new Vector2(200, 200));
    var geometry = _geometry?.Transform(transform);
    _animatedGeometryMaskSurface?.Redraw(_rectGeometry.CombineWith(_geometry, transform, CanvasGeometryCombine.Exclude));
}
```

### Masked Backdrop Brush

To create a masked backdrop brush, you can use either of the following Compositor extension methods

```cs
public static CompositionEffectBrush CreateMaskedBackdropBrush(this Compositor compositor, IGeometryMaskSurface mask, Color blendColor, float blurAmount, CompositionBackdropBrush backdropBrush = null);
public static CompositionEffectBrush CreateGaussianMaskedBackdropBrush(this Compositor compositor, IGaussianMaskSurface mask, Color blendColor, float blurRadius, CompositionBackdropBrush backdropBrush = null);
```

![Masked Backdrop Brush](../resources/images/Surface/MaskedBackdropBrush.jpg 'Masked Backdrop Brush')

The above example can be created using the following code

```cs
var compositor = Window.Current.Compositor;

// Get the Composition Generator
var generator = CompositionGenerator.Instance;

// Create the container visual to hold all visuals
var container = compositor.CreateContainerVisual();
container.Size = new Vector2(400, 400);
container.Offset = new Vector3(50, 50, 0);

// Create the background visual
var bgVisual = compositor.CreateSpriteVisual();
bgVisual.Size = new Vector2(200, 200);
bgVisual.Offset = new Vector3(100, 100, 0);
bgVisual.Brush = compositor.CreateColorBrush(Colors.Red);

// Create the foreground visual
var visual = compositor.CreateSpriteVisual();
visual.Size = new Vector2(400, 400);

// Create the combined geometry
var ellipse1 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 150, 75);
var ellipse2 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 75, 150);
var combinedGeometry = ellipse1.CombineWith(ellipse2, Matrix3x2.Identity, CanvasGeometryCombine.Union);
var rectGeometry = CanvasGeometry.CreateRoundedRectangle(generator.Device, new Rect(0, 0, 400, 400), 20, 20);
var finalGeometry = rectGeometry.CombineWith(combinedGeometry, Matrix3x2.Identity, CanvasGeometryCombine.Exclude);

// Create the MaskedBackdropSurfaceBrush
var maskSurface = generator.CreateGeometryMaskSurface(visual.Size.ToSize(), finalGeometry);
var maskedBackdropSurfaceBrush = compositor.CreateMaskedBackdropBrush(maskSurface, Colors.AntiqueWhite, 20, compositor.CreateBackdropBrush());

// Apply the brush to the visual
visual.Brush = maskedBackdropSurfaceBrush;

// Add the visuals to the container
container.Children.InsertAtBottom(bgVisual);
container.Children.InsertAtTop(visual);

ElementCompositionPreview.SetElementChildVisual(RenderGrid, container);
```

### Animated Masked Backdrop Brush

Just like the animated GeometrySurface and animated GeometryMaskSurface, the MaskedBackdropBrush can also be animated.

![Animated Masked Backdrop Brush](../resources/images/Surface/AnimatedMaskedBackdropBrush.gif 'Animated Masked Backdrop Brush')

```cs
private CanvasGeometry _geometry;
private CanvasGeometry _rectGeometry;
private IGeometryMaskSurface _animatedGeometryMaskSurface;
private float _angle = 0;

private void CreateAnimatedMaskedBackdropSurface()
{
    var compositor = Window.Current.Compositor;

    // Get the Composition Generator
    var generator = CompositionGenerator.Instance;

    // Create the container visual to hold all visuals
    var container = compositor.CreateContainerVisual();
    container.Size = new Vector2(400, 400);
    container.Offset = new Vector3(50, 50, 0);

    // Create the background visual
    var bgVisual = compositor.CreateSpriteVisual();
    bgVisual.Size = new Vector2(200, 200);
    bgVisual.Offset = new Vector3(100, 100, 0);
    bgVisual.Brush = compositor.CreateColorBrush(Colors.Blue);

    // Create the foreground visual
    var visual = compositor.CreateSpriteVisual();
    visual.Size = new Vector2(400, 400);

    // Create the combined geometry
    var ellipse1 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 150, 75);
    var ellipse2 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 75, 150);
    _geometry = ellipse1.CombineWith(ellipse2, Matrix3x2.Identity, CanvasGeometryCombine.Union);
    _rectGeometry = CanvasGeometry.CreateRectangle(generator.Device, new Rect(0, 0, 400, 400));
    var finalGeometry = _rectGeometry.CombineWith(_geometry, Matrix3x2.Identity, CanvasGeometryCombine.Exclude);

    // Create the MaskSurface
    _animatedGeometryMaskSurface = generator.CreateGeometryMaskSurface(visual.Size.ToSize(), finalGeometry);
    var maskedBackdropSurfaceBrush = compositor.CreateMaskedBackdropBrush(_animatedGeometryMaskSurface, Colors.AntiqueWhite, 20, compositor.CreateBackdropBrush());

    // Apply the brush to the visual
    visual.Brush = maskedBackdropSurfaceBrush;

    // Add the visuals to the container
    container.Children.InsertAtBottom(bgVisual);
    container.Children.InsertAtTop(visual);

    ElementCompositionPreview.SetElementChildVisual(AnimatedCanvas, container);
}

/// <summary>
/// Handler for the Draw event of CanvasAnimatedControl.
/// </summary>
/// <param name="sender">CanvasAnimatedControl.</param>
/// <param name="args">CanvasAnimatedDrawEventArgs.</param>
private void OnDraw(ICanvasAnimatedControl sender, CanvasAnimatedDrawEventArgs args)
{
    _angle = (_angle + 0.5f) % 360f;
    var angleInRadians = _angle * (float)Math.PI / 180f;
    var transform = Matrix3x2.CreateRotation(angleInRadians, new Vector2(200, 200));
    var geometry = _geometry?.Transform(transform);
    _animatedGeometryMaskSurface?.Redraw(_rectGeometry.CombineWith(_geometry, transform, CanvasGeometryCombine.Exclude));
}
```

### Using GaussianMaskSurface

![Gaussian Mask Surface Brush](../resources/images/Surface/GaussianMaskSurface.gif 'Gaussian Mask Surface Brush')

```cs
var compositor = Window.Current.Compositor;

// Get the Composition Generator
var generator = CompositionGenerator.Instance;

var size = new Vector2(400, 400);

// Create the image visual
var imageVisual = compositor.CreateSpriteVisual();
imageVisual.Size = size;
var imageSurface = await generator.CreateImageSurfaceAsync(new Uri("ms-appx:///Assets/Images/cat.png"), size.ToSize(), ImageSurfaceOptions.Default);
imageVisual.Brush = compositor.CreateSurfaceBrush(imageSurface);
ElementCompositionPreview.SetElementChildVisual(ImageGrid, imageVisual);

// Create the mask visual
var maskVisual = compositor.CreateSpriteVisual();
maskVisual.Size = size;

// Create the combined geometry
var ellipse1 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 150, 75);
var ellipse2 = CanvasGeometry.CreateEllipse(generator.Device, 200, 200, 75, 150);
var combinedGeometry = ellipse1.CombineWith(ellipse2, Matrix3x2.Identity, CanvasGeometryCombine.Union);

ElementCompositionPreview.SetElementChildVisual(MaskGrid, maskVisual);

// Create SurfaceBrush from MaskSurface
var outputVisual = compositor.CreateSpriteVisual();
outputVisual.Size = size;

var maskedBrush = compositor.CreateMaskBrush();
maskedBrush.Source = imageVisual.Brush;
var gaussianSurface = generator.CreateGaussianMaskSurface(size.ToSize(), combinedGeometry, Vector2.Zero, 0);
maskedBrush.Mask = compositor.CreateSurfaceBrush(gaussianSurface);

maskVisual.Brush = compositor.CreateSurfaceBrush(gaussianSurface);
outputVisual.Brush = maskedBrush;

ElementCompositionPreview.SetElementChildVisual(OutputGrid, outputVisual);
```

### Using ImageSurface

![Image Surface Brush](../resources/images/Surface/ImageSurface.jpg 'Image Surface Brush')

```cs
var compositor = Window.Current.Compositor;

// Get the Composition Generator
var generator = CompositionGenerator.Instance;

var size = new Vector2(400, 400);

// Create the image visual
var sourceImageVisual = compositor.CreateSpriteVisual();
sourceImageVisual.Size = size;
var sourceImageSurface = await generator.CreateImageSurfaceAsync(new Uri("ms-appx:///Assets/Images/cat.png"), size.ToSize(), ImageSurfaceOptions.Default);
sourceImageVisual.Brush = compositor.CreateSurfaceBrush(sourceImageSurface);
ElementCompositionPreview.SetElementChildVisual(ImageGrid, sourceImageVisual);
```

### Using ImageMaskSurface

![Image Mask Surface Brush](../resources/images/Surface/ImageMaskSurface.gif 'Image Mask Surface Brush')

```cs
var compositor = Window.Current.Compositor;

// Get the Composition Generator
var generator = CompositionGenerator.Instance;

var size = new Vector2(400, 400);

// Create the image visual
var sourceImageVisual = compositor.CreateSpriteVisual();
sourceImageVisual.Size = size;
var sourceImageSurface = await generator.CreateImageSurfaceAsync(new Uri("ms-appx:///Assets/Images/cat.png"), size.ToSize(), ImageSurfaceOptions.Default);
sourceImageVisual.Brush = compositor.CreateSurfaceBrush(sourceImageSurface);
ElementCompositionPreview.SetElementChildVisual(ImageGrid, sourceImageVisual);

// Create the mask visual
var maskVisual = compositor.CreateSpriteVisual();
maskVisual.Size = size;

// Create the image mask surface from source image surface
var imageMaskSurface = generator.CreateImageMaskSurface(sourceImageSurface, size.ToSize(), new Thickness(5), ImageSurfaceOptions.GetDefaultImageMaskOptionsForBlur(10));

ElementCompositionPreview.SetElementChildVisual(MaskGrid, maskVisual);

// Create SurfaceBrush from MaskSurface
var outputVisual = compositor.CreateSpriteVisual();
outputVisual.Size = size;

var maskedBrush = compositor.CreateMaskBrush();
maskedBrush.Source = sourceImageVisual.Brush;
maskedBrush.Mask = compositor.CreateSurfaceBrush(imageMaskSurface);

maskVisual.Brush = compositor.CreateSurfaceBrush(imageMaskSurface);
outputVisual.Brush = maskedBrush;

ElementCompositionPreview.SetElementChildVisual(OutputGrid, outputVisual);
```
