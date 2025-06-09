# 📖 Lộ Trình Học Kotlin Multiplatform - 8 Tuần

*Lộ trình chi tiết từ cơ bản đến production-ready*

## 🎯 Cấu Trúc Học Tập

**Tổng cộng:** 8 tuần × 3 buổi/tuần × 1-2 giờ/buổi = **24-48 giờ**

### 📅 Lịch Học Đề Xuất
- **Thứ 2:** Lý thuyết + Setup
- **Thứ 4:** Hands-on Coding
- **Thứ 6:** Thực hành + Review

---

## 🏗️ Tuần 1-2: Thiết Lập và Cơ Bản

### 📋 Tuần 1: Làm Quen Với KMP

#### **Buổi 1: Thiết Lập Môi Trường & Hello World** (2h)
**Mục tiêu:** Tạo project KMP đầu tiên

**Lý thuyết (45p):**
- Tổng quan KMP: Code sharing, targets, source sets
- So sánh Compose Multiplatform vs Jetpack Compose
- Cấu trúc project: `commonMain`, `androidMain`, `iosMain`

**Thực hành (75p):**
```bash
# Cài đặt tools
- Android Studio + KMP Plugin
- Xcode (macOS only)
- Tạo project bằng KMP Wizard
```

**Deliverable:**
- Chạy Hello World trên Android & iOS
- Hiểu cấu trúc file `build.gradle.kts`

#### **Buổi 2: Cấu Trúc Project & Gradle Config** (1.5h)
**Mục tiêu:** Hiểu sâu về build system

**Lý thuyết (30p):**
- Phân tích `build.gradle.kts`: sourceSets, dependencies, targets
- Android-KMP plugin vs traditional Android library

**Thực hành (60p):**
- Thêm Ktor dependency vào các source sets
- Tạo module mới với KMP template
- Configure Gradle cho multiple targets

#### **Buổi 3: Platform-Specific Code** (2h)
**Mục tiêu:** Làm chủ `expect/actual` declarations

**Lý thuyết (45p):**
- `expect/actual` pattern
- Interop với Swift/Objective-C
- Best practices cho platform code

**Thực hành (75p):**
```kotlin
// commonMain
expect class FileManager {
    fun readFile(path: String): String
}

// androidMain
actual class FileManager {
    actual fun readFile(path: String): String {
        // Android File API implementation
    }
}

// iosMain
actual class FileManager {
    actual fun readFile(path: String): String {
        // NSFileManager implementation
    }
}
```

### 📋 Tuần 2: Compose Multiplatform UI

#### **Buổi 4: Basic Components** (1.5h)
**Mục tiêu:** Làm chủ UI components cơ bản

**Lý thuyết (30p):**
- Text, Button, TextField, Image components
- Layout: Column, Row, Box
- Modifiers: padding, clickable, size

**Thực hành (60p):**
- Xây dựng form đăng nhập với validation
- Custom theme với MaterialTheme
- Responsive layout cho Android/iOS

#### **Buổi 5: Navigation & State Management** (2h)
**Mục tiêu:** Quản lý navigation và state

**Lý thuyết (45p):**
- Navigation Compose: NavController, NavHost
- State hoisting: remember, mutableStateOf
- Lifecycle awareness trong KMP

**Thực hành (75p):**
```kotlin
@Composable
fun AppNavigation() {
    val navController = rememberNavController()
    NavHost(navController, startDestination = "login") {
        composable("login") { LoginScreen(navController) }
        composable("home") { HomeScreen(navController) }
        composable("profile") { ProfileScreen(navController) }
    }
}
```

#### **Buổi 6: Platform-Specific UI** (2h)
**Mục tiêu:** Tích hợp native UI components

**Thực hành (120p):**
- Nhúng Google Maps (Android) + MapKit (iOS)
- Custom platform UI với expect/actual
- Handle platform-specific gestures

---

## 🌐 Tuần 3-4: Networking & Data Layer

### 📋 Tuần 3: Networking với Ktor

#### **Buổi 7: Ktor Client Setup** (2h)
**Mục tiêu:** Thiết lập networking layer

**Lý thuyết (30p):**
- Ktor engines: OkHttp (Android), Darwin (iOS)
- JSON serialization với kotlinx.serialization
- Error handling và timeout

**Thực hành (90p):**
```kotlin
val httpClient = HttpClient {
    install(ContentNegotiation) {
        json(Json {
            prettyPrint = true
            isLenient = true
            ignoreUnknownKeys = true
        })
    }
    install(Logging) {
        logger = Logger.DEFAULT
        level = LogLevel.BODY
    }
}

suspend fun fetchUsers(): List<User> {
    return httpClient.get("https://jsonplaceholder.typicode.com/users")
        .body()
}
```

#### **Buổi 8: Room KMP & SQLDelight** (2h)
**Mục tiêu:** Local database implementation

**Lý thuyết (45p):**
- So sánh Room KMP vs SQLDelight
- Database migration strategies
- Transaction management

