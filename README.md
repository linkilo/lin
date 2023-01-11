#include<iostream>

using namespace std;

typedef struct node {
	int v;
	struct node* next;
}node;

void in(node* l) {//输入链表，以-1结束
	int n;
	cin >> n;
	while (n != -1){
		node* p = (node*)malloc(sizeof(node));
		p->v = n;
		p->next = NULL;
		l->next = p;
		l = l->next;
		cin >> n;
	} 
}

void show(node* l) {//输出链表
	while (l->next) {
		cout << l->next->v;
		l = l->next;
	}
	cout << endl;
}

void insert(node* l, int k, int x) {//插入链表
	node* p = NULL;
	node* a = (node*)malloc(sizeof(node));
	a->v = x;
	a->next = NULL;
	while (k && l->next) {
		p = l;
		l = l->next;
		k--;
	}
	if (k > 0) {
		l->next = a;
		l = l->next;
	}
	else {
		p->next = a;
		a->next = l;
	}
}

int  hl(node* l) {//求链表长度
	int n = 0;
	while (l->next) {
		l = l->next;
		n++;
	}
	return n;
}

void shan(node* l, int x) {//删除节点值为下的节点
	if (hl(l) <= 0) {
		cout << "空链表" << endl;
		return;
	}
	node* p = l->next;
	node* a = l;
	while (p) {
		if (p->v == x) {
			a->next = p->next;
			free(p);
			return;
		}
		a = p;
		p = p->next;
	}
}

void shan1(node* l, int k) {//删除k节点的值
	if (hl(l) <= 0) {
		cout << "空链表" << endl;
		return;
	}
	node* p = l->next;
	node* a = l;
	k = k - 1;
	while (k-- && p)
	{
		a = p;
		p = p->next;
	}
	if (p==NULL||k>0){
		cout << "不存在该节点" << endl;
	}
	else {
		a->next = p->next;
		free(p);
	}
}

bool p(node* l) {//判断链表是否为空
	if (l->next == NULL) {
		return true;
	}
	else return false;
}

int find(node* l, int k) {
	node* p = l;
	while (k>0 && p->next) {
		p = p->next;
		k--;
	}
	if (k == 0 && p != NULL) return p->v;
	else {
		cout << "该位置不存在数值" << endl;
		return -1;
	}
}

void clear(node* l) {//清空链表
	node* p = l;
	if (hl(l) > 0) {
		while (p->next) {
			node* a = p->next;
			p->next = p->next->next;
			free(a);
		}
	}
}

int main(void) {
	node* l = (node*)malloc(sizeof(node));

	l->next = NULL;
	while (1)
	{
		cout << "**********************************************" << endl;
		cout << "* 1、创建单链表(以-1结束)     2、打印单链表  *" << endl;
		cout << "* 3、插入单链表               4、单链表删除  *" << endl;
		cout << "* 5、判断是否为空             6、单链表长度  *" << endl;
		cout << "* 7、查找                     8、退出        *" << endl;
		cout << "**********************************************" << endl;
		int k;
		cin >> k;
		switch (k) {
		case 1:
			in(l);
			system("pause");
			system("cls");
			continue;

		case 2:
			show(l);
			system("pause");
			system("cls");
			continue;
		case 3:
			int i, x;
			cin >> i >> x;
			insert(l, i, x);
			show(l);
			system("pause");
			system("cls");
			continue;
		case 4:
			int k;
			cin >> k;
			shan(l, k);
			system("pause");
			system("cls");
			continue;
		case 5:
			if (hl(l)) cout << "空链表";
			else cout << "非空链表";
			system("pause");
			system("cls");
			continue;
		case 6:
			cout << "链表长度为：" << hl(l) << endl;
			system("pause");
			system("cls");
			continue;
		case 7:
			int n;
			cin >> n;
			find(l, n);
			system("pause");
			system("cls");
			continue;
		case 8:
			break;

		default :
			cout << "请输入正确的选项" << endl;
			system("pause");
			system("cls");
			continue;
	    }
	} 
	system("pause");
	
}
