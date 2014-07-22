#简介
Hitar是基于Doctrine-DBAL的ORM框架。

#安装

通过composer安装

    {
        "require":{
            "kasonyang/hitar" : "*"
        }
    }

#在项目中使用Hitar

    require "vendor/autoload.php";
    
    //初始化Hitar
    \Hitar\DatabaseManager::addDatabase('mydb', array(
        'dbname' => 'your_db',
        'user' => 'user',
        'password' => 'your_password',
        'host' => 'localhost',
        'driver' => 'pdo_mysql'
    ));
    \Hitar\DatabaseManager::selectDatabase('mydb');
    
    //构建ORM模型
    /**
     * @table article Article
    class Article extends \Hitar\RecordBase{
        
        /**
         * @field integer
         * @primary
         * @generator increment
        protected $id;
        
        /**
         *
         * @field string
         */
        public $title;

        function getId(){
            return $this->id;
        }
        
    }
    
    //向数据库插入一条新数据
    $article = new \Article();
    $article->title = '一本书';
    $article->save();
    
    //取得Table对象
    $tb = \Article::table();
    //读取记录的条数
    echo $tb->count();
    //读取所有记录
    $list = $tb->select();
    foreach($list as $art){
        echo $art->title;
    }



#支持的数据库

Hitar支持的数据库由Doctrine-DBAL决定，到目前为止，支持的数据库有

* MySQL
* Oracle
* MSSQL
* PostgreSQL
* SAP Sybase SQL Anywhere
* SQLite
* Drizzle

具体情况请浏览[Doctrine DBAL的文档](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/index.html)