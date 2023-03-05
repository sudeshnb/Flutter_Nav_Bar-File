# Flutter Bottom Navigation Bar
How to use?

Add `SlidingClippedNavBar()` or `WaterDropNavBar()` to `bottomNavigationBar` property of `Scaffold()` and add `PageView()` to body with `NeverScrollableScrollPhysics()` don't try to upate the seleted index from `onPageChanged` or will see some weird behaviour. You can use `Stack()` or `AnimatedSwitcher()` for custom page transition animation.

<details><summary><strong><h3>Sliding Clipped Nav Bar</h3></strong></summary>


Do and don't
+ Don't make icon size too big.
  - FontAwesomeIcons: 24
  - MaterialIcons: 30
+ Using `SlidingClippedNavBar()` when you want global active and inactive color.

```dart
 return Scaffold(
     
      body: PageView(
      physics: NeverScrollableScrollPhysics(),       
      controller: controller,
...
      ),
      bottomNavigationBar: SlidingClippedNavBar(
        backgroundColor: Colors.white,
        onButtonPressed: (index) {
          setState(() {
            selectedIndex = index;
          });
          controller.animateToPage(selectedIndex,
              duration: const Duration(milliseconds: 400),
              curve: Curves.easeOutQuad);
        },
        iconSize: 30,
        activeColor: Color(0xFF01579B),
        selectedIndex: selectedIndex,
        barItems: [
          BarItem(
            icon: Icons.event,
            title: 'Events',
          ),
          BarItem(
            icon: Icons.search_rounded,
            title: 'Search',
          ),
           /// Add more BarItem if you want
        ],
      ),
    );
```
Using `SlidingClippedNavBar.colorful()` when you want to set individual item active & inactive color.
```dart
return Scaffold(
    
     body: PageView(
     physics: NeverScrollableScrollPhysics(),
     controller: controller,
...
     ),
     bottomNavigationBar: SlidingClippedNavBar.colorful(
       backgroundColor: Colors.white,
       onButtonPressed: (index) {
         setState(() {
           selectedIndex = index;
         });
         controller.animateToPage(selectedIndex,
             duration: const Duration(milliseconds: 400),
             curve: Curves.easeOutQuad);
       },
       iconSize: 30,
       selectedIndex: selectedIndex,
       barItems: [
         BarItem(
           icon: Icons.event,
           title: 'Events',
           activeColor: Colors.amber,
           inactiveColor: Colors.red,
         ),
         BarItem(
           icon: Icons.search_rounded,
           title: 'Search',
           activeColor: Colors.red,
           inactiveColor: Colors.green,
         ),
        /// Add more BarItem if you want

       ],
     ),
   );
```

</details>
<details><summary><strong><h3>Water Drop Nav Bar</h3></strong></summary>

#### Do and don't
+ Don't make icon size too big.
  - FontAwesomeIcons: 24
  - MaterialIcons: 30
+ Use complementary filled and outlined icons for best result.
+ `backgroundColor` and `waterDropColor` of `WaterDropNavBar()` and `Scaffold()`'s backgroundColor (or whatever widget you are using) must be different (see the example app) This will visualize that the water drop is hanging from the top.
Short example
```dart
 return Scaffold(
     
      body: PageView(
      physics: NeverScrollableScrollPhysics(),       
      controller: pageController,
       ...
      ),
      bottomNavigationBar: WaterDropNavBar(
        backgroundColor: Colors.white,
        onItemSelected: (index) {
          setState(() {
            selectedIndex = index;
          });
          pageController.animateToPage(selectedIndex,
              duration: const Duration(milliseconds: 400),
              curve: Curves.easeOutQuad);
        },
        selectedIndex: selectedIndex,
        barItems: [
          BarItem(
            filledIcon: Icons.bookmark_rounded,
            outlinedIcon: Icons.bookmark_border_rounded,
          ),
          BarItem(
              filledIcon: Icons.favorite_rounded,
              outlinedIcon: Icons.favorite_border_rounded),
        ],
      ),
    );
```
### ❗️ Issues ❗️
+ Android
Some android phones might have black navigation bar, this looks ugly. It's recommended to wrap Scaffold with `AnnotatedRegion<SystemUiOverlayStyle>` to change that black navigation bar color to `WaterDropNavBar` backgroundColor. Check the example app. Like this 👇
```dart
return AnnotatedRegion<SystemUiOverlayStyle>(
     value: const SystemUiOverlayStyle(
       //this color must be equal to the WaterDropNavBar backgroundColor
       systemNavigationBarColor: Colors.white, 
       systemNavigationBarIconBrightness: Brightness.dark,
     ),
     child: Scaffold(
       body: // code here
     )
);
```
You can additionally provide some bottomPadding to add padding at the bottom of the bar, I think 8 is enough.
+ iOS
iPhones without swipe home gesture might have such issue where icons are pushed to the bottom. Provide some bottomPadding. I added 8 padding here.
Now you might ask how do you know which phone is using swipe home gesture?

Well, you can check bottom padding (using MediaQuery.of(context).padding.bottom) and if it's less than 34 or something then provide some bottom padding. Definitely try running different simulators and see.

</details>

### How do I change the height?
  - The height must be constant because the animation is in vertical direction. According to me 60 is perfect. But if you think needs to be reduced then please create an issue with a screenshot. I will see if I can do something.
### How do I add drop shadow?
  - Wrap `SlidingClippedNavBar` or `WaterDropNavBar()` with `DecoratedBox` or `Container` and pass `BoxDecoration` to decoration property. BoxDecoration takes list of boxShadow there you can pass your drop shadow.
```dart
DecoratedBox(
    decoration: BoxDecoration(
      boxShadow: [
        BoxShadow(
            color: Colors.black.withOpacity(0.2),
            offset: Offset(0, 4),
            blurRadius: 8.0)
      ],
    ),
    child: SlidingClippedNavBar()
)
```
### How do I change the corner radius of the navigation bar?
  - Wrap `SlidingClippedNavBar` with `ClipRRect` and pass `BorderRadius` to borderRadius property.
```dart
  ClipRRect(
      borderRadius: const BorderRadius.vertical(
        top: Radius.circular(16),
      ),
      child: SlidingClippedNavBar(
    )                
```


| Sliding Clipped Nav Bar|  Water Drop Nav Bar |Sliding Clipped Nav Bar |
|:---:|:---:|:---:|
|<img src='https://user-images.githubusercontent.com/33403844/222962426-86343a13-1624-4690-855d-418424186a11.gif' >  | <img src='https://user-images.githubusercontent.com/33403844/222962526-67e2a0e4-60be-4a10-9ed0-4b6fe4cd2804.gif' >  ||


