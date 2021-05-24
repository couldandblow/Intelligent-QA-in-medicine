# 基于医药知识图谱的智能问答系统
* 这是一个基于Python模块REfO实现的知识库问答初级系统. 该问答系统可以解析输入的自然语言问句生成 SPARQL 查询，进一步请求后台基于TDB知识库的Apache Jena Fuseki 服务, 进而得到问题的结果。
* 提供疾病症状、疾病用药、药品查询等功能。

# 需要环境
* python3.7.1
    * 安装jieba中文分词组件
    * 安装sparqlwrapper，python与Apache Jena Fuseki服务的交互组件
    * Django，Web应用框架，用于交互展示
* Apache Jena，是一个开源的Java语义网框架（open source Semantic Web Framework for Java），用于构建语义网和链接数据应用
    * apache-jena-fuseki，开启Apache Jena Fuseki 服务
* Java环境，Apache Jena需要在Java环境下运行,jena-fuseki要与java版本一致，否则会报错
* 数据
    * [TDB药品疾病知识库](https://pan.baidu.com/s/1V7yqs4HKcQYJqDznf2MbSA)   

# 怎么运行
* 下载TDB药品疾病知识库数据 & clone项目代码
* 开启Apache Jena Fuseki 服务
    *  将TDB数据和Apache Jena Fuseki放在同一个目录下。
    *  进入Apache Jena Fuseki文件夹，运行fuseki-server.bat，然后退出。程序为我们在当前目录自动创建“run”文件夹
    *  将项目代码apache_configuration文件夹下的kgdrug.tll和rules.tll文件移动到“run”文件夹下。
        * kgdrug.tll：知识库本体文件
        * rules.tll：规则推理配置文件
    * 将项目代码apache_configuration文件夹下的fuseki_conf.ttl文件移动到“run”文件夹下。
        * fuseki_conf.ttl：Fuseki配置文件，主要配置上述两个文件的路径和TDB知识库路径
    * 上述操作配置好后，再次运行fuseki-server.bat，开启Apache Jena Fuseki 服务
* 安装python环境需要的包
```python
pip install requirements.txt
```
* 这里需要修改项目代码中setting.py文件中的字典导入路劲，因为我们的文件路径可能不一样。
* 运行KB_query文件夹中的query_main.py，开启命令行模式。
```python
python query_main.py
```
* 在项目根目录下运行manage.py,开启项目的web模式
```
python manage.py runserver

fuseki数据库中添加数据
	把tdb_drug_new文件夹上传到fuseki数据库中
	命令 fuseki-server --loc=path1 /db
	path1是tdb_drug_new的路径，db是数据库名称
修改jena_sparql_endpoint.py文件
	endpoint_url='http://localhost:3030/ds/query' 把它修改为当前数据库中的路径
可以访问了
```
# 参考
[基于 REfO 的 KBQA 实现及示例](http://www.openkg.cn/tool/refo-kbqa)
