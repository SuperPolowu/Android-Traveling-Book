# LifeCycle

#### onCreate
* 對Activity類別的屬性作初始化。
* 此階段還不會顯示畫面。

#### onRestart
* 從 onStop 狀態回到 onStart 狀態。
* 重新開啟 Activity 時觸發。

#### onStart
* Activiy 可見

#### onResumed
* Activity 可見。
* 適合執行動畫的階段。
* 重新取回硬體資源。

#### onPaused
* 開啟 Dialog 雖會讓Activity畫面加暗並顯示視窗，但不會導致Activity進入此狀態。
* Activity 可見。
* 不執行程式碼。
* 釋放硬體資源。

#### onStopped
* Activity 不可見。
* Activity 不再前台。

#### onDestory
* Activity 關閉。

```java
public class MainActivity extends ActionBarActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Log.d("Activity Flow", "onCreate");
    }

    @Override
    protected void onRestart() {
        super.onRestart();
        Log.d("Activity Flow", "onRestart");
    }

    @Override
    protected void onStart() {
        super.onStart();
        Log.d("Activity Flow", "onStart");
    }

    @Override
    protected void onResume() {
        super.onResume();
        Log.d("Activity Flow", "onResume");
    }

    @Override
    protected void onPause() {
        super.onPause();
        Log.d("Activity Flow", "onPause");
    }

    @Override
    protected void onStop() {
        super.onStop();
        Log.d("Activity Flow", "onStop");
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        Log.d("Activity Flow", "onDestroy");
    }
}

```

## 開啟 Activity
```
07-28 10:13:24.552    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onCreate
07-28 10:13:24.552    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onStart
07-28 10:13:24.556    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onResume
```

## 關閉 Activity
```
07-28 10:13:24.552    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onPause
07-28 10:13:24.552    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onStop
07-28 10:13:24.556    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onDestroy
```

## 進入其他 Activity
```
07-28 10:16:13.552    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onPause
07-28 10:16:14.400    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onStop
```

## 重新回到 Activity
```
07-28 10:16:47.508    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onRestart
07-28 10:16:47.508    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onStart
07-28 10:16:47.508    2343-2343/com.chriske.rotationandscalar D/Activity Flow﹕ onResume
```
