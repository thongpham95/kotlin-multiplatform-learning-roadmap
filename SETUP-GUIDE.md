# 🚀 Hướng Dẫn Setup Kotlin Multiplatform - Bước Đầu

*Hướng dẫn chi tiết để thiết lập môi trường và tạo project KMP đầu tiên*

---

## 📋 Yêu Cầu Hệ Thống

### 🖥️ Hardware Requirements
- **RAM:** Tối thiểu 8GB (khuyến nghị 16GB+)
- **Storage:** Ít nhất 10GB trống cho tools
- **OS:** 
  - macOS (để phát triển iOS)
  - Windows/Linux (chỉ Android)

### 💻 Software Prerequisites
- **JDK 11 hoặc mới hơn**
- **Git** (version control)
- **Homebrew** (macOS) hoặc equivalent package manager

---

## 🛠️ 1. Cài Đặt Development Environment

### 1.1. Android Studio Setup

```bash
# Download Android Studio từ official website
# https://developer.android.com/studio

# Sau khi cài đặt, mở Android Studio và:
# 1. Install SDK Platforms (API 34+)
# 2. Install SDK Tools
# 3. Install NDK (nếu cần native development)
```

**Cài đặt KMP Plugin:**
1. Mở **Android Studio**
2. **File → Settings → Plugins**
3. Search "**Kotlin Multiplatform**"
4. Install và restart

### 1.2. Xcode Setup (macOS only)

```bash
# Install Xcode từ App Store hoặc:
xcode-select --install

# Verify installation:
xcode-select -p
```

### 1.3. Command Line Tools

```bash
# Install Homebrew (macOS)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install kdoctor (KMP environment checker)
brew install kdoctor

# Check environment
kdoctor
```

---

## 🆕 2. Tạo Project Đầu Tiên

### 2.1. Sử dụng KMP Wizard (Khuyến nghị)

