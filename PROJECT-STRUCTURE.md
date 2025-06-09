# 🏗️ Cấu Trúc Project Kotlin Multiplatform

*Template và best practices cho việc tổ chức project KMP*

---

## 📂 1. Cấu Trúc Thư Mục Cơ Bản

```
my-kmp-app/
├── composeApp/                          # Main application module
│   ├── src/
│   │   ├── commonMain/kotlin/           # Shared UI code
│   │   │   ├── ui/
│   │   │   │   ├── components/          # Reusable UI components
│   │   │   │   ├── screens/             # Screen-level composables
│   │   │   │   └── theme/               # Design system
│   │   │   ├── navigation/              # Navigation logic
│   │   │   └── App.kt                   # Root composable
│   │   ├── androidMain/kotlin/          # Android-specific UI code
│   │   │   └── MainActivity.kt
│   │   ├── iosMain/kotlin/              # iOS-specific UI code
│   │   │   └── MainViewController.kt
│   │   ├── commonTest/kotlin/           # Shared UI tests
│   │   ├── androidUnitTest/kotlin/      # Android unit tests
│   │   └── iosTest/kotlin/              # iOS tests
│   └── build.gradle.kts
├── shared/                              # Business logic module
│   ├── src/
│   │   ├── commonMain/kotlin/           # Shared business logic
│   │   │   ├── data/                    # Data layer
│   │   │   │   ├── repository/          # Repository implementations
│   │   │   │   ├── datasource/          # Data sources (API, Database)
│   │   │   │   ├── model/               # Data models
│   │   │   │   └── mapper/              # Data mapping
│   │   │   ├── domain/                  # Domain layer
│   │   │   │   ├── usecase/             # Use cases
│   │   │   │   ├── repository/          # Repository interfaces
│   │   │   │   └── model/               # Domain models
│   │   │   ├── presentation/            # Presentation layer
│   │   │   │   ├── viewmodel/           # ViewModels
│   │   │   │   └── state/               # UI states
│   │   │   └── di/                      # Dependency injection
│   │   ├── androidMain/kotlin/          # Android-specific implementations
│   │   │   ├── data/
│   │   │   │   └── database/            # Room database
│   │   │   └── di/                      # Android DI modules
│   │   ├── iosMain/kotlin/              # iOS-specific implementations
│   │   │   ├── data/
│   │   │   │   └── database/            # Core Data or SQLite
│   │   │   └── di/                      # iOS DI modules
│   │   ├── commonTest/kotlin/           # Shared tests
│   │   ├── androidUnitTest/kotlin/      # Android unit tests
│   │   └── iosTest/kotlin/              # iOS tests
│   └── build.gradle.kts
├── iosApp/                              # iOS application
│   ├── iosApp/
│   │   ├── ContentView.swift
│   │   └── iosAppApp.swift
│   └── iosApp.xcodeproj/
├── gradle/
│   └── wrapper/
├── build.gradle.kts                     # Root build file
├── gradle.properties
├── settings.gradle.kts
└── README.md
```

---

## 📋 2. Build Configuration

### 2.1. Root `build.gradle.kts`

```kotlin
plugins {
    // KMP plugins
    alias(libs.plugins.kotlinMultiplatform) apply false
    alias(libs.plugins.androidApplication) apply false
    alias(libs.plugins.androidLibrary) apply false
    alias(libs.plugins.jetbrainsCompose) apply false
    alias(libs.plugins.compose.compiler) apply false
    
    // Room KMP
    alias(libs.plugins.room) apply false
    alias(libs.plugins.ksp) apply false
    
    // Serialization
    alias(libs.plugins.kotlinx.serialization) apply false
}
```

### 2.2. Shared Module `build.gradle.kts`

