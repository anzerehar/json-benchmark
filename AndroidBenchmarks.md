# Benchmarking JSON parsers on Android #

We use [vogar](http://code.google.com/p/vogar/) to run benchmarks on Android. Vogar is a handy tool that takes care of compiling, dxing, copying code to the device, and running benchmarks on the device. You can get it from that project's [Google Code SVN repository](http://code.google.com/p/vogar/source/checkout).

You'll also need an [Android SDK](http://developer.android.com/sdk/), and the benchmarks to run. For this example we're running Dalvik's [ParseBenchmark.java](http://code.google.com/p/dalvik/source/browse/trunk/benchmarks/regression/ParseBenchmark.java) from that project's [Google Code SVN repository](http://code.google.com/p/dalvik/source/checkout). The Dalvik benchmark compares both JSON and XML. It includes a .zip file of JSON and XML files that should be representative of real world data.

You'll also need the JSON parsers to benchmark. For this test we're using [GSON](http://code.google.com/p/google-gson/), [Jackson](http://jackson.codehaus.org/), [json-smart](http://code.google.com/p/json-smart/) and the two parsers built into the Android 3.0 SDK. We're running the benchmark on a production Motorola XOOM tablet. Its best to run Android benchmarks on real hardware! The emulator performance is not representative of real world performance.
```
dalvik$ ~/Projects/vogar/bin/vogar --benchmark \
  --classpath ~/Projects/dalvik/benchmarks/regression/ParseBenchmarkData.zip \
  --classpath ~/Downloads/gson-1.7.2-SNAPSHOT.jar \
  --classpath ~/Downloads/jackson-core-asl-1.8.1.jar  \
  ~/Projects/dalvik/benchmarks/regression/ParseBenchmark.java
```

This benchmark yields the following results:
```
                        TWEETS                              
           api run   ms linear runtime                    % 
ANDROID_STREAM   B 28.8 =================              207% 
JACKSON_STREAM   B 13.9 ========                       100% 
   GSON_STREAM   B 33.1 ===================            238% 
      ORG_JSON   B 36.2 =====================          260% 
     JSON_MINI   B 50.0 ============================== 360% 

                         READER_SHORT                        
           api run    ms linear runtime                    % 
ANDROID_STREAM   B  6.78 ================               177% 
JACKSON_STREAM   B  3.82 =========                      100% 
   GSON_STREAM   B  7.07 ================               185% 
      ORG_JSON   B  7.61 ==================             199% 
     JSON_MINI   B 12.49 ============================== 327% 

                        READER_LONG                         
           api run   ms linear runtime                    % 
ANDROID_STREAM   B 69.6 =====================          254% 
JACKSON_STREAM   B 27.4 ========                       100% 
   GSON_STREAM   B 68.1 =====================          248% 
      ORG_JSON   B 68.9 =====================          251% 
     JSON_MINI   B 95.0 ============================== 347% 
```
You can use the [Caliper microbenchmarking framework](http://code.google.com/p/caliper/) to run benchmarks and its [web app](http://microbenchmarks.appspot.com/run/limpbizkit@gmail.com/benchmarks.regression.ParseBenchmark) to analyze results.