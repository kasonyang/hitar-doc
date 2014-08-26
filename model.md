#数据库模型

Hitar数据库模型对象以`\Hitar\RecordBase`为基类，采用文档标注的方式实现ORM映射。

##数据库模型标注

1. `@table`标注

    格式：`@table 真实数据表名 数据表的别名`

    @table标注是数据表的标注，标注于模型类。

1. `@field`标注

    格式：`@field 字段类型`

    @field标注是字段标注，标注于属性，带有此标注的都被认为数据表字段，字段名与属性名一致。

1. `@primary`标注

    格式：`@primary`

    @primary标注是主键字段标注，标注于属性，必须与`@field`标注一起使用，带有此标注的字段被认为是数据表的主键，同一个模型，若有多个@primary标注，则认为模型对应的数据表为联合主键。

1. `@generator`标注

    格式：`@generator 生成器类型`

    @generator必须和@field标注一起使用，代表字段为生成器字段，即数据由数据库自动生成的字段，比如自增字段、序列字段等。Hitar暂时支持的生成器类型为`increment`,即自增字段。


数据库模型示例

    /**
     * @table article Article
     */
    class Article extends \Hitar\RecordBase{
        
        /**
         * id字段，主键，自增字段，前面加上protected修饰符，可以防止外部直接修改id字段
         * @field integer
         * @primary
         * @generator increment
        protected $id;
        
        /**
         * title字段，字符串类型，如MySQL的varchar类型
         * @field string
         */
        public $title;

        function getId(){
            return $this->id;
        }
        
    }

##数据的读取

    定义好模型后，我们就可以通过模型对数据库进行查询修改删除的操作了。

1. 读取一条记录

    如果知道记录的主键，那么就可以通过主键获得唯一的记录了，此时，我们可以简单的通过模型的静态方法`get`来读取到主键对应的记录。

例如：

    $article = Article::get(['id' => 1]);//读取id为1的记录，如果记录不存在，返回`false`,如果存在，返回Article实例


