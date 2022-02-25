# JetpackRoom 
## JetpackRoom 简介
Room 持久性库在 SQLite 的基础上提供了一个抽象层，让用户能够在充分利用 SQLite 的强大功能的同时，获享更强健的数据库访问机制。 -- Android Developers  
## 引入依赖 基本配置
``` Gradle
implementation "androidx.room:room-runtime:2.4.1"
kapt "androidx.room:room-compiler:2.4.1"
implementation "androidx.room:room-ktx:2.4.1"
```
之后导入一个 kotlin-kapt 插件
``` Gradle
plugins {
    id 'com.android.application'
    id 'org.jetbrains.kotlin.android'
    id 'kotlin-kapt'
}
```
下面要配置下kotlin一些修饰符啥的，避免编译的时候警告  
将这个放在 android-deafultConfig 里面  
``` Gradle
javaCompileOptions {
    annotationProcessorOptions {
        arguments += ["room.schemaLocation": "$projectDir/schemas".toString()]
    }
}
```
至此，基础配置结束
## 基本使用
### 建立数据库
AppDatabase.kt  
Sample 代码如下
``` Kotlin
package com.sanenchen.jetpackroom
import androidx.room.*
import kotlinx.coroutines.flow.Flow

@Entity
data class User(
    @PrimaryKey(autoGenerate = true) val id: Long,
    @ColumnInfo(name = "user") val user: String
)

@Dao
interface UserDao {
    @Insert
    fun insertUser(user: User)

    @Query("select * from User order by id desc")
    fun selectAll(): Flow<List<User>>

    @Query("delete from User")
    fun dropAll()

    @Query("delete from User where id=:ids")
    fun dropID(ids: String)
}

@Database(version = 1, entities = [User::class])
abstract class AppDatabase() : RoomDatabase() {
    abstract fun userDao(): UserDao
}
```
这里注意下查询时候用 Flow 包一下，Flow 可以转换为 LiveData，当然对于 JetpackCompose 来说，可以直接转换为它可以理解的形式  
简单来说，就是变量订阅，当数据更改时，自动更新界面
### 使用
``` Kotlin
val db = Room.databaseBuilder(applicationContext, AppDatabase::class.java, "database").allowMainThreadQueries().build()
// 简单说下查询吧，什么增添，删除就直接调用方法就好
val result = db.userDao().selectAll().collectAsState(listOf()).value
// 此处的 result 就可以直接被 JetpackCompose 所使用的
// 写下 Insert
db.userDao().insertUser(user)
```
## Done
