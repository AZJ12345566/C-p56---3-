# C-p56---3-
C语言学习笔记 p56 自定义数据类型-结构体(3)
struct S
{
    int a;
    char c;
    double d;
};
void Init(struct S* ps)
{
    ps->a=100;
    ps->c='w';
    ps->d=3.14;
}

void Print1(struct S tmp)
{
    printf("%d %c %lf\n",tmp.a,tmp.c,tmp.d);
}

void Print2(const struct S* ps)
{
    printf("%d %c %lf\n",ps->a,ps->c,ps->d);
}
#include<stdio.h>
int main()
{
    struct S s=={0};
    Init(&s);//注：这里一定要传地址，因为函数在外部要改变main函数内部的变量一定要传地址
    Print1(s)//传值
    Print2(&s);//传址
    /*s.a=100;
    s.c='w';
    s.d=3.14;*/
    
    return 0;
}



//P57 自定义数据类型-位段
//1.位段的成员必须是int，unsigned int，signed int
//2.位段的成员名后面有一个冒号和一个数字

struct S
{
    int a:2;//这里的冒号意味着这里a只需要2个比特位就够了
    int b:5;
    int c:10;
    int d:30;
};//这里就显现了不跨平台性
//47个bite位-6个字节，但是前面3个放在前四个字节的时候，第4个需要30个比特位不够放了所以重新开辟了新的4个字节
//如果元素大于32则无效
int main()
{
    struct S s;
    printf("%d\n",sizeof(s));
    return 0;
}//输出为8

struct S
{
    char a:3;
    char b:4;
    char c:5;
    char d:4;
};

int main()
{
    struct S s={0};

    s.a=10;
    s.b=20;
    s.c=3;
    s.d=4;
    return 0;
}//输出为220304，因为10，20的高位放不下去，所以产生了这样的结果
//位段具有不跨平台性
