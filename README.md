# Flutter Nav Bars 
How to use?
Add `SlidingClippedNavBar()` to `bottomNavigationBar` property of `Scaffold()` and add `PageView()` to body with `NeverScrollableScrollPhysics()` don't try to upate the seleted index from `onPageChanged` or will see some weird behaviour. You can use `Stack()` or `AnimatedSwitcher()` for custom page transition animation.

<details><summary><strong><h3>Sliding Clipped Nav Bar</h3></strong></summary>
<p>

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
</p>
</details>
