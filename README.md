# SQLFlow插件在Zeppelin中的部署说明
## 1.  项目简介
通过将蚂蚁金服开源机器学习工具[SQLFlow](http://sqlflow.org/sqlflow)，集成至基于Web的notebook工具[Apache Zeppelin](http://zeppelin.apache.org/)，从而拓展Zeppelin支持的解释器语言。
## 2.  环境依赖
Zeppelin 版本：zeppelin-0.9.0-SNAPSHOT，安装文档可以参考：[如何安装启动Apache Zeppelin](https://blog.csdn.net/u013686990/article/details/102890085)
## 3.  安装解释器
安装分为以下步骤：

步骤一：准备好解释器项目代码jar包`zeppelin-sqlflow-0.9.0.jar`、配置文件 `interpreter-setting.json`；

步骤二：切换到Zeppelin的安装目录下，创建`interpreter/sqlflow`子目录：
```bash
mkdir ~/zeppelin-0.9.0-SNAPSHOT/interpreter/sqlflow
```
步骤三：将步骤一中的 jar 包和配置文件拷贝到步骤二创建的目录中：
```bash
# 这是在我机器上的路径，仅供参考。
cp ~/zeppelin-sqlflow-0.9.0.jar ~/zeppelin-0.9.0-SNAPSHOT/interpreter/sqlflow
cp ~/interpreter-setting.json ~/zeppelin-0.9.0-SNAPSHOT/interpreter/sqlflow
```
步骤四：启动zeppelin
```bash
cd ~/zeppelin-0.9.0-SNAPSHOT/bin/
./zeppelin-daemon.sh start
```
## 4.  使用说明
进入zeppelin首页，点击右上角的用户，选择interpreter后，进入解释器的参数配置页面。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210315171233284.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p5NDgyODkxOA==,size_16,color_FFFFFF,t_70#pic_center)

填写5个配置参数，分别是：
- sqlflow.serverAddr：sqlflow服务器地址
- mysql.username：数据库登录用户名
- mysql.password：数据库登录密码
- mysql.serverAddr：数据库服务器地址
- mysql.databaseName：数据库名称

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210316103230953.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p5NDgyODkxOA==,size_16,color_FFFFFF,t_70#pic_center)

回到首页，创建一个新的 note，选择默认解释器为 `sqlflow`，如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210315181859518.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p5NDgyODkxOA==,size_16,color_FFFFFF,t_70#pic_center)

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-J5Wp2lpU-1615798656458)(C:/Users/Administrator/Desktop/Create_New_Note.jpg)\]](https://img-blog.csdnimg.cn/20210315165757865.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p5NDgyODkxOA==,size_16,color_FFFFFF,t_70#pic_center)

在打开的笔记本中，开始使用sqflow语法，然后运行，进行功能测试。
下图所示案例中，在 [iris 数据集](https://en.wikipedia.org/wiki/Iris_flower_data_set) 上训练 `DNNClassifier` 分类器，利用训练好的 `DNNClassifier` 对三种类别的鸢尾花进行预测。通过作图能更直观地展示每个特征字段对模型预测的影响程度。

注：每个段落，必须以`" %sqlflow "`开头。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210316104837416.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p5NDgyODkxOA==,size_16,color_FFFFFF,t_70#pic_center)
## 5.  团队简介
本项目由交通银行太平洋信用卡中心信息技术管理部基础平台开发团队发起，旨在加强Athena机器学习平台在数据探索及模型试验方面的功能拓展，为数据科学家提供更加全面、丰富的数据处理工具。通过与蚂蚁金服团队合作，共同编写此插件。最后，也对zeppelin平台开发人员表示鸣谢。

Athena机器学习平台是交通银行太平洋信用卡中心开发的一款覆盖机器学习从模型构建到应用全流程的产品：
- 可视化建模方式，简单拖拉拽即可进行建模，且兼容多种机器学习框架。
- 为数据科学家提供集成化工作 IDE，为模型开发工作提供工具化、自动化支持。
- 为模型离线训练，在线预测提供可管理，可监控，可扩展的运行环境。
- 监控模型训练，模型预测的运行状态，评估模型运行效率，快速验证效果。

以下为Athena机器学习平台部分功能界面展示图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210316163223683.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p5NDgyODkxOA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210316163223634.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p5NDgyODkxOA==,size_16,color_FFFFFF,t_70)
