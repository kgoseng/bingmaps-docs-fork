
# Events

The Bing Maps API provides events that allow your application to respond to user actions.

## Examples

### Map holding event

The following example show how to add a pushpin when user hold over a map.

**Swift**

> ``` swift
> mapView.addUserIsHoldingHandler{ (point:CGPoint) -> Bool in
>     var location:MSGeolocation!
>     if self.mapView.try(toConvertOffset: point, intoLocation: &location) {
>         let pushpin = MSMapIcon()
>         pushpin.location = location
>         self.pinLayer.elements.add(pushpin)
>
>         return true
>     }
>
>    return false
> }
>```

### Map tapped event

The following example shows how to change [MapIcon](../map-control-api/MapIcon-class.md) image and z index of containing layer when a pusphin is tapped.

**Swift**

At first, add extension for [MSMapElementCollection](../map-control-api/MapElementCollection-class.md) to conform to the Sequence Protocol in order to use for-in loop. 

> ```swift
> // This will allow for-in works on MSMapElementCollection.elements
> extension MSMapElementCollection: Sequence {
>     public func makeIterator() -> NSFastEnumerationIterator {
>         return NSFastEnumerationIterator(self)
>     }
> }
> ```

Second, add the following methods and variables to UIViewController

> ```swift
> // Create two layers in ViewController
> private var buildingsLayer: MSMapElementLayer!
> private var cityParksLayer: MSMapElementLayer!
> 
> // Create and add pushpin to building locations in  building layer
> func createCityBuildingsCollection() {
>     buildingsLayer = MSMapElementLayer()
>     let pushpin = MSMapIcon()
>     pushpin.location = MSGeolocation(latitude: 47.603830, longitude: -122.329900)
>     pushpin.title = "Seattle City Hall"
>     buildingsLayer.elements.add(pushpin)
>     let pushpin2 = MSMapIcon()
>     pushpin2.location = MSGeolocation(latitude: 47.606709, longitude:  -122.332672)
>     pushpin2.title = "Seattle Public Library"
>     buildingsLayer.elements.add(pushpin2)
>     let pushpin3 = MSMapIcon()
>     pushpin3.location = MSGeolocation(latitude: 47.604100, longitude:  -122.329204)
>     pushpin3.title = "Municipal Court of Seattle"
>     buildingsLayer.elements.add(pushpin3)
> }
> 
> // Create and add pusphin to city park locaiton in city parks layer
> func createCityParksCollection() {
>     cityParksLayer = MSMapElementLayer()
>     let pushpin = MSMapIcon()
>     pushpin.location = MSGeolocation(latitude: 47.608313, longitude: -122.331218)
>     pushpin.title = "Freeway Park"
>     cityParksLayer.elements.add(pushpin)
>     let pushpin2 = MSMapIcon()
>     pushpin2.location = MSGeolocation(latitude: 47.602029, longitude:  -122.333971)
>     pushpin2.title = "Pioneer Square"
>     cityParksLayer.elements.add(pushpin2)
>     let pushpin3 = MSMapIcon()
>     pushpin3.location = MSGeolocation(latitude: 47.601990, longitude:  -122.330681)
>     pushpin3.title = "City Hall Park"
>     cityParksLayer.elements.add(pushpin3)
>     let pushpin4 = MSMapIcon()
>     pushpin4.location = MSGeolocation(latitude: 47.600619, longitude:  -122.324957)
>     pushpin4.title = "Kobe Terrace Park"
>     cityParksLayer.elements.add(pushpin4)
> }
> 
> // Change z index of layer and icon images 
> func selectLayer(selectedLayer: MSMapElementLayer) {
>     var deselectedLayer: MSMapElementLayer
>     if selectedLayer == buildingsLayer {
>         deselectedLayer = cityParksLayer
>     }
>     else {
>         deselectedLayer = buildingsLayer
>     }
>
>     deselectedLayer.zIndex = 0
>     for element in deselectedLayer.elements {
>         let mapIcon = element as! MSMapIcon
>         mapIcon.image = MSMapImage(uiImage:UIImage(named: "selectedMappin")!)
>     }
>
>     selectedLayer.zIndex = 0
>     for element in selectedLayer.elements {
>         let mapIcon = element as! MSMapIcon
>         mapIcon.image = MSMapImage(uiImage:UIImage(named: "defaultMappin")!)
>     }
> }
>```


Finally add the buildings/parks layer to map and impelment handler for user tapped interaction. 

> ``` swift
> override func viewDidLoad() {
>
>     createCityBuildingsCollection();
>     createCityParksCollection();
>     mapView.layers.add(buildingsLayer)
>     mapView.layers.add(cityParksLayer)
>     mapView.addUserDidTapHandler { (point:CGPoint) -> Bool in
>         let tappedElements = self.mapView.findMapElements(atOffset: point)
>         if tappedElements.isEmpty {
>             return false
>         }
>
>         let mapIcon = tappedElements.first as? MSMapIcon
>         if mapIcon == nil {
>             return false
>         }
>
>         if self.buildingsLayer.elements.contains(where: tappedElements[0]) {
>             self.selectLayer(selectedLayer: self.buildingsLayer)
>         }
>         else{
>             self.selectLayer(selectedLayer: self.cityParksLayer)
>         }
>         return true
>     }
> }
>```
