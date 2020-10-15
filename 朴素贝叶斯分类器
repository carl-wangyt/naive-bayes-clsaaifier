#功能：朴素贝叶斯分类器
#作者: 王滢涛


#训练样本
doc = [['chinese','beijing','chinese'],
       ['chinese','chinese','shanghai'],
       ['chinese','macao',''],
       ['tokyo','japan','chinese']]
#训练样本类别
lnc = ['yes','yes','yes','no']
#训练样本包含单词种类
mv = 0
#类c下单词tk在各文档出现的次数之和
tk = 0
#类c下单词总数
total = 0
#新样本
test = ['beijing','beijing','beijing','shanghai','japan']
#新样本每种单词的集合
test_d =[]
#新样本字典，记录每个单词出现的次数
test_dic = {}
#先验概率
fpy = fpn = 0.0
#类条件概率
py = pn = 1   

#先验概率计算
def fp():
    global fpy,fpn
    tt = 0
    fpy_n = fpn_n = 0
    for i in range (0,len(lnc)):
        for j in range (0,3):
            if (lnc[i] == 'yes')and(doc[i][j] != ''):
                fpy_n += 1
                tt += 1
            elif (lnc[i] == 'no')and(doc[i][j] != ''):
                fpn_n += 1
                tt += 1
    fpy = fpy_n/tt
    fpn = fpn_n/tt
        

#类条件概率计算
def ccprobability(d,y):
    global mv,tk,total
    tk = 0
    total = 0
    length = len(doc)
    for i in range(0,length):
        for j in range(0,3):
            if (lnc[i] == y)and(doc[i][j] == d):
                tk += 1
    for i in range(0,length):
        for j in range(0,3):
            if (lnc[i] == y)and(doc[i][j] != ''):
                total += 1
    #print('tk = {},total = {}'.format(tk,total))
    return (tk +1)/(total +mv)

#计算训练样本包含单词种类数
def cmv():
    global mv
    length = len(doc)
    doc_dic = {}
    for i in range(0,length):
        for j in range(0,3):
            if (doc[i][j] not in doc_dic)and(doc[i][j] != ''):
                doc_dic[doc[i][j]] = 1
            elif (doc[i][j]  in doc_dic):
                doc_dic[doc[i][j]] += 1
    mv = len(doc_dic)

#计算新样本单词种类和出现次数
def test_div(test_x):
    global test_d,test_dic
    length = len(test_x)
    
    for i in range(0,length):
        if test_x[i] not in test_dic:
            test_dic[test_x[i]] = 1
            test_d.append(test[i])
        elif test_x[i] in test_dic:
            test_dic[test_x[i]] += 1    

#计算后验概率并判断文档类别
def pd(d):
    global py,pn,fpy,fpn,test_dic
    for i in range (0,len(d)):
        for j in range (0,test_dic[d[i]]):
            py = ccprobability(d[i],'yes')*py
    for i in range (0,len(d)):
        for j in range (0,test_dic[d[i]]):
            pn = ccprobability(d[i],'no')*pn       
    print('p(yes|d) = ',(py*fpy))
    print('p(no|d) = ',(pn*fpn))
    if (py*fpy) > (pn*fpn):
        print('这个文档类别属于china')
    else:
        print('这个文档类别不属于china')    

def main():
    cmv()
    test_div(test)
    fp()
    pd(test_d)

main()
