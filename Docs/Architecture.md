# Kiến trúc thư mục

Nội dung game nằm dưới `Assets/_Game`. Tài nguyên bên ngoài nằm dưới `Assets/ThirdParty` khi được đưa vào Unity. File làm việc của họa sĩ, tài liệu và bản RPG Maker được đặt ngoài `Assets` để tách khỏi nội dung Unity import.

Đây là cách tổ chức cho một game indie 2D; các thư mục gameplay đã được chuẩn bị, chưa chứa hệ thống gameplay được lập trình sẵn.

## Tài nguyên và bối cảnh

| Thư mục trong `_Game` | Dùng cho |
| --- | --- |
| `Art/Characters/Ha`, `Thu`, `NPCs` | Sprite sheet của Hà, Thư, học sinh, giáo viên, người dân |
| `Art/Environment/Tilesets/Home` | Tileset nhà, cầu thang, tường và nội thất hiện có |
| `Art/Environment/Tilesets/School` | Tileset lớp học, hành lang, sân trường |
| `Art/Environment/Tilesets/Neighborhood` | Tileset khu phố, đường đi, cửa hàng |
| `Art/Environment/Tilesets/Shared` | Sàn, tường dùng chung giữa các bối cảnh |
| `Art/Environment/Backgrounds` | Bầu trời, nền xa, ảnh nền |
| `Art/Props/Home`, `School` | Sprite đồ vật tách lẻ để tạo prefab tương tác |
| `Art/UI/Icons`, `Portraits` | Icon đồ dùng, chân dung hội thoại |
| `Art/VFX` | Hình ảnh hiệu ứng |
| `Animations/Characters`, `Environment`, `UI` | AnimationClip, AnimatorController và animation liên quan |
| `Audio/Music`, `Ambience`, `SFX`, `UI` | Nhạc, âm thanh môi trường, hiệu ứng và phản hồi UI |
| `Tilemaps/Tiles`, `Palettes`, `Rules` | Tile asset, Tile Palette và RuleTile tạo trong Unity |

PNG tileset gốc nằm trong `Art`; Tile asset và palette tạo từ PNG nằm trong `Tilemaps`. Sprite đồ vật chỉ chuyển sang `Props` sau khi đã tách thành tài nguyên riêng. Không cần sao chép cả sheet vào nhiều thư mục.

## Scene và prefab

`Scenes/Bootstrap/Bootstrap.unity` là scene khởi đầu hiện có. Khi triển khai game, có thể dùng scene này để tạo các dịch vụ dùng chung như save, âm thanh và chuyển cảnh. Hiện scene chỉ có nội dung nền của template Universal 2D.

`Scenes/Menus` dành cho menu. `Scenes/World/Home`, `School`, `Neighborhood` dành cho từng khu vực. `Scenes/Sandbox` dành cho thử nghiệm map, tương tác và animation. Ví dụ tên scene tương lai: `Home_GroundFloor.unity`, `School_Classroom.unity`.

`Prefabs/Characters` chứa player/NPC; `Environment` chứa cụm cảnh vật; `Interactables` chứa cửa, bàn học, bảng tin, đồ vật nhặt được; `UI` chứa hộp thoại, menu, HUD. Các ví dụ này là quy ước cho nội dung được tạo về sau.

## Code và dữ liệu

| Thư mục script | Trách nhiệm dự kiến | Dữ liệu liên quan |
| --- | --- | --- |
| `Core` | Khởi tạo và vòng đời game | Cấu hình dùng chung |
| `Characters` | Di chuyển, hướng nhìn, animation player/NPC | `Data/Characters` |
| `Interaction` | Phát hiện và thực hiện tương tác | Prefab và cấu hình đối tượng |
| `Dialogue` | Trình tự hội thoại, lựa chọn, điều kiện | `Data/Dialogue`, `Data/Localization` |
| `Inventory` | Đồ dùng học tập và vật phẩm | `Data/Items` |
| `Quests` | Nhiệm vụ và tiến độ | `Data/Quests` |
| `Relationships` | Mối quan hệ và sự kiện nhân vật | `Data/Relationships` |
| `TimeAndSchedule` | Buổi học, giờ giấc, lịch NPC | `Data/Schedules` |
| `World` | Chuyển khu vực, cửa, điểm xuất hiện | Scene và prefab môi trường |
| `SaveSystem` | Đọc/ghi trạng thái chơi | File save tại `Application.persistentDataPath` |
| `Audio`, `UI` | Phát âm thanh và hiển thị giao diện | Asset audio và prefab UI |

`Scripts` chứa logic C#. `Data` chứa định nghĩa nội dung, ví dụ ScriptableObject hoặc JSON do hệ thống tương ứng đọc. Save thay đổi trong lúc chơi nằm ở `Application.persistentDataPath`, không ghi vào `Assets/Data`.

Code gọi `UnityEditor` đặt trong `_Game/Editor`. Chỉ thêm assembly definition khi đã có code và nhu cầu quản lý phụ thuộc cụ thể. Tránh tạo các thư mục chung chung như `Misc`, `New Folder`, `Scripts2`.

## Quy tắc làm việc

- Dùng tên tiếng Anh, chữ ASCII và PascalCase cho thư mục; dùng `Character_Outfit_Action` cho sprite và `Location_Area` cho scene khi cần phân biệt.
- Giữ phần đuôi file đúng loại. Đã sửa tên có hai dấu chấm như `All_wall..png` thành `AllWall.png`.
- Di chuyển/đổi tên asset trong cửa sổ Project của Unity. Nếu di chuyển bằng công cụ ngoài, di chuyển cả file `.meta` tương ứng, bao gồm `.meta` của thư mục.
- Commit `Assets`, `Packages`, `ProjectSettings`, `SourceArt`, `Docs` và `Legacy`. Các thư mục trống dùng `.gitkeep` để tồn tại sau khi clone.
- Đặt cấu hình render trong `Settings/Rendering`, input trong `Settings/Input`, preset import trong `Settings/Presets`.
- Chỉ đưa tài nguyên cần cho bản Unity vào `Assets`. Bản RPG Maker, map JSON và plugin cũ ở `Legacy` để tham chiếu khi port.

Tham khảo: [Unity — tổ chức project](https://unity.com/how-to/organizing-your-project), [Unity — metadata và GUID](https://docs.unity3d.com/6000.5/Documentation/Manual/AssetMetadata.html).
