
# How to Install

Follow the guide here.

Quick tip regarding Visual studio:

* Even though Flutter says it support `Visual Studio Build Tools 2022`, I currently have `2019` version, and latest version of flutter (flutter: 3.32.7, dart: 3.8.1) works perfectly:

![](Attachments%20-%20Flutter%20Notes/Pasted%20image%2020250719153502.png)

Side note 1: When using flutter's debugger, if you see an error like "path to cmake not found", then go to the visual studio installer then click `Modify` (which will give you the screenshot above), then uncheck the `C++ Cmake tools for Windows`, then install... Then after that, install it again; it will be installed properly this time `:]`.

Side note 2: To know the current flutter/dart versions:

```bash
flutter --version; dart --version
```

# Quick Tips

If you want to run flutter while displaying logs (that will show full stack trace if an error occurs) and target device is windows, run this:

```shell
flutter run -d windows -v
```

Moreover, related to displaying errors: flutter is a little bit tedious in showing the full stack trace when an error occurs (i.e., VSCode's `debug console` shows the top level error only (usually)). To mitigate this, we can use the [stack trace](https://pub.dev/packages/stack_trace) library so that instead of something like this in `main.dart`:

```dart
void main() {
  runApp(
    const ProviderScope(
      child: SurahAnnotatorApp(),
    ),
  );
}
```


We can instead write something like this ([source](https://andrewzuo.com/how-to-make-your-stack-traces-not-suck-in-flutter-5bb2a5583c73)):

```dart
import 'package:stack_trace/stack_trace.dart';

// Debugging logic is based on this great article:
// https://andrewzuo.com/how-to-make-your-stack-traces-not-suck-in-flutter-5bb2a5583c73
// NOTE to self: it seems that any error will be shown by `Chain.capture` even if
//   the line which caused the error is surrounded and handled by a try-catch block
//   Need to verify this further though...
void main() async {
  await Chain.capture(() async {
    WidgetsFlutterBinding.ensureInitialized();
    
    runApp(
      const ProviderScope(
        child: SurahAnnotatorApp(),
      ),
    );
  }, onError: (Object error, Chain chain) {
    // Log unhandled errors for debugging
    debugPrint('Unhandled error captured by Chain.capture: $error');
    debugPrint('Async stack trace chain:\n${chain.terse}');
  });
}

```

This will show the relevant stack trace when an error occurs.

