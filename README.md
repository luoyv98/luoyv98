#define _CRT_SECURE_NO_WARNINGS

#define _CRT_SECURE_NO_WARNINGS
#include<stdlib.h>
#include<stdio.h>

typedef struct LNode
{
	int data;
	struct LNode* next;
}LNode, * LinkList;

LinkList Head_Insert(LinkList L, int& m)
{


	LNode* s;//定义一个新的结点地址；

	int x;
	scanf("%d", &x);//输入x
	for (; x != 9999;)//定义一个终止数
	{
		s = (LNode*)malloc(sizeof(LNode));
		s->data = x;
		s->next = L->next;
		L->next = s;
		m++;
		scanf("%d", &x);
	}                    //利用for循环完成头插法的执行
	return L;
}

LNode* GetElem(LinkList L, int i)
{
	int j = 1;
	LNode* p = L->next;
	if (i == 0)
		return L;
	if (i < 1)
		return NULL;
	while (p != NULL && j < i)
	{
		p = p->next;
		j++;
	}
	return p;
}

void Head_ListInsert(LinkList& L, int i, int x)
{
	LNode* p = GetElem(L, i - 1);
	LNode* s;
	s = (LNode*)malloc(sizeof(LNode));

	s->data = x;
	s->next = p->next;
	p->next = s;
}

//删除第一个元素

//通过查找第一个元素，如果为x，则删除
void Del_x(LinkList &L, int x)
{
	LNode *q=L->next,*p;

	
	while (q != NULL)
	{
		if (q->data == x)
		{
			p = q->next;
			q->data = p->data;
			q->next = p->next;
			free(p);
		}
		else
			q = q->next;
	}
}

int main()
{
	LinkList L;
	puts("请输入一个单链表，且以输入9999结束");
	int m = 0;
	L = (LinkList)malloc(sizeof(LNode));//为头节点申请空间
	L->next = NULL;//完成头节点的定义；
	L = Head_Insert(L, m);

	printf("请输入要插入的值：");
	int x = 0;
	scanf("%d", &x);
	printf("请输入要插入的位置：");
	int i = 0;
	scanf("%d", &i);
	Head_ListInsert(L, i, x);
	
	printf("请输入要删除的数：");
	int k;
	scanf("%d", &k);
	Del_x(L, k);


	puts("是否要打印单链表？\n1.是  2.否");
	int n = 0;
	scanf("%d", &n);
	if (n == 1)
	{
		L = L->next;
		for (int i = 0; i < m + 1; i++)
		{
			printf("%d ", L->data);
			L = L->next;
		}
	}
	return 0;


}
