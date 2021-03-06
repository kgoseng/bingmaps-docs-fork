
# MapPolyline class

Displays a line on a map.

**Android**

>```java
> class MapPolyline extends MapElement
>```

**iOS**

>```objectivec
> @interface MSMapPolyline : MSMapPathElement
>```

_See also:_ [MSMapPathElement](iOS/MSMapPathElement-class.md)

## Properties

### Path

The path making up this line.

**Android**

>```java
> Geopath getPath()
> void setPath(Geopath path)
>```

**iOS**

Inherited from [MSMapPathElement](iOS/MSMapPathElement-class.md)

>```objectivec
> @property (nonatomic) MSGeopath *path  
>```

### StrokeColor

The color to use to draw the border of the polygon.

**Android**

>```java
> int getStrokeColor()  
> void setStrokeColor(int strokeColor)
>```

**iOS**

>```objectivec
> @property (nonatomic) UIColor *strokeColor
>```  

### StrokeDashed

Indicates whether the line is dashed.

**Android**

>```java
> boolean getStrokeDashed()  
> void setStrokeDashed(boolean isDashed)
>```

**iOS**

>```objectivec
> @property BOOL strokeDashed
>```  

### StrokeWidth

The width of the line to use for the outside of the polygon.

**Android**

>```java
> float getStrokeWidth()  
> void setStrokeWidth(float strokeWidth)
>```

**iOS**

>```objectivec
> @property int strokeWidth
>```  

## See Also

[Drawing with Polylines and Polygons](../map-control-concepts/map-polylines-and-polygons.md)
