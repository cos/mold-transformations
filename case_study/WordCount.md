#WordCount 

```
for (int i = 0; i < docs.length; i++) {
  String[] split = docs[i].split(" ");
  for (int j = 0; j < split.length; j++) {
    String word = split[j];
    Integer prev = m.get(word);
    if (prev == null) prev = 0;
    m.put(word, prev + 1);
  }
}
```
Java to Lambda
```
Range(0, docs.size).fold(m)({
    case (v34, i) => 
      val split = docs(i).splitString(" ");
      val v10 = split.size;
      Range(0, v10).fold(v34)({
          case (v33, j) => 
            val v13 = v33(split(j));
            val prev = { if (v13 != null) v13 else 0 };
            v33.updated(split(j), prev + 1)
        })
  })
```

S:eliminate-null-check
```
Range(0, docs.size).fold(m)({
    case (v34, i) => 
      val v6 = docs(i).splitString(" ");
      val v4 = Range(0, v6.size).groupBy({
          case (j) => 
            v6(j)
        });
      val v5 = v4.mapM({
          case (v2, v3) => 
            v3.fold(v34(v2))({
                case (v1, j) => 
                  v1 + 1
              })
        });
      v34 ++ v5
  })
```

S:reduce-monoid-identity-op
```
Range(0, docs.size).fold(m)({
    case (v34, i) => 
      val v6 = docs(i).splitString(" ");
      val v4 = Range(0, v6.size).groupBy({
          case (j) => 
            v6(j)
        });
      val v5 = v4.mapM({
          case (v2, v3) => 
            v34(v2) + v3.size
        });
      v34 ++ v5
  })
```

E:localize-map-accesses
```
Range(0, docs.size).fold(m)({
    case (v34, i) => 
      val v7 = docs(i).splitString(" ");
      val v4 = Range(0, v7.size).groupBy({
          case (j) => 
            v7(j)
        });
      val v5 = v4.zip(v34).mapM({
          case (v2, (v3, v6)) => 
            v6 + v3.size
        });
      v34 ++ v5
  })
```

E:localize-group-by-accesses
```
Range(0, docs.size).fold(m)({
    case (v34, i) => 
      val v4 = docs(i).splitString(" ").groupBy(ID).__2;
      val v5 = v4.zip(v34).mapM({
          case (v2, (v3, v6)) => 
            v6 + v3.size
        });
      v34 ++ v5
  })
```

E:pull-map-from-fold-by-subexpression-extract
```
Range(0, docs.size).mapM({
    case (i) => 
      docs(i).splitString(" ").groupBy(ID).__2
  }).fold(m)({
    case (v34, (i, v8)) => 
      v34 ++ v8.zip(v34).mapM({
          case (v2, (v3, v6)) => 
            v6 + v3.size
        })
  })
```

E:map-vertical-fission
```
Range(0, docs.size).mapM({
    case (i) => 
      docs(i).splitString(" ").groupBy(ID).__2
  }).fold(m)({
    case (v34, (i, v8)) => 
      v34 ++ v8.mapM({
          case (v2, v3) => 
            v3.size
        }).zip(v34).mapM({
          case (v2, (v9, v6)) => 
            v6 + v9
        })
  })
```

E:identify-map-monoid-plus
```
Range(0, docs.size).mapM({
    case (i) => 
      docs(i).splitString(" ").groupBy(ID).__2
  }).fold(m)({
    case (v34, (i, v8)) => 
      v8.mapM({
          case (v2, v3) => 
            v3.size
        }) |+| v34
  })
```

E:pull-map-from-fold-by-subexpression-extract
```
Range(0, docs.size).mapM({
    case (i) => 
      docs(i).splitString(" ").groupBy(ID).__2
  }).mapM({
    case (i, v8) => 
      v8.mapM({
          case (v2, v3) => 
            v3.size
        })
  }).fold(m)({
    case (v34, (i, v10)) => 
      v10 |+| v34
  })
```

E:swap-map-with-fold
```
val v8 = Range(0, docs.size).mapM({
    case (i) => 
      docs(i).splitString(" ").groupBy(ID).__2
  }).fold("ZERO-TOKEN")({
    case (v11, (i, v12)) => 
      v11 |+| v12
  });
v8.mapM({
    case (v2, v3) => 
      v3.size
  })
```

E:localize-map-accesses
```
docs.mapM({
    case (i, v13) => 
      v13.splitString(" ").groupBy(ID).__2
  }).fold("ZERO-TOKEN")({
    case (v11, (i, v12)) => 
      v11 |+| v12
  }).mapM({
    case (v2, v3) => 
      v3.size
  })
```

E:map-horizontal-fission
```
docs.mapM({
    case (i, v13) => 
      v13.splitString(" ").groupBy(ID)
  }).mapM({
    case (i, v14) => 
      v14.__2
  }).fold("ZERO-TOKEN")({
    case (v11, (i, v12)) => 
      v11 |+| v12
  }).mapM({
    case (v2, v3) => 
      v3.size
  })
```

E:map-horizontal-fission
```
docs.mapM({
    case (i, v13) => 
      v13.splitString(" ")
  }).mapM({
    case (i, v15) => 
      v15.groupBy(ID)
  }).mapM({
    case (i, v14) => 
      v14.__2
  }).fold("ZERO-TOKEN")({
    case (v11, (i, v12)) => 
      v11 |+| v12
  }).mapM({
    case (v2, v3) => 
      v3.size
  })
```

E:map-fusion
```
docs.mapM({
    case (i, v13) => 
      v13.splitString(" ")
  }).mapM({
    case (i, v15) => 
      v15.groupBy(ID).__2
  }).fold("ZERO-TOKEN")({
    case (v11, (i, v12)) => 
      v11 |+| v12
  }).mapM({
    case (v2, v3) => 
      v3.size
  })
```

E:swap-map-with-fold
```
val v15 = docs.mapM({
    case (i, v13) => 
      v13.splitString(" ")
  }).fold(Map())({
    case (v16, (i, v17)) => 
      v16 |+| v17
  });
val v18 = v15.groupBy(ID).__2;
v18.mapM({
    case (v2, v3) => 
      v3.size
  })
```
