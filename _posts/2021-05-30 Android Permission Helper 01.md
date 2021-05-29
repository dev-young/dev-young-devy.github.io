---
title: "안드로이드 권한 요청 쉽게 하기!"
date: 2021-05-30 06:30:00 -0400
categories: [Android] 
---

## 권한이 필요한 작업 수행을 도와줄 RunWithPermission.kt

[dev-young/DevyStudy](https://github.com/dev-young/DevyStudy/blob/master/app/src/main/java/io/ymsoft/devystudy/RunWithPermission.kt)

### 사용법은 아래와 같다!

```kotlin
private val task by lazy {
    RunWithPermission(requireActivity(), Manifest.permission.READ_EXTERNAL_STORAGE)
        .setActionWhenGranted {
            /**권한이 승인되었을 때 작업*/
        }.setActionWhenDenied { rwp ->
            /** rwp: RunWithPermission 객체*/
            /**권한 요청 팝업이 떴지만 승인하지 않았거나 옵션 변경 화면에서 권한을 승인하지 않았을 때 작업
             * 권한 요청 이유와 함께 스낵바 혹은 다이얼로그 출력 후 rwp.requestPermission() 사용 권장*/
        }.setActionInsteadPopup { rwp ->
            /**다시보지않기를 체크했거나 안드로이드 11버전 이상에서 2회 이상 거부를 눌렀을 경우 권한을 요청해도 팝업창이 안뜨는데 이때 취할 작업
             * rwp.startPermissionIntent() 사용 권장 */
        }
}

private fun startTask() = task.run()
```

초기화 방법은 각자의 취향대로!
