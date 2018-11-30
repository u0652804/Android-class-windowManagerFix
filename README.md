# Android-class-windowManagerFix
<br>

# Issue
Android在SDK > 23後 使用WindowManager.LayoutParams.TYPE_SYSTEM_ALERT將會報錯.
<br>

# Solution
1. 開啟APP時 => 判斷裝置SDK版本，如果版本>=23，
調用intent開啟'權限設定頁面'，必需要由使用者允許Overlay權限
2. 設定WindowManager.LayoutParams時，判斷裝置SDK版本，如果版本>=23，
設定參數WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY，
否則可使用WindowManager.LayoutParams.TYPE_PHONE
<br>

# 引用
https://blog.bam.tech/developper-news/fix-permission-denied-window-type-error-when-integrating-react-native-in-existing-android-application
https://stackoverflow.com/questions/45867533/system-alert-window-permission-on-api-26-not-working-as-expected-permission-den
https://developer.android.com/about/versions/oreo/android-8.0-changes.html#cwt
