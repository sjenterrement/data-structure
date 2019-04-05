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
