##R中常见的好的代码
add labels
```
library(tidyverse)
data4 <- select(data,Survived,Pclass)
data4$Pclass <- factor(data4$Pclass,levels=c(1,2,3),labels=c("1","2","3"))   //将数字型变量转化为字符型
data4$Survived <- factor(data4$Survived,levels=c(0,1),labels=c("死亡","存活"))    //将数字转化为文字（属于加标签，原本的类型不变）
ggplot(data4)+
   geom_bar(mapping=aes(x=Survived,fill=Pclass),
            stat="count",binwidth=0.3,position="dodge")
count(data4$Survived)
```
fill NA data
``` 
data10 <- select(data,Survived,Cabin)
data10$Cabin[data10$Cabin==""] <- "0"             //填充空白数据
data10$Cabin[data10$Cabin!="0"] <- "1"

data10$Cabin <- factor(data10$Cabin,levels=c(0,1),
                       labels=c("无船舱号","有船舱号"))
                       
ggplot(data10)+
  geom_bar(mapping=aes(x=Cabin,fill=Survived),
           stat="count",binwidth=0.3,position="dodge")
```
draw a boxplot with significant marks
```
library(ggsignif)
compaired <- list(c("合瓣花","离瓣花"),c("合瓣花（浅裂）","离瓣花"),c("合瓣花（浅裂）","合瓣花"))
ggplot(data2,aes(petal,insect,fill=petal))+
           geom_boxplot()+
   geom_signif(comparisons = compaired,step_increase = 0.1,
               map_signif_level = F,test = wilcox.test)            //箱线图加显著性


data$insect[data$petal=="离瓣花"]           //提取petal中所有为“离瓣花”的insect数据
```
dataframe reshape
```
my2 <- group_by(myd,City_county,道路1,name)
my2 <- summarise(my2,count=n())
  my3 <- filter(my2,City_county=="大庆市大同区")
  my4 <- acast(my3,道路1~name)                      //数据的重塑，其中reshape包的重铸函数为cast()，reshape2包的重铸函数为dcast()和acast()
  my4[is.na(my4)] <- 0                               
  write.csv(my4,"C:\\Users\\50293\\Desktop\\summaryx.csv") 
```
