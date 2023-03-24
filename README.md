# Umpty-dah
#### Video Demo:  <https://youtu.be/lrL-VSv4E7c>
#### Description:
 > Umpty-dah is android application made using java which converts english alphabets into morse code.

 MORSE CODE is a telecomunication language which was used by the military and the aircraft pilots to easily communicate with each other without using much energy.

 morse code was also used by the army in the world war to encrypt the communication between the troops without the enemy knowing.

 to know more click here [MORSE CODE.](https://en.wikipedia.org/w/index.php?title=Morse_code&oldid=1145114509)

### umpty-dah app has:
 1. interactive home page.
 2. text to morsecode page.
 3. morse code info page.
 4. about page.

Application look

![application](/workspaces/81160682/project/app.png)

the applicationa apk file can be found in the file path:
##### umptydah\app\release\app-release.apk

 Splashactivity.java

````java

@SuppressLint("CustomSplashScreen")
public class SplashActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_splash);

        Intent i = new Intent(SplashActivity.this, Navigation.class);
        new Handler().postDelayed(() -> {
            startActivity(i);
            finish();
        },3000);
    }
}
````
the activity is passing intent from splash activity to navigation, for the duration of 3000 miliseconds. for this to work is changed the

AndroidManifest.xml

````xml
 <activity
            android:name=".Navigation"
            android:exported="true"
            android:theme="@style/myTheme.Umptydah"/>
        <activity
            android:name=".SplashActivity"
            android:exported="true"
            android:theme="@style/myTheme.Umptydah">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
````
 if the activity intent filter is not changed the app always starts with the default main activity.

 here i changed the intent activity from navigation activity to splach activity after the execution of the splachactivity the intent is passed to navigation activity.

as i wanted to add my own tool bar it changed the theme.xml to no action bar.

````xml
<resources>
    <!-- Base application theme. -->
    <style name="Theme.Umptydah" parent="Theme.MaterialComponents.DayNight.NoActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/teal_700</item>
        <item name="colorPrimaryVariant">#515152</item>
        <item name="colorOnPrimary">@color/white</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">#5EA586</item>
        <item name="colorSecondaryVariant">#A8A8A8</item>
        <item name="colorOnSecondary">@color/black</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
    </style>
</resources>
````

for creating the navigation view i created a xml called activity_navigation.xml

````xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:context=".Navigation"
    android:id="@+id/drawerlayout"
    tools:openDrawer="start">
    <include layout="@layout/appbarmain"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        />
    <com.google.android.material.navigation.NavigationView
        android:id="@+id/navView"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        app:itemIconTint="#CCE3DE"
        android:layout_gravity="start"
        android:background="#445A5B"
        android:fitsSystemWindows="true"
        app:itemTextColor="#CCE3DE"
        app:headerLayout="@layout/header"
        app:menu="@menu/navitems"/>

</androidx.drawerlayout.widget.DrawerLayout>
````
which consists a drawerlayout and a navigation view which takes a xml called appbarmain.xml using include tag.


````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical">
    <com.google.android.material.appbar.AppBarLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        >
        <androidx.appcompat.widget.Toolbar
            android:layout_width="match_parent"
            app:titleTextColor="#a4c3b2"
            android:layout_height="wrap_content"
            android:background="#445A5B"
            app:title="Umpty-dah"
            android:id="@+id/toolbar"/>

    </com.google.android.material.appbar.AppBarLayout>
    <include layout="@layout/frame"/>
</LinearLayout>
````
it takes the toolbar and the navigation items and the navigation frame layout container where each fragment is displayed by navigationview the navitems are made using android menue and passed in the ActivityNavigation.xml

all the logo and vector graphics dispayed are inside the drawable folder.
 the file path for the project resourse folder is

  #### umptydah\app\src\main\java\com\example\umpty_dah

Navigation has 4 fragments :

1. hFragment.java and corresponding fragment_h.xml .

2. aFragment.java and corresponding fragment_a.xml .

3. rFragment.java and corresponding fragment_r.xml .

4. iFragment.java and corresponding fragment_i.xml .


hfragment has all the alphabets arranged in the order in xml file all linked to button naming same alpabet and then on creation of the fragment the database is loaded and the onclick listener if the corresponding letter is pressed the alphabet is passed to for loop to check wether the alohabet is in the database and if found the morse code is shown.

```` java

public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        view = inflater.inflate(R.layout.fragment_h, container, false);
        MyDb dbhelper = MyDb.getInstance(getActivity());
        ArrayList<MorsecodeDB> receive = (ArrayList<MorsecodeDB>) dbhelper.morsecodeDao().getAllmorsecodeDB();
         textView = view.findViewById(R.id.textView);

        init();

        a.setOnClickListener(view -> {
            a.setBackgroundColor(-5);
            for (int i = 0; i < receive.size(); i++) {
                if(a.getText().toString().toUpperCase().equals(receive.get(i).getAlphabet())){
                    textView.setText(receive.get(i).getMorse_code());
                }
            }
        });
    }

````

same is done for all the letters of the english alphabet.


 ## Database
 database is created upon creation of the hfragment (home fragment)
 here i have used room library to store data internally to prepopulate the data base with the key and value pairs of morse code and alphabets.


 for creating database you must first create entity morsecodedb.class structure of the data for the databse table having all the column names and the values to be passed. using a constructor to set the value.

````java
@Entity(tableName = "morsecodeDB")
public class MorsecodeDB {
    @PrimaryKey(autoGenerate = true)
    private int id;
    @ColumnInfo (name = "alphabet")
    private final String alphabet;
    @ColumnInfo (name = "morse_code")

