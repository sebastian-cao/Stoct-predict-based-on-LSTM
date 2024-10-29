# Stoct-predict-based-on-LSTM
Use LSTM to predict stock
# 一、数据配置
## 数据来源
通过tushare获取start_date到end_date期间的五类数据：开盘价，收盘价，最高价，最低价，成交量。使用tushare需要添加自己的APT，去官网注册即可[tushare官网](https://tushare.pro/document/2)
## 数据清洗
Stock_Price_LSTM_Data_precesing函数用来进行数据预处理以及标准化。  
> **三个参数：**  
  **df：** 上面用tushare获取的源数据。  
  **mem_his_days：** 用来记忆的天数。  
  **pre_days：** 预测未来多少天的股价。  
> **三个返回值：**  
  **X：** 处理好的训练集  
  **y：** 处理好的测试集  
  **X_lately：** 最近的mem_his_days天的数据,用于实际预测未来pre_days天的股价，不参与训练和测试。  
# 二、模型训练和验证
**Step 1：** 用数组多设置几个参数循环遍历（save_weights_only设置成True），模型保存至model文件夹，循环结束后挑出最优mape的模型参数。  
**Step 2：** 用最优的参数再跑一遍（save_weights_only设置成False），结果保存至best文件夹，获取best_model。  
**Step 3：** 用上一步中的路径加载best_model，传入X_test进行验证，结果与y_test比较。  
**Step 4：** 最终使用X_lately作为参数传入模型，如果X_lately为最新数据，结果就是未来两个交易日的股价。  