1. **Truy cập:** [kmp.jetbrains.com](https://kmp.jetbrains.com/)
2. **Cấu hình project:**
   ```
   Project name: MyKMPApp
   Project ID: com.example.mykmapp
   Platforms: ✅ Android, ✅ iOS
   UI Framework: ✅ Compose Multiplatform
   ```
3. **Download** và extract project
4. **Open** trong Android Studio

### 2.2. Hoặc Sử dụng Android Studio

1. **File → New → Project**
2. **Chọn "Kotlin Multiplatform App"**
3. **Configuration:**
   ```
   Name: MyKMPApp
   Package: com.example.mykmapp
   Save location: [your-workspace]
   Language: Kotlin
   Build configuration: Kotlin DSL
   
   ✅ Add sample code
   ✅ Share UI between Android and iOS
   ```

---

## 🔧 3. Project Configuration

### 3.1. Gradle Configuration

**Kiểm tra `gradle/libs.versions.toml`:**
```toml
[versions]
kotlin = "2.1.0"
compose = "1.7.1"
composeMultiplatform = "1.7.1"
androidx-activityCompose = "1.9.3"
androidx-lifecycle = "2.8.7"
navigation = "2.8.5"
ktor = "3.0.2"
room = "2.7.1"
koin = "4.0.1"

[libraries]
kotlin-test = { module = "org.jetbrains.kotlin:kotlin-test", version.ref = "kotlin" }
androidx-activity-compose = { module = "androidx.activity:activity-compose", version.ref = "androidx-activityCompose" }
androidx-lifecycle-viewmodel = { module = "androidx.lifecycle:lifecycle-viewmodel", version.ref = "androidx-lifecycle" }
androidx-lifecycle-runtime-compose = { module = "androidx.lifecycle:lifecycle-runtime-compose", version.ref = "androidx-lifecycle" }
navigation-compose = { module = "org.jetbrains.androidx.navigation:navigation-compose", version.ref = "navigation" }

# Ktor
ktor-client-core = { module = "io.ktor:ktor-client-core", version.ref = "ktor" }
ktor-client-okhttp = { module = "io.ktor:ktor-client-okhttp", version.ref = "ktor" }
ktor-client-darwin = { module = "io.ktor:ktor-client-darwin", version.ref = "ktor" }
ktor-client-content-negotiation = { module = "io.ktor:ktor-client-content-negotiation", version.ref = "ktor" }
ktor-serialization-kotlinx-json = { module = "io.ktor:ktor-serialization-kotlinx-json", version.ref = "ktor" }

# Room
room-runtime = { module = "androidx.room:room-runtime", version.ref = "room" }
room-compiler = { module = "androidx.room:room-compiler", version.ref = "room" }
room-sqlite-bundled = { module = "androidx.room:room-sqlite-bundled", version.ref = "room" }

# Koin
koin-core = { module = "io.insert-koin:koin-core", version.ref = "koin" }
koin-compose = { module = "io.insert-koin:koin-compose", version.ref = "koin" }

[plugins]
kotlinMultiplatform = { id = "org.jetbrains.kotlin.multiplatform", version.ref = "kotlin" }
androidApplication = { id = "com.android.application", version.ref = "agp" }
androidLibrary = { id = "com.android.library", version.ref = "agp" }
jetbrainsCompose = { id = "org.jetbrains.compose", version.ref = "compose" }
compose-compiler = { id = "org.jetbrains.kotlin.plugin.compose", version.ref = "kotlin" }
kotlinx-serialization = { id = "org.jetbrains.kotlin.plugin.serialization", version.ref = "kotlin" }
room = { id = "androidx.room", version.ref = "room" }
ksp = { id = "com.google.devtools.ksp", version.ref = "ksp" }
```

### 3.2. Environment Variables (macOS)

**Add to `~/.zshrc` or `~/.bash_profile`:**
```bash
# Android SDK
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools

# Java
export JAVA_HOME=$(/usr/libexec/java_home)

# Reload shell
source ~/.zshrc  # or source ~/.bash_profile
```

---

## 🏃‍♂️ 4. First Run

### 4.1. Build và Run Android

```bash
cd MyKMPApp

# Build project
./gradlew assembleDebug

# Run trên emulator/device
./gradlew installDebug
```

**Hoặc trong Android Studio:**
1. **Select "composeApp"** configuration
2. **Choose Android device/emulator**
3. **Click Run ▶️**

### 4.2. Build và Run iOS (macOS only)

```bash
# Build iOS framework
./gradlew embedAndSignAppleFrameworkForXcode

# Open Xcode project
open iosApp/iosApp.xcodeproj
```

**Trong Xcode:**
1. **Select iOS Simulator** (iPhone 15 Pro)
2. **Click Run ▶️**

---

## ✅ 5. Verification Checklist

### 5.1. Environment Check
```bash
# Run kdoctor để check environment
kdoctor

# Expected output:
✅ Android Studio
✅ Xcode (macOS)
✅ Kotlin Multiplatform Mobile plugin
✅ Cocoapods (macOS)
```

### 5.2. Project Health Check
- [ ] Project builds successfully
- [ ] Android app runs trên emulator
- [ ] iOS app runs trên simulator (macOS)
- [ ] Shared code được sử dụng trong cả 2 platforms
- [ ] Navigation hoạt động
- [ ] No build warnings/errors

---

## 🐛 6. Troubleshooting

### 6.1. Common Issues

**🔴 "Module not found" khi build iOS:**
```bash
# Clean và rebuild
./gradlew clean
./gradlew build

# Hoặc trong Xcode:
# Product → Clean Build Folder
```

**🔴 "ANDROID_HOME not set":**
```bash
# Check current path
echo $ANDROID_HOME

# Set correctly:
export ANDROID_HOME=$HOME/Library/Android/sdk  # macOS
export ANDROID_HOME=$HOME/Android/Sdk          # Linux
```

**🔴 iOS build fails với "Command PhaseScriptExecution failed":**
```bash
# Ensure Xcode command line tools installed
xcode-select --install

# Update CocoaPods
sudo gem install cocoapods
pod repo update
```

**🔴 Gradle sync fails:**
```bash
# Invalidate caches
# Android Studio → File → Invalidate Caches and Restart

# Or delete .gradle folder
rm -rf .gradle
./gradlew clean build
```

### 6.2. Performance Issues

**Slow builds:**
```kotlin
// Add to gradle.properties
org.gradle.jvmargs=-Xmx4g -XX:MaxMetaspaceSize=512m
org.gradle.parallel=true
org.gradle.caching=true
kotlin.incremental=true
kotlin.incremental.multiplatform=true
```

---

## 📱 7. Next Steps

### 7.1. Immediate Goals
1. **Thêm một màn hình mới** với navigation
2. **Implement một API call** đơn giản
3. **Add local storage** với DataStore
4. **Write first unit test**

### 7.2. Learning Path
1. **Week 1-2:** Follow [ROADMAP.md](./ROADMAP.md) - Tuần 1-2
2. **Practice:** Build simple calculator app
3. **Study:** [PROJECT-STRUCTURE.md](./PROJECT-STRUCTURE.md) để hiểu architecture
4. **Code:** Implement Todo app theo checklist

### 7.3. Resources
- **📖 Documentation:** [RESOURCES.md](./RESOURCES.md)
- **✅ Progress Tracking:** [CHECKLIST.md](./CHECKLIST.md)
- **💬 Community:** Join [Kotlin Slack](https://kotlinlang.slack.com)

---

## 🎯 8. Quick Start Code Examples

### 8.1. Simple Screen với State

```kotlin
// composeApp/src/commonMain/kotlin/SimpleCounterScreen.kt
@Composable
fun SimpleCounterScreen() {
    var count by remember { mutableStateOf(0) }
    
    Column(
        modifier = Modifier.fillMaxSize().padding(16.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text(
            text = "Count: $count",
            style = MaterialTheme.typography.headlineMedium
        )
        
        Spacer(modifier = Modifier.height(16.dp))
        
        Row {
            Button(onClick = { count-- }) {
                Text("-")
            }
            
            Spacer(modifier = Modifier.width(16.dp))
            
            Button(onClick = { count++ }) {
                Text("+")
            }
        }
    }
}
```

### 8.2. Platform-Specific Code

```kotlin
// shared/src/commonMain/kotlin/Platform.kt
expect class Platform() {
    val name: String
}

expect fun getPlatform(): Platform

// shared/src/androidMain/kotlin/Platform.android.kt
actual class Platform actual constructor() {
    actual val name: String = "Android ${android.os.Build.VERSION.SDK_INT}"
}

actual fun getPlatform(): Platform = Platform()

// shared/src/iosMain/kotlin/Platform.ios.kt
import platform.UIKit.UIDevice

actual class Platform actual constructor() {
    actual val name: String = UIDevice.currentDevice.systemName() + " " + UIDevice.currentDevice.systemVersion
}

actual fun getPlatform(): Platform = Platform()
```

---

**🎉 Congratulations!** Bạn đã setup thành công Kotlin Multiplatform development environment. Giờ là lúc bắt đầu coding!

**📚 Next:** Đọc [ROADMAP.md](./ROADMAP.md) để bắt đầu learning journey của bạn.