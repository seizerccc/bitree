#include "stdafx.h"
#include <regex>
#include <string>
#include <iostream>
#include<queue>

using namespace std;
//二叉树节点
struct BiNode
{
	char data;
	BiNode *lChild = nullptr; 
	BiNode *rChild = nullptr;
	int count = 0;
};
//临时的存储结构体
struct Member
{
	string self;
	string parent;
};

//用于遍历的入口
static BiNode *root;

void BuildTree(string s) {
	//正则表达式（还不太会，暂时只能跑静态的例子）
	const regex pattern("(\\w)\\s(\\w)\\((\\wR?)\\)\\s?(\\w)\\((\\wR?)\\)\\s?(\\w)\\((\\wR?)\\)\\s?(\\w)\\((\\wR?)\\)\\s?(\\w)\\((\\wR?)\\)\\s?(\\w)\\((\\wR?)\\)\\s?(\\w)\\((\\wR?)\\)\\s?");
	const regex rg("\\wR");
	queue<Member> readQueue;
	queue<BiNode*>buildQueue;
	//把正则表达式匹配的对象全部都放到result中
	match_results<string::const_iterator> result;
	BiNode *T;

	//匹配正则表达式，读入第一个队列
	if (regex_match(s, result, pattern)) {
		Member member = { (string)result[1],"" };
		readQueue.push(member);
		cout <<"当前输入的序列是："<<"\""<< result[0] <<"\""<< endl;
		cout << result[1] << " enqueue" << endl;
		//把“暂时不会操作的正则表达式提取内容”放到临时结构体中
		for (int i = 2; i < 16; i+=2) {
			Member member = { (string)result[i], (string)result[i + 1] };
			readQueue.push(member);
			cout << result[i] <<" enqueue"<< endl;
		}

		//根据第两个队列构建二叉树
		while (!readQueue.empty())
		{
			//第一个值（根）
			if (readQueue.front().parent == "") {
				T = new BiNode;
				T->data = readQueue.front().self[0];
				T->count = 0;
				root = T;
				buildQueue.push(T);
				readQueue.pop();
			}
			//当前值应该成为左孩子
			else if(!regex_match(readQueue.front().parent, rg)&&
				      buildQueue.front()->count==0&&
				      readQueue.front().parent[0]==buildQueue.front()->data){
				T = new BiNode;
				T->data = readQueue.front().self[0];
				buildQueue.front()->lChild = T;
				buildQueue.front()->count +=1;
				buildQueue.push(T);
				readQueue.pop();

			}
			//当前值应该成为右孩子（这里只考虑了没有单独子的情况）
			else if (!regex_match(readQueue.front().parent, rg) &&
				buildQueue.front()->count == 1 &&
				readQueue.front().parent[0] == buildQueue.front()->data) {
				T = new BiNode;
				T->data = readQueue.front().self[0];
				buildQueue.front()->rChild = T;
				buildQueue.front()->count += 1;
				buildQueue.push(T);
				buildQueue.pop();//当前父节点已满，不会再使用，dequeue
				readQueue.pop();

			}
			//当前值应该成为右独子
			else if(regex_match(readQueue.front().parent,rg)&&
				       readQueue.front().parent[0]==buildQueue.front()->data){
				T = new BiNode;
				T->data = readQueue.front().self[0];
				buildQueue.front()->rChild = T;
				buildQueue.front()->count = 2;
				buildQueue.push(T);
				buildQueue.pop();//当前节点已经添加右独子，不会再使用，dequeue
				readQueue.pop();
			}
			//当前值不是当前节点的孩子
			else if (readQueue.front().parent[0] != buildQueue.front()->data) {
				buildQueue.pop();
			}
		}
	}
	else {
		cout << "Invalid Input!" << endl;
	}
}

//中序遍历方法
void InOrderTaverser(BiNode *&T) {
	if (T->lChild) {
		InOrderTaverser(T->lChild);
	}
	cout << T->data;
	if (T->rChild) {
		InOrderTaverser(T->rChild);
	}
}



int main()
{
	string s = "A B(A) C(A) D(BR) E(C) F(C) G(E) H(E) ";

	//生成二叉树
	BuildTree(s);

	//遍历二叉树
	cout << "二叉树已生成" << endl;
	cout << "中序遍历树的结果为：";
	InOrderTaverser(root);

    return 0;
}
