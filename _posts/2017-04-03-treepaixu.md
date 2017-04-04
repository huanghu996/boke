---
layout: post
title: 二叉排序树
categories: CPPNotes
description: 
keywords: Cpp
---
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(1).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(2).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(3).PNG)
```
#include<iostream>
using namespace std;
int a[10005];
struct node{
	int data;
	int lc;
	int rc;
}q[10005];
int b(int root,int i)
{
	if(q[root].data>=a[i])
	{
		if(q[root].lc==0)
		{
			q[i].data=a[i];
			q[root].lc=i;	
		}
		else{
			b(q[root].lc,i);
		}
	}
	else{
		if(q[root].rc==0)
		{
			q[i].data=a[i];
			q[root].rc=i;	
		}
		else{
			b(q[root].rc,i);
		}
	}
}
void input(int l,int root,int r)
{
	if(q[root].lc!=0)
	{
		input(q[q[root].lc].lc,q[root].lc,q[q[root].lc].rc);
	}
	cout<<q[root].data<<" ";
	if(q[root].rc!=0)
	{
		input(q[q[root].rc].lc,q[root].rc,q[q[root].rc].rc);
	}
}
int main(){
	freopen("mir.in","r",stdin);
	freopen("mir.out","w",stdout);
	int n;
	cin>>n;
	int dy;
	cin>>dy;
	a[1]=dy;
	q[1].data=a[1];
	for(int i=2;i<=n;i++)
	{
	    cin>>a[i];
	   	
	}
 	for(int i=2;i<=n;i++)
	b(1,i);
	input(q[1].lc,1,q[1].rc);
}
```
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(4).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(5).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(6).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(7).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(8).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(9).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(10).PNG)
![image](http://hboke.nos-eastchina1.126.net/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91%20(11).PNG)
动态
```
#include<stdio.h>
#include<stdlib.h>
int n,a[100];
struct node
{
	
	int data;
	struct node *lchild,*rchild;
 } *root;
 void build(struct node *p,int i)
 {
 	if(p->data>a[i])
 	{
 	    if(p->lchild==NULL)
		{
			struct node *q;
			q=(struct node *)malloc(sizeof(struct node));
			q->data=a[i];
			q->lchild =NULL;
			q->rchild =NULL;
			p->lchild=q;
		}
		else build(p->lchild,i);
	}
	 else
	 {
	 	if(p->rchild==NULL)
		{
			struct node *q;
			q=(struct node *)malloc(sizeof(struct node));
			q->data=a[i];
			q->lchild =NULL;
			q->rchild =NULL;
			p->rchild=q;
		}
		else build(p->rchild,i);
	 	
	 }
 }
void inorder(struct node *p)
{
	if(p!=NULL)
	{
		inorder(p->lchild);
		printf("%d ",p->data);
		inorder(p->rchild);
	}
}


void del(struct node *p,int k)
{
	struct node *f;
    while(1)
	{
		if(p==NULL)return;
	    if(p->data==k)break;
	    f=p;
		 if(p->data>k)p=p->lchild;
		else p=p->rchild;	
	}	
	if(p->lchild==NULL&&p->rchild==NULL)  //叶子节点 
	 {
	     if(f->lchild==p)f->lchild=NULL;
	     else f->rchild =NULL;
	     free(p);
	 }
	 else if(p->lchild!=NULL&&p->rchild==NULL)//有左孩子节点 
	 {
	     if(f->lchild==p)f->lchild=p->lchild;
	     else f->rchild =p->lchild;
	     free(p);
	  } 
	  
	else if(p->lchild==NULL&&p->rchild!=NULL) //右孩子节点 
	{
		 if(f->rchild==p)f->rchild=p->rchild;
	     else f->lchild =p->rchild;
	     free(p);
	} 
	else    //有两个孩子的节点 
	{
		
		struct node *q,*f1;
		q=p;
		p=p->lchild;
		f1=p;
		while(p->rchild!=NULL)
		{
		    f1=p;
			p=p->rchild;
		}
	    q->data=p->data;
	    if(f1!=p)
	      f1->rchild=p->lchild;  
	    else
	      q->lchild=p->lchild;
	    
	    
	    free(p);
	 } 
	
} 

int main()
{
	
	int i,k;
	scanf("%d",&n);
	for(i=1;i<=n;i++)
	{
		scanf("%d",&a[i]);
	}
	root=(struct node *)malloc(sizeof(struct node));
	root->data=a[1];
	root->lchild =NULL;
	root->rchild =NULL;
	
	for(i=2;i<=n;i++)
	{
		build(root,i);
	}
	//inorder(root);
	scanf("%d",&k);
	del(root,k);
	inorder(root);
	return 0;
	
}
```
静态
```
#include<stdio.h>
int a[100],q;
struct node
{
	int data;
	int lchild,rchild;
}t[100];
void build(int p,int i)  //构建二叉树 
{
	if(t[p].data==0)
	{
		t[p].data=a[i];
	}
	else
	{
		if(t[p].data >a[i])
		{
			if(t[p].lchild==0)
			{
				t[p].lchild =i;
				t[i].data=a[i];
			}
			else build(t[p].lchild,i);
		}
		if(t[p].data <a[i])
		{
			if(t[p].rchild==0)
			{
				t[p].rchild =i;
				t[i].data=a[i];
			}
			else build(t[p].rchild,i);
		}
	}
}
void inorder(int root)//中序遍历 
{	 
   
	if(t[root].lchild!=0)inorder(t[root].lchild);
printf("%d ",t[root].data);
	if(t[root].rchild!=0)inorder(t[root].rchild);
}

void del(int p,int k)//k是我们要删除的数 
{
	int q;
	while(1)
	{
		 
		if(t[p].data==k)
		  break;
		  q=p;
	  
	   if(t[p].data>k)
		  p=t[p].lchild;
		else
		  p=t[p].rchild; 
	}
	if(t[p].lchild==0&&t[p].rchild==0)
	{
		if(t[q].lchild ==p)
		  t[q].lchild=0;
		else 
		  t[q].rchild=0;
	}
	

	else if(t[p].lchild==0)//p有右子树 
	{
		
		if(t[q].lchild==p)
			t[q].lchild =t[p].rchild;
	
		else t[q].rchild =t[p].rchild;
	}
	
	
	else if(t[p].rchild==0)//p有左子树 
	{
		
		if(t[q].lchild==p)
			t[q].lchild =t[p].lchild;
		
		else t[q].rchild =t[p].lchild;
	}
	else  //说明p有双子树 
	{
		int f;
	     q=p;
	     p=t[p].lchild;
	     while(t[p].rchild!=0)
	     {
	     	f=p;
	     	p=t[p].rchild;
		 }
		 
		 t[q].data=t[p].data;   //q的值直接指向p的值 
		 	
		 if(t[q].lchild==p)    //如果p没有右孩子直接提上去 
		 {
		 	t[q].lchild=t[p].lchild;
		 }
		 else     //有右孩子，父节点f指向子节点 p的左孩子 
		 {
		    t[f].rchild=t[p].lchild;
		 }
		 
	}	
 } 

int main()
{
	int n,i,k;
	scanf("%d",&n);
	for(i=1;i<=n;i++)
	{
	   scanf("%d",&a[i]); 
		build(1,i);
	} 
	scanf("%d",&k);
	del(1,k);
	inorder(1);
	return 0;
 } 
```
