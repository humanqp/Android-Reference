# Android-Reference
>### Device Key 
- 안드로이드 기기 식별 방법 : http://boxfoxs.tistory.com/269
```
public class MainActivity extends Activity {
 
    private Activity activity;
     
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        activity = this;
         
        String device_unique = getUniqueID(activity.getApplicationContext());
         
        Log.d("device_key", device_unique);
         
    }
     
    // 장치별 유니크 아이디
    public String getUniqueID(Context context) {
        final TelephonyManager tm = (TelephonyManager) context.getSystemService(Context.TELEPHONY_SERVICE);
 
        final String tmDevice, tmSerial, androidId;
        tmDevice = "" + tm.getDeviceId();
        tmSerial = "" + tm.getSimSerialNumber();
        androidId = "" + android.provider.Settings.Secure.getString(context.getContentResolver(), android.provider.Settings.Secure.ANDROID_ID);
 
        UUID deviceUuid = new UUID(androidId.hashCode(), ((long)tmDevice.hashCode() << 32) | tmSerial.hashCode());
        String deviceId = deviceUuid.toString();
        return deviceId;
    }
}

```

>### Android 7.0  이상 installer  사용 시 FileUriExposedException 오류
- Link : [참고](https://starrysky.co.kr/2017/06/uri-fromfile-%EC%82%AC%EC%9A%A9-%EC%8B%9C-fileuriexposedexception-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EA%B2%BD%EC%9A%B0/)
