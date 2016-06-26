##文件说明

analyse程序用来分析一本英文电子书的单词的词频，并把结果保存成文件。

add_word则是根据单词文件自动的将其中的单词上传到自己的扇贝单词书中，避免了自己一个个手动敲打。

config.json是add_word程序的配置文件。

配置文件说明：

- username: 用户名
- password: 用户密码
- bookurl:所添加的单词书的链接地址
- unitname:这里是用户自定义的单元名称，如果自定义的单元名称用完而单词还未添加完，程序会自动停止。如果不填写该内容，程序会自动从1开始作为第一个单元名，之后是2，以此类推。

black_word.txt 是黑名单文件。

test_text.txt 是测试文件。

result.txt 是analyse.py对测试文件的结果输出。

##使用说明

###analyse

该程序在命令行下使用。

1. analyse.py [待分析的文本名] [要输出的文件名] [最小词频] [最大词频]
2. 如果不要求有最大词频，那么将其设置为 $ 
3. 黑名单文件默认为 black_word.txt，该文件必须存在，不需要设置黑名单的话置其内容为空即可
若需设置黑名单，则每行为一个单词，出现在黑名单中的单词将不会出现在最终结果中。

输出的文件中，左边的是相应的单词，右边的数字表示的相应的词频。

###add_word

在使用该程序前，需要提前把配置文件相关的内容填写好。

需要填写的内容有：

- username，用户名
- password，密码
- bookurl，自己创建的单词书的链接地址
- unitname，因为单词书下添加单词是以单元为单位的，每个单元最多添加2000个单词，如果用户想要将单词添加到自定义的单元中，那么就在这里填写想要创建的单元名。需要注意的是，如果所有用户自定义的单元都已经添加满，但是单词还未添加完时，程序是会自动停止的。如果不填写该内容，程序会自动从1开始作为第一个单元名，之后是2，以此类推。

该程序同样在命令行下使用。

add_word.py [[unit_url]] [word.txt]

假如用户只想在某个单元中继续添加单词，那么就指定unit_url参数，该参数是用户想要添加的单元的链接地址。

如果用户不想指定，忽略该参数即可，只需要指定 word.txt 参数，该参数为包含待添加单词的文件名。该文件中，每个单词占一行，analyse程序分析的结果文件可直接作为该程序的参数输入。 

在添加单词过程中，某些单词因为结尾是ed、ing、s、es的形式而无法添加到扇贝单词中，扇贝单词需要原型才能够添加成功，程序一旦发现添加失败，并且单词是属于上述集中情况的，会自动尝试去ed、ing、s、es，之后再进行添加。