**Thực hành (75p):**
```kotlin
@Database(
    entities = [UserEntity::class],
    version = 1
)
@ConstructedBy(AppDatabaseConstructor::class)
abstract class AppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
}

@Suppress("NO_ACTUAL_FOR_EXPECT")
expect object AppDatabaseConstructor : RoomDatabaseConstructor<AppDatabase>
```

#### **Buổi 9: DataStore Multiplatform** (1.5h)
**Mục tiêu:** Preferences và session management

**Thực hành (90p):**
- Setup DataStore cho user preferences
- Store/retrieve authentication tokens
- Sync data across app sessions

### 📋 Tuần 4: Data Repository Pattern

#### **Buổi 10: Repository Implementation** (2h)
**Mục tiêu:** Implement Repository pattern

**Thực hành (120p):**
```kotlin
interface UserRepository {
    suspend fun getUsers(): Flow<List<User>>
    suspend fun getUser(id: String): User?
    suspend fun saveUser(user: User)
}

class UserRepositoryImpl(
    private val apiService: UserApiService,
    private val userDao: UserDao
) : UserRepository {
    override suspend fun getUsers(): Flow<List<User>> = flow {
        // Cache-first strategy
        emit(userDao.getAllUsers())
        try {
            val remoteUsers = apiService.getUsers()
            userDao.insertUsers(remoteUsers)
            emit(userDao.getAllUsers())
        } catch (e: Exception) {
            // Handle error
        }
    }
}
```

#### **Buổi 11: Offline-First Architecture** (2h)
**Mục tiêu:** Sync strategy và offline support

**Thực hành (120p):**
- Implement cache-first strategy
- Network connectivity detection
- Sync queue cho offline actions

#### **Buổi 12: Error Handling & Loading States** (1.5h)
**Mục tiêu:** Robust error handling

**Thực hành (90p):**
- Result wrapper class
- Loading, Success, Error states
- Retry mechanisms

---

## 🏛️ Tuần 5-6: Clean Architecture & DI

### 📋 Tuần 5: Clean Architecture

#### **Buổi 13: Layer Separation** (2h)
**Mục tiêu:** Tách biệt concerns theo layers

**Lý thuyết (45p):**
- Data Layer: Repository, DataSource, Models
- Domain Layer: Use Cases, Business Logic
- Presentation Layer: ViewModels, UI State

**Thực hành (75p):**
```
:shared
├── data/
│   ├── repository/
│   ├── datasource/
│   └── model/
├── domain/
│   ├── usecase/
│   ├── repository/
│   └── model/
└── presentation/
    ├── viewmodel/
    └── state/
```

#### **Buổi 14: Use Cases & Business Logic** (1.5h)
**Mục tiêu:** Implement business logic layer

**Thực hành (90p):**
```kotlin
class GetUsersUseCase(
    private val userRepository: UserRepository
) {
    suspend operator fun invoke(): Flow<Resource<List<User>>> = flow {
        emit(Resource.Loading())
        try {
            userRepository.getUsers().collect { users ->
                emit(Resource.Success(users))
            }
        } catch (e: Exception) {
            emit(Resource.Error(e.message ?: "Unknown error"))
        }
    }
}
```

#### **Buổi 15: Koin Multiplatform DI** (2h)
**Mục tiêu:** Dependency injection setup

**Thực hành (120p):**
```kotlin
val dataModule = module {
    single<HttpClient> { createHttpClient() }
    single<AppDatabase> { createDatabase() }
    single<UserRepository> { UserRepositoryImpl(get(), get()) }
}

val domainModule = module {
    factory { GetUsersUseCase(get()) }
    factory { GetUserUseCase(get()) }
}

val presentationModule = module {
    factory { UserListViewModel(get()) }
    factory { UserDetailViewModel(get()) }
}
```

### 📋 Tuần 6: Design Patterns & State Management

#### **Buổi 16: MVI Pattern** (2h)
**Mục tiêu:** Implement MVI architecture

**Thực hành (120p):**
```kotlin
data class UserListState(
    val users: List<User> = emptyList(),
    val isLoading: Boolean = false,
    val error: String? = null
)

sealed class UserListIntent {
    object LoadUsers : UserListIntent()
    data class SelectUser(val user: User) : UserListIntent()
    object Refresh : UserListIntent()
}

class UserListViewModel : ViewModel() {
    private val _state = MutableStateFlow(UserListState())
    val state = _state.asStateFlow()
    
    fun handleIntent(intent: UserListIntent) {
        when (intent) {
            is UserListIntent.LoadUsers -> loadUsers()
            // Handle other intents
        }
    }
}
```

#### **Buổi 17: State Persistence** (1.5h)
**Mục tiêu:** Persist UI state across configurations

**Thực hành (90p):**
- SavedStateHandle trong KMP
- State restoration strategies
- Navigation state persistence

#### **Buổi 18: Testing Strategy** (2h)
**Mục tiêu:** Unit testing approach

