# PUT

####Приведу текст скрипта на lua:

[Lua put script](java/ok/dht/test/galeev/reports/scritps/put.lua)
```
cnt = 0
request = function()
    uri = "/v0/entity?id=K:" .. cnt
    wrk.body = "V:" .. cnt
    cnt = cnt + 1
    return wrk.format("PUT", uri)
end
```

## 13.5K
После перебора кучи вариантов параметра `-R` - пришел к выводу, что это наиболее оптимальный

```
└─$ wrk -t 1 -c 1 -d 60s -s /media/coradead/Windows1/Users/CORADEAD/IdeaProjects/2022-highload-dht/src/main/java/ok/dht/test/galeev/reports/scritps/put.lua -L http://localhost:19234 -R 13500
Running 1m test @ http://localhost:19234
  1 threads and 1 connections
  Thread calibration: mean lat.: 32.014ms, rate sampling interval: 342ms
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     2.18ms    7.12ms  86.53ms   95.52%
    Req/Sec    13.52k   232.48    15.20k    91.78%
  Latency Distribution (HdrHistogram - Recorded Latency)
 50.000%  745.00us
 75.000%    1.07ms
 90.000%    2.22ms
 99.000%   46.17ms
 99.900%   70.78ms
 99.990%   85.06ms
 99.999%   86.59ms
100.000%   86.59ms

  Detailed Percentile spectrum:
       Value   Percentile   TotalCount 1/(1-Percentile)

       0.032     0.000000            1         1.00
       0.204     0.100000        67768         1.11
       0.345     0.200000       135129         1.25
       0.482     0.300000       202486         1.43
       0.615     0.400000       270378         1.67
       0.745     0.500000       337887         2.00
       0.809     0.550000       371206         2.22
       0.874     0.600000       404953         2.50
       0.939     0.650000       439081         2.86
       1.003     0.700000       472806         3.33
       1.066     0.750000       506413         4.00
       1.097     0.775000       523069         4.44
       1.129     0.800000       539957         5.00
       1.185     0.825000       556860         5.71
       1.313     0.850000       573695         6.67
       1.598     0.875000       590555         8.00
       1.853     0.887500       599017         8.89
       2.221     0.900000       607434        10.00
       2.781     0.912500       615869        11.43
       3.567     0.925000       624312        13.33
       4.655     0.937500       632751        16.00
       5.543     0.943750       636967        17.78
       7.231     0.950000       641178        20.00
       9.823     0.956250       645392        22.86
      11.951     0.962500       649633        26.67
      14.407     0.968750       653831        32.00
      16.735     0.971875       655941        35.56
      20.255     0.975000       658047        40.00
      23.231     0.978125       660157        45.71
      28.943     0.981250       662271        53.33
      34.783     0.984375       664373        64.00
      38.495     0.985938       665428        71.11
      42.687     0.987500       666497        80.00
      45.087     0.989062       667542        91.43
      46.719     0.990625       668602       106.67
      49.599     0.992188       669652       128.00
      50.879     0.992969       670184       142.22
      52.191     0.993750       670704       160.00
      53.823     0.994531       671238       182.86
      55.071     0.995313       671755       213.33
      56.735     0.996094       672290       256.00
      57.375     0.996484       672549       284.44
      58.911     0.996875       672810       320.00
      60.511     0.997266       673075       365.71
      62.303     0.997656       673337       426.67
      63.711     0.998047       673603       512.00
      64.575     0.998242       673736       568.89
      66.367     0.998437       673865       640.00
      69.055     0.998633       674004       731.43
      69.823     0.998828       674134       853.33
      70.911     0.999023       674261      1024.00
      71.871     0.999121       674326      1137.78
      73.535     0.999219       674392      1280.00
      75.135     0.999316       674457      1462.86
      76.863     0.999414       674524      1706.67
      78.527     0.999512       674590      2048.00
      79.423     0.999561       674624      2275.56
      80.319     0.999609       674656      2560.00
      81.087     0.999658       674688      2925.71
      81.983     0.999707       674721      3413.33
      82.879     0.999756       674754      4096.00
      83.327     0.999780       674770      4551.11
      83.775     0.999805       674788      5120.00
      84.095     0.999829       674804      5851.43
      84.543     0.999854       674824      6826.67
      84.863     0.999878       674844      8192.00
      84.863     0.999890       674844      9102.22
      85.119     0.999902       674853     10240.00
      85.375     0.999915       674862     11702.86
      85.567     0.999927       674869     13653.33
      85.823     0.999939       674877     16384.00
      85.951     0.999945       674881     18204.44
      86.079     0.999951       674886     20480.00
      86.207     0.999957       674891     23405.71
      86.335     0.999963       674895     27306.67
      86.399     0.999969       674898     32768.00
      86.463     0.999973       674900     36408.89
      86.527     0.999976       674907     40960.00
      86.527     0.999979       674907     46811.43
      86.527     0.999982       674907     54613.33
      86.591     0.999985       674918     65536.00
      86.591     1.000000       674918          inf
#[Mean    =        2.182, StdDeviation   =        7.119]
#[Max     =       86.528, Total count    =       674918]
#[Buckets =           27, SubBuckets     =         2048]
----------------------------------------------------------
  809970 requests in 1.00m, 51.75MB read
Requests/sec:  13499.82
Transfer/sec:      0.86MB
```
## Графики:
### 1. Plotted latency graph для `put`
![put graph](./PNGs/PutHistogram.png)

### 2. CPU async profiler
![put cpu](./PNGs/cpu_put.png)

### 3. Alloc async profiler
![put alloc](./PNGs/alloc_put.png)

# GET

Для тестирования `get` была создана БД на 3Гб(примерно 70млн `entry`), размер файла 8Мб

####Так же код на lua:
[Lua get script](java/ok/dht/test/galeev/reports/scritps/get.lua)
```
cnt = 0
request = function()
    uri = string.format("/v0/entity?id=k%010d", cnt)
    cnt = cnt + 1
    return wrk.format("GET", uri, {})
end
```

## 500
Пожалуй сразу попали в приемлемый результат
```
└─$ wrk -t 1 -c 1 -d 60s -s /media/coradead/Windows1/Users/CORADEAD/IdeaProjects/2022-highload-dht/src/main/java/ok/dht/test/galeev/reports/scritps/get.lua -L http://localhost:19234 -R 500  
Running 1m test @ http://localhost:19234
  1 threads and 1 connections
  Thread calibration: mean lat.: 2.104ms, rate sampling interval: 10ms
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     1.92ms  484.60us  12.91ms   71.75%
    Req/Sec   526.14     66.87   800.00     63.94%
  Latency Distribution (HdrHistogram - Recorded Latency)
 50.000%    1.92ms
 75.000%    2.22ms
 90.000%    2.48ms
 99.000%    2.81ms
 99.900%    5.14ms
 99.990%   11.50ms
 99.999%   12.92ms
100.000%   12.92ms

  Detailed Percentile spectrum:
       Value   Percentile   TotalCount 1/(1-Percentile)

       0.436     0.000000            1         1.00
       1.317     0.100000         2500         1.11
       1.549     0.200000         5008         1.25
       1.686     0.300000         7502         1.43
       1.803     0.400000        10008         1.67
       1.920     0.500000        12518         2.00
       1.979     0.550000        13758         2.22
       2.035     0.600000        15005         2.50
       2.093     0.650000        16272         2.86
       2.153     0.700000        17524         3.33
       2.221     0.750000        18765         4.00
       2.257     0.775000        19382         4.44
       2.297     0.800000        20023         5.00
       2.337     0.825000        20636         5.71
       2.381     0.850000        21268         6.67
       2.427     0.875000        21880         8.00
       2.453     0.887500        22197         8.89
       2.479     0.900000        22512        10.00
       2.509     0.912500        22831        11.43
       2.535     0.925000        23144        13.33
       2.563     0.937500        23453        16.00
       2.579     0.943750        23607        17.78
       2.595     0.950000        23754        20.00
       2.613     0.956250        23914        22.86
       2.631     0.962500        24060        26.67
       2.653     0.968750        24222        32.00
       2.665     0.971875        24299        35.56
       2.683     0.975000        24378        40.00
       2.703     0.978125        24452        45.71
       2.723     0.981250        24535        53.33
       2.743     0.984375        24610        64.00
       2.759     0.985938        24646        71.11
       2.775     0.987500        24686        80.00
       2.799     0.989062        24724        91.43
       2.833     0.990625        24763       106.67
       2.881     0.992188        24802       128.00
       2.917     0.992969        24822       142.22
       2.965     0.993750        24841       160.00
       3.057     0.994531        24862       182.86
       3.159     0.995313        24880       213.33
       3.405     0.996094        24900       256.00
       3.547     0.996484        24910       284.44
       3.661     0.996875        24919       320.00
       3.821     0.997266        24929       365.71
       3.955     0.997656        24939       426.67
       4.039     0.998047        24949       512.00
       4.151     0.998242        24954       568.89
       4.255     0.998437        24958       640.00
       4.491     0.998633        24963       731.43
       4.659     0.998828        24968       853.33
       5.171     0.999023        24973      1024.00
       5.547     0.999121        24976      1137.78
       5.859     0.999219        24978      1280.00
       6.095     0.999316        24980      1462.86
       6.431     0.999414        24983      1706.67
       6.919     0.999512        24985      2048.00
       7.763     0.999561        24987      2275.56
       8.095     0.999609        24988      2560.00
       8.439     0.999658        24989      2925.71
       8.927     0.999707        24990      3413.33
       9.431     0.999756        24991      4096.00
       9.847     0.999780        24992      4551.11
      10.655     0.999805        24993      5120.00
      10.655     0.999829        24993      5851.43
      11.031     0.999854        24994      6826.67
      11.031     0.999878        24994      8192.00
      11.503     0.999890        24995      9102.22
      11.503     0.999902        24995     10240.00
      11.503     0.999915        24995     11702.86
      12.263     0.999927        24996     13653.33
      12.263     0.999939        24996     16384.00
      12.263     0.999945        24996     18204.44
      12.263     0.999951        24996     20480.00
      12.263     0.999957        24996     23405.71
      12.919     0.999963        24997     27306.67
      12.919     1.000000        24997          inf
#[Mean    =        1.920, StdDeviation   =        0.485]
#[Max     =       12.912, Total count    =        24997]
#[Buckets =           27, SubBuckets     =         2048]
----------------------------------------------------------
  30000 requests in 1.00m, 2.12MB read
Requests/sec:    500.00
Transfer/sec:     36.13KB
```

###Графики:
#### 1. Plotted latency graph для `get`
![get graph](./PNGs/GetHistogram.png)

### 2. CPU async profiler
![get cpu](./PNGs/cpu_get.png)

### 3. Alloc async profiler
![get alloc](./PNGs/alloc_get.png)