https://blog.csdn.net/u012701023/article/details/82984026


 git format-patch -1 e1ecedf03980d2c581e912433be2d3435899a819
 
 生成:
 
 0001-del-patch.patch
 
 测试patch
 
  git apply --check 0001-del-patch.patch
  
 应用patch
 
 git am --signoff < 0001-del-patch.patch
