# NotePad

This is an AndroidStudio rebuild of google SDK sample NotePad

Android development experiment  

## 功能如下：

### 添加时间戳


### 笔记查询



### 修改背景色


### UI界面设计


### 编辑和删除笔记



一、进入`Main界面`，如图所示：  


![主界面](https://github.com/Beautyohbetty/note/blob/master/app/build/image/111.png)  


二、点击右下角`添加`按钮


![界面1](https://github.com/Beautyohbetty/note/blob/master/app/build/image/222.jpg)  


三、进入一个`newnote`界面


![界面2](https://github.com/Beautyohbetty/note/blob/master/app/build/image/333.png  "新界面")  

UI界面美化，在notelistitem.xml进行界面图标格式大小颜色的修改

```java
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
```
![界面3](https://github.com/Beautyohbetty/note/blob/master/app/build/image/444.jpg)





四、添加几个不同笔记之后的界面，每一条notes下方显示`时间戳`。 




1 修改noteslist_item.xml，增加显示时间戳的TextView。

```java
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
```
2 在NotePadProvider中变量值添加


```java

private static final String[] READ_NOTE_PROJECTION = new String[] {
            NotePad.Notes._ID,               // Projection position 0, the note's id
            NotePad.Notes.COLUMN_NAME_NOTE,  // Projection position 1, the note's content
            NotePad.Notes.COLUMN_NAME_TITLE, // Projection position 2, the note's title
            NotePad.Notes.COLUMN_NAME_CREATE_DATE, // Projection position 3, the note's createdate
    };


    private static final int READ_NOTE_NOTE_INDEX = 1;
    private static final int READ_NOTE_TITLE_INDEX = 2;
    private static final int READ_NOTE_CREATE_DATE_INDEX = 3;

    ```
3
```java

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
```


 4
 在NotePad中修改成为最合适的字符串格式
 ```java
 
 
  if (values.containsKey(NotePad.Notes.COLUMN_NAME_CREATE_DATE) == false) {
            values.put(NotePad.Notes.COLUMN_NAME_CREATE_DATE, now);
        }

        // If the values map doesn't contain the modification date, sets the value to the current
        // time.
        if (values.containsKey(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE) == false) {
            values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, now);


```

5  显示时间戳最关键代码：




![*](https://github.com/Beautyohbetty/note/blob/master/app/build/image/17.png) 




最终显示正确的时间戳




![界面3](https://github.com/Beautyohbetty/note/blob/master/app/build/image/444.jpg) 



五、点击`输入标题查询`，得到相应结果

1 在noteList_layout中添加搜索查询功能

```java
 <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"

        >
        <EditText
            android:layout_width="match_parent"
            android:layout_height="40dp"
            android:layout_weight="1"
            android:layout_marginLeft="10dp"
            android:textColor="#000000"
            android:id="@+id/et_Search"
            android:hint="输入标题查找"
            android:textCursorDrawable="@drawable/contact_edit_edittext_normal"


```
2 在NotesList.java中，建立`搜索`实例

```java
public class NotesList extends ListActivity implements View.OnClickListener {


    private EditText et_Search;//搜索框控件实例
    private ImageView iv_searchnotes;//搜索按钮实例
    private ListView lv_notesList;
    private NotesListAdapter adapter;
    private ImageView iv_addnotes;//添加按钮
    private LinearLayout ll_noteList;
    
    
  ```
  3  search法
   
   ```java
   public void Search(String searchTitle){
        searchData=new ArrayList<Note>();
        for(Note noteBean:mDate){
            if(noteBean.getTitle().equals(searchTitle)){
                searchData.add(noteBean);
            }
        }
        mDate.clear();
        mDate.addAll(searchData);
        notifyDataSetChanged();
    }
```
4设置当点击查询标题按钮时触发的方法
```java
 public void onClick(View v) {
        switch (v.getId()){
            case R.id.fab:
                startActivity(new Intent(Intent.ACTION_INSERT, getIntent().getData()));
                break;
            case R.id.iv_searchnotes:
                showOrhide();
                if(et_Search.getText().toString().equals("")){
                    Cursor cursor1 = managedQuery(
                            getIntent().getData(),            // Use the default content URI for the provider.
                            PROJECTION,                       // Return the note ID and title for each note.
                            null,                             // No where clause, return all records.
                            null,                             // No where clause, therefore no where column values.
                            NotePad.Notes.DEFAULT_SORT_ORDER  // Use the default sort order.
                    );
                    adapter.readDate(cursor1);
                    adapter.notifyDataSetChanged();
                }else{
                    adapter.Search(et_Search.getText().toString());
                }

                break;
        }
    }
```

5 显示在app中的查询界面


![界面4](https://github.com/Beautyohbetty/note/blob/master/app/build/image/555.png)  






六、主界面右上角可以选择复制文字或者背景颜色

1 运用了`SharedPreferences`修改背景颜色


```java



ublic class SharedPreferenceUtil {

    private static String FILENAME = "Config";

    /**
     * CommitDate该方法是一个有返回值的同步的提交方式，true表示数据保存成功，false表示数据保存失败
     */
    public static boolean CommitDate(String key, String date) {
        SharedPreferences sp = MyApplication.getContext().getSharedPreferences(FILENAME, Context.MODE_PRIVATE);
        SharedPreferences.Editor editor = sp.edit();
        editor.putString(key, date);
        return editor.commit();
    }

    /**
     * ApplyDate:是一个异步操作的保存数据的方法
     */
    public static void ApplyDate(String key, String date) {
        SharedPreferences sp = MyApplication.getContext().getSharedPreferences(FILENAME, Context.MODE_PRIVATE);
        SharedPreferences.Editor editor = sp.edit();
        editor.putString(key, date);
        editor.apply();
    }

    /*
    *获取数据
     */
    public static String getDate(String key) {
        SharedPreferences sp = MyApplication.getContext().getSharedPreferences(FILENAME, Context.MODE_PRIVATE);
        String str = sp.getString(key, "");
        if (!str.isEmpty()) {
            return str;
        } else {
            return null;
        }
    }
    
    
```
  /*
        读取配置文件中的背景颜色
         */
    public static void readBackground(){
        if(SharedPreferenceUtil.getDate("background")==null||SharedPreferenceUtil.getDate("background").equals("")){

        }
        else{
            background= SharedPreferenceUtil.getDate("background");
        }

    }

    /*
   读取配置文件中的背景颜色
  */
    public static void saveBackground(){
        SharedPreferenceUtil.CommitDate("background",background);
    }
}

2 创建value color.xml
```java

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="GREEN">#d9ffcc</color>
    <color name="Pink">#FFC0CB</color>
    <color name="PaleVioletRed">#DB7093</color>
    <color name="LightGrey">#D3D3D3</color>
    <color name="MediumPurple">#9370DB</color>
    <color name="LightSteelBlue">#B0C4DE</color>
    <color name="AliceBlue">#F0F8FF</color>
    <color name="Snow">	#FFFAFA</color>
    <color name="DarkGray">#A9A9A9</color>
    <color name="PapayaWhip">#FFEFD5</color>
</resources>
```

3建立一个myapplication类用于背景颜色
```java
public class MyApplication extends Application {

    private static Context context;
    private static String background="#ffffff";//背景颜色的十六进制值,默认为白色

    @Override
    public void onCreate() {
        super.onCreate();
        context=getApplicationContext();
        readBackground();
    }

    public static Context getContext() {
        return context;
    }

    public static void setContext(Context context) {
        MyApplication.context = context;
    }

    public static String getBackground() {
        return background;
    }

    public static void setBackground(String background) {
        MyApplication.background = background;
    }
```
  
![界面5](https://github.com/Beautyohbetty/note/blob/master/app/build/image/666.png)  



七、选择background背景颜色，得到结果


![界面6](https://github.com/Beautyohbetty/note/blob/master/app/build/image/777.png)  



八、选择米黄色，界面变换



![界面7](https://github.com/Beautyohbetty/note/blob/master/app/build/image/888.png)  




九、对每一条笔记可以进行编辑和删除


```java
 private final void cancelNote() {
        if (mCursor != null) {
            if (mState == STATE_EDIT) {
                // Put the original note text back into the database
                mCursor.close();
                mCursor = null;
                ContentValues values = new ContentValues();
                values.put(NotePad.Notes.COLUMN_NAME_NOTE, mOriginalContent);
                getContentResolver().update(mUri, values, null, null);
            } else if (mState == STATE_INSERT) {
                // We inserted an empty note, make sure to delete it
                deleteNote();
            }
        }
        setResult(RESULT_CANCELED);
        finish();
    }

    /**
     * 
    重复确认是否要删除部分代码 */
    private final void deleteNote() {
        if (mCursor != null) {
            mCursor.close();
            mCursor = null;
            getContentResolver().delete(mUri, null, null);
            mText.setText("");
        }
    }
}
```


![界面8](https://github.com/Beautyohbetty/note/blob/master/app/build/image/999.jpg)  



十、进入笔记，点击右上角按钮，可以进行标题编辑



![界面9](https://github.com/Beautyohbetty/note/blob/master/app/build/image/1111.jpg)  



十一、修改标题成功


![界面10](https://github.com/Beautyohbetty/note/blob/master/app/build/image/2222.png) 



![界面11](https://github.com/Beautyohbetty/note/blob/master/app/build/image/22221.jpg) 



 



 
