# This Package is correlation matrix principal component analysis.

## package example1

cor pca use iris data

```
from sklearn.datasets import load_iris
import pandas as pd
df= load_iris()

df=pd.concat([pd.DataFrame(df.data),pd.Series(df.target)],axis=1)
df.columns=['sepal_len', 'sepal_wid', 'petal_len', 'petal_wid', 'class']

df.tail()
X = df.iloc[:,0:4].values
y = df.iloc[:,4].values

#sklearn default is PCA(X,cor=False,cov_scaling=True,center=True)

finelDF,mean,std,matrix_w=PCA(X,cor=False,cov_scaling=False)
finelDF,mean,std,matrix_w=PCA(X,cor=True)

from matplotlib import pyplot as plt

fig = plt.figure(figsize = (8,8))
ax = fig.add_subplot(1,1,1) 
ax.set_xlabel('Principal Component 1', fontsize = 15)
ax.set_ylabel('Principal Component 2', fontsize = 15)
ax.set_title('2 component PCA', fontsize = 20)
targets = [2, 1, 0]
colors = ['r', 'g', 'b']
for target, color in zip(targets,colors):
    indicesToKeep = y== target
    ax.scatter(finelDF[indicesToKeep ,0]
               , finelDF[indicesToKeep ,1]
               , c = color
               , s = 50)
ax.legend(targets)
ax.grid()

#pca prediction 
a=PCA(X[1:50],cor=False,cov_scaling=False)
#prediction
pred=(X[51:,:]-a[1]).dot(a[3])
```

## package example2

```
#sklearn kernel PCA method but scale is diffrence

X, y = make_moons(n_samples=100, random_state=123)
X_skernpca ,lambdas= kernel_PCA(X,n_components=2, gamma=15,scaling=False)

plt.scatter(X_skernpca[y == 0, 0], X_skernpca[y == 0, 1],
            color='red', marker='^', alpha=0.5)
plt.scatter(X_skernpca[y == 1, 0], X_skernpca[y == 1, 1],
            color='blue', marker='o', alpha=0.5)

plt.xlabel('PC1')
plt.ylabel('PC2')
plt.tight_layout()
plt.show()

 
```
