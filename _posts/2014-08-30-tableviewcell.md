---
layout: post

title: "UITableViewCell responsibility"
cover_image: scale-preface.jpg

excerpt: "If I see configureCell method in a UIViewController again Im going to scream."

author:
  name: John Hatvani
  twitter: jhatvani
---


If I see configureCell method in a UIViewController again Im going to scream.


###Rant
Too many times have I seen UITableViewCell configured in ViewControllers; heights calculated for various custom cells done in heightForRowAtIndexPath: Cell layout and population done in cellForRowAtIndexPath:

**This is wrong**

Get into the habit early and put in the time to separate these layers. Make the cell responsible for itself, for its own layout and height. This can be achieved with a single interface (protocol for us) which defines this common interaction.

<img src="http://yuml.me/09617949" />

```
@protocol ConfigurableCell

+ (CGFloat) heightForCellWithObject:(id<NSObject>) obj;
- (void) configureCellWithObject:(id<NSObject>) obj;

@end
```
concrete implementation
```
@interface ConcreteCustomTableViewCell : UITableViewCell
<ConfigurableCell>

@end
```

```
@implementation ConcreteCustomTableViewCell

+ (CGFloat) heightForCellWithObject:(myConcreteObject *)obj {
    ...
    return x;
}

- (void) configureCellWithObject:(myConcreteObject *) obj {
    ...
}

@end
```

**Thats it.**

You have separated your ViewController from your Cells and made life easier for future-you or whoever is evolving the code.
