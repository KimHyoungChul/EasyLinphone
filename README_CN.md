# EasyLinphone
EasyLinphone 可以帮助你在项目中很轻松的使用 Linphone Android SDK。

[English DOC]()

## 导入

## 使用
### 1. 初始化 LinphoneService

```java
// 开启服务
EasyLinphone.startService(mContext);
// 添加登录状态回调和通话回调
EasyLinphone.addCallback(new RegistrationCallback() {
    @Override
    public void registrationOk() {
        super.registrationOk();
        // do something
    }

    @Override
    public void registrationFailed() {
        super.registrationFailed();
        // do something
    }
}, new PhoneCallback() {
    @Override
    public void incomingCall(LinphoneCall linphoneCall) {
        super.incomingCall(linphoneCall);
        // do something
    }

    @Override
    public void callConnected() {
        super.callConnected();
        // do something
    }

    @Override
    public void callEnd() {
        super.callEnd();
        // do something
    }
});
```

可以根据实际情况，在不同的地方分别添加登录状态回调和通话状态回调。

### 2. 登录

```java
// 配置 Sip 账户信息
EasyLinphone.setAccount("1003", "123456", "192.168.9.60");
// 注册到 Sip 服务器
EasyLinphone.login();
```

### 3. 管理音频通话

```java
// 呼叫指定号码
EasyLinphone.callTo("1001");
// 挂断当前通话
EasyLinphone.hangUp();
// 接听当前来电
EasyLinphone.acceptCall();
// 切换静音
EasyLinphone.toggleMicro(!EasyLinphone.getLC().isMicMuted());
// 切换免提
EasyLinphone.toggleSpeaker(!EasyLinphone.getLC().isSpeakerEnabled());
```

### 4. 管理视频通话

视频通话示例如下：

```java
public class VideoActivity extends AppCompatActivity {
    @BindView(R.id.video_rendering) SurfaceView mRenderingView;
    @BindView(R.id.video_preview) SurfaceView mPreviewView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_video);
        ButterKnife.bind(this);
        EasyLinphone.setAndroidVideoWindow(new SurfaceView[]{mRenderingView}, new SurfaceView[]{mPreviewView});
    }

    @Override
    protected void onResume() {
        super.onResume();
        EasyLinphone.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
        EasyLinphone.onPause();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        EasyLinphone.onDestroy();
    }

    @OnClick(R.id.video_hang)
    public void hang() {
        EasyLinphone.hangUp();
        finish();
    }
}
```

可以看到，通过本库可以很简单的使用 Linphone Android SDK。代码质量不高，还有很多疵漏之处，还请大家多多指教。