```kotlin
plugins {
    alias(libs.plugins.kotlinMultiplatform)
    alias(libs.plugins.androidLibrary)
    alias(libs.plugins.jetbrainsCompose)
    alias(libs.plugins.compose.compiler)
    alias(libs.plugins.kotlinx.serialization)
    alias(libs.plugins.room)
    alias(libs.plugins.ksp)
}

kotlin {
    androidTarget {
        compilations.all {
            kotlinOptions {
                jvmTarget = "11"
            }
        }
    }
    
    listOf(
        iosX64(),
        iosArm64(),
        iosSimulatorArm64()
    ).forEach { iosTarget ->
        iosTarget.binaries.framework {
            baseName = "Shared"
            isStatic = true
        }
    }
    
    sourceSets {
        commonMain.dependencies {
            // Compose Multiplatform
            implementation(compose.runtime)
            implementation(compose.foundation)
            implementation(compose.material3)
            implementation(compose.ui)
            implementation(compose.components.resources)
            implementation(compose.components.uiToolingPreview)
            
            // Navigation
            implementation(libs.navigation.compose)
            
            // Networking
            implementation(libs.ktor.client.core)
            implementation(libs.ktor.client.content.negotiation)
            implementation(libs.ktor.serialization.kotlinx.json)
            implementation(libs.ktor.client.logging)
            
            // Database
            implementation(libs.room.runtime)
            implementation(libs.room.sqlite.bundled)
            
            // DataStore
            implementation(libs.datastore.preferences)
            
            // Dependency Injection
            implementation(libs.koin.core)
            implementation(libs.koin.compose)
            
            // Coroutines
            implementation(libs.kotlinx.coroutines.core)
            
            // DateTime
            implementation(libs.kotlinx.datetime)
            
            // Serialization
            implementation(libs.kotlinx.serialization.json)
        }
        
        androidMain.dependencies {
            implementation(libs.ktor.client.okhttp)
            implementation(libs.koin.android)
        }
        
        iosMain.dependencies {
            implementation(libs.ktor.client.darwin)
        }
        
        commonTest.dependencies {
            implementation(libs.kotlin.test)
            implementation(libs.kotlinx.coroutines.test)
            implementation(libs.turbine)
        }
    }
}

android {
    namespace = "com.example.shared"
    compileSdk = 35
    
    defaultConfig {
        minSdk = 24
    }
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_11
        targetCompatibility = JavaVersion.VERSION_11
    }
}

room {
    schemaDirectory("$projectDir/schemas")
}

dependencies {
    add("kspCommonMainMetadata", libs.room.compiler)
}

tasks.withType<org.jetbrains.kotlin.gradle.dsl.KotlinCompile<*>>().configureEach {
    if (name != "kspCommonMainKotlinMetadata") {
        dependsOn("kspCommonMainKotlinMetadata")
    }
}
```

### 2.3. App Module `build.gradle.kts`

```kotlin
plugins {
    alias(libs.plugins.kotlinMultiplatform)
    alias(libs.plugins.androidApplication)
    alias(libs.plugins.jetbrainsCompose)
    alias(libs.plugins.compose.compiler)
}

kotlin {
    androidTarget {
        compilations.all {
            kotlinOptions {
                jvmTarget = "11"
            }
        }
    }
    
    listOf(
        iosX64(),
        iosArm64(),
        iosSimulatorArm64()
    ).forEach { iosTarget ->
        iosTarget.binaries.framework {
            baseName = "ComposeApp"
            isStatic = true
        }
    }
    
    sourceSets {
        androidMain.dependencies {
            implementation(compose.preview)
            implementation(libs.androidx.activity.compose)
        }
        commonMain.dependencies {
            implementation(compose.runtime)
            implementation(compose.foundation)
            implementation(compose.material3)
            implementation(compose.ui)
            implementation(compose.components.resources)
            implementation(compose.components.uiToolingPreview)
            implementation(libs.androidx.lifecycle.viewmodel)
            implementation(libs.androidx.lifecycle.runtime.compose)
            implementation(projects.shared)
        }
    }
}

android {
    namespace = "com.example.mykmapp"
    compileSdk = 35

    defaultConfig {
        applicationId = "com.example.mykmapp"
        minSdk = 24
        targetSdk = 35
        versionCode = 1
        versionName = "1.0"
    }
    packaging {
        resources {
            excludes += "/META-INF/{AL2.0,LGPL2.1}"
        }
    }
    buildTypes {
        getByName("release") {
            isMinifyEnabled = false
        }
    }
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_11
        targetCompatibility = JavaVersion.VERSION_11
    }
}
```

---

## 🏗️ 3. Architecture Layers

### 3.1. Data Layer

```kotlin
// shared/src/commonMain/kotlin/data/model/UserDto.kt
@Serializable
data class UserDto(
    val id: Int,
    val name: String,
    val email: String,
    val phone: String?
)

// shared/src/commonMain/kotlin/data/datasource/UserApiService.kt
interface UserApiService {
    suspend fun getUsers(): List<UserDto>
    suspend fun getUser(id: Int): UserDto
    suspend fun createUser(user: UserDto): UserDto
}

class UserApiServiceImpl(
    private val httpClient: HttpClient
) : UserApiService {
    override suspend fun getUsers(): List<UserDto> {
        return httpClient.get("users").body()
    }
    
    override suspend fun getUser(id: Int): UserDto {
        return httpClient.get("users/$id").body()
    }
    
    override suspend fun createUser(user: UserDto): UserDto {
        return httpClient.post("users") {
            contentType(ContentType.Application.Json)
            setBody(user)
        }.body()
    }
}

// shared/src/commonMain/kotlin/data/repository/UserRepositoryImpl.kt
class UserRepositoryImpl(
    private val apiService: UserApiService,
    private val userDao: UserDao
) : UserRepository {
    override suspend fun getUsers(): Flow<List<User>> = flow {
        // Cache-first strategy
        emit(userDao.getAllUsers().map { it.toDomain() })
        
        try {
            val remoteUsers = apiService.getUsers()
            val entities = remoteUsers.map { it.toEntity() }
            userDao.insertUsers(entities)
            emit(userDao.getAllUsers().map { it.toDomain() })
        } catch (e: Exception) {
            // Log error but continue with cached data
        }
    }
}
```

