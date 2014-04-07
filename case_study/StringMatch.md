#StringMatch 

```
String key1 = "aa";
String key2 = "bb";
String key3 = "cc";

int foundKey1 = 0;
int foundKey2 = 0;
int foundKey3 = 0; 

for(int i=0;i<words.length;i++) {
	if(matchString(key1, words[i]))
		foundKey1 = 1;
	else 
		foundKey1 = foundKey1;
	
	if(matchString(key2, words[i]))
		foundKey2 = 1;
	else
		foundKey2 = foundKey2;
	
	if(matchString(key3, words[i]))
		foundKey3 = 1;
	else 
		foundKey3 = foundKey3;
}
```
Java to Lambda
```
val v7 = words.size;
val l1 = Range(0, v7).fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), i) => 
      val v10 = matchString("aa", words(i));
      val foundKey1 = { if (v10 == 0) foundKey122 else 1 };
      val v15 = matchString("bb", words(i));
      val foundKey2 = { if (v15 == 0) foundKey223 else 1 };
      val v19 = matchString("cc", words(i));
      val foundKey3 = { if (v19 == 0) foundKey324 else 1 };
      (foundKey1, foundKey2, foundKey3)
  });
l1
```

E:pull-map-from-fold-by-subexpression-extract
```
val v7 = words.size;
val l1 = Range(0, v7).mapM({
    case (i) => 
      (matchString("aa", words(i)) == 0, matchString("bb", words(i)) == 0, matchString("cc", words(i)) == 0)
  }).fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), (i, (v1, v2, v3))) => 
      ({ if (v1) foundKey122 else 1 }, { if (v2) foundKey223 else 1 }, { if (v3) foundKey324 else 1 })
  });
l1
```

E:pull-map-from-fold-by-subexpression-extract
```
val v4 = Range(0, words.size).fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), i) => 
      ({ if (matchString("aa", words(i)) == 0) foundKey122 else 1 }, { if (matchString("bb", words(i)) == 0)
      foundKey223 else 1 }, { if (matchString("cc", words(i)) == 0) foundKey324 else 1 })
  });
(Range(0, words.size).mapM({
    case (i) => 
      (matchString("aa", words(i)) == 0, matchString("bb", words(i)) == 0, matchString("cc", words(i)) == 0)
  }).fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), (i, (v1, v2, v3))) => 
      ({ if (v1) foundKey122 else 1 }, { if (v2) foundKey223 else 1 }, { if (v3) foundKey324 else 1 })
  }))(v4._2)(v4._3)
```

E:localize-map-accesses
```
val v7 = words.size;
val l1 = Range(0, v7).zip(words).mapM({
    case (i, v4) => 
      (matchString("aa", v4) == 0, matchString("bb", v4) == 0, matchString("cc", v4) == 0)
  }).fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), (i, (v1, v2, v3))) => 
      ({ if (v1) foundKey122 else 1 }, { if (v2) foundKey223 else 1 }, { if (v3) foundKey324 else 1 })
  });
l1
```

E:localize-map-accesses
```
val v7 = Range(0, words.size).mapM({
    case (i) => 
      (matchString("aa", words(i)) == 0, matchString("bb", words(i)) == 0, matchString("cc", words(i)) == 0)
  });
val v6 = v7.fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), (i, (v1, v2, v3))) => 
      ({ if (v1) foundKey122 else 1 }, { if (v2) foundKey223 else 1 }, { if (v3) foundKey324 else 1 })
  });
val v5 = v7;
val v8 = v5.fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), (i, (v1, v2, v3))) => 
      ({ if (v1) foundKey122 else 1 }, { if (v2) foundKey223 else 1 }, { if (v3) foundKey324 else 1 })
  });
(words.mapM({
    case (i, v4) => 
      (matchString("aa", v4) == 0, matchString("bb", v4) == 0, matchString("cc", v4) == 0)
  }).fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), (i, (v1, v2, v3))) => 
      ({ if (v1) foundKey122 else 1 }, { if (v2) foundKey223 else 1 }, { if (v3) foundKey324 else 1 })
  }))(v8._2)(v8._3)
```

E:localize-map-accesses
```
val v5 = Range(0, words.size).fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), i) => 
      ({ if (matchString("aa", words(i)) == 0) foundKey122 else 1 }, { if (matchString("bb", words(i)) == 0)
      foundKey223 else 1 }, { if (matchString("cc", words(i)) == 0) foundKey324 else 1 })
  });
(words.mapM({
    case (i, v4) => 
      (matchString("aa", v4) == 0, matchString("bb", v4) == 0, matchString("cc", v4) == 0)
  }).fold((0, 0, 0))({
    case ((foundKey122, foundKey223, foundKey324), (i, (v1, v2, v3))) => 
      ({ if (v1) foundKey122 else 1 }, { if (v2) foundKey223 else 1 }, { if (v3) foundKey324 else 1 })
  }))(v5._2)(v5._3)
```
