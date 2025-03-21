Sources : https://docs.flutter.dev/ui/layout/constraints , https://www.youtube.com/watch?v=jckqXR5CrPI , https://github.com/marcglasberg/flutter_layout_article

**Understanding constraints**
Flutter layout can't really be understood without knowing this rule, so Flutter developers should learn it early on.

**Limitations**
Flutter's layout engine is designed to be a one-pass process. This means that Flutter lays out its widgets very efficiently, but does result in a few limitations:

* A widget can decide its own size only within the constraints given to it by its parent. This means a widget usually can't have any size it wants.
* A widget can't know and doesn't decide its own position in the screen, since it's the widget's parent who decides the position of the widget.
* Since the parent's size and position, in its turn, also depends on its own parent, it's impossible to precisely define the size and position of any widget without taking into consideration the tree as a whole.
* If a child wants a different size from its parent and the parent doesn't have enough information to align it, then the child's size might be ignored. Be specific when defining alignment.

**Generally, there are three kinds of boxes, in terms of how they handle their constraints:**

* Those that try to be as big as possible. For example, the boxes used by Center and ListView.
* Those that try to be the same size as their children. For example, the boxes used by Transform and Opacity.
* Those that try to be a particular size. For example, the boxes used by Image and Text.

**Unbounded constraints**

The most common case where a render box ends up with an unbounded constraint is within a flex box (Row or Column), and within a scrollable region (such as ListView and other ScrollView subclasses).

**Flex**

* A flex box with a bounded constraint in its primary direction tries to be as big as possible.

* A flex box with an unbounded constraint in its primary direction tries to fit its children in that space. Each child's flex value must be set to zero, meaning that you can't use Expanded when the flex box is inside another flex box or a scrollable; otherwise it throws an exception.