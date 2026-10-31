# Sắp xếp repository cho Unity

Ngày thực hiện: **31/10/2026**.

Repository ban đầu chứa project **RPG Maker MZ**, thư mục `assets` chứa PNG/Aseprite và thư mục `tang1` chứa bản vẽ tầng một. Không có project Unity, C# hay file `.meta` Unity cần giữ từ trước.

## Thay đổi

- Di chuyển nguyên thư mục `HaGames` vào `Legacy/RPGMaker/HaGames`. Giữ đủ engine, plugin, map, database, font, âm thanh, ảnh, hiệu ứng, file project và save, với các đường dẫn tương đối nội bộ như cũ.
- Đưa 10 PNG từ `assets` vào `Assets/_Game/Art`, chia theo nhân vật Hà/Thư, tileset nhà, nền trời và tileset dùng chung.
- Đưa ba Aseprite trong `assets` vào `SourceArt/Environment/Tilesets`. Đưa ba Aseprite trong `tang1` vào `SourceArt/Archive/HomeGroundFloor` để giữ các phiên bản khác nhau.
- Sao chép thêm năm PNG nhân vật tùy chỉnh từ bản RPG Maker vào `Art/Characters/*/LegacyExports`. Tất cả bản gốc vẫn nằm trong `Legacy`.
- Chuyển ba ghi chú `.txt` sang `Docs/Notes`. Giữ README cũ ở `Docs/History/OriginalREADME.md` và viết hướng dẫn mới tại thư mục gốc.
- Tạo `Assets/_Game`, `Assets/ThirdParty`, `Packages` và `ProjectSettings`. Sử dụng cấu hình và scene từ template **Universal 2D** đi kèm Unity **6000.5.4f1** đã cài trên máy. Giữ GUID của các asset template khi chuyển sang đường dẫn mới.
- Chuyển `SampleScene` thành `Scenes/Bootstrap/Bootstrap.unity`, cập nhật đường dẫn trong Build Settings. Cấu hình render ở `Settings/Rendering`, Input Actions ở `Settings/Input`.
- Ghim phiên bản package theo bộ package của Editor đã cài, gồm URP `17.5.0`. Bỏ các trường tài nguyên cũ không còn trong mã nguồn renderer đi kèm phiên bản này.
- Thêm `.meta`, `.gitkeep`, `.gitignore`, `.gitattributes` và tài liệu quy ước.

Xem toàn bộ nhóm đường dẫn đổi tên và các bản sao bổ sung trong [AssetMoves.csv](AssetMoves.csv).

## Phạm vi

Đây là việc sắp xếp thư mục và chuẩn bị project Unity 2D. Chưa chuyển gameplay, event, map, save hoặc plugin RPG Maker sang hệ thống Unity. Các thư mục hội thoại, quan hệ, lịch sinh hoạt, nhiệm vụ và prefab là cấu trúc để triển khai tiếp.

Chỉ có scene nền `Bootstrap` từ template. Các sprite sheet được giữ nguyên hình ảnh; `.meta` thiết lập import pixel art, chưa slice thành frame/Tile asset.

## Kiểm chứng

Đã lập danh sách và SHA-256 của **1.348 file gốc**, tổng **106.763.476 byte**, trước khi di chuyển. Sau khi sắp xếp, đối chiếu từng file tại đường dẫn mới: nội dung nguyên vẹn, bao gồm README cũ và cả file `game.rmmzproject`.

Kiểm tra tĩnh cuối cùng đạt:

- Đối chiếu lại cả 1.348 file gốc với Git: nội dung khớp; tổng dung lượng giữ nguyên.
- 96 asset/thư mục Unity có `.meta`, GUID hợp lệ, không trùng và không có `.meta` mồ côi.
- 138 tham chiếu GUID trong scene/cấu hình tìm thấy đích trong project hoặc package đi kèm Editor; đường dẫn scene và Build Settings trỏ tới `Bootstrap`.
- Bảy package khai báo trực tiếp khớp phiên bản được cung cấp trong bản Unity đã cài.
- 15 PNG có thiết lập import pixel art; các liên kết tài liệu nội bộ và file JSON được kiểm tra.

Các phép kiểm tra trên đọc file và metadata; chúng chưa xác nhận Unity import hoặc chạy gameplay.

Unity Editor được gọi ở chế độ batch để import và kiểm tra scene. Editor dừng trước khi import với thông báo **“No valid Unity Editor license found. Please activate your license.”** Vì vậy chưa xác nhận được việc import package, mở scene hay chạy Play Mode trong Editor. Log cục bộ nằm ở `Logs/FolderReorganization.log` (Git bỏ qua).

Sau khi kích hoạt license, mở project trong Unity Hub bằng phiên bản ghi tại `ProjectSettings/ProjectVersion.txt`, đợi Package Manager hoàn tất, mở `Bootstrap` và kiểm tra Console. Unity sẽ bổ sung các giá trị cấu hình mặc định còn thiếu khi import/lưu lần đầu.

Tài liệu gốc: [Unity — tổ chức project](https://unity.com/how-to/organizing-your-project), [Unity — metadata](https://docs.unity3d.com/6000.5/Documentation/Manual/AssetMetadata.html).
