# Auto Shape Detection Canvas

A simple Flutter app that lets you **draw with your finger or mouse** and tries to **recognize basic shapes** like lines and circles automatically.

---

## What this app does

This app works like a drawing canvas:

1. You press and drag on the screen to draw.
2. The app records the path of your drawing.
3. When you lift your finger/mouse, it tries to figure out what shape you drew.
4. If it recognizes a shape, it redraws it as a clean geometric shape.

In simple words:  
**you sketch something roughly, and the app converts it into a neat shape.**

---

## What kind of shapes it recognizes

From the code currently visible, the app can detect:

- **Line**
- **Circle**

The README file also mentions more shapes like:

- Triangle
- Rectangle / Square
- Pentagon
- Hexagon

But in the visible Dart code, only **line and circle detection are clearly present**.

---

## How the app works

### 1. Drawing input
The app listens to touch or mouse drag actions using Flutter’s gesture system.

When you drag:

- every point of the stroke is stored
- the screen shows the line you are currently drawing

### 2. Shape detection
When you stop drawing, the app checks the recorded points and tries to classify them.

The detection logic is in a class called `ShapeDetector`.

It tries shapes in this order:

1. **Polygon**
2. **Circle**
3. **Line**

If it finds a match, that shape is saved and drawn permanently on the canvas.

### 3. Redrawing shapes
The screen uses a custom painter to redraw:

- the shapes already recognized
- the current unfinished stroke

---

## Main parts of the code

### `main()`
Starts the app and shows the drawing screen.

### `ShapeCanvas`
This is the main screen.

It:

- stores the points being drawn
- stores recognized shapes
- handles drag updates
- handles end of drawing
- calls the shape detector

### `ShapePainter`
This class draws everything on the canvas.

It draws:

- completed recognized shapes
- the current freehand stroke

### `Shape`
This is an abstract base class for drawable shapes.

### `CircleShape`
Represents a circle with:

- a center point
- a radius

### `LineShape`
Represents a line with:

- a start point
- an end point

### `ShapeDetector`
This is the “brain” of the app.

It looks at the drawn points and decides what shape they represent.

---

## Shape detection logic in plain English

### Line detection
The app checks whether:

- the first and last points are far enough apart
- all points stay close to the same straight path

If yes, it treats the stroke as a line.

### Circle detection
The app finds the center of the stroke and checks whether the points are roughly the same distance from that center.

If yes, it treats the stroke as a circle.

### Polygon detection
The README mentions polygon detection, but the visible code is incomplete in the snippet, so I could not verify the full polygon logic from the data returned.

---

## File overview

### `lib/main.dart`
The most important file.

Contains:

- the app entry point
- drawing screen
- shape painter
- shape classes
- shape detection logic

### `pubspec.yaml`
Flutter project configuration.

It shows:

- Flutter SDK requirement
- package name currently set to `untitled`
- basic Flutter dependencies

### `ios/` and `android/`
Standard Flutter platform folders so the app can run on iPhone/iPad and Android.

These mostly contain platform setup code, not app logic.

---

## User experience

When using the app:

1. Open the app.
2. Draw a rough shape on the canvas.
3. Lift your finger or mouse.
4. The app checks the drawing.
5. If it recognizes the shape, it replaces the sketch with a cleaner version.

---

## Best way to draw for better recognition

The code and README suggest these tips:

- Draw in **one continuous stroke**
- Try to make the shape closed if it is a circle or polygon
- Don’t make the sketch too messy
- Pause a little when making corners

---

## What this project is good for

This project is useful as:

- a learning project for Flutter drawing
- a basic example of gesture handling
- a simple geometric shape detection demo
- a starting point for more advanced sketch recognition

---

## Limitations

From the visible code:

- the detection is fairly simple
- it may not recognize messy drawings well
- only some shapes are clearly implemented in the code snippet
- the `pubspec.yaml` still has the default app name `untitled`
- the README looks more advanced than the currently visible implementation

---

## How to run it

From the README:

```bash
flutter pub get
flutter run
