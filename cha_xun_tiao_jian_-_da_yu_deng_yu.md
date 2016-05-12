# 查詢條件 - 是否有值

User.java
```java
public class User extends RealmObject {
    private int id;
    private String name;

    public void setId(int id) {
        this.id = id;
    }

    public int getId() {
        return id;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

MainActivity.java
```java
public class MainActivity extends AppCompatActivity {

    @RealmModule(classes = {User.class})
    public static class Module {
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        RealmConfiguration config = new RealmConfiguration.Builder(this)
                .name("database_name.realm")
                .setModules(new Module())
                        // 如之前有建立過相同資料庫，將其移除。
                .deleteRealmIfMigrationNeeded()
                .build();
        Realm realm = Realm.getInstance(config);
        realm.beginTransaction();
        User item1 = realm.createObject(User.class);
        item1.setId(0);
        item1.setName("");
        User item2 = realm.createObject(User.class);
        item2.setId(1);
        item2.setName(null);
        realm.commitTransaction();

        final String NAME = "name";

        String text = "";
        // Name 為空的資料項。
        text += realm.where(User.class).isEmpty(NAME).findFirst().getId() + "\n";
        // Name 為 NUll的資料項。
        text += realm.where(User.class).isNull(NAME).findFirst().getId() + "\n";
        // Name 不為 NUll的資料項。
        text += realm.where(User.class).isNotNull(NAME).findFirst().getId() + "\n";

        TextView v = new TextView(this);
        v.setText(text);
        setContentView(v);
    }
}
```