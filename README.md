# log-in-Screen
Simple log-in screen for your android.


<img src="https://i.imgur.com/cA3qzkn.gif"/>


<img src="https://i.imgur.com/7cKmbiw.jpg"/>

Credits and Inspired by:

https://www.tutorialspoint.com/android/android_login_screen.htm

How to use:

// In your res/layout/log_in.xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="fill_parent"
	android:layout_height="fill_parent">

	<com.doctoror.particlesdrawable.ParticlesView
		xmlns:app="http://schemas.android.com/apk/res-auto"
		android:layout_width="fill_parent"
		android:layout_height="fill_parent"
		app:minDotRadius="1.0dip"
		app:maxDotRadius="3.0dip"
		app:lineThickness="1.0dip"
		app:lineDistance="86.0dip"
		app:numDots="60"
		app:dotColor="#ffffffff"
		app:lineColor="#ffffffff"
		app:frameDelayMillis="10"
		app:stepMultiplier="1.0"/>

	<LinearLayout
		android:layout_margin="5.0dip"
		android:gravity="center"
		android:layout_width="fill_parent"
		android:layout_height="fill_parent"
		android:orientation="vertical">

		<LinearLayout
			android:layout_margin="10.0dip"
			android:gravity="center"
			android:layout_width="fill_parent"
			android:layout_height="600dp"
			android:orientation="vertical">

			<ImageView
				android:id="@+id/sample"
				android:layout_width="200dp"
				android:layout_height="200dp"
				android:background="@drawable/image_1"
				android:textAppearance="?android:attr/textAppearanceLarge"/>

			<EditText
				android:layout_width="250dp"
				android:inputType="textPersonName"
				android:layout_height="wrap_content"
				android:ems="10"
				android:id="@+id/editText"
				android:hint="sample@owellsky-username"
				android:typeface="monospace"
				android:gravity="center"
				android:layout_marginTop="100dp"/>

			<EditText
				android:layout_width="250dp"
				android:inputType="textPassword"
				android:layout_height="wrap_content"
				android:ems="10"
				android:id="@+id/editText2"
				android:hint="sample@owellsky-password"
				android:typeface="monospace"
				android:gravity="center"/>

			<Button
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:text="LOGIN"
				android:id="@+id/button"
				android:typeface="monospace"/>

			<TextView
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:id="@+id/textView3"
				android:text="text"
				android:layout_alignTop="@+id/textView2"
				android:layout_alignParentRight="true"
				android:layout_alignParentEnd="true"
				android:layout_alignBottom="@+id/textView2"
				android:layout_toEndOf="@+id/textview"
				android:textSize="25dp"
				android:layout_toRightOf="@+id/textview"/>

		</LinearLayout>

		<LinearLayout
			android:orientation="horizontal"
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:layout_margin="5dp"
			android:gravity="center">

			<TextView
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:text="ALL RIGHTS RESERVED MMXVIII"
				android:typeface="monospace"
				android:textStyle="bold"/>

		</LinearLayout>

	</LinearLayout>

</RelativeLayout>



//In your res/anim "alpha_translate.xml 
//This is a combinatio of fade_in.xml and translate.xml.

<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
	<alpha 
		android:fromAlpha="0.0" 
		android:toAlpha="1.0"
		android:interpolator="@android:anim/accelerate_interpolator"
		android:duration="5000"/>
	<translate xmlns:android="http://schemas.android.com/apk/res/android" android:duration="5000" android:zAdjustment="top" android:fromXDelta="0.0%" android:toXDelta="0.0%" android:fromYDelta="200.0%" android:toYDelta="0.0%" />
</set>



// In your res/values/styles and also values-v21

<style name="AppTheme.NoActionBar">
		<item name="windowNoTitle">true</item>
		<item name="windowActionBar">false</item>
		<item name="android:windowFullscreen">true</item>
		<item name="android:windowContentOverlay">@null</item>
		<item name="android:background">@color/black1</item>
	</style>
  
  
  
  // In your Manifest.xml add this line.
  
  <activity
            android:name="org.network.owellsky.LogIn" 
			android:theme="@style/AppTheme.NoActionBar" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
      
      
      
        // Create java class to call
        
        import android.app.*;
import android.os.*;

import android.app.Activity;
import android.graphics.Color;
import android.os.Bundle;
import android.view.View;

import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;
import android.content.*;
import android.support.v7.app.*;
import net.openvpn.openvpn.*;
import android.widget.*;
import android.view.animation.*;

public class LogIn extends Activity 
{

	Button b1,b2;
	EditText ed1,ed2;

	TextView tx1;
	int counter = 3;

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.log_in);
		
    // This your logo animation from bottom to center
		ImageView myImageView= (ImageView)findViewById(R.id.sample);
		Animation myAlpha_TranslateAnimation = AnimationUtils.loadAnimation(this, R.anim.alpha_translate);
		myImageView.startAnimation(myAlpha_TranslateAnimation);
			
		b1 = (Button)findViewById(R.id.button);
		ed1 = (EditText)findViewById(R.id.editText);
		ed2 = (EditText)findViewById(R.id.editText2);

		tx1 = (TextView)findViewById(R.id.textView3);
		tx1.setVisibility(View.GONE);

		b1.setOnClickListener(new View.OnClickListener() {
				@Override
				public void onClick(View v) {
					if(ed1.getText().toString().equals("admin") &&
					   ed2.getText().toString().equals("admin")) {

// Call second activity 
						Intent intent = new Intent(LogIn.this,
												   OpenVPNClient.class);
						intent.setFlags(Intent.FLAG_ACTIVITY_NO_ANIMATION);
						startActivity(intent);
						LogIn.this.finish();

						Toast.makeText(getApplicationContext(),"Welcome to infiniteVPN",Toast.LENGTH_SHORT).show();
					}else{
						Toast.makeText(getApplicationContext(), "Wrong Credentials",Toast.LENGTH_SHORT).show();

						tx1.setVisibility(View.VISIBLE);

						counter--;
						tx1.setText(Integer.toString(counter));

						if (counter == 0) {
							finish();
							b1.setEnabled(false);


						}
					}
				}
			});
	}
}
        
        // Finish run your application now.
        
        Thanks to:
