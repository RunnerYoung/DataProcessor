# DataProcessor
+ Analys matlab data and csv data
####文件夹结构分析 Analysis of the dir
+ Mat file
```    
    stock 按照月建立文件夹 
        tickab200701
            *.SH.mat  
            *.SZ.mat 
            （本月 可能不会同时都有SH SZ）
        tickab200701
            *.SH.mat  
            *.SZ.mat
    2016/2017 按照天
        201601Sh股票五档分笔
            20160104 （注意 日期中 天有间隔）
                000001_20160104.csv
                000002_20160104.csv
                000003_20160104.csv
                000004_20160104.csv
            20160105
            20160106
        201601SZ股票五档分笔
        201602SH股票五档分笔
        201602SZ股票五档分笔
```        
    
×××    
#####压缩比计算估算  
```
  文件压缩比：6.1--6,。25
  解压前|解压后
   |2.1G  |13 G|
   | 1.6G |10 G|
```   
#####磁盘需求量估算
+ stock 约566G        
+ 2016  约77G    
+ 2017  约42G
MAX_NEED_DISK = 566+(77+42)*6.2 = 1280G
####StocklistA
+ 按照股票代码文件夹中stocklistA文件里的第一列进行处理   

####Matlab文件2016年9月之前
+ 1.从mat文件中提取date和time，转换成时间戳，
+ 2.StockTickAB.Price (col 1 只有一列)
+ 3.StockTickAB.Volume (col 1 只有一列)
+ 4-8.StockTickAB.BidPrice10 （col1-5）
+ 9-13.StockTickAB.BidVolume10 （col1-5）
+ 14-18.StockTickAB.AskPrice10（col1-5）
+ 19-23．StockTickAB.AskVolume10（col1-5）


>ps:2016年九月之后的时间按照2016/2017文件夹里取
Mat文件到20160930结束,之后的股票时间信息从 2016/2017获取

####2016年九月之后 
+ 第一列：csv文件中提取date和time，转换成时间戳，
+ 第二列：成交价，stock文件夹里的StockTickAB.Price，2016/2017文件夹里的成交价，Stk_Tick_2016/2017文件夹里的最新价
+ 第三列：成交量，stock文件夹里的StockTickAB.Volume，2016/2017文件夹里的成交量*100，Stk_Tick_2016/2017文件夹里的成交量*100
+ 第四列到八列：买一到五价，stock文件夹里的StockTickAB.BidPrice10前五列，2016/2017文件夹里的b1价，b2价~b5价，Stk_Tick_2016/2017文件夹里的买一价，买二价~买五价
+ 第九列到十三列：买一到五量，stock文件夹里的StockTickAB.BidVolume10前五列，2016/2017文件夹里的量，b1量~b5量，Stk_Tick_2016/2017文件夹里的买一量，买二量~买五量
+ 第十四列到十八列：麦一到五价，stock文件夹里的StockTickAB.AskPrice10前五列，2016/2017文件夹里的s1价，s2价~s5价，Stk_Tick_2016/2017文件夹里的卖一价，卖二价~卖五价
+ 第十九列到二十三列：卖一到五量，stock文件夹里的StockTickAB.AskVolume10前五列，2016/2017文件夹里的量，s2量~s5量，Stk_Tick_2016/2017文件夹里的卖一量，卖二量~卖五量

####时间区间要求
+ 只获取此区间之内9:30~11.30，13：00~15:00
