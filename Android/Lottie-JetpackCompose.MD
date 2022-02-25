# Lottie For JetpackCompose
## 简介
一个动画库 For Jetpack Compose，并且跨平台
## 引入依赖 
``` Gradle
implementation 'com.airbnb.android:lottie-compose:5.0.1'
```
### 基本使用
``` Kotlin
val lottieComposition by rememberLottieComposition(spec = LottieCompositionSpec.Url("https://assets9.lottiefiles.com/packages/lf20_rbtawnwz.json"))
val lottieAnimationState by animateLottieCompositionAsState(composition = lottieComposition, iterations = LottieConstants.IterateForever)
LottieAnimation(composition = lottieComposition, progress = lottieAnimationState)
```
这边是最基本的使用  
下面是一些进阶东西的配置
``` Kotlin
// 对于加载方式，Lottie提供了其他方式  在 第一行中的 spec 使用
sealed interface LottieCompositionSpec {
    // 加载 res/raw 目录下的静态资源
    inline class RawRes(@androidx.annotation.RawRes val resId: Int) : LottieCompositionSpec

    // 加载 URL
    inline class Url(val url: String) : LottieCompositionSpec

    // 加载手机目录下的静态资源
    inline class File(val fileName: String) : LottieCompositionSpec

    // 加载 asset 目录下的静态资源
    inline class Asset(val assetName: String) : LottieCompositionSpec

    // 直接加载 json 字符串
    inline class JsonString(val jsonString: String) : LottieCompositionSpec
}
```
对于 lottieCompositionState 可以这么配置
``` Kotlin
val lottieAnimationState by animateLottieCompositionAsState (
    composition = lottieComposition, // 动画资源句柄 必填
    iterations = LottieConstants.IterateForever, // 播放次数 此处为永久循环
    isPlaying = true, // 动画播放状态
    speed = 1.0f, // 动画速度状态
    restartOnPlay = false // 暂停后重新播放是否从头开始
)
```