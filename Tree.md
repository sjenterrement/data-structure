#### 树的遍历
###### 1.  先序中序转后序
<pre><code>代码：
void post(int preRoot,int inStart,int inEnd){
    if(inStart>inEnd) return ;
    int i=inStart;
    while(i < inEnd && pre[preRoot] != in[i]) i++;
    post(preRoot+1,inStart,i-1);
    post(preroot+(i-inStart+1),i+1,inEnd);//preroot+(i-inStart+1)：根节点+左子树节点个数
    printf("%d",pre[root]);
}
</code></pre>
###### 2.  后序中序转前序
<pre><code>代码：
void pre(int postRoot,int inStart,int inEnd){
    if(inStart>inEnd) return;
    int i=inStart;
    while(i < inEnd && post[postRoot] != in[i]) i++;
    printf("%d",post[postRoot]);
    pre(postRoot-(inEnd-i+1),inStart,i-1);//postRoot-(inEnd-i+1)：根节点-右子树节点个数
    pre(postRoot-1,i+1,inEnd);
}
</code></pre>
###### 3. 后序中序转层序
<pre><code>代码：
void pre_level(int postRootroot, int inStart, int inEnd, int index) {
	if (inStart > inEnd) return;
	int i = inStart;
	while (i < inEnd&&in[i] != post[postRootroot]) i++;
	level.push_back({ index,post[postRootroot] });
	pre_level(postRootroot - (inEnd - i + 1), inStart, i - 1, 2 * index + 1);//postRootroot - (inEnd - i + 1):即为当前根结点-右子树的个数
	pre_level(postRootroot - 1, i + 1, inEnd, 2 * index + 2);//postRootroot-1:后序右子树根节点
}
</code></pre>
###### 4.  前序中序转层序
<pre><code>代码：
void post_level(int preRoot,int inStart,int inEnd,int index){
    if(inStart>inEnd) return ;
    int i=inStart;
    while(i < inEnd && pre[preRoot] != in[i]) i++;
    post(preRoot+1,inStart,i-1,2 * index + 1);
    post(preroot+(i-inStart+1),i+1,inEnd,2 * index + 2);//preroot+(i-inStart+1)：根节点+左子树节点个数
    level.push_back({ index,pre[preRootroot] });
}
</code></pre>
###### 3. 后序中序转之字
<pre><code>代码：
void pre_level(int postRootroot, int inStart, int inEnd, int level) {
	if (inStart > inEnd) return;
	int i = inStart;
	while (i < inEnd&&in[i] != post[postRootroot]) i++;
  vector<int> v[10000];
  v[level].push_back(post[postRoot]);
	pre_level(postRootroot - (inEnd - i + 1), inStart, i - 1, 2 * index + 1);//postRootroot - (inEnd - i + 1):即为当前根结点-右子树的个数
	pre_level(postRootroot - 1, i + 1, inEnd, 2 * index + 2);//postRootroot-1:后序右子树根节点
}
</code></pre>
#### 树的建造
###### 二叉搜索树插入（建造）
<pre><code>代码：
struct node {
	int val;
	node *left, *right;
};
node *rotateLeft(node *root) {
	node *t = root->right;
	root->right = t->left;
	t->left = root;
	return t;
}
node *rotateRight(node *root) {
	node *t = root->left;
	root->left = t->right;
	t->right = root;
	return t;
}
node *rotateLeftRight(node *root) {
	root->left = rotateLeft(root->left);
	return rotateRight(root);
}
node *rotateRightLeft(node *root) {
	root->right = rotateRight(root->right);
	return rotateLeft(root);
}
int getHeight(node *root) {
	if (root == NULL) return 0;
	return max(getHeight(root->left), getHeight(root->right)) + 1;
}
node *insert(node *root,int val){
	if (root == NULL) {
		root = new node();
		root->val = val;
		root->left = root->right = NULL;
	}
	else if (val < root->val) {
		root->left = insert(root->left, val);
		if (getHeight(root->left) - getHeight(root->right) == 2)
			root = val < root->left->val ? rotateRight(root) : rotateLeftRight(root);
	}
	else
	{
		root->right = insert(root->right, val);
		if (getHeight(root->left) - getHeight(root->right) == 2)
			root = val > root->right->val ? rotateLeft(root) : rotateRightLeft(root);
	}
	return root;
}
int main() {
	int n, val;
	scanf("%d", &n);
	node *root = NULL;
	for (int i = 0; i < n; i++) {
		scanf("%d", &val);
		root = insert(root, val);
	}
	printf("%d", root->val);
	return 0;
}

node *build(node *root,int val){
	if (root == NULL) {
		root = new node();
		root->val = val;
		root->left = root->right = NULL;
	}
	else if (val < root->val) {
		root->left = build(root->left, val);
	}
	else
	{
		root->right = build(root->right, val);
	}
	return root;
}
</code><pre>
