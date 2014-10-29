Public
======
  xmlns:android="http://schemas.android.com/apk/res/android">
    <RelativeLayout android:id="@id/menu_bar_parent" android:layout_width="fill_parent" android:layout_height="fill_parent">
        <LinearLayout android:id="@id/main_tabs_radio" android:background="@drawable/foot_bar" android:layout_width="fill_parent" android:layout_height="wrap_content" android:layout_alignParentBottom="true">
            <RadioGroup android:gravity="center_vertical" android:orientation="horizontal" android:id="@id/tabs_radio" android:layout_width="fill_parent" android:layout_height="wrap_content" android:layout_weight="1.0">
                <RadioButton android:gravity="center" android:id="@id/radio_button1" android:text="@string/tab_search_medicine" android:drawableTop="@drawable/tab1_radiobtn" style="@style/tab_bottom" />
                <RadioButton android:gravity="center" android:id="@id/radio_button2" android:text="@string/tab_category" android:drawableTop="@drawable/tab2_radiobtn" style="@style/tab_bottom" />
                <RadioButton android:gravity="center" android:id="@id/radio_button3" android:text="@string/tab_symptom" android:drawableTop="@drawable/tab3_radiobtn" style="@style/tab_bottom" />
                <RadioButton android:gravity="center" android:id="@id/radio_button4" android:text="@string/tab_guidecatelist" android:drawableTop="@drawable/tab4_radiobtn" style="@style/tab_bottom" />
            </RadioGroup>
            <TextView android:textColor="@color/more_line" android:gravity="center" android:layout_gravity="center_vertical" android:id="@id/radio_button5" android:background="@null" android:text="@string/tab_more" android:drawableTop="@drawable/tab5_radiobtn" android:layout_weight="4.0" style="@style/tab_bottom" />
        </LinearLayout>
        <FrameLayout android:id="@id/tabcontent" android:layout_width="fill_parent" android:layout_height="fill_parent" android:layout_above="@id/main_tabs_radio" />
    </RelativeLayout>
    <include android:layout_gravity="start" android:layout_width="fill_parent" android:layout_height="fill_parent" layout="@layout/main_menu" />
</android.support.v4.widget.DrawerLayout>
