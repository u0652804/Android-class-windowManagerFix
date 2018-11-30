# Android-class-windowManagerFix
<br>

# Issue
Android在SDK > 23後 使用WindowManager.LayoutParams.TYPE_SYSTEM_ALERT將會報錯.
<br>

# Solution
part1. 
開啟APP時 => 判斷裝置SDK版本，如果版本>=23，
調用intent開啟'權限設定頁面'，必需要由使用者允許Overlay權限

part2. 
設定WindowManager.LayoutParams時，判斷裝置SDK版本，如果版本>=23，
設定參數WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY，
否則可使用WindowManager.LayoutParams.TYPE_PHONE
#
part1. code
```ruby
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        if (Build.VERSION.SDK_INT >= 23) {
            if (!Settings.canDrawOverlays(this)) {

                // Open the permission page
                Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION,
                        Uri.parse("package:" + getPackageName()));
                startActivityForResult(intent, OVERLAY_PERMISSION_CODE);
                return;
            }
        }
```

part2. code
```ruby
        if (Build.VERSION.SDK_INT < Build.VERSION_CODES.O) {
            params = new WindowManager.LayoutParams(
                    WindowManager.LayoutParams.WRAP_CONTENT,
                    WindowManager.LayoutParams.WRAP_CONTENT,
                    WindowManager.LayoutParams.TYPE_PHONE,
                    WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE,
                    PixelFormat.TRANSLUCENT);
        }else{
            params = new WindowManager.LayoutParams(
                    WindowManager.LayoutParams.WRAP_CONTENT,
                    WindowManager.LayoutParams.WRAP_CONTENT,
                    WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY,
                    WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE,
                    PixelFormat.TRANSLUCENT);
        }
```


# 引用
https://blog.bam.tech/developper-news/fix-permission-denied-window-type-error-when-integrating-react-native-in-existing-android-application

https://stackoverflow.com/questions/45867533/system-alert-window-permission-on-api-26-not-working-as-expected-permission-den

https://developer.android.com/about/versions/oreo/android-8.0-changes.html#cwt
