# Gta San Online Launcher

SA-MP Mobile Launcher สำหรับ Android  
Fork จาก Alyn SA-MP Mobile v17.x

## Requirements
- GTA: San Andreas Android **version 2.10** (arm64-v8a)
- Android 7.0+ (API 24+)

## Build via GitHub Actions
1. Fork repo นี้ไปที่ GitHub account ของคุณ
2. Push code → GitHub Actions จะ build อัตโนมัติ
3. ไปที่ **Actions** tab → เลือก workflow ล่าสุด → download `GtaSanOnlineLauncher-release`

## Build locally
```
Android Studio + JDK 17 + NDK 25.1.8937393 + CMake
./gradlew assembleRelease
```

## Credits
- Original source: Alyn SA-MP Mobile (released publicly, March 2025)
