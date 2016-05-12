# 查詢條件 - 數值比對

User.java
```java
public class User extends RealmObject {
    private int id;
    private String name;

    public void setId(int id) { this.id = id; }
    public int getId() { return id; }

    public void setName(String name) { this.name = name; }
    public String getName() { return name; }
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
                // 如上次以建立過相同名稱資料庫，但欄位結構已經改變時，會刪除舊資料庫，不是實務上的必要動作。
                .deleteRealmIfMigrationNeeded()
                .build();
        Realm realm = Realm.getInstance(config);
        
        realm.beginTransaction();
        // 這裡清空資料表，只是為了保持乾淨讓執行結果正常，不是實務上的必要動作。
        realm.clear(User.class);
        for (int i = 0; i < 200; i++) {
            User item = realm.createObject(User.class);
            item.setId(i);
            item.setName(String.valueOf(i));
        }
        realm.commitTransaction();

        final String ID = "id";
        final String NAME = "name";
        String text = "";
        // id = 6 的資料項。
        text += realm.where(User.class).equalTo(ID, 6).findFirst().getId() + "\n";
        // id >= 6 的資料項。
        text += realm.where(User.class).greaterThanOrEqualTo(ID, 8).findFirst().getId() + "\n";
        // id <= 6 的資料項。
        text += realm.where(User.class).lessThanOrEqualTo(ID, 6).findFirst().getId() + "\n";
        // id > 6 的資料項。
        text += realm.where(User.class).greaterThan(ID, 6).findFirst().getId() + "\n";
        // id < 6 的資料項。
        text += realm.where(User.class).lessThan(ID, 6).findFirst().getId() + "\n";
        // id 在 50 ~ 100 之間 的資料項。
        text += realm.where(User.class).between(ID, 50, 100).findFirst().getId() + "\n";
        // Name 是 1 開頭的資料項。
        text += realm.where(User.class).beginsWith(NAME, "1").findFirst().getName() + "\n";
        // Name 是 1 結尾的資料項。
        text += realm.where(User.class).endsWith(NAME, "1").findFirst().getName() + "\n";
        // Name 裡包含 1 的資料項。
        text += realm.where(User.class).contains(NAME, "1").findFirst().getName() + "\n";

        TextView v = new TextView(this);
        v.setText(text);
        setContentView(v);
    }
}
```