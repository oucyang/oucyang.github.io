---
layout: post
title:  "墨卡托投影"
date:   2019-11-23 11:17:47 +0800
categories: jekyll update
---
{% include scripts.html %}

墨卡托投影，是正轴等角圆柱投影增加等角条件得到的，被广泛使用的原因是，第一：等角特性，可以保证地理对象绘制之后不变形，但形状越靠近极地，面积变得越大；第二：如果航行员想从地图上的A点到B点，只需在地图上画一条连接A点、B两点的直线，再用量角器读出这条线与子午线之间的角度，在罗盘上调出这个角度，保持同一角度航行就能从A点到达B点，但是地图上的直线不是地球上的两点最短距离。

# 建模
<img src="{{ site.baseurl }}/images/Cylindrical_Projection_basics2.svg" style="width: 600px;"/>

如图，假设将地图放入一个圆柱内部，在中心放入一盏灯，光将地球表面投影到圆柱表面，将圆柱展开成为长方形，得到的投影就是地球表面的投影。

<img src="{{ site.baseurl }}/images/CylProj_infinitesimals2.svg" style="width: 600px;"/>

如图，(a)是地球表面，(b)是(a)映射到圆柱表面的部分，将$$\delta\lambda$$和$$\delta\varphi$$看成极小的数。
由于$$\angle PKQ$$接近直角，因此，
\begin{equation}
   \tan\alpha\approx\frac{R\cos\varphi\delta\lambda}{R\delta\varphi}
\end{equation}
\begin{equation}
	\tan\beta=\frac{\delta{x}}{\delta{y}}
\end{equation}
同时，经度的缩放比例是
\begin{equation}
   k(\varphi)=\frac{P'M'}{PM}=\frac{\delta{x}}{Rcos\varphi\delta\lambda}
\end{equation}
维度的缩放比例是
\begin{equation}
   h(\varphi)=\frac{P'K'}{PK}=\frac{\delta{y}}{R\delta\varphi}
\end{equation}
由于经度是线性映射的，所以$$x=R(\lambda-\lambda_{0})$$，同时$$\delta{x}=R\delta\lambda$$（弧度）。
根据以上公式，可以得到
\begin{equation}
  \tan\beta=\frac{R\sec\varphi}{y\'(\varphi)}\tan\alpha
\end{equation}
\begin{equation}
  k=\sec\varphi
\end{equation}
\begin{equation}
  h=\frac{y\'(\varphi)}{R}
\end{equation}
# 求解
## 等角条件
图中$$\angle\alpha=\angle\beta$$，带入公式可得$$y'=Rsec\varphi$$
## 各向同性条件
该条件指的是在经度和维度两个方向上，坐标的变化比例是相等的，所以，$$h=k$$。同样，代入上面的公式，得到$$y'(\varphi)=Rsec\varphi$$
于是，得到微分方程
\begin{equation}
  y'(\varphi)=Rsec\varphi
\end{equation}
求解即可得出投影的公式，主要步骤如下
\begin{equation}
  \int\sec\varphi{d\varphi}=\int\frac{d\varphi}{\cos\varphi} \\
  =\int\frac{\cos\varphi{d\varphi}}{cos^2\varphi} \\
  =\int\frac{d\sin\varphi}{1-sin^2\varphi}
\end{equation}
替换变量
\begin{equation}
  \int\frac{du}{1-u^2}=\int\frac{du}{(1-u)(1+u)} \\
  =\frac{1}{2}\int(\frac{1}{1+u}+\frac{1}{1-u})du
\end{equation}
省略后续步骤，最终可以求得从经纬度映射到墨卡托坐标的公式是
\begin{equation}
 x=R(\lambda-\lambda_{0}), y=Rln[\tan(\frac{\pi}{4}+\frac{\varphi}{2})]
\end{equation}
反向求解的公式是
\begin{equation}
 \lambda=\lambda_{0}+\frac{x}{R}, \varphi=2tan^{-1}[e^{\frac{y}{R}}]-\frac{\pi}{2}
\end{equation}

# 特点
由于增加了等角条件，墨卡托映射得到的地图的形状保持不变，这也是很多地图选择墨卡托的原因。
在墨卡托映射中，北极和南极永远无法映射到地图上，并且，随着纬度的增加，面积变大越来越大。
由于墨卡托无法显示全部地球，一般地图选择一定的纬度范围进行投影，比如，设定投影是正方形，
那么，横轴长度就是$$W=2\pi{R}$$，选取纵轴$$y=\pm\frac{W}{2}$$，于是$$\frac{y}{R}=\pi$$
于是可以推出，最北（或最南）的维度值是
\begin{equation}
 \varphi=tan^{-1}[\sinh(\frac{y}{R})]=tan^{-1}[sinh\pi]=tan^{-1}[11.5487]=85.05113^\circ
\end{equation}
# 椭球
上面的所有推导都是基于球面的，实际上地球更近似一个椭球。使用椭球推导的公式如下
\begin{equation}
 x=R(\lambda-\lambda_{0}), \\
 y=Rln[tan(\frac{\pi}{4}+\frac{\varphi}{2})(\frac{1-e\sin\varphi}{1+e\sin\varphi})^{\frac{e}{2}}], \\
 k=\sec\varphi\sqrt{1-e^2\sin^2\varphi}
\end{equation}

# 参考
[Mercator_projection](https://en.wikipedia.org/wiki/Mercator_projection)