**Thực hành (120p):**
```kotlin
class GetUsersUseCaseTest {
    @Test
    fun `should return users when repository succeeds`() = runTest {
        // Given
        val mockRepository = mockk<UserRepository>()
        val useCase = GetUsersUseCase(mockRepository)
        
        // When & Then
        useCase().test {
            assertEquals(Resource.Loading(), awaitItem())
            assertEquals(Resource.Success(expectedUsers), awaitItem())
            awaitComplete()
        }
    }
}
```

---

## 🚀 Tuần 7-8: Production & Deployment

### 📋 Tuần 7: Optimization & Performance

#### **Buổi 19: Build Optimization** (1.5h)
**Mục tiêu:** Tối ưu build time và performance

**Thực hành (90p):**
- Gradle build cache configuration
- Kotlin/Native memory model
- R8/ProGuard rules cho KMP

#### **Buổi 20: Error Monitoring** (2h)
**Mục tiêu:** Production error tracking

**Thực hành (120p):**
- Crashlytics integration (Android)
- iOS crash reporting
- Custom logging solutions

#### **Buổi 21: Performance Profiling** (2h)
**Mục tiêu:** Memory và performance analysis

**Thực hành (120p):**
- Android Studio profiler với KMP
- Xcode Instruments cho iOS
- Memory leak detection

### 📋 Tuần 8: CI/CD & Deployment

#### **Buổi 22: GitHub Actions Setup** (2h)
**Mục tiêu:** Automated testing và building

**Thực hành (120p):**
```yaml
name: KMP CI
on: [push, pull_request]
jobs:
  test:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
      - name: Run tests
        run: ./gradlew testDebugUnitTest
      - name: Build iOS
        run: ./gradlew linkDebugFrameworkIosSimulatorArm64
```

#### **Buổi 23: Android Deployment** (1.5h)
**Mục tiêu:** Deploy lên Google Play

**Thực hành (90p):**
- Build Android App Bundle
- Play Console upload với Fastlane
- Staged rollout strategies

#### **Buổi 24: iOS Deployment** (2h)
**Mục tiêu:** Deploy lên App Store

**Thực hành (120p):**
- Xcode Archive process
- TestFlight distribution
- App Store submission với Fastlane

---

## 🎯 Dự Án Tổng Hợp

### **Todo List App** - Production Ready
**Yêu cầu:**
- Authentication (JWT)
- CRUD operations với offline sync
- Push notifications (Firebase + APNs)
- Dark/Light theme
- Localization (EN/VI)

**Tech Stack:**
```
📱 UI: Compose Multiplatform
🌐 Networking: Ktor Client
💾 Database: Room KMP
🔧 DI: Koin
🧪 Testing: kotlin.test + Mockk
🚀 CI/CD: GitHub Actions + Fastlane
```

**Timeline:** Tuần 7-8 (song song với deployment topics)

## 📈 Đánh Giá Tiến Độ

### 🎖️ Milestones
- **Tuần 2:** ✅ Chạy app đơn giản trên cả Android & iOS
- **Tuần 4:** ✅ Hoàn thành networking & local storage
- **Tuần 6:** ✅ Implement Clean Architecture hoàn chỉnh  
- **Tuần 8:** ✅ Deploy app lên stores

### 📝 Self-Assessment
Sau mỗi tuần, đánh giá bản thân:
- **Hiểu concept:** 1-5 ⭐
- **Implement được:** 1-5 ⭐
- **Tự tin apply:** 1-5 ⭐

**Mục tiêu:** Đạt tối thiểu 4⭐ trước khi chuyển tuần tiếp theo

## 🔗 Resources Mỗi Tuần

| Tuần | Official Docs | Video Tutorial | Sample Code |
|------|---------------|----------------|-------------|
| 1-2 | [KMP Basics](https://kotlinlang.org/docs/multiplatform-get-started.html) | [Setup Guide](https://www.youtube.com/watch?v=mdGIRnMRxyk) | [Hello World](https://github.com/JetBrains/compose-multiplatform) |
| 3-4 | [Ktor Docs](https://ktor.io/docs/client.html) | [Networking Tutorial](https://www.youtube.com/watch?v=qrNjSNOGwng) | [Network Sample](https://github.com/ktorio/ktor-samples) |
| 5-6 | [Clean Architecture](https://developer.android.com/topic/architecture) | [Architecture Guide](https://www.youtube.com/watch?v=4jNenCLwzxQ) | [Architecture Sample](https://github.com/skydoves/android-developer-roadmap) |
| 7-8 | [KMP Production](https://kotlinlang.org/docs/multiplatform-publish-lib.html) | [CI/CD Tutorial](https://www.youtube.com/watch?v=8D5YCvMDCIw) | [Production Sample](https://github.com/JetBrains/kotlinconf-app) |

---

**💡 Tips:**
- Code mỗi ngày ít nhất 30 phút
- Join [KotlinLang Slack](https://kotlinlang.slack.com) để hỏi đáp
- Follow [Official KMP Blog](https://blog.jetbrains.com/kotlin/category/multiplatform/) để cập nhật
- Tham gia [Community Events](https://kotlinlang.org/community/events/) để networking
