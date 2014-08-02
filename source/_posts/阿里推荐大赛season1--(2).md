title: 阿里推荐大赛season1--(2)
date: 2014-07-31 22:31:31
tags: [Alidata, Python, Recommender]
categories: [Recommender]
description: Season1使用Python这把利器！用它数据处理，数据分析；用它画图；用它写算法。用它就意味着效率！

---
早在去年暑假在[无锡为立][weili]实习的时候，我就接触到了*推荐系统*相关知识，那时候把[《推荐系统实践》][ref1]一书研究了下，并照着实现了大部分算法，尤其是其中的*协同过滤*跟*LFM*模型，也是在那个时候接触到了Python。

这次比赛开始，我们就确定使用Python作为第一阶段的开发语言，因为方便直观，上手快，开发效率高。Season1前前后后，算上一些垃圾代码，一万行代码还是有的。仅以此文纪念我们曾经写过的Python代码。

# 轻松开好头
数据量不大，基本可以暴力读到内存操作。原始数据的时间列是中文日期格式，利用正则先转成可处理的日期格式，假设数据是2013年的。
```python
def get_date(origin_date):
    month_day = re.findall(r"[\d|.]+", origin_date)
    month = int(month_day[0])
    day = int(month_day[1])
    return date(2013, month, day)
```
这样我们按照
```python
def classify_data(origin_path):
    reader = csv.reader(open(origin_path))
    train_writer = csv.writer(file(train_path, 'wb'))
    test_writer = csv.writer(file(test_path, 'wb'))
    for user,brand,action,r_date in reader:
        now = get_date(r_date)
        if now >= date(2013,4,15) and now < date(2013,7,15):
            train_writer.writerow((user,brand,action,r_date))
        elif now >= date(2013,7,15) and now <= date(2013,8,15):
            test_writer.writerow((user,brand,action,r_date))
```













[weili]:http://58.214.255.186:3000/
[ref1]:http://book.douban.com/subject/10769749/