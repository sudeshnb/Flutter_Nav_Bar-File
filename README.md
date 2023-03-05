# Flutter Nav Bars 
How to use?
Add `SlidingClippedNavBar()` to `bottomNavigationBar` property of `Scaffold()` and add `PageView()` to body with `NeverScrollableScrollPhysics()` don't try to upate the seleted index from `onPageChanged` or will see some weird behaviour. You can use `Stack()` or `AnimatedSwitcher()` for custom page transition animation.

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
### How do I change the height?
  - The height must be constant because the animation is in vertical direction. According to me 60 is perfect. But if you think needs to be reduced then please create an issue with a screenshot. I will see if I can do something.
### How do I add drop shadow?
  - Wrap `SlidingClippedNavBar` with `DecoratedBox` or `Container` and pass `BoxDecoration` to decoration property. BoxDecoration takes list of boxShadow there you can pass your drop shadow.
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
</details>

| Sliding Clipped Nav Bar|Sliding Clipped Nav Bar |Sliding Clipped Nav Bar |
|:---:|:---:|:---:|
|<img src='https://raw.githubusercontent.com/watery-desert/assets/main/sliding_clipped_nav_bar/demo_recording.gif' width='30'>|||
