//activity_main.xml


# Student-Registration-Form<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="10dp"
    tools:context=".MainActivity">
  <TextView
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:textColor="@color/colorPrimary"
      android:gravity="center"
      android:textSize="30sp"
      android:text="Student Registration Form"/>

  <EditText
      android:id="@+id/rollnum"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:hint="Enter Roll Number"
      android:inputType="textCapWords" />
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter name"
        android:inputType="textCapWords"
        android:digits="abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ "
        android:id="@+id/name"
        />
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter email id"
        android:inputType="textEmailAddress"
        android:id="@+id/email"
        />

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Password"
        android:inputType="textPassword"
        android:id="@+id/password"

        />

  <EditText
      android:id="@+id/phone"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:hint="Phone number"
      android:inputType="phone" />
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Gender"
        android:textSize="30sp"

        />
    <RadioGroup
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
        <RadioButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/male"
            android:text="Male"
            />
        <RadioButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/female"
            android:text="Female"
            />
    </RadioGroup>
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Select Branch"
        android:textSize="20dp"

        />
    <Spinner
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/branches"
        android:entries="@array/branches"
        />
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Save and Display Data"
        android:layout_margin="10dp"
        android:layout_gravity="center"
        android:id="@+id/btn"
        />

</LinearLayout>




// activity_second.xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".SecondActivity">
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/tv_data"
        android:text="Your Data"
        android:gravity="center"
        android:textSize="30dp"
        />

</LinearLayout>




//MainActivity.java

package com.example.reg_16f01f0006;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.RadioButton;
import android.widget.Spinner;

public class MainActivity extends AppCompatActivity {
    EditText et_rollnum,et_name,et_mailid,et_password,et_phonenumber;
    Button myButton;
    RadioButton r_male,r_feamle;
    Spinner sp_branch;
    String gender;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        et_rollnum=findViewById(R.id.rollnum);
        et_name=findViewById(R.id.name);
        et_mailid=findViewById(R.id.email);
        et_password=findViewById(R.id.password);
        et_phonenumber=findViewById(R.id.phone);
        myButton=findViewById(R.id.btn);
        myButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String name=et_name.getText().toString();
                String rno=et_rollnum.getText().toString();
                String mail=et_mailid.getText().toString();
                String pwd=et_password.getText().toString();
                String pno=et_phonenumber.getText().toString();
                r_male=findViewById(R.id.male);
                r_feamle=findViewById(R.id.female);
                sp_branch=findViewById(R.id.branches);
                if(r_male.isChecked()){
                    gender=r_male.getText().toString();
                }
                else
                {
                    gender=r_feamle.getText().toString();
                }
                String branch=sp_branch.getSelectedItem().toString();
                Intent intentObject=new Intent(MainActivity.this,SecondActivity.class);
                intentObject.putExtra("keyname",name);
                intentObject.putExtra("keyrno",rno);
                intentObject.putExtra("keymail",mail);
                intentObject.putExtra("keypwd",pwd);
                intentObject.putExtra("keypno",pno);
                intentObject.putExtra("keygender",gender);
                intentObject.putExtra("keybranch",branch);
                startActivity(intentObject);


            }
        });
    }
}




//SecondActivity.java


package com.example.reg_16f01f0006;
import androidx.appcompat.app.AppCompatActivity;

import android.annotation.SuppressLint;
import android.content.Intent;
import android.os.Bundle;
import android.widget.RadioButton;
import android.widget.Spinner;
import android.widget.TextView;

public class SecondActivity extends AppCompatActivity {
    TextView tv;

    @SuppressLint("SetTextI18n")
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        tv = findViewById(R.id.tv_data);
        Intent i = getIntent();
        String res1 = i.getStringExtra("keyname");
        String res2 = i.getStringExtra("keyrno");
        String res3 = i.getStringExtra("keymail");
        String res4 = i.getStringExtra("keypwd");
        String res5 = i.getStringExtra("keypno");
        String res6 = i.getStringExtra("keygender");
        String res7 = i.getStringExtra("keybranch");
        tv.setText("RollNum:"+res2 + "\n Name:" + res1 +"\n EmailID:"+ res3 +"\n Password:" + res4 +"\n PhoneNum:" + res5 +"\n Gender:"+res6+"\n Branch:"+res7);

    }
}



// strings.xml


<resources>
    <string name="app_name">Reg_16F01F0006</string>
    <string-array name="branches">
        <item>CSE</item>
        <item>ECE</item>
        <item>CIVIL</item>
        <item>EEE</item>
        <item>IT</item>
        <item>Mech</item>
    </string-array>
</resources>



//androidManifest.xml

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.reg_16f01f0006">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".SecondActivity"
            android:parentActivityName=".MainActivity"></activity>
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
