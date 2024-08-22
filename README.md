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
- Khai báo biến trong Screen tách biệt Bloc, Variable
```dart
 //Bloc
  late UserBloc userBloc;
  late EditUserBloc editUserBloc;
  //Variable
  String? id;
  String? domain;
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

- Bắt đầu bằng **Verd**
- Kết thúc với hậu tố **Event**

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
### Kiến trúc clean architecture

![image](https://github.com/user-attachments/assets/f191eeac-0348-45e4-8ef6-3673612afcf3)

Sử dụng 3 tầng: Presentation, Domain and Data.

### Tầng Presentation(UI)
Ở tầng này chúng ta sẽ tổ chức code theo feature-first, sẽ bao gồm bloc, widget, screen. Chức năng chính của **Presentation** là: 

- Quản lý trạng thái(State management)
- Xử lý UI của ứng dụng, hiển thị dữ liệu,...
### Tầng Domain
Ở tầng Domain này chúng ta sẽ có: 

- Triển khai use cases
- Triển khai interface repositories

**Use case**: Tùy vào tính năng để có thể triển khai use case hay không.

Ví dụ: Minh họa cho tác dụng của use cases là có logic logout tài khoản, ở đây phải thực hiện các công việc như: Xóa các thông tin lưu trữ về người dùng và hủy đăng ký fcm. Và trong ứng dụng có 2 nơi có thể bấm logout để thoát đăng nhập: 1 là ở trang profile, 2 là ở trang chủ cũng có nút cho phép logout. Nếu gặp phải trường hợp như này sẽ đơn giản khi có thể tái sử dụng 1 hàm xử lý LogoutUseCases duy nhất.Một UseCases luôn được định nghĩa rõ ràng đầu vào và đầu ra, chính vì thế nó cũng rất dễ dàng để có thể kiểm thử tại đây.

![image](https://github.com/user-attachments/assets/bfda5115-7f4e-4c52-980b-b16b193023f6)

**Repository**: Tầng domain chỉ chứa các interface cho repo còn việc thực thi chúng thì nằm ở tầng data
### Tầng Data
Tầng Data thường được chia thành ba phần chính:

**Repositories**: Là các lớp triển khai cụ thể của các abstract repositories, implements phương thức định nghĩa trong abstract repositories.

**Data Sources**:

Remote Data Source: Chịu trách nhiệm làm việc với các nguồn dữ liệu từ xa, như API RESTful, ...
Local Data Source: Chịu trách nhiệm làm việc với các nguồn dữ liệu cục bộ như SQLite, SharedPreferences,...

**Models (Data Models)**: Map json sang model sử dụng ![json_serializable](https://pub.dev/packages/json_serializable) để generate code.
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
