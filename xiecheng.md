# Э���ŵ�
* �����ó�CPU�����������Ƭ�����̲߳�ͬ��Э�����Լ������ó�CPU������������������һ��Э�����У����������κ�ʱ���п��ܱ�ϵͳ���ȴ�ϡ����Э�̵�ʹ�ø��������׶������Ҷ�������²���Ҫ�����ơ�
* ���߳���ȣ�Э�̵��л��ɳ�����ƣ��������û��ռ�����ں˿ռ䣬����л��Ĵ��۷ǳ���С��
* ĳ�������ϣ�Э�����̵߳Ĺ�ϵ�������߳�����̵Ĺ�ϵ�����Э�̻���ͬһ���̵߳�������֮�����У�����Ҫ��	

## python ����
```
import time

def comsumer():
    ret = ''
    while True:
        product = yield ret
        if not product:
            print("there is not any product")
            return
        print('[COMSUMER]: comsume %s '%product)
        time.sleep(1)
        ret = 'Done'

def produce(generator):
    generator.__next__() # ִ�е�yield��,���ص�retΪnull,�����ȡ
    n = 0
    while n < 10 :
        n += 1
        product = "prod" + str(n)
        print("[PRODUCT] product %s "% product) 
        ret = generator.send(product)
        print("[PRODUCT] result: %s"%ret)
    generator.close()

if __name__=='__main__':
    c = comsumer()
    produce(c)

```