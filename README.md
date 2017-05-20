# NotePad
This is an AndroidStudio rebuild of google SDK sample NotePad

Android development experiment  
功能如下：

添加时间戳


笔记查询



修改背景色


UI界面设计


一、进入Main界面，如图所示：  


![主界面](https://github.com/Beautyohbetty/note/blob/master/app/build/image/111.png)  


二、点击右下角添加按钮


![界面1](https://github.com/Beautyohbetty/note/blob/master/app/build/image/222.jpg)  


三、进入一个newnote界面


![界面2](https://github.com/Beautyohbetty/note/blob/master/app/build/image/333.png)  



四、添加几个不同笔记之后的界面，每一条notes下方显示时间戳。 


1 修改noteslist_item.xml，增加显示时间戳的TextView。
···java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:id="@+id/ll_notesItems"
    android:layout_marginBottom="5dp"
    >

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="1dp"
        android:background="#00000000"
        android:layout_marginTop="10dp"
        >

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <ImageView
            android:layout_width="79dp"
            android:layout_height="70dp"
            android:layout_marginTop="5dp"
            android:background="@drawable/app_note" />

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="vertical"
            android:weightSum="1">

            <TextView
                android:id="@+id/tv_title"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginLeft="10dp"
                android:layout_marginTop="5dp"
                android:text="Title"
                android:textColor="#3333FF"
                android:textSize="20sp"
                android:layout_weight="0.38" />

            <TextView
                android:id="@+id/tv_data"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginLeft="10dp"
                android:layout_marginTop="5dp"
                android:text="2017/4/25 16:25:30"
                android:textColor="#000000" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="82dp"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:orientation="horizontal"
            android:weightSum="1">

            <ImageView
                android:id="@+id/iv_editNote"
                android:layout_width="36dp"
                android:layout_height="match_parent"
                android:layout_marginRight="10dp"
                android:background="@drawable/ic_menu_edit" />

            <ImageView
                android:id="@+id/iv_deleteNote"
                android:layout_width="37dp"
                android:layout_height="wrap_content"
                android:background="@drawable/ic_menu_delete" />
        </LinearLayout>

    </LinearLayout>
</LinearLayout>
···
2 在NotePadProvider中变量值添加


private static final String[] READ_NOTE_PROJECTION = new String[] {
            NotePad.Notes._ID,               // Projection position 0, the note's id
            NotePad.Notes.COLUMN_NAME_NOTE,  // Projection position 1, the note's content
            NotePad.Notes.COLUMN_NAME_TITLE, // Projection position 2, the note's title
            NotePad.Notes.COLUMN_NAME_CREATE_DATE, // Projection position 3, the note's createdate
    };

    private static final int READ_NOTE_NOTE_INDEX = 1;
    private static final int READ_NOTE_TITLE_INDEX = 2;
    private static final int READ_NOTE_CREATE_DATE_INDEX = 3;

3

/*
    读取数据库中的数据存到mDate中
     */
    public void readDate()
    {
        mDate.clear();
        while(cursor.moveToNext())
        {
            mDate.add(new Note(cursor.getString(COLUMN_INDEX_TITLE),cursor.getString(COLUMN_INDEX_MODIFICATION_DATE),cursor.getString(COLUMN_INDEX_ID)));
            Log.d("hhh",cursor.getString(COLUMN_INDEX_TITLE)+","+cursor.getString(COLUMN_INDEX_MODIFICATION_DATE)+","+cursor.getString(COLUMN_INDEX_ID));
        }
    }

 4
 在NotePad中修改成为最合适的字符串格式
 
 
 
  if (values.containsKey(NotePad.Notes.COLUMN_NAME_CREATE_DATE) == false) {
            values.put(NotePad.Notes.COLUMN_NAME_CREATE_DATE, now);
        }

        // If the values map doesn't contain the modification date, sets the value to the current
        // time.
        if (values.containsKey(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE) == false) {
            values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, now);

显示时间戳最关键代码：




![*](https://github.com/Beautyohbetty/note/blob/master/app/build/image/17.png) 




最终显示正确的时间戳




![界面3](https://github.com/Beautyohbetty/note/blob/master/app/build/image/444.jpg) 
五、点击输入标题查询，得到相应结果


![界面4](https://github.com/Beautyohbetty/note/blob/master/app/build/image/555.png)  

关键代码：

![*](https://github.com/Beautyohbetty/note/blob/master/app/build/image/18.png)

六、主界面右上角可以选择复制文字或者背景颜色

![界面5](https://github.com/Beautyohbetty/note/blob/master/app/build/image/666.png)  



七、选择background背景颜色，得到结果


![界面6](https://github.com/Beautyohbetty/note/blob/master/app/build/image/777.png)  



八、选择米黄色，界面变换



![界面7](https://github.com/Beautyohbetty/note/blob/master/app/build/image/888.png)  




九、对每一条笔记可以进行编辑和删除



![界面8](https://github.com/Beautyohbetty/note/blob/master/app/build/image/999.jpg)  



十、进入笔记，点击右上角按钮，可以进行标题编辑



![界面9](https://github.com/Beautyohbetty/note/blob/master/app/build/image/1111.jpg)  



十一、修改标题成功


![界面10](https://github.com/Beautyohbetty/note/blob/master/app/build/image/2222.png) 



![界面11](https://github.com/Beautyohbetty/note/blob/master/app/build/image/22221.jpg) 



 



 
