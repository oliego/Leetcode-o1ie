## No.633 Sum of Squared Numbers
1. 第一想法：第一个指针从1开始，第二个指针从Math.sqrt(c)开始。若sum < c，l++；反之，r--
    + 错误：l需要从0开始
    + 反例：c = 4
2. 第二想法&答案
    + 第一个指针从0开始，第二个指针从Math.sqrt(c)开始
    + 若sum < c，l++；反之，r--
    