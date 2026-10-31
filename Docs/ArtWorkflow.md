# Quy trình art 2D

## File nguồn và file dùng trong Unity

Chỉnh sửa file Aseprite trong `SourceArt`, xuất PNG vào `Assets/_Game/Art`. Giữ tên và đường dẫn PNG ổn định khi xuất lại để Unity tiếp tục sử dụng `.meta` hiện có.

| File nguồn | PNG xuất ra |
| --- | --- |
| `SourceArt/Environment/Tilesets/Shared/AllFloor.aseprite` | `Assets/_Game/Art/Environment/Tilesets/Shared/AllFloor.png` |
| `SourceArt/Environment/Tilesets/Shared/AllWall.aseprite` | `Assets/_Game/Art/Environment/Tilesets/Shared/AllWall.png` |
| `SourceArt/Environment/Tilesets/Home/KitchenProps.aseprite` | `Assets/_Game/Art/Environment/Tilesets/Home/KitchenProps.png` |

`SourceArt/Archive/HomeGroundFloor` giữ ba file Aseprite từ thư mục `tang1` cũ. Đây là các bản nguồn khác, không ghi đè chúng lên bản hiện tại. `SourceArt/Characters` dành cho file nguồn nhân vật khi có; repository ban đầu chỉ có PNG nhân vật.

## Import và cắt sprite

Các PNG hiện có được thiết lập `Sprite (2D and UI)`, `Point`, không mipmap, không nén và **48 pixels/unit**. Giá trị 48 lấy từ `tileSize` của bản RPG Maker, giúp một ô bản đồ 48 px tương ứng một Unity unit. Khi tạo PNG mới, áp dụng cùng thiết lập hoặc tạo Preset trong `Settings/Presets`.

Các ảnh đang dùng `Sprite Mode: Single` để giữ nguyên sheet ban đầu. Chưa tạo animation, Tile asset hoặc tự động cắt lại hình vẽ.

1. Với sprite sheet nhân vật, đổi sang `Multiple`, mở Sprite Editor và kiểm tra kích thước từng frame trước khi Slice. Ba ảnh `Ha_Home.png`, `Ha_School.png`, `Thu_School.png` có kích thước 384 × 384; bố cục 8 cột × 4 hàng tương ứng frame 48 × 96 px.
2. Các ảnh trong thư mục `LegacyExports` là năm bản nhân vật riêng từ runtime RPG Maker, khác nội dung với PNG ban đầu trong `assets`. Tên cũ có số frame trong `%(8)` hoặc `%(3)`; xem [bảng di chuyển](Migration/AssetMoves.csv). Kiểm tra bố cục từng sheet trước khi slice.
3. Với tileset thường, bắt đầu kiểm tra grid 48 × 48. Riêng props lớn hoặc vật thể cần tương tác, chọn vùng cắt phù hợp để không chia vụn đồ vật.
4. Tạo Tile asset trong `Tilemaps/Tiles`, palette trong `Tilemaps/Palettes`, RuleTile trong `Tilemaps/Rules`. RuleTile dành cho quy tắc nối tường/sàn khi triển khai.

RPG Maker autotile dùng cách ghép ô riêng. Chuyển thư mục không tự chuyển thuật toán autotile, collision, event hoặc dữ liệu `Map001.json` sang Unity Tilemap. Dùng map cũ trong `Legacy/RPGMaker/HaGames/data` làm tài liệu đối chiếu khi dựng lại.

## Hình ảnh và không gian học đường

Giữ tỉ lệ nhân vật và độ phân giải thống nhất giữa nhà, trường và khu phố. Chia trang phục theo bối cảnh (`Ha_Home`, `Ha_School`) trong cùng thư mục nhân vật, thay vì nhân bản cả nhân vật sang nhiều bối cảnh.

Nội thất, lớp học và đồ vật đời thường được tổ chức theo địa điểm. Chân dung hội thoại và icon nằm trong `Art/UI`. Các thư mục `School`, `Neighborhood`, `NPCs` được chuẩn bị cho nội dung mới; chúng chưa chứa bộ art mới.

Âm thanh, font, hiệu ứng và tài nguyên mặc định của bản RPG Maker được giữ tại `Legacy`; chúng chưa được đưa vào thư viện art/audio Unity. Chọn tài nguyên phù hợp khi triển khai từng khu vực.

Tham khảo: [Unity — quy trình phát triển game 2D](https://docs.unity3d.com/6000.5/Documentation/Manual/2d-game-creation-wokflow.html).
