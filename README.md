SwipeBackLayout
===

An Android library that help you to build app with swipe back gesture.


![](https://github.com/Issacw0ng/SwipeBackLayout/blob/master/art/screenshot.png?raw=true)


Demo Apk
===
[GooglePlay](https://play.google.com/store/apps/details?id=me.imid.swipebacklayout.demo)


Requirement
===
The latest android-support-v4.jar should be referenced by your project.

Usage
===
1. Add SwipeBackLayout as a dependency to your existing project.
2. To enable SwipeBackLayout, you can simply make your `Activity` extend `SwipeBackActivity`:
	* In `onCreate` method, `setContentView()` should be called as usual.
	* You will have access to the `getSwipeBackLayout()` method so you can customize the `SwipeBackLayout`. 
3. Make window translucent by adding `<item name="android:windowIsTranslucent">true</item>` to your theme.

Simple Example
===
```
public class DemoActivity extends SwipeBackActivity implements View.OnClickListener {
    private int[] mBgColors;

    private static int mBgIndex = 0;

    private String mKeyTrackingMode;

    private RadioGroup mTrackingModeGroup;

    private SwipeBackLayout mSwipeBackLayout;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_demo);
        changeActionBarColor();
        findViews();
        mKeyTrackingMode = getString(R.string.key_tracking_mode);
        mSwipeBackLayout = getSwipeBackLayout();

        mTrackingModeGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup group, int checkedId) {
                int edgeFlag;
                switch (checkedId) {
                    case R.id.mode_left:
                        edgeFlag = SwipeBackLayout.EDGE_LEFT;
                        break;
                    case R.id.mode_right:
                        edgeFlag = SwipeBackLayout.EDGE_RIGHT;
                        break;
                    case R.id.mode_bottom:
                        edgeFlag = SwipeBackLayout.EDGE_BOTTOM;
                        break;
                    default:
                        edgeFlag = SwipeBackLayout.EDGE_ALL;
                }
                mSwipeBackLayout.setEdgeTrackingEnabled(edgeFlag);
                saveTrackingMode(edgeFlag);
            }
        });
    }
...
```
This SwipeBackActivity  extends FragmentActivity,if you create an Actity extends what you want and implements SwipeBackActivityBase

This is an example of AppcompatActivity
```

public class MySwipeBackActivity extends AppCompatActivity implements SwipeBackActivityBase {

    private SwipeBackActivityHelper mHelper;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        mHelper = new SwipeBackActivityHelper(this);
        mHelper.onActivityCreate();
    }

    @Override
    protected void onPostCreate(Bundle savedInstanceState) {
        super.onPostCreate(savedInstanceState);
        mHelper.onPostCreate();
    }

    @Override
    public View findViewById(int id) {
        View v = super.findViewById(id);
        if (v == null && mHelper != null)
            return mHelper.findViewById(id);
        return v;
    }

    @Override
    public SwipeBackLayout getSwipeBackLayout() {
        return mHelper.getSwipeBackLayout();
    }

    @Override
    public void setSwipeBackEnable(boolean enable) {
        getSwipeBackLayout().setEnableGesture(enable);
    }

    @Override
    public void scrollToFinishActivity() {
        Utils.convertActivityToTranslucent(this);
        getSwipeBackLayout().scrollToFinishActivity();
    }
}
...
```
Download
===
Download via Jcenter:
```
compile 'me.imid.swipebacklayout.lib:library:+'
```


Pull Requests
===
I will gladly accept pull requests for fixes and feature enhancements but please do them in the develop branch.

License
===

   Copyright 2013 Issac Wong

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
