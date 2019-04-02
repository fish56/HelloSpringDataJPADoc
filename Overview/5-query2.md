## Query2

下面很简单，就是把之前`CrudRepository`接口里面的方法都用一遍

![Screen Shot 2019-03-24 at 9.23.40 PM](assets/Screen Shot 2019-03-24 at 9.23.40 PM.png)



```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MonkeyRepoTest {
    @Autowired
    private MonkeyRepo monkeyRepo;

    @Test
    public void save(){
        // Monkey monkey = new Monkey("Jack");
        // monkeyRepo.save(monkey);

        List<Monkey> monkeys = new ArrayList<>();
        Monkey monkey1 = new Monkey("Bob");
        Monkey monkey2 = new Monkey("Peter");
        monkeys.add(monkey1);
        monkeys.add(monkey2);
        monkeyRepo.saveAll(monkeys);
    }


    @Test
    public void find(){
        Optional<Monkey> monkey1 = monkeyRepo.findById(3l);
        System.out.println(monkey1.map(Monkey::getId).get() + ": " 
                + monkey1.map(Monkey::getName).get());

        Iterable<Monkey> monkeys = monkeyRepo.findAll();
        for(Monkey monkey : monkeys){
            System.out.println(monkey.getId() + ": " + monkey.getName());
        }
    }

    @Test
    public void update(){
        Monkey monkey = new Monkey("Jack");
        monkey.setBirthDay(new Date());
        monkey.setId(1l);
        monkeyRepo.save(monkey);
    }

    @Test
    public void delete(){
        monkeyRepo.deleteById(2l);
    }
}
```

我直接把所有的代码都贴上来了，大家先自己可以一个个尝试下。

然后我们来看下代码，其实很简单，就是对应的SQL基本的增删改查。

#### 插入数据

- `monkeyRepo.save(monkey)`

  -> `insert into monkey (birth_day, name) values (?, ?)`

- `monkeyRepo.saveAll(monkeys)`

  -> 多次调用 `insert into monkey (birth_day, name) values (?, ?)`

![Screen Shot 2019-03-24 at 9.13.22 PM](assets/Screen Shot 2019-03-24 at 9.13.22 PM.png)

#### 查询数据

- `monkeyRepo.findById(3l)`

  -> `select * from monkey where id = 3`

- `monkeyRepo.findAll()`

  -> `select * from monkey`

程序中调用SQL语句有一个问题就是，如果SQL查询只返回一条数据，那么这算是一个对象，还是算一个列表，只是列表中只有一个元素？

得益于Java的强类型，我们可以很清楚的知道结果。

![Screen Shot 2019-03-24 at 9.14.33 PM](assets/Screen Shot 2019-03-24 at 9.14.33 PM.png)

#### 更新

更新和save是一个api。当我们调用`monkeyRepo.save(monkey)`的时候，如果Spring Data JPA发现这个monkey里面存在主键，就会把它翻译成`update monkey ... where id=? `而不是 `insert  …`

![Screen Shot 2019-03-24 at 9.16.00 PM](assets/Screen Shot 2019-03-24 at 9.16.00 PM.png)

#### 删除

``` java
    @Test
    public void delete(){
        monkeyRepo.deleteById(2l);
    }
```



![Screen Shot 2019-03-24 at 9.16.23 PM](assets/Screen Shot 2019-03-24 at 9.16.23 PM.png)

## Git

```bash
$ git show Crud
```

