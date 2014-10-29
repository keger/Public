Public
======
    <style name="tab_bottom">
        <item name="android:textSize">@dimen/bottom_tab_font_size</item>
        <item name="android:textColor">@drawable/tab_text_color</item>
        <item name="android:gravity">center</item>
        <item name="android:background">@drawable/tabs_btn_bg</item>
        <item name="android:paddingTop">5.0dip</item>
        <item name="android:paddingBottom">5.0dip</item>
        <item name="android:layout_width">fill_parent</item>
        <item name="android:layout_height">fill_parent</item>
        <item name="android:button">@null</item>
        <item name="android:singleLine">true</item>
        <item name="android:layout_weight">1.0</item>
    </style>

<?xml version="1.0" encoding="utf-8"?>
<selector
  xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_enabled="true" android:state_checked="true" android:color="@color/read_text" />
    <item android:state_selected="true" android:color="@color/read_text" />
    <item android:color="@color/news_title" />
</selector>

<?xml version="1.0" encoding="utf-8"?>
<selector
  xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_focused="true" android:drawable="@drawable/foot_bar_line" />
    <item android:state_pressed="true" android:drawable="@drawable/foot_bar_line" />
    <item android:state_checked="true" android:drawable="@drawable/foot_bar_line" />
    <item android:drawable="@drawable/none" />
</selector>

<color name="read_text">#ffe66767</color>
<color name="news_title">#ff666666</color>

<dimen name="bottom_tab_font_size">11.0sp</dimen>
