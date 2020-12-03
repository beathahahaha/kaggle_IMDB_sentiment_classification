# kaggle_IMDB_sentiment_classification
two ways to solve problems, lstm and bert

kaggle链接：https://www.kaggle.com/c/word2vec-nlp-tutorial/overview

简介：给出 50,000 IMDB movie reviews，进行0和1情感二分类   

用法：
LSTM代码只要放好train和test数据，运行ipynb文件即可（并且该代码可复用，原数据格式修改后，只要保证ipynb处理数据得到的X和y格式正确即可）

bert代码使用方法：

（建议先阅读https://github.com/wangjiwu/BERT-sentiment--classification）

一、准备好数据

第一是准备预训练数据在uncased目录下，需要从bert，github官网下载uncased预训练模型

第二是准备训练测试数据，格式要和bert中的一致（process_data.ipynb的作用）,把（未拆分9:1的数据）data.tsv和test.tsv文件放在glue下（bert用的都是tsv文件）

二、执行data_cut_off.py
将data.tsv拆分成train.tsv和dev.tsv(训练和验证集9:1)

三、修改run_classifier.py

四、python run_classifier.py -带训练参数

五、python run_classifier.py -带预测参数

其他建议：
1.保存csv文件时小心index=False

2.每次运行时候要从tmp删除checkpoint记录

3.调参时小心内存爆炸


****

给出两段代码，都值得借鉴：  

* 第一个是，lstm实现的pytorch版本，调参以后从0.90569提升到了0.95718（主要是优化器用adam,学习率用0.001，句子长度设置为200），排名大概是100/577，前17%，其实还可以进一步提高

* 环境：python 3,pytorch 1.3.1
  

* 未来的建议：结合word2vec，试一试xgboost和bilstm（可以参考kaggle上其他人的解答）     

 
****
* 第二个是，利用github开源的bert模型进行训练，（但是没有用到官网给的语料库unlabeledTrainData.tsv， 第一个代码的gensim中的word2vec用到了），二分类情感分类模型

* 环境： python 3 ， tensorflow 1.12

* 虽然用到了预训练模型，但是效果还是没有那么好，最后效果大概是0.90896.

可能原因分析：可能是超参数没有调好（bert输入参数没有完全理解透彻，后续还要跟进，另外可以研究bert的loss的可视化输出，网上有修改的源码），也可能是没有用上语料库的原因，总之效果并不理想

 
****
综上，两段代码都有需要改进的地方，未来值得深究（另外备注一点：bert还可以做多标签情感分类，多标签情感分类属于另一主题，留给未来研究，kaggle相关比赛建toxic comment：https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge ）

 
附录： kaggle——情感分类专辑：https://zhuanlan.zhihu.com/p/70361361
