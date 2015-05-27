# Testing Environment: Beagleboard #

  * Beagleboard (TI OMAP353x) runs at 500 MHz
  * Display resolution: 1024x768

## CPU Tests ##

beagle-donut + armv5-interp
```
CPU: Dhrystones:        39918.0 stones/sec
CPU: Whetstones(10):    26874.0 KWIPS
CPU: Himeno:    3.3709999322891235 
CPU: Spectral Normalization:    1996.0 msec
```

beagle-donut + armv7-jit
```
CPU: Dhrystones:        60240.0 stones/sec
CPU: Whetstones(10):    46905.0 KWIPS
CPU: Himeno:    2.2440000772476196 
CPU: Spectral Normalization:    1404.0 msec
```

## 3D Tests ##

  * Engine: libagl (software)

original donut on beagleboard
```
3d: Colored Cube: 64 fps
3d: Lighting: 37 fps
3d: Textures: 13 fps
3d: Blending: 6 fps
3d: Fog: 11 fps
3d: Reflection: 13 fps
3d: Multitexture: 8 fps
3d: Teapot: 25 fps
3d: Gears: 16 fps
```

beagle-donut-0x3
```
3d: Colored Cube: 61 fps
3d: Lighting: 39 fps
3d: Textures: 15 fps
3d: Blending: 8 fps
3d: Fog: 13 fps
3d: Reflection: 14 fps
3d: Multitexture: 61 fps
3d: Teapot: 25 fps
3d: Gears: 18 fps
```

## 2D Tests ##

original donut on beagle (without Software Cursor)
```
2d: Arcs:       138 fps
2d: FillRate:   78 fps
2d: Circles:    139 fps
2d: Rectangles: 167 fps
2d: Alpha:      61 fps
```

beagle-donut + Software Cursor
```
2d: Arcs:       79 fps
2d: FillRate:   106 fps
2d: Circles:    103 fps
2d: Rectangles: 101 fps
2d: Alpha:      61 fps
```

beagle-donut-0x3 (+Software Cursor)
```
2d: Arcs:       94 fps
2d: FillRate:   111 fps
2d: Circles:    97 fps
2d: Rectangles: 117 fps
2d: Alpha:      61 fps
```

  * NOTE: continuous mouse surface tracking and update dramatically reduce the performance of simple 2D operations like Arcs, Circles, and Rectangles.  However, we need this feature to make Android environment usable.

# Testing Environment: Devkit8000 #

  * Devkit8000 (TI OMAP353x)
  * Display resolution: 272x480

## CPU Tests ##

beagle-donut + armv5-interp
```
CPU: Dhrystones:        39320.0 stones/sec
CPU: Whetstones(10):    28225.0 KWIPS
CPU: Himeno:    3.322999954223633
CPU: Spectral Normalization:    1896.0 msec
```

beagle-donut + armv7-jit
```
CPU: Dhrystones:        56398.0 stones/sec
CPU: Whetstones(10):    47741.0 KWIPS
CPU: Himeno:    2.1570000648498535
CPU: Spectral Normalization:    1257.0 msec
```

beagle-eclair + armv5-interp
```
CPU: Dhrystones:        38192.0 stones/sec
CPU: Whetstones(10):    28031.0 KWIPS
CPU: Himeno:    3.256999969482422 
CPU: Spectral Normalization:    1916.0 msec
```

beagle-eclair + armv7-jit
```
CPU: Dhrystones:        57487.0 stones/sec
CPU: Whetstones(10):    46663.0 KWIPS
CPU: Himeno:    2.384000062942505 
CPU: Spectral Normalization:    1232.0 msec
```

## 3D Tests ##

beagle-donut-0x3 (without Software Cursor)
```
3d: Colored Cube:       67 fps
3d: Lighting:   67 fps
3d: Textures:   45 fps
3d: Blending:   20 fps
3d: Fog:        40 fps
3d: Reflection: 61 fps
3d: Multitexture:       67 fps
3d: Teapot:     44 fps
3d: Gears:      67 fps
```

beagle-donut-0x3
```
3d: Colored Cube:       67 fps
3d: Lighting:   67 fps
3d: Textures:   44 fps
3d: Blending:   24 fps
3d: Fog:        38 fps
3d: Reflection: 62 fps
3d: Multitexture:       67 fps
3d: Teapot:     44 fps
3d: Gears:      67 fps
```

beagle-eclair-0x4
```
                  Eclair   Eclair-20100319
3d: Colored Cube: 67 fps   67 fps
3d: Lighting:     67 fps   67 fps
3d: Textures:     35 fps   49 fps*
3d: Blending:     17 fps   26 fps*
3d: Fog:          31 fps   39 fps
3d: Reflection:   53 fps   59 fps
3d: Multitexture: 21 fps   68 fps*
3d: Teapot:       42 fps   42 fps
3d: Gears:        66 fps   66 fps
```

## 2D Tests ##

beagle-donut-0x3 (without Software Cursor)
```
2d: Arcs:       70 fps
2d: FillRate:   78 fps
2d: Circles:    69 fps
2d: Rectangles: 69 fps
2d: Alpha:      67 fps
```

beagle-donut-0x3
```
2d: Arcs:       70 fps
2d: FillRate:   84 fps
2d: Circles:    70 fps
2d: Rectangles: 70 fps
2d: Alpha:      67 fps
```

beagle-eclair-0x4
```
2d: Arcs:       67 fps
2d: FillRate:   72 fps
2d: Circles:    69 fps
2d: Rectangles: 67 fps
2d: Alpha:      67 fps
```

  * NOTE: It seems that extremely small screen doesn't encounter the evident performance drop problems comparing to the same software stack on XGA (1024x768).

The 2D result is almost vsync bound.