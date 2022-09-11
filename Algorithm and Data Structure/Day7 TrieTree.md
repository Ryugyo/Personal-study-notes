## TrieTree
什么是TrieTree？假设有一组字符串["abc","bck","abd","ace"]需要依次加入tree，加入"abc"时，先看a，发现tree里没有路径就创建两个空node然后把edge赋值为a，再看b，也没有路径，就再建立一个空node然后和a edge的toNode连接，edge设置为b，c也一样，所以就是4个空nodes，其中3个edge相连分别为a，b，c，这样就建好了第一个字符串“abc”。再假设加入“abd”，a的路有了，b的路也有了，但是b之后只有通向c的路没有通向d的路，那就再给b edge的toNode建立一个right node，edge赋d，这样“abd”也加入了。
TrieTree可以做出特别的操作，比如求总共有多少字符以“ab”开头，那么只需从root出发走向ab连接后的node，然后返回pass值（指有多少其他node通过过b）就能求得整个array有多少字符串是ab开头。