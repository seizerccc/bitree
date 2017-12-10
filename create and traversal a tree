#include "stdafx.h"
#include <stack>
#include <iostream>

using namespace std;
//节点
struct BiNode
{
	char data;
	BiNode *lChild, *rChild;
};
//创建二叉树
void CreateBiTree(BiNode * &T) {
	char ch;
	ch = getchar();
	if (ch == '#') {
		T = NULL;
	}
	else {
		T = new BiNode;
		T->data = ch;
		CreateBiTree(T->lChild);
		CreateBiTree(T->rChild);
	}
}

//递归遍历法
void InOrderTaverser(BiNode *&T) {
	if (T->lChild) {
		InOrderTaverser(T->lChild);
	}
	cout << T->data;
	if (T->rChild) {
		InOrderTaverser(T->rChild);
	}
}
//非递归遍历法
void InOrderTaverseByStack(BiNode* &T) {
	if (T == NULL) return ;
	stack<BiNode*> s;
	BiNode *p = T;
	do {
		while (p) {
			s.push(p);
			p = p->lChild;
		}
		if (!s.empty()) {
			p = s.top();
			s.pop();
			cout << p->data;
			p = p->rChild;
		}
		
	} while (p || !s.empty());
}


BiNode *T;

int main()
{
	cout << "创建一颗树，其中A->Z字符代表树的数据，用“#”表示空树:"
		    <<"\n"<<"(请用前序遍历的字符串表示）->" << endl;
	CreateBiTree(T);
	cout << "中序遍历的结果为：";
	//递归遍历
	//InOrderTaverser(T);
	InOrderTaverseByStack(T);
	cout << endl;

    return 0;
}
