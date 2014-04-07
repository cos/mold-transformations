#LinearRegression 

```
double sx_ll = 0, sy_ll = 0, sxX_ll = 0, syY_ll = 0, sxY_ll = 0;

for (int i = 0; i < points.length; i++) {
  // Compute sx, sy, syY, sxX, sxY
  sx_ll += points[i].x;
  sxX_ll += points[i].x * points[i].x;
  sy_ll += points[i].y;
  syY_ll += points[i].y * points[i].y;
  sxY_ll += points[i].y * points[i].y;
}
```
Java to Lambda
```
val v5 = points.size;
val l1 = Range(0, v5).fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), i) => 
      val v7 = points(i).x;
      val sx_ll8 = sx_ll + v7;
      val v10 = points(i).x;
      val v12 = points(i).x;
      val sxX_ll14 = sxX_ll + v10 * v12;
      val v16 = points(i).y;
      val sy_ll17 = sy_ll + v16;
      val v19 = points(i).y;
      val v21 = points(i).y;
      val syY_ll23 = syY_ll + v19 * v21;
      val v25 = points(i).y;
      val v27 = points(i).y;
      val sxY_ll29 = sxY_ll + v25 * v27;
      (sx_ll8, sy_ll17, sxX_ll14, syY_ll23, sxY_ll29)
  });
l1
```

E:pull-map-from-fold-by-subexpression-extract
```
val v5 = points.size;
val l1 = Range(0, v5).mapM({
    case (i) => 
      val v7 = points(i).y;
      val v6 = points(i).x;
      (v6, v7, v6 * v6, v7 * v7, v7 * v7)
  }).fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), (i, (v1, v2, v3, v4, v5))) => 
      (sx_ll + v1, sy_ll + v2, sxX_ll + v3, syY_ll + v4, sxY_ll + v5)
  });
l1
```

E:pull-map-from-fold-by-subexpression-extract
```
val v6 = Range(0, points.size).fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), i) => 
      val v10 = points(i).y;
      val v9 = points(i).x;
      (sx_ll + v9, sy_ll + v10, sxX_ll + v9 * v9, syY_ll + v10 * v10, sxY_ll + v10 * v10)
  });
(Range(0, points.size).mapM({
    case (i) => 
      val v8 = points(i).y;
      val v7 = points(i).x;
      (v7, v8, v7 * v7, v8 * v8, v8 * v8)
  }).fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), (i, (v1, v2, v3, v4, v5))) => 
      (sx_ll + v1, sy_ll + v2, sxX_ll + v3, syY_ll + v4, sxY_ll + v5)
  }))(v6._2)(v6._3)(v6._4)(v6._5)
```

E:localize-map-accesses
```
val v5 = points.size;
val l1 = Range(0, v5).zip(points).mapM({
    case (i, v6) => 
      (v6.x, v6.y, v6.x * v6.x, v6.y * v6.y, v6.y * v6.y)
  }).fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), (i, (v1, v2, v3, v4, v5))) => 
      (sx_ll + v1, sy_ll + v2, sxX_ll + v3, syY_ll + v4, sxY_ll + v5)
  });
l1
```

E:localize-map-accesses
```
val v8 = Range(0, points.size).mapM({
    case (i) => 
      val v10 = points(i).y;
      val v9 = points(i).x;
      (v9, v10, v9 * v9, v10 * v10, v10 * v10)
  });
val v7 = v8.fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), (i, (v1, v2, v3, v4, v5))) => 
      (sx_ll + v1, sy_ll + v2, sxX_ll + v3, syY_ll + v4, sxY_ll + v5)
  });
(points.mapM({
    case (i, v6) => 
      (v6.x, v6.y, v6.x * v6.x, v6.y * v6.y, v6.y * v6.y)
  }).fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), (i, (v1, v2, v3, v4, v5))) => 
      (sx_ll + v1, sy_ll + v2, sxX_ll + v3, syY_ll + v4, sxY_ll + v5)
  }))(v7._2)(v7._3)(v7._4)(v7._5)
```

E:localize-map-accesses
```
val v7 = Range(0, points.size).fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), i) => 
      val v9 = points(i).y;
      val v8 = points(i).x;
      (sx_ll + v8, sy_ll + v9, sxX_ll + v8 * v8, syY_ll + v9 * v9, sxY_ll + v9 * v9)
  });
(points.mapM({
    case (i, v6) => 
      (v6.x, v6.y, v6.x * v6.x, v6.y * v6.y, v6.y * v6.y)
  }).fold((0.0, 0.0, 0.0, 0.0, 0.0))({
    case ((sx_ll, sy_ll, sxX_ll, syY_ll, sxY_ll), (i, (v1, v2, v3, v4, v5))) => 
      (sx_ll + v1, sy_ll + v2, sxX_ll + v3, syY_ll + v4, sxY_ll + v5)
  }))(v7._2)(v7._3)(v7._4)(v7._5)
```
