# 基于NotePad应用的功能扩展
##  一、Notelist中显示调目增加时间显示

从数据库中可以看出已经插入时间字段
![数据库](https://img-blog.csdnimg.cn/20190519225724472.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)


将当前Activity所用到的数据定义在PROJECTION中，在PROJECTION中定义显示的时间（修改时间）
![PROJECTION](https://img-blog.csdnimg.cn/20190520115518439.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

通过Cursor从数据库中读取出来
![cursor](https://img-blog.csdnimg.cn/20190520115605621.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

运行结果：
![主页面](https://img-blog.csdnimg.cn/20190520115707995.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

---

## 二、笔记内容的搜索功能

在文件notelist_latout中添加笔记查询功能
![搜索功能](https://img-blog.csdnimg.cn/20190520120048957.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

在NoteList中找到onOptionsItemSelected方法，在switch中添加搜索的case语句:
![搜索功能](https://img-blog.csdnimg.cn/20190520120211503.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

NotesListAdapter文件的搜索函数：

```
public void Search(String searchTitle){
        searchData=new ArrayList<NoteBean>();
        for(NoteBean noteBean:mDate){
            if(noteBean.getTitle().indexOf(searchTitle)!=-1){
                searchData.add(noteBean);
            }
        }
        mDate.clear();
        mDate.addAll(searchData);
        notifyDataSetChanged();
    }
```

功能展示：
![搜索展示](https://img-blog.csdnimg.cn/20190520120915827.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

---

## 三、主题更换功能

设置背景图dialog_bg_select_layout.xml:

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:weightSum="0.7">

    <ImageView
        android:layout_width="40dp"
        android:layout_height="60dp"
        android:id="@+id/pink"
        android:background="@drawable/pink"
        android:layout_weight="0.1"
        android:onClick="ColorSelect"
        />
    <ImageView
        android:layout_width="40dp"
        android:layout_height="60dp"
        android:layout_weight="0.1"
        android:id="@+id/Yello"
        android:background="@drawable/yellow"
        android:onClick="ColorSelect"
        />
    <ImageView
        android:layout_width="40dp"
        android:layout_height="60dp"
        android:id="@+id/PaleVioletRed"
        android:layout_weight="0.1"
        android:background="@drawable/violetred"
        android:onClick="ColorSelect"
        />
    <ImageView
        android:layout_width="40dp"
        android:layout_height="60dp"
        android:layout_weight="0.1"
        android:id="@+id/LightGrey"
        android:background="@drawable/grey"
        android:onClick="ColorSelect"
        />
    <ImageView
        android:layout_width="40dp"
        android:layout_height="60dp"
        android:layout_weight="0.1"
        android:id="@+id/MediumPurple"
        android:background="@drawable/purple"
        android:onClick="ColorSelect"
        />
    <ImageView
        android:layout_width="40dp"
        android:layout_height="60dp"
        android:layout_weight="0.1"
        android:id="@+id/DarkGray"
        android:background="@drawable/gray"
        android:onClick="ColorSelect"
        />
    <ImageView
        android:layout_width="40dp"
        android:layout_height="60dp"
        android:layout_weight="0.1"
        android:id="@+id/Snow"
        android:background="@drawable/snow"
        android:onClick="ColorSelect"
        />

</LinearLayout>
```

NotesList中背景更改的监听：

```
/*
       背景颜色选择框
        */
    private  void showpopSelectBgWindows(){
        LayoutInflater inflater = LayoutInflater.from(this);
        View view = inflater.inflate(R.layout.dialog_bg_select_layout, null);
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("背景");//设置标题
        builder.setView(view);
        AlertDialog dialog = builder.create();//获取dialog
        dialog.show();//显示对话框
    }

    /*
    背景改变的监听
     */
    public void ColorSelect(View view){
        String color;
        switch(view.getId()){
            case R.id.pink:
                /*此处进行背景颜色修改,后改为主题效果*/
//                color="#FFC0CB";
//                ll_noteList.setBackgroundColor(Color.parseColor(color));
//                lv_notesList.setBackgroundColor(Color.parseColor(color));
//                adapter.setBackground(color);
//                adapter.notifyDataSetChanged();
//                MyApplication.setBackground(color);
//                MyApplication.saveBackground();
                Drawable btnDrawable1 = getResources().getDrawable(R.drawable.pink);
                ll_noteList.setBackgroundDrawable(btnDrawable1);
                lv_notesList.setBackgroundDrawable(btnDrawable1);

                break;
            case R.id.Yello:
                Drawable btnDrawable2 = getResources().getDrawable(R.drawable.yellow);
                ll_noteList.setBackgroundDrawable(btnDrawable2);
                lv_notesList.setBackgroundDrawable(btnDrawable2);
                break;
            case R.id.PaleVioletRed:
                Drawable btnDrawable3 = getResources().getDrawable(R.drawable.violetred);
                ll_noteList.setBackgroundDrawable(btnDrawable3);
                lv_notesList.setBackgroundDrawable(btnDrawable3);
                break;
            case R.id.LightGrey:
                Drawable btnDrawable4 = getResources().getDrawable(R.drawable.grey);
                ll_noteList.setBackgroundDrawable(btnDrawable4);
                lv_notesList.setBackgroundDrawable(btnDrawable4);
                break;
            case R.id.MediumPurple:
                Drawable btnDrawable5 = getResources().getDrawable(R.drawable.purple);
                ll_noteList.setBackgroundDrawable(btnDrawable5);
                lv_notesList.setBackgroundDrawable(btnDrawable5);
                break;
            case R.id.DarkGray:
                Drawable btnDrawable6 = getResources().getDrawable(R.drawable.gray);
                ll_noteList.setBackgroundDrawable(btnDrawable6);
                lv_notesList.setBackgroundDrawable(btnDrawable6);
                break;
            case R.id.Snow:
                Drawable btnDrawable7 = getResources().getDrawable(R.drawable.snow);
                ll_noteList.setBackgroundDrawable(btnDrawable7);
                lv_notesList.setBackgroundDrawable(btnDrawable7);
                break;
        }

    }
```

功能展示：

![背景更换](https://img-blog.csdnimg.cn/20190520135838750.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

![背景更换2](https://img-blog.csdnimg.cn/20190520135902739.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

## 四、点击+,新建note界面，UI美化

noteslist_layout.xml:

```
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
           />
       <ImageView
           android:layout_width="30dp"
           android:layout_height="30dp"
           android:background="@drawable/search1"
           android:layout_marginRight="10dp"
           android:layout_marginTop="5dp"
           android:layout_marginLeft="10dp"
           android:id="@+id/iv_searchnotes"
           />
   </LinearLayout>

    <FrameLayout
    android:layout_width="match_parent"
    android:layout_weight="1"
    android:orientation="vertical"
    android:layout_height="wrap_content">
    <ListView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:cacheColorHint="#00000000"
        android:divider="#FFFFCC"
        android:dividerHeight="0dp"
        android:id="@id/android:list"
        >
    </ListView>
    <ImageButton
        android:id="@+id/fab"
        android:layout_width="60dp"
        android:layout_height="60dp"
        android:layout_gravity="bottom|center"
        android:layout_margin="45dp"
        android:background="@drawable/tianjia"
        android:backgroundTintMode="add"/>
```
