# Phần mềm edit game ursina python

![show](./doc/image/_01.png)

Video hướng dẫn dùng Editor Ursina: [Xem tại đây](https://youtu.be/GD9Hri9hNwM?si=SqajFnuZKAPyPpwc)

Theo dõi kênh: [Tại đây](https://www.youtube.com/@Dev8Sync/SeattleWebSearch?sub_confirmation=1)

> Sẽ có cập nhật trong tương lai 🥰 !!!

Video Hướng Dẫn Chi Tiết Game Minecraft Ursina Phần 1: [Xem tại đây](https://youtu.be/Zcn9NJtCNas?si=6rpZcZ-MGsIxsx7j)

Video Hướng Dẫn Chi Tiết Game Minecraft Ursina Phần 2 (Đa người chơi) Mới: [Xem tại đây](https://youtu.be/yRDzIuzuBOQ)


Website: [Xem tại đây](https://8syncdev.com/)

<p>Tài liệu sẽ được cập nhật định kì và thông báo trong group nên các bạn chú ý nhen .</p>
<p>
    Các khóa học khác xem tại : <a href="https://educated-energy-e8f.notion.site/L-tr-nh-h-c-2a4a2cb8f9e445df8cef231c8b45f31d">8 Sync Dev</a>
</p>
<p>
    Hoặc liên hệ trực tiếp qua fb: <a href="https://www.facebook.com/8sync">Kevin Nguyễn</a> để được hỗ trợ
</p>

### Giải thích mã nguồn

#### 1. Nhập thư viện
```python
from ursina import *
from ursina.editor.level_editor import *
```
- `from ursina import *`: Nhập toàn bộ các module và class từ thư viện `Ursina`.
- `from ursina.editor.level_editor import *`: Nhập toàn bộ module liên quan đến trình chỉnh sửa cấp độ từ `Ursina`.

#### 2. Hàm `main()`
```python
def main():
    app = Ursina(vsync=False)
```
- `def main()`: Đây là hàm chính, nơi mọi thứ bắt đầu.
- `app = Ursina(vsync=False)`: Tạo một ứng dụng `Ursina` với `vsync` tắt. `vsync` (Vertical Synchronization) giúp đồng bộ hóa tốc độ khung hình của ứng dụng với tốc độ làm mới của màn hình, nhưng trong trường hợp này, nó bị tắt để tăng hiệu suất.

#### 3. Lớp `Tree`
```python
class Tree(Entity):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.model = 'cube'
        self.color = color.brown

        self.top = Entity(name='tree_top', parent=self, y=1.5, model='cube', color=color.green, selectable=True)
        LEVEL_EDITOR.entities.append(self.top)
```
- `class Tree(Entity)`: Khai báo lớp `Tree` kế thừa từ `Entity`, là một đối tượng cơ bản trong Ursina.
- `def __init__(self, **kwargs)`: Hàm khởi tạo của lớp, cho phép truyền các tham số linh hoạt.
- `super().__init__(**kwargs)`: Gọi hàm khởi tạo của lớp cha (`Entity`).
- `self.model = 'cube'`: Thiết lập mô hình hình học của đối tượng là một hình lập phương.
- `self.color = color.brown`: Đặt màu của thân cây là màu nâu.
- `self.top = Entity(...)`: Tạo phần ngọn cây với màu xanh, đặt nó là con của đối tượng `Tree`.
- `LEVEL_EDITOR.entities.append(self.top)`: Thêm phần ngọn cây (`tree_top`) vào danh sách các thực thể trong trình chỉnh sửa cấp độ.

#### 4. Khởi tạo trình chỉnh sửa cấp độ
```python
level_editor = LevelEditor()
```
- `level_editor = LevelEditor()`: Tạo một đối tượng trình chỉnh sửa cấp độ (`LevelEditor`), cho phép người dùng tạo và chỉnh sửa các đối tượng trong không gian 3D.

#### 5. Thêm các lớp vào menu trình chỉnh sửa
```python
from ursina.prefabs.first_person_controller import FirstPersonController
level_editor.class_menu.available_classes |= {'WhiteCube': WhiteCube, 'EditorCamera':EditorCamera, 'FirstPersonController':FirstPersonController}
```
- `from ursina.prefabs.first_person_controller import FirstPersonController`: Nhập lớp `FirstPersonController`, cung cấp khả năng di chuyển góc nhìn như trong các game bắn súng góc nhìn thứ nhất.
- `level_editor.class_menu.available_classes |= ...`: Thêm các lớp (`WhiteCube`, `EditorCamera`, `FirstPersonController`) vào menu lớp của trình chỉnh sửa cấp độ. Người dùng có thể chọn và thêm các đối tượng này vào cảnh trong trình chỉnh sửa.

#### 6. Cấu hình và chạy ứng dụng
```python
from ursina.shaders import ssao_shader
window.borderless=False
app.run()
```
- `from ursina.shaders import ssao_shader`: Nhập shader SSAO (Screen Space Ambient Occlusion) để tạo hiệu ứng bóng tối dựa trên không gian màn hình, giúp cải thiện chất lượng hình ảnh.
- `window.borderless=False`: Thiết lập cửa sổ không viền (fullscreen không viền), cho phép người dùng di chuyển và thay đổi kích thước cửa sổ.
- `app.run()`: Chạy ứng dụng `Ursina`.

#### 7. Điểm bắt đầu của chương trình
```python
if __name__ == '__main__':
    main()
```
- `if __name__ == '__main__':`: Kiểm tra xem file này có phải là file chính được thực thi không. Nếu đúng, hàm `main()` sẽ được gọi để bắt đầu chương trình.
