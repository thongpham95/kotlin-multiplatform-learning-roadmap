# 🚀 Hành trình chinh phục Kotlin Multiplatform

Chào mừng đến với kho lưu trữ cá nhân của tôi! Đây là nơi ghi lại toàn bộ lộ trình, tiến độ và các dự án thực hành trong hành trình 3 tháng để chinh phục **Kotlin Multiplatform (KMP)** và **Compose Multiplatform**.

## 🎯 Mục tiêu

Trở thành một lập trình viên có khả năng xây dựng ứng dụng full-stack (Android & iOS) bằng cách chia sẻ tối đa code logic và cả UI, sử dụng bộ công nghệ hiện đại nhất từ Kotlin.

---

## 🗺️ Lộ trình học tập chi tiết

Đây là kế hoạch chi tiết được chia thành 3 giai đoạn chính. Tôi sẽ đánh dấu ✔️ vào các mục đã hoàn thành để theo dõi tiến độ.

<details>
<summary><strong>🗓️ Tháng 1: Nền tảng KMP & Logic chung</strong></summary>

| Tuần | Ngày | Chủ đề | Nội dung & Thực hành | Tài liệu tham khảo | Trạng thái |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | **T2** | Giới thiệu `KMP` | - Hiểu triết lý & kiến trúc `KMP`.<br>- Vai trò của `commonMain`, `androidMain`, `iosMain`. | [Tổng quan về KMP](https://kotlinlang.org/docs/multiplatform-mobile-overview.html) | - [ ] |
| | **T4** | Cài đặt môi trường | - Cài đặt plugin `KMM`, `Xcode`.<br>- Chạy `kdoctor` để kiểm tra. | [Cài đặt môi trường](https://kotlinlang.org/docs/multiplatform-mobile-setup.html) | - [ ] |
| | **T6** | "Hello World!" | - Tạo dự án `KMP` bằng wizard.<br>- Build và chạy trên máy ảo Android & iOS. | [Tạo dự án đầu tiên](https://kotlinlang.org/docs/multiplatform-mobile-create-first-app.html) | - [ ] |
| **2** | **T2** | Cấu trúc dự án | - Khám phá các file `build.gradle.kts`.<br>- Tìm hiểu về `source set`. | [Chia sẻ code trong KMP](https://kotlinlang.org/docs/multiplatform-mobile-share-code.html) | - [ ] |
| | **T4** | `expect` / `actual` | - Học lý thuyết về `expect` (khai báo) và `actual` (triển khai). | [Platform-specific declarations](https://kotlinlang.org/docs/multiplatform-expect-actual.html) | - [ ] |
| | **T6** | Thực hành `e`/`a` | - Tạo hàm `getPlatformName()` và hiển thị kết quả lên UI. | [Ví dụ về expect/actual](https://play.kotlinlang.org/hands-on/Targeting%20iOS%20and%20Android%20with%20Kotlin%20Multiplatform/03_Using_platform_specific_APIs) | - [ ] |
| **3** | **T2** | Networking (`Ktor`) | - Tìm hiểu `Ktor Client`.<br>- Xử lý bất đồng bộ với `Coroutines`. | [Ktor client setup](https://ktor.io/docs/client-create-new-application.html) | - [ ] |
| | **T4** | Serialization | - Học `kotlinx.serialization`.<br>- Tạo data class với `@Serializable`. | [Kotlinx Serialization Guide](https://github.com/Kotlin/kotlinx.serialization/blob/master/docs/basic-serialization.md) | - [ ] |
| | **T6** | Dự án API nhỏ | - Gọi API, parse JSON và log kết quả ra console. | [Networking & Data Storage](https://www.kodeco.com/26496499-networking-and-data-storage-in-kmm) | - [ ] |
| **4** | **T2** | Kiến trúc `MVVM` | - Thiết kế một `SharedViewModel` cơ bản.<br>- Dùng `StateFlow` để giao tiếp với UI. | [Kiến trúc trong KMM](https://www.icerockdev.com/blog/mobile-app-architecture-for-kotlin-multiplatform) | - [ ] |
| | **T4** | Xây dựng ViewModel | - Tạo `ViewModel` chứa logic gọi API và quản lý trạng thái. | [MOKO MVVM](https://github.com/icerockdev/moko-mvvm) | - [ ] |
| | **T6** | Tái cấu trúc | - Refactor dự án API.<br>- UI Android lắng nghe `StateFlow`. | [KMM ViewModel Sample](https://github.com/touchlab/KMM-ViewModel) | - [ ] |

</details>

<details>
<summary><strong>🗓️ Tháng 2: Chuyên sâu & Tích hợp Native</strong></summary>

| Tuần | Ngày | Chủ đề | Nội dung & Thực hành | Tài liệu tham khảo | Trạng thái |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **5** | **T2** | Database (`SQLDelight`)| - Hiểu cách `SQLDelight` hoạt động.<br>- Cài đặt plugin & dependency. | [SQLDelight - Getting Started](https://cashapp.github.io/sqldelight/2.0.0/multiplatform/) | - [ ] |
| | **T4** | Viết câu lệnh SQL | - Viết câu lệnh SQL trong file `.sq`.<br>- Build dự án để `SQLDelight` tạo code. | [Viết câu lệnh SQL](https://cashapp.github.io/sqldelight/2.0.0/writing-sql/) | - [ ] |
| | **T6** | Dự án Ghi chú | - Tạo ứng dụng "Ghi chú" với các chức năng CRUD. | [KMM Note App Sample](https://github.com/Kashif-E/KMM-Note-App) | - [ ] |
| **6** | **T2** | Dependency Injection| - Tìm hiểu về `Koin` và cách nó hỗ trợ KMP. | [Koin for KMP](https://insert-koin.io/docs/setup/koin#kotlin-multiplatform) | - [ ] |
| | **T4** | Cài đặt `Koin` | - Thêm dependency.<br>- Viết file khởi tạo Koin cho Android & iOS. | [Koin - Start Koin](https://insert-koin.io/docs/reference/koin-core/start-koin) | - [ ] |
| | **T6** | Tích hợp `Koin` | - Áp dụng DI vào ứng dụng Ghi chú. | [PeopleInSpace Sample với Koin](https://github.com/joreilly/PeopleInSpace) | - [ ] |
| **7** | **T2** | Tương tác Kotlin-Swift| - Đọc về cách các kiểu dữ liệu Kotlin được chuyển đổi sang Swift. | [Swift/Objective-C interop](https://kotlinlang.org/docs/native-objc-interop.html) | - [ ] |
| | **T4** | Gọi API Native iOS | - Dùng `expect`/`actual` để gọi API gốc của iOS (ví dụ `UIDevice`). | [Calling iOS Frameworks from KMM](https://www.youtube.com/watch?v=ffypVvY1bM8) | - [ ] |
| | **T6** | Thực hành Interop | - Tạo hàm lấy phiên bản OS của thiết bị và hiển thị nó. | [Ví dụ thực tế về Interop](https://medium.com/proandroiddev/kotlin-multiplatform-mobile-call-platform-specific-api-s-expect-actual-8a11050e21a8) | - [ ] |
| **8** | **T2** | Testing trong `KMP` | - Tìm hiểu về source set `commonTest`.<br>- Thêm dependency `kotlin.test`. | [Testing multiplatform projects](https://kotlinlang.org/docs/multiplatform-testing.html) | - [ ] |
| | **T4** | Viết Unit Test | - Viết Unit Test cho `Repository` của ứng dụng Ghi chú. | [Unit Testing trong KMM](https://phauer.com/2022/unit-testing-kotlin-multiplatform/) | - [ ] |
| | **T6** | Test `ViewModel` | - Viết Unit Test để xác nhận các thay đổi trạng thái trong `SharedViewModel`. | [Cách test ViewModel trong KMM](https://github.com/arkivanov/MVIKotlin#testing-stores) | - [ ] |

</details>

<details>
<summary><strong>🗓️ Tháng 3: Giao diện với Compose Multiplatform & Hoàn thiện</strong></summary>

| Tuần | Ngày | Chủ đề | Nội dung & Thực hành | Tài liệu tham khảo | Trạng thái |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **9** | **T2** | Giới thiệu `Compose MP` | - Tìm hiểu cách `Compose` được render trên iOS.<br>- Cấu trúc project UI. | [Compose Multiplatform for iOS](https://www.jetbrains.com/help/kotlin-multiplatform-dev/compose-multiplatform-getting-started.html) | - [ ] |
| | **T4** | UI đầu tiên | - Tạo màn hình Compose đơn giản trong `commonMain`.<br>- Host trong `UIViewController`. | [Tạo UI chung đầu tiên](https://github.com/JetBrains/compose-multiplatform/blob/master/tutorials/Getting_Started_with_Compose_for_iOS/README.md) | - [ ] |
| | **T6** | Chuyển đổi UI | - Chuyển đổi UI của ứng dụng gọi API (Tháng 1) sang dùng `Compose MP`. | [Bắt đầu với Compose Multiplatform](https://www.youtube.com/watch?v=3uB5uYpGZkM) | - [ ] |
| **10**| **T2** | Navigation (Lý thuyết) | - Tìm hiểu thư viện `Decompose` hoặc `Voyager`. | [Decompose](https://github.com/arkivanov/Decompose) / [Voyager](https://github.com/adrielcafe/voyager) | - [ ] |
| | **T4** | Cài đặt Navigation | - Thêm dependency và cấu hình stack điều hướng cơ bản. | [Decompose Quick Start](https://arkivanov.github.io/Decompose/getting-started/) | - [ ] |
| | **T6** | Thực hành Navigation| - Áp dụng điều hướng vào ứng dụng API, chuyển màn hình. | [Decompose Sample Project](https://github.com/arkivanov/Decompose/tree/master/sample) | - [ ] |
| **11**| **T2** | Shared Resources | - Tìm hiểu thư viện `MOKO-Resources` để quản lý tài nguyên chung. | [MOKO-Resources](https://github.com/icerockdev/moko-resources) | - [ ] |
| | **T4** | Thực hành Resources | - Chuyển tất cả chuỗi text trong ứng dụng vào file `strings.xml` chung. | [Cách dùng với Strings](https://github.com/icerockdev/moko-resources#strings) | - [ ] |
| | **T6** | UI đặc thù | - Dùng `expect`/`actual` cho một `Composable` để gọi component gốc. | [UI đặc thù với expect/actual](https://www.kodeco.com/39373493-kotlin-multiplatform-tutorial-sharing-views-on-ios-android) | - [ ] |
| **12**| **T2** | Lên kế hoạch dự án | - Ôn tập và chọn ý tưởng cho dự án cuối khóa. | [KMP Sample Projects](https://github.com/Kotlin/kmp-samples) | - [ ] |
| | **T4** | `//TODO: Build Project` | - Xây dựng các chức năng cốt lõi của dự án cuối khóa. | - | - [ ] |
| | **T6** | `//RELEASE` | - Hoàn thiện và build ứng dụng ra file AAB/APK và Archive. | [Đóng gói App](https://developer.android.com/studio/publish) | - [ ] |

</details>

---

## 💻 Các dự án sẽ xây dựng

Trong quá trình học, tôi sẽ xây dựng các dự án nhỏ để áp dụng kiến thức:

1.  **Hello KMP:** Dự án khởi đầu để kiểm tra môi trường và cấu trúc.
2.  **API Consumer App:** Ứng dụng gọi API public để thực hành Networking, Serialization và `SharedViewModel`.
3.  **Notes App:** Ứng dụng ghi chú đơn giản để thực hành lưu trữ dữ liệu với `SQLDelight` và Dependency Injection với `Koin`.
4.  **Final Project (Chưa quyết định):** Một ứng dụng hoàn chỉnh kết hợp tất cả kiến thức đã học với `Compose Multiplatform`.

## 🛠️ Tech Stack & Công cụ

-   **Ngôn ngữ:** Kotlin
-   **Framework:** Kotlin Multiplatform, Compose Multiplatform
-   **Kiến trúc:** MVVM
-   **Networking:** Ktor
-   **Database:** SQLDelight
-   **Dependency Injection:** Koin
-   **Async:** Kotlin Coroutines
-   **IDE:** Android Studio & Xcode

---

> This repository is a living document of my learning journey. Feel free to follow along, star the repo if you find it useful, or open an issue if you have suggestions!
