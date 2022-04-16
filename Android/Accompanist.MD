# Accompanist
## Accompanist SystemUIController
快速改变状态栏的颜色，以及深色以及浅色模式
### 引入依赖
``` Gradle
implementation "com.google.accompanist:accompanist-systemuicontroller:0.24.3-alpha"
```
### 简单使用
``` kotlin
    val systemUiController = rememberSystemUiController()
    systemUiController.setStatusBarColor(Color.Transparent, !isSystemInDarkTheme())
```
## Accompanist Insets
Compose 的沉浸式状态栏
### 引入依赖
``` Gradle
implementation "com.google.accompanist:accompanist-insets:0.24.3-alpha"
implementation "com.google.accompanist:accompanist-insets-ui:0.24.3-alpha"
```
### 简单使用
``` kotlin
// 每个 Activity 都要写
WindowCompat.setDecorFitsSystemWindows(window, false)
// 用 ProvideWindowInsets 包住就好
ProvideWindowInsets {
    // Your UI Code
}
```
