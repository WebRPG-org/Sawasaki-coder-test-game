# Đi Qua Mùa Hạ

Game 2D học đường, đời thường, sử dụng sprite và tileset mang cảm hứng RPG/indie.

Repository đã được sắp xếp thành project Unity. Bản game RPG Maker MZ trước đây được giữ nguyên trong `Legacy/RPGMaker/HaGames` để chạy và đối chiếu khi chuyển engine.

```text
Thu/                         ← thêm thư mục này vào Unity Hub
├── Assets/
│   ├── _Game/               # Nội dung riêng của Đi Qua Mùa Hạ
│   │   ├── Animations/
│   │   ├── Art/             # Nhân vật, tileset, đồ vật, UI, VFX
│   │   ├── Audio/           # Music, Ambience, SFX, UI
│   │   ├── Data/            # Hội thoại, nhân vật, nhiệm vụ, lịch sinh hoạt
│   │   ├── Editor/          # Công cụ dành cho Unity Editor
│   │   ├── Prefabs/
│   │   ├── Scenes/          # Bootstrap, Menus, World, Sandbox
│   │   ├── Scripts/         # C# chia theo chức năng gameplay
│   │   ├── Settings/       # Rendering, Input, Presets
│   │   └── Tilemaps/        # Tiles, Palettes, Rules
│   └── ThirdParty/          # Asset/plugin bên ngoài khi cần dùng
├── Packages/                # Các package Unity cần cho project
├── ProjectSettings/         # Cấu hình Unity 2D
├── SourceArt/               # File Aseprite gốc và bản vẽ lưu trữ
├── Docs/                    # Kiến trúc, quy trình art, ghi chú, bảng di chuyển
└── Legacy/RPGMaker/HaGames/  # Bản game cũ, gồm map, event, âm thanh và save
```

Mở bản Unity:

1. Kích hoạt license Unity trong Unity Hub. Project dùng **Unity 6000.5.4f1**, phiên bản đã có trên máy khi sắp xếp.
2. Chọn **Add project from disk**, trỏ đến thư mục `Thu` chứa README này.
3. Đợi Unity tải/import các package, sau đó mở `Assets/_Game/Scenes/Bootstrap/Bootstrap.unity`.

`Bootstrap` là scene nền từ template Universal 2D chính thức, có camera 2D và cấu hình render. Gameplay, map JSON, event và plugin JavaScript của bản RPG Maker **chưa được chuyển sang C# hoặc Tilemap Unity**. Các thư mục hệ thống gameplay hiện là chỗ để phát triển tiếp.

Các PNG đã có thiết lập import sprite: Point, không mipmap, không nén và 48 pixels/unit. Sprite sheet được giữ nguyên ảnh; cần slice trước khi tạo animation/Tile Palette. Xem [quy trình art](Docs/ArtWorkflow.md).

Để mở bản cũ bằng RPG Maker MZ, dùng `Legacy/RPGMaker/HaGames/game.rmmzproject`. Toàn bộ đường dẫn tương đối bên trong bản cũ được giữ nguyên.

- [Kiến trúc thư mục và quy tắc đặt tên](Docs/Architecture.md)
- [Quy trình Aseprite, sprite sheet và Tilemap](Docs/ArtWorkflow.md)
- [Chi tiết di chuyển và kết quả kiểm tra](Docs/Migration/README.md)
- [Bảng đường dẫn cũ → mới](Docs/Migration/AssetMoves.csv)

Các thư mục `Library`, `Temp`, `Logs`, `UserSettings` và bản build được Git bỏ qua. Commit các file `.meta` cùng asset để giữ liên kết Unity.