    private final String morse_code;
    public MorsecodeDB(int id, String alphabet, String morse_code) {
        this.id = id;
        this.alphabet = alphabet;
        this.morse_code = morse_code;
    }
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getAlphabet() {
        return alphabet;
    }
    public String getMorse_code() {
        return morse_code;
    }
}
````

now you have to create a dao interface to pass the query to select and insert all the data into the database.

````java
public interface MorsecodeDao {
    @Query("SELECT * FROM morsecodeDB")
    List<MorsecodeDB> getAllmorsecodeDB();
    @Insert
    void insertAll(MorsecodeDB[] morsecodeDBS);
}
````

now create a data pool to insert into the database constructor to add data to database to populatedb class.

````java
public class populateDB {
    public static MorsecodeDB[] populatedb() {
        return new MorsecodeDB[]{
                new MorsecodeDB(1, "A", ". ---"),
                //insert all the data here           ------------"--"----------------,
                new MorsecodeDB(36, "9", "--- --- --- --- .")};
    }
}
````
and finally in the mydata class which extends RoomDatabase

````java
@Database(entities = {MorsecodeDB.class}, exportSchema = false ,version = 1)
public abstract class MyDb extends RoomDatabase {
    public static final Object LOCK = new Object();
    private static final String DB_NAME = "morsecodeDB.db";
    private static MyDb sinstance;
    public static MyDb getInstance(final Context context){
    if(sinstance == null){
        synchronized (LOCK) {
            sinstance = Room.databaseBuilder(context.getApplicationContext(), MyDb.class, MyDb.DB_NAME)
                    .allowMainThreadQueries()
                    .fallbackToDestructiveMigration()
                    .addCallback(new Callback() {
                        @Override
                        public void onCreate(@NonNull SupportSQLiteDatabase db) {
                            super.onCreate(db);
                            AppExecutors.getInstance().getDiskIO().execute(() -> getInstance(context).morsecodeDao().insertAll(populateDB.populatedb()));
                        }
                    }).build();
        }
    }
    return sinstance;
}
    public abstract MorsecodeDao morsecodeDao();
}
````

this finishes the database setup and whenever you call a database it will prepopulate the database and then we can use the dbhelper to search and do db operations.

aFragment.java

````java
public class aFragment extends Fragment {
    public aFragment() {
        // Required empty public constructor
    }
    EditText editText,textView;
    AppCompatButton button;
    @SuppressLint("MissingInflatedId")
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        View view = inflater.inflate(R.layout.fragment_a, container, false);

        MyDb dbhelper = MyDb.getInstance(getActivity());

        ArrayList<MorsecodeDB> receive = (ArrayList<MorsecodeDB>) dbhelper.morsecodeDao().getAllmorsecodeDB();

        textView = view.findViewById(R.id.morseview);

        editText = view.findViewById(R.id.edittext);

        button = view.findViewById(R.id.convertbtn);

        button.setOnClickListener(view1 -> {
            String morse;

            String words = editText.getText().toString();

            String [] sepwords = words.toUpperCase().split("");

            ArrayList<String> text = new ArrayList<>(Arrays.asList(sepwords));

            StringBuilder result = new StringBuilder();

            for (int i = 0; i < text.size(); i++) {
                if (text.get(i).equals(" ")) {
                    result.append("       ");
                }
                for (int j = 0; j < receive.size(); j++) {
                    if (text.get(i).equals(receive.get(j).getAlphabet())){
                            morse = receive.get(j).getMorse_code();
                            result.append(morse).append("   ");
                    }
                }
            }
            textView.setText(result);
        });
        return view;
    }
}
````

important point when you want to use the find view by id in fragment use a local variable to make it simpler
````java

View view = inflater.inflate(R.layout.fragment_a
container, false);

textView = view.findViewById(R.id.morseview)
editText = view.findViewById(R.id.edittext);
button = view.findViewById(R.id.convertbtn);
````

in the corrospond frangment and its xml file i have taken a edit text view and a button calle convert when ever you type text inside the edit text view and then click convert the text is taken inside a for loop where the text is first converted to string and then to string array and then passed onto a arraylist as list having a nested for loop where the loop compares the text to the database and if present the morsecode sent to a string builder and then it is shown in the textview.

rfragment.java

i wanted to create a simple information page in the for understanding how morse code works and to use the app so i just crated a linear layout and added information inside text view,simple and clean.

ifragment.java

here i wnated to create a simple about page but it would take me long time to create it by my own so i used a package

by declaring the dependensies in the gradel module.
````xml
implementation 'com.github.medyo:android-about-page:1.2.5'
````

adding this
````java
public class iFragment extends Fragment {
    public iFragment() {
        // Required empty public constructor
    }
    public View onCreateView(@NonNull LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        new Element();
        View aboutPage = new AboutPage(getActivity())
                .isRTL(false)
                .setDescription("Umpty_dah\n"+"this is my cs50 project\n" +
                        "International Morse Code\n" +
                        "was standardized at the International Telegraphy Congress in 1865 in Paris and was later made the standard by the" +
                        "International Telecommunication Union (ITU).")
                .setImage(R.drawable.logo)
                .addItem(new Element().setTitle("Version 1.0"))
                .addWebsite("https://en.wikipedia.org/w/index.php?title=Morse_code&oldid=1145114509","more about morsecode")
                .addGroup("Connect with us")
                .addEmail("mr.pheus4@gmail.com")
                .addYoutube("UCia6Fqzt6n16tTX1PAU4Gxw")
                .create();

        setContentView();

        return aboutPage;
    }
    public void setContentView() {
    }
}
````

combing all this the gradel build will finish the app.

for designing my app logo i used [inkscape.](https://inkscape.org/)

and for colorgrading my app i used an opensource software called[Rickrack.](https://eigenmiao.com/rickrack/)