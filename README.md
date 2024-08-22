# Coding Convention (Dart - Flutter)

- Classes, enum types, typedefs, và type parameters thì sử dụng `UpperCamelCase`.

```dart
class SliderMenu { ... }

class HttpRequest { ... }

typedef Predicate<T> = bool Function(T value);
```

- Tên libraries, packages, directories, và source files sử dụng `lowercase_with_underscores`.

```dart
library peg_parser.source_scanner;

import 'file_system.dart';
import 'slider_menu.dart';
```

- Trường hợp còn lại sử dụng `lowerCamelCase`.

```dart
var count = 3;

HttpRequest httpRequest;

void align(bool clearItems) {
  // ...
}
```

- Sử dụng `single quote`

```dart
var foo = 'bar'; // Good
var foo = "bar"; // Bad
```

- Sắp xếp `import` đúng thứ tự

```dart
import 'dart:async';
import 'dart:html';

import 'package:bar/bar.dart';
import 'package:foo/foo.dart';
```

- Comment mô tả chức năng của các `Functions`, `Properties`.

````dart
/// URL avatar.
///
/// ```dart
/// var example = CodeBlockExample();
/// print(example.isItGreat); // "Yes."
/// ```
/// ABC XYZ.
String? avatarPath;
````
### Bloc

##### Bloc Events

- Start with verb 
- End with suffix **Event**

Example:
```
- ToDosEvent
- LoadToDosEvent
- DeleteToDoEvent
```

##### Bloc States

Example:
```
- Loading
- Loaded
- LoadFailed
```
## Cấu trúc source

>

      lib
      ├── app
      ├── common
      │   ├── config
      │   ├── constant                                  # Biến dùng chung
      │   ├── model                                     # Model của toàn bộ app
      │   ├── preference                                # Function shared_preference
      │   ├── route                                     # Route cho toàn bộ app
      │   ├── util                                      # Các Function sử dụng lại
      │   └── widget
      ├── feature                                       # Danh sách các tính năng của app
      │   ├── login
      │   │   ├── bloc                                  # Bloc của tính năng (nhiều bloc khác nhau)
      │   │   │   ├── export.dart                       # Export chung của Bloc
      │   │   │   ├── login_bloc.dart                   # Bloc xử lý của login feature
      │   │   │   ├── login_event.dart                  # Event Bloc của login feature
      │   │   │   └── login_state.dart                  # State Bloc của login feature
      │   │   ├── repository
      │   │   │   └── login_repository.dart             # Repository (sử dụng để call API Login)
      │   │   └── screen
      │   │   │   └── login.dart                        # Screen chính login tổng hợp từ các widget
      │   │   └── widget
      │   │       └── button_login.dart                 # Widget của screen login
      │   └── ...
      └── translations                                  # Cấu hình đa ngôn ngữ
