## 简介
安卓动态权限申请框架封装

## 效果展示

## 使用方法
  //申请权限统一处理
  RxPermissions rxPermissions = new RxPermissions(this);
        rxPermissions.request(
                Manifest.permission.CAMERA,
                Manifest.permission.WRITE_EXTERNAL_STORAGE,
                Manifest.permission.READ_PHONE_STATE).subscribe(new Consumer<Boolean>() {
            @Override
            public void accept(Boolean aBoolean) throws Exception {
                if (aBoolean) {
                    //表示用户同意权限
                    Toast.makeText(MainActivity.this, "用户同意使用权限", Toast.LENGTH_SHORT).show();
                } else {
                    //表示用户不同意权限
                    Toast.makeText(MainActivity.this, "用户拒绝使用权限", Toast.LENGTH_SHORT).show();
                }
            }
        });
   //申请权限分别处理
   RxPermissions rxPermissions = new RxPermissions(this);
        rxPermissions.requestEach(
                           Manifest.permission.WRITE_EXTERNAL_STORAGE,
                           Manifest.permission.READ_PHONE_STATE).subscribe(new Consumer<Permission>() {
                       @Override
                       public void accept(Permission permission) throws Exception {
                           if (permission.name.equals(Manifest.permission.WRITE_EXTERNAL_STORAGE)) {
                               //使用permission.name可以获得指定权限获得后的操作
                               if (permission.granted) {
                                   //用户已经同意该权限
                                   Log.e("MainActivity", "同意 WRITE_EXTERNAL_STORAGE");
                               } else {
                                   Log.e("MainActivity", "拒绝 WRITE_EXTERNAL_STORAGE");
                               }
                           }else if (permission.name.equals(Manifest.permission.READ_PHONE_STATE)){
                               if (permission.granted) {
                                   //用户已经同意该权限
                                   Log.e("MainActivity", "同意 READ_PHONE_STATE");
                               } else {
                                   Log.e("MainActivity", "拒绝 READ_PHONE_STATE");
                               }
                           }
                       }
                   });



项目根目录：build.gradle 添加以下代码

```groovy
buildscript {
    repositories {
        google()
        jcenter()
        maven{
            url 'http://192.168.126.254:8081/repository/maven-releases/'
        }// 添加maven库地址
    }
    dependencies {
    classpath "com.android.tools.build:gradle:4.1.1"
    }
}
allprojects {
    repositories {
        google()
        jcenter()
        maven{
            url 'http://192.168.126.254:8081/repository/maven-releases/'
        }// 添加maven库地址
    }
}
```
然后项目 module 中启用插件，可以是`application`也可以是`library`

添加类库依赖：
```groovy
dependencies {
implementation 'com.sesxh.android-rxpermissions:rxpermissions:1.0.0'
}
```