### 3.2. Domain Layer

```kotlin
// shared/src/commonMain/kotlin/domain/model/User.kt
data class User(
    val id: Int,
    val name: String,
    val email: String,
    val phone: String?
)

// shared/src/commonMain/kotlin/domain/repository/UserRepository.kt
interface UserRepository {
    suspend fun getUsers(): Flow<List<User>>
    suspend fun getUser(id: Int): User?
    suspend fun saveUser(user: User)
    suspend fun deleteUser(id: Int)
}

// shared/src/commonMain/kotlin/domain/usecase/GetUsersUseCase.kt
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

### 3.3. Presentation Layer

```kotlin
// shared/src/commonMain/kotlin/presentation/state/UserListState.kt
data class UserListState(
    val users: List<User> = emptyList(),
    val isLoading: Boolean = false,
    val error: String? = null
)

// shared/src/commonMain/kotlin/presentation/viewmodel/UserListViewModel.kt
class UserListViewModel(
    private val getUsersUseCase: GetUsersUseCase
) : ViewModel() {
    
    private val _state = MutableStateFlow(UserListState())
    val state = _state.asStateFlow()
    
    init {
        loadUsers()
    }
    
    fun loadUsers() {
        viewModelScope.launch {
            getUsersUseCase().collect { resource ->
                _state.value = when (resource) {
                    is Resource.Loading -> _state.value.copy(isLoading = true, error = null)
                    is Resource.Success -> _state.value.copy(
                        users = resource.data,
                        isLoading = false,
                        error = null
                    )
                    is Resource.Error -> _state.value.copy(
                        isLoading = false,
                        error = resource.message
                    )
                }
            }
        }
    }
    
    fun refresh() {
        loadUsers()
    }
}
```

---

## 🔧 4. Dependency Injection Setup

### 4.1. Koin Modules

```kotlin
// shared/src/commonMain/kotlin/di/NetworkModule.kt
val networkModule = module {
    single<HttpClient> {
        HttpClient {
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
    }
    
    single<UserApiService> { UserApiServiceImpl(get()) }
}

// shared/src/commonMain/kotlin/di/DatabaseModule.kt
val databaseModule = module {
    single<AppDatabase> { createDatabase() }
    single<UserDao> { get<AppDatabase>().userDao() }
}

// shared/src/commonMain/kotlin/di/RepositoryModule.kt
val repositoryModule = module {
    single<UserRepository> { UserRepositoryImpl(get(), get()) }
}

// shared/src/commonMain/kotlin/di/UseCaseModule.kt
val useCaseModule = module {
    factory { GetUsersUseCase(get()) }
    factory { GetUserUseCase(get()) }
    factory { SaveUserUseCase(get()) }
}

// shared/src/commonMain/kotlin/di/ViewModelModule.kt
val viewModelModule = module {
    factory { UserListViewModel(get()) }
    factory { UserDetailViewModel(get(), get()) }
}
```

### 4.2. Platform-Specific Modules

```kotlin
// shared/src/androidMain/kotlin/di/PlatformModule.kt
val androidModule = module {
    single<Context> { androidContext() }
    single<HttpClient> {
        HttpClient(OkHttp) {
            install(ContentNegotiation) {
                json()
            }
        }
    }
}

// shared/src/iosMain/kotlin/di/PlatformModule.kt
val iosModule = module {
    single<HttpClient> {
        HttpClient(Darwin) {
            install(ContentNegotiation) {
                json()
            }
        }
    }
}
```

---

## 📱 5. UI Structure

### 5.1. App Entry Point

```kotlin
// composeApp/src/commonMain/kotlin/App.kt
@Composable
fun App() {
    MaterialTheme {
        AppNavigation()
    }
}

// composeApp/src/commonMain/kotlin/navigation/AppNavigation.kt
@Composable
fun AppNavigation() {
    val navController = rememberNavController()
    
    NavHost(
        navController = navController,
        startDestination = "user_list"
    ) {
        composable("user_list") {
            UserListScreen(
                onUserClick = { user ->
                    navController.navigate("user_detail/${user.id}")
                }
            )
        }
        
        composable(
            route = "user_detail/{userId}",
            arguments = listOf(navArgument("userId") { type = NavType.IntType })
        ) { backStackEntry ->
            val userId = backStackEntry.arguments?.getInt("userId") ?: 0
            UserDetailScreen(
                userId = userId,
                onBackClick = { navController.popBackStack() }
            )
        }
    }
}
```

### 5.2. Screen Examples

```kotlin
// composeApp/src/commonMain/kotlin/ui/screens/UserListScreen.kt
@Composable
fun UserListScreen(
    viewModel: UserListViewModel = koinViewModel(),
    onUserClick: (User) -> Unit
) {
    val state by viewModel.state.collectAsState()
    
    Column(
        modifier = Modifier.fillMaxSize().padding(16.dp)
    ) {
        when {
            state.isLoading -> {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    CircularProgressIndicator()
                }
            }
            
            state.error != null -> {
                Column {
                    Text(
                        text = "Error: ${state.error}",
                        color = MaterialTheme.colorScheme.error
                    )
                    Button(
                        onClick = { viewModel.refresh() }
                    ) {
                        Text("Retry")
                    }
                }
            }
            
            else -> {
                LazyColumn {
                    items(state.users) { user ->
                        UserItem(
                            user = user,
                            onClick = { onUserClick(user) }
                        )
                    }
                }
            }
        }
    }
}

@Composable
fun UserItem(
    user: User,
    onClick: () -> Unit
) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(vertical = 4.dp)
            .clickable { onClick() }
    ) {
        Column(
            modifier = Modifier.padding(16.dp)
        ) {
            Text(
                text = user.name,
                style = MaterialTheme.typography.titleMedium
            )
            Text(
                text = user.email,
                style = MaterialTheme.typography.bodyMedium,
                color = MaterialTheme.colorScheme.onSurfaceVariant
            )
        }
    }
}
```

---

## 🧪 6. Testing Structure

### 6.1. Common Tests

```kotlin
// shared/src/commonTest/kotlin/domain/usecase/GetUsersUseCaseTest.kt
class GetUsersUseCaseTest {
    
    private val mockRepository = mockk<UserRepository>()
    private val useCase = GetUsersUseCase(mockRepository)
    
    @Test
    fun `should emit loading then success when repository returns data`() = runTest {
        // Given
        val expectedUsers = listOf(
            User(1, "John Doe", "john@example.com", null)
        )
        every { mockRepository.getUsers() } returns flowOf(expectedUsers)
        
        // When & Then
        useCase().test {
            assertEquals(Resource.Loading<List<User>>(), awaitItem())
            assertEquals(Resource.Success(expectedUsers), awaitItem())
            awaitComplete()
        }
    }
    
    @Test
    fun `should emit loading then error when repository throws exception`() = runTest {
        // Given
        val exception = RuntimeException("Network error")
        every { mockRepository.getUsers() } returns flow { throw exception }
        
        // When & Then
        useCase().test {
            assertEquals(Resource.Loading<List<User>>(), awaitItem())
            assertEquals(Resource.Error<List<User>>("Network error"), awaitItem())
            awaitComplete()
        }
    }
}
```

### 6.2. ViewModel Tests

```kotlin
// shared/src/commonTest/kotlin/presentation/viewmodel/UserListViewModelTest.kt
class UserListViewModelTest {
    
    private val mockGetUsersUseCase = mockk<GetUsersUseCase>()
    private lateinit var viewModel: UserListViewModel
    
    @BeforeTest
    fun setup() {
        viewModel = UserListViewModel(mockGetUsersUseCase)
    }
    
    @Test
    fun `should update state to loading then success when use case returns data`() = runTest {
        // Given
        val expectedUsers = listOf(
            User(1, "John Doe", "john@example.com", null)
        )
        every { mockGetUsersUseCase() } returns flowOf(
            Resource.Loading(),
            Resource.Success(expectedUsers)
        )
        
        // When
        viewModel.loadUsers()
        
        // Then
        viewModel.state.test {
            val loadingState = awaitItem()
            assertTrue(loadingState.isLoading)
            assertNull(loadingState.error)
            
            val successState = awaitItem()
            assertFalse(successState.isLoading)
            assertEquals(expectedUsers, successState.users)
            assertNull(successState.error)
        }
    }
}
```

---

**📝 Lưu ý:** Cấu trúc này có thể được customize dựa trên yêu cầu cụ thể của project. Hãy bắt đầu với structure đơn giản và evolve theo thời gian.

**🔧 Tools hỗ trợ:**
- Android Studio Project Templates
- JetBrains KMP Wizard
- Gradle Build Scripts
- Version Catalogs (libs.versions.toml)