# Linux Terminal Command

参考链接： [nohup](https://www.cnblogs.com/mandywang/p/11093032.html)
忽略打印的输出。
  nohup ./service >service.log 2>&1 &
  nohup的日志错误

  0    标准输入
  1    标准输出
  2    标准错误信息输出

  2>&1 指的是将错误信息汇入1
