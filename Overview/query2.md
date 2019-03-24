## Query

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

我直接把所有的代码都贴上来了。大家可以一个个尝试

我们来看代码，其实很简单，就是对应的结构

#### 插入数据

我们想ca

![Screen Shot 2019-03-24 at 9.13.22 PM](assets/Screen Shot 2019-03-24 at 9.13.22 PM.png)

#### 查询数据

![Screen Shot 2019-03-24 at 9.14.33 PM](assets/Screen Shot 2019-03-24 at 9.14.33 PM.png)

#### 更新

![Screen Shot 2019-03-24 at 9.16.00 PM](assets/Screen Shot 2019-03-24 at 9.16.00 PM.png)

#### 删除

![Screen Shot 2019-03-24 at 9.16.23 PM](assets/Screen Shot 2019-03-24 at 9.16.23 PM.png)

## Git

```bash
$ git show Crud
```

