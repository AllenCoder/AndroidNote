#gradle 生成字段属性值

>1.在工程目录下配置gradle.properties文件：

```
# Project-wide Gradle settings.

# IDE (e.g. Android Studio) users:
# Gradle settings configured through the IDE *will override*
# any settings specified in this file.

# For more details on how to configure your build environment visit
# http://www.gradle.org/docs/current/userguide/build_environment.html

# Specifies the JVM arguments used for the daemon process.
# The setting is particularly useful for tweaking memory settings.
# Default value: -Xmx10248m -XX:MaxPermSize=256m
# org.gradle.jvmargs=-Xmx2048m -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8

# When configured, Gradle will run in incubating parallel mode.
# This option should only be used with decoupled projects. More details, visit
# http://www.gradle.org/docs/current/userguide/multi_project_builds.html#sec:decoupled_projects
# org.gradle.parallel=true
android.useDeprecatedNdk=true
passcodelock.password_salt=11-maggio-2014-osvaldo-al-49novesimo!
passcodelock.password_enc_secret=5-maggio-2002-Karel-Poborsky
```

在末尾加上了三句 
>2.在你的APP目录下编辑build.gradle文件

```
	android.buildTypes.all { buildType ->
    project.properties.any { property ->
        if (property.key.toLowerCase().startsWith("passcodelock.")) {
            buildType.buildConfigField "String", property.key.replace("passcodelock.", "").replace(".", "_").toUpperCase(), "\"${property.value}\""
        }
    }
}

```

----------------
>3.编译你的工程 
>4.之后就可以在你的工程能随意调用你生成的字段了
BuildConfig.PASSWORD_PREFERENCE_KEY

----------------
```gradle

  // Fields from build type: debug
  
  public static final String PASSWORD_ENC_SECRET = "PASSWORD_ENC_SECRET";
  
  public static final String PASSWORD_SALT = "PASSWORD_SALT!";
  
```