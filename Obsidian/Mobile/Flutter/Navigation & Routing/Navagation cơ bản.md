### 1. Cơ chế
- Việc điều hướng cơ bản của Flutter dựa trên cơ chế Stack (LIFO: Last In First Out - Vào sau ra trước)
- Để chuyển sang một màn hình mới sử dụng `Navigator.push(context, route`. Màn hình đích sẽ được xếp chồng lên màn hình hiện tại. Khi cần chuyển màn hình trước đó sử dụng `Navigator.pop(context)`. Màn hình hiện tại sẽ bị gỡ khỏi ngăn xếp và quay về màn hình trước.
```dart
// Within the `FirstRoute` widget:
onPressed: () {
  Navigator.push(
    context,
    MaterialPageRoute<void>(
      builder: (context) => const SecondRoute(),
    ),
  );
}
```

```dart
// Within the 'SecondRoute' widget:
onPressed: () {
  Navigator.pop(context);
}
```


- `context`: `Build Context` là vị trí của widget đó trong widget tree (như một thể định vị). Mỗi widget cần có một BuildContext của riêng nó.
- `MaterialPageRoute`: option mặc định bao gồm hiệu ứng chuyển theo từng nền tàng (ios/android) và có quy chuẩn giao diện theo Material Design của Google. Ngoài ra còn 2 option khác:
	- `CupertinoPageRoute()`: phong cách IOS - trượt từ phải sang
	- `PageRouteBuilder()`: tự tạo hiệu ứng 
```dart
// Using PageRouteBuilder() with custom animation
Navigator.push(
  context,
  PageRouteBuilder(
    pageBuilder: (context, animation, secondaryAnimation) => const SecondScreen(),
    transitionsBuilder: (context, animation, secondaryAnimation, child) {
      // Tạo hiệu ứng mờ dần trong 0.5 giây
      return FadeTransition(
        opacity: animation,
        child: child,
      );
    },
    transitionDuration: const Duration(milliseconds: 500), // Chỉnh tốc độ
  ),
)
```

