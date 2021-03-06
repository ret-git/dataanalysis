---
title       : Summarizing data
subtitle    : 
author      : Jeffrey Leek, Assistant Professor of Biostatistics 
job         : Johns Hopkins Bloomberg School of Public Health
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : zenburn   # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---




## Why summarize?

* Data are often too big to look at the whole thing
* The first step in an analysis is to find problems
* When you do these summaries you should be looking for
  * Missing values
  * Values outside of expected ranges
  * Values that seem to be in the wrong units
  * Mislabled variables/columns 
  * Variables that are the wrong class

---

## Earthquake data

<img class=center src=assets/img/earthquakes.png height='80%'/>

[https://explore.data.gov/Geography-and-Environment/Worldwide-M1-Earthquakes-Past-7-Days/7tag-iwnu](https://explore.data.gov/Geography-and-Environment/Worldwide-M1-Earthquakes-Past-7-Days/7tag-iwnu)


---

## Earthquake data


```r
fileUrl <- "http://earthquake.usgs.gov/earthquakes/catalogs/eqs7day-M1.txt"
download.file(fileUrl,destfile="./data/earthquakeData.csv",method="curl")
dateDownloaded <- date()
dateDownloaded
```

```
[1] "Sun Jan 27 00:23:22 2013"
```

```r
eData <- read.csv("./data/earthquakeData.csv")
```


---

## Looking at data - the whole thing

```r
eData
```

```
     Src     Eqid Version                                 Datetime
1     nc 71929481       1    Sunday, January 27, 2013 05:03:01 UTC
2     ci 15278017       0    Sunday, January 27, 2013 04:59:04 UTC
3     ak 10645573       1    Sunday, January 27, 2013 04:55:09 UTC
4     nc 71929476       0    Sunday, January 27, 2013 04:51:48 UTC
5     nn 00401016       9    Sunday, January 27, 2013 04:45:19 UTC
6     ak 10645564       1    Sunday, January 27, 2013 04:16:45 UTC
7     hv 60459531       2    Sunday, January 27, 2013 04:15:57 UTC
8     ak 10645555       1    Sunday, January 27, 2013 04:14:35 UTC
9     ci 15278009       0    Sunday, January 27, 2013 04:07:44 UTC
10    us c000ewb3       7    Sunday, January 27, 2013 04:05:42 UTC
11    ci 15278001       0    Sunday, January 27, 2013 03:54:27 UTC
12    hv 60459521       1    Sunday, January 27, 2013 03:50:13 UTC
13    hv 60459516       2    Sunday, January 27, 2013 03:43:56 UTC
14    ak 10645533       1    Sunday, January 27, 2013 03:25:17 UTC
15    ak 10645528       1    Sunday, January 27, 2013 03:18:17 UTC
16    us c000ewax       6    Sunday, January 27, 2013 03:17:57 UTC
17    ci 15277993       0    Sunday, January 27, 2013 02:47:04 UTC
18    ci 15277985       0    Sunday, January 27, 2013 02:25:12 UTC
19    nc 71929446       0    Sunday, January 27, 2013 02:24:30 UTC
20    ci 15277977       0    Sunday, January 27, 2013 02:17:27 UTC
21    nc 71929426       1    Sunday, January 27, 2013 01:55:51 UTC
22    nc 71929411       1    Sunday, January 27, 2013 01:23:15 UTC
23    us c000ewag       4    Sunday, January 27, 2013 00:56:18 UTC
24    hv 60459466       2    Sunday, January 27, 2013 00:34:27 UTC
25    pr 13027000       0    Sunday, January 27, 2013 00:29:54 UTC
26    us c000ewaa       5    Sunday, January 27, 2013 00:27:18 UTC
27    nc 71929386       0    Sunday, January 27, 2013 00:24:22 UTC
28    ak 10645501       1    Sunday, January 27, 2013 00:04:28 UTC
29    ak 10645497       2    Sunday, January 27, 2013 00:04:18 UTC
30    ak 10645491       1  Saturday, January 26, 2013 22:47:33 UTC
31    nn 00400996       9  Saturday, January 26, 2013 22:13:21 UTC
32    ci 15277945       0  Saturday, January 26, 2013 22:09:24 UTC
33    nn 00400994       9  Saturday, January 26, 2013 22:07:32 UTC
34    ci 15277929       0  Saturday, January 26, 2013 22:02:55 UTC
35    nc 71929331       1  Saturday, January 26, 2013 22:01:24 UTC
36    nc 71929326       0  Saturday, January 26, 2013 21:54:11 UTC
37    nn 00400985       9  Saturday, January 26, 2013 21:38:24 UTC
38    ak 10645479       2  Saturday, January 26, 2013 21:19:45 UTC
39    ak 10645475       2  Saturday, January 26, 2013 21:01:43 UTC
40    ci 15277913       0  Saturday, January 26, 2013 20:38:03 UTC
41    ci 15277897       0  Saturday, January 26, 2013 20:33:08 UTC
42    ci 15277881       0  Saturday, January 26, 2013 20:06:02 UTC
43    ci 15277873       0  Saturday, January 26, 2013 19:52:53 UTC
44    nc 71929286       1  Saturday, January 26, 2013 19:23:34 UTC
45    nc 71929281       0  Saturday, January 26, 2013 18:52:09 UTC
46    nc 71929271       1  Saturday, January 26, 2013 18:39:24 UTC
47    ci 15277849       0  Saturday, January 26, 2013 17:56:46 UTC
48    nc 71929251       0  Saturday, January 26, 2013 17:51:08 UTC
49    nc 71929246       3  Saturday, January 26, 2013 17:49:43 UTC
50    nc 71929236       0  Saturday, January 26, 2013 17:46:13 UTC
51    us c000ew2h       6  Saturday, January 26, 2013 17:31:13 UTC
52    nc 71929201       1  Saturday, January 26, 2013 16:59:55 UTC
53    nc 71929191       1  Saturday, January 26, 2013 16:52:03 UTC
54    us c000evyz       8  Saturday, January 26, 2013 16:25:05 UTC
55    nn 00400967       9  Saturday, January 26, 2013 15:58:40 UTC
56    us c000evx5       A  Saturday, January 26, 2013 15:41:16 UTC
57    nc 71929156       0  Saturday, January 26, 2013 15:10:53 UTC
58    us c000evwx       5  Saturday, January 26, 2013 15:10:51 UTC
59    uw 60497617       3  Saturday, January 26, 2013 15:10:00 UTC
60    nn 00400963       9  Saturday, January 26, 2013 15:08:21 UTC
61    nn 00400962       9  Saturday, January 26, 2013 14:34:28 UTC
62    ak 10645400       1  Saturday, January 26, 2013 14:32:26 UTC
63    ci 15277753       0  Saturday, January 26, 2013 14:20:20 UTC
64    ci 15277745       0  Saturday, January 26, 2013 14:11:24 UTC
65    ci 15277737       0  Saturday, January 26, 2013 14:04:25 UTC
66    ci 15277729       0  Saturday, January 26, 2013 14:02:40 UTC
67    ci 15277713       0  Saturday, January 26, 2013 14:00:34 UTC
68    ak 10645390       1  Saturday, January 26, 2013 13:23:57 UTC
69    nc 71929141       4  Saturday, January 26, 2013 13:10:38 UTC
70    ci 15277697       0  Saturday, January 26, 2013 12:52:13 UTC
71    nc 71929126       1  Saturday, January 26, 2013 12:46:43 UTC
72    nc 71929121       0  Saturday, January 26, 2013 12:34:08 UTC
73    nc 71929106       0  Saturday, January 26, 2013 12:10:44 UTC
74    ak 10645373       1  Saturday, January 26, 2013 11:51:59 UTC
75    ak 10645366       1  Saturday, January 26, 2013 11:32:45 UTC
76    nc 71929081       1  Saturday, January 26, 2013 11:23:30 UTC
77    ci 15277673       0  Saturday, January 26, 2013 11:17:49 UTC
78    ak 10645358       1  Saturday, January 26, 2013 11:15:04 UTC
79    ak 10645355       1  Saturday, January 26, 2013 11:12:30 UTC
80    ci 15277665       0  Saturday, January 26, 2013 11:12:21 UTC
81    us c000evw5       6  Saturday, January 26, 2013 11:01:41 UTC
82    ci 15277657       0  Saturday, January 26, 2013 10:48:29 UTC
83    ci 15277649       0  Saturday, January 26, 2013 10:33:58 UTC
84    ak 10645348       1  Saturday, January 26, 2013 10:19:00 UTC
85    hv 60458951       1  Saturday, January 26, 2013 10:12:19 UTC
86    hv 60458946       1  Saturday, January 26, 2013 10:12:06 UTC
87    hv 60458941       1  Saturday, January 26, 2013 10:11:59 UTC
88    hv 60458936       2  Saturday, January 26, 2013 10:11:03 UTC
89    hv 60458931       2  Saturday, January 26, 2013 10:08:41 UTC
90    hv 60458926       5  Saturday, January 26, 2013 10:08:33 UTC
91    uw 60497597       3  Saturday, January 26, 2013 10:06:52 UTC
92    ak 10645333       1  Saturday, January 26, 2013 10:06:44 UTC
93    ak 10645329       1  Saturday, January 26, 2013 09:57:17 UTC
94    nn 00400956       9  Saturday, January 26, 2013 09:39:03 UTC
95    us c000evvj       6  Saturday, January 26, 2013 09:36:41 UTC
96    nm  012613a       A  Saturday, January 26, 2013 09:34:11 UTC
97    nc 71929041       0  Saturday, January 26, 2013 09:13:51 UTC
98    hv 60458881       2  Saturday, January 26, 2013 09:09:42 UTC
99    ak 10645321       1  Saturday, January 26, 2013 08:53:37 UTC
100   ak 10645315       1  Saturday, January 26, 2013 08:12:52 UTC
101   ak 10645306       1  Saturday, January 26, 2013 07:41:19 UTC
102   ak 10645305       1  Saturday, January 26, 2013 07:40:46 UTC
103   ci 15277625       0  Saturday, January 26, 2013 07:21:24 UTC
104   ci 15277617       0  Saturday, January 26, 2013 06:17:50 UTC
105   nc 71929011       1  Saturday, January 26, 2013 06:12:45 UTC
106   ci 15277609       0  Saturday, January 26, 2013 06:00:21 UTC
107   ci 15277601       0  Saturday, January 26, 2013 05:48:37 UTC
108   nn 00400954       9  Saturday, January 26, 2013 05:42:18 UTC
109   ak 10645287       2  Saturday, January 26, 2013 05:28:45 UTC
110   us c000evua       8  Saturday, January 26, 2013 05:16:01 UTC
111   hv 60458721       1  Saturday, January 26, 2013 05:12:55 UTC
112   pr 13026000       0  Saturday, January 26, 2013 04:58:39 UTC
113   hv 60458711       1  Saturday, January 26, 2013 04:40:24 UTC
114   ak 10645273       1  Saturday, January 26, 2013 03:40:28 UTC
115   ci 15277585       0  Saturday, January 26, 2013 02:56:37 UTC
116   nc 71928936       0  Saturday, January 26, 2013 02:34:42 UTC
117   nc 71928921       0  Saturday, January 26, 2013 02:25:01 UTC
118   nc 71928916       1  Saturday, January 26, 2013 02:12:12 UTC
119   nc 71928911       1  Saturday, January 26, 2013 02:03:29 UTC
120   ak 10645157       1  Saturday, January 26, 2013 01:29:23 UTC
121   ak 10645156       1  Saturday, January 26, 2013 01:24:18 UTC
122   ak 10645139       1  Saturday, January 26, 2013 01:11:51 UTC
123   ci 15277561       0  Saturday, January 26, 2013 01:05:10 UTC
124   nc 71928871       0  Saturday, January 26, 2013 01:04:42 UTC
125   nc 71928861       1  Saturday, January 26, 2013 00:59:17 UTC
126   ci 15277545       0  Saturday, January 26, 2013 00:55:01 UTC
127   nn 00400946       9  Saturday, January 26, 2013 00:45:25 UTC
128   ak 10644925       1  Saturday, January 26, 2013 00:18:08 UTC
129   ak 10644924       2  Saturday, January 26, 2013 00:03:40 UTC
130   nc 71928836       1    Friday, January 25, 2013 23:50:54 UTC
131   us c000evr6       7    Friday, January 25, 2013 23:37:01 UTC
132   nc 71928831       2    Friday, January 25, 2013 23:31:40 UTC
133   nc 71928816       0    Friday, January 25, 2013 23:04:48 UTC
134   us c000evqn       4    Friday, January 25, 2013 22:40:56 UTC
135   ak 10644904       1    Friday, January 25, 2013 22:38:10 UTC
136   nc 71928796       2    Friday, January 25, 2013 22:33:47 UTC
137   ci 15277521       0    Friday, January 25, 2013 22:21:56 UTC
138   uw 60497447       1    Friday, January 25, 2013 22:13:02 UTC
139   ak 10644890       1    Friday, January 25, 2013 22:11:55 UTC
140   nc 71928766       0    Friday, January 25, 2013 22:05:53 UTC
141   nn 00400936       9    Friday, January 25, 2013 22:05:49 UTC
142   ak 10644876       1    Friday, January 25, 2013 21:44:57 UTC
143   ak 10644865       1    Friday, January 25, 2013 21:31:50 UTC
144   mb 13930962       2    Friday, January 25, 2013 21:14:36 UTC
145   nc 71928756       0    Friday, January 25, 2013 21:10:25 UTC
146   us c000evlt       4    Friday, January 25, 2013 21:08:43 UTC
147   nc 71928746       0    Friday, January 25, 2013 20:53:14 UTC
148   ak 10644843       1    Friday, January 25, 2013 20:31:03 UTC
149   pr 13025004       0    Friday, January 25, 2013 20:25:04 UTC
150   ak 10644838       1    Friday, January 25, 2013 20:23:26 UTC
151   nc 71928716       1    Friday, January 25, 2013 19:55:28 UTC
152   us c000evi7       A    Friday, January 25, 2013 19:53:28 UTC
153   us c000evhf       D    Friday, January 25, 2013 19:43:03 UTC
154   nc 71928696       2    Friday, January 25, 2013 19:12:35 UTC
155   us c000evg1       4    Friday, January 25, 2013 18:52:26 UTC
156   nc 71928686       3    Friday, January 25, 2013 18:51:53 UTC
157   uw 60497417       1    Friday, January 25, 2013 18:35:04 UTC
158   ci 15277457       4    Friday, January 25, 2013 18:23:06 UTC
159   ci 15277449       2    Friday, January 25, 2013 18:08:35 UTC
160   us c000evei       6    Friday, January 25, 2013 17:46:18 UTC
161   nc 71928651       8    Friday, January 25, 2013 17:38:58 UTC
162   ak 10644754       1    Friday, January 25, 2013 17:20:59 UTC
163   nc 71928641       0    Friday, January 25, 2013 17:00:48 UTC
164   ci 15277441       2    Friday, January 25, 2013 16:57:09 UTC
165   ci 15277433       2    Friday, January 25, 2013 16:48:02 UTC
166   nc 71928626       1    Friday, January 25, 2013 16:34:25 UTC
167   nc 71928616       5    Friday, January 25, 2013 16:10:58 UTC
168   ak 10644734       1    Friday, January 25, 2013 15:53:53 UTC
169   ak 10644730       1    Friday, January 25, 2013 15:48:19 UTC
170   uu 60011387       4    Friday, January 25, 2013 15:44:37 UTC
171   nn 00400893       9    Friday, January 25, 2013 15:22:15 UTC
172   nn 00400891       9    Friday, January 25, 2013 15:20:29 UTC
173   nc 71928591       2    Friday, January 25, 2013 15:19:27 UTC
174   nn 00400886       9    Friday, January 25, 2013 15:04:05 UTC
175   us c000evax       8    Friday, January 25, 2013 14:48:18 UTC
176   nc 71928566       3    Friday, January 25, 2013 14:26:41 UTC
177   ak 10644704       2    Friday, January 25, 2013 14:22:08 UTC
178   mb 13580113       2    Friday, January 25, 2013 14:19:19 UTC
179   nc 71928556       1    Friday, January 25, 2013 14:13:34 UTC
180   uu 60011377       2    Friday, January 25, 2013 14:02:47 UTC
181   uu 60011372       4    Friday, January 25, 2013 13:57:59 UTC
182   uu 60011367       2    Friday, January 25, 2013 13:56:28 UTC
183   nc 71928536       0    Friday, January 25, 2013 13:36:57 UTC
184   ak 10644694       2    Friday, January 25, 2013 13:36:29 UTC
185   ak 10644686       1    Friday, January 25, 2013 13:22:32 UTC
186   uw 60497397       1    Friday, January 25, 2013 13:18:04 UTC
187   nc 71928531       0    Friday, January 25, 2013 13:09:25 UTC
188   ak 10644683       1    Friday, January 25, 2013 12:55:22 UTC
189   hv 60458386       5    Friday, January 25, 2013 12:53:14 UTC
190   nn 00400879       9    Friday, January 25, 2013 12:51:38 UTC
191   ak 10644667       2    Friday, January 25, 2013 12:19:17 UTC
192   nc 71928526       2    Friday, January 25, 2013 12:13:21 UTC
193   us c000ev9v       6    Friday, January 25, 2013 12:11:24 UTC
194   ak 10644662       1    Friday, January 25, 2013 12:05:00 UTC
195   nc 71928511       3    Friday, January 25, 2013 11:50:19 UTC
196   uu 60011362       3    Friday, January 25, 2013 11:26:07 UTC
197   ak 10644656       1    Friday, January 25, 2013 11:09:46 UTC
198   hv 60458356       1    Friday, January 25, 2013 10:37:11 UTC
199   nc 71928481       2    Friday, January 25, 2013 10:00:09 UTC
200   ak 10644647       1    Friday, January 25, 2013 09:49:09 UTC
201   nc 71928471       0    Friday, January 25, 2013 09:43:45 UTC
202   nc 71928466       1    Friday, January 25, 2013 09:35:38 UTC
203   ak 10644636       1    Friday, January 25, 2013 09:21:30 UTC
204   nc 71928456       0    Friday, January 25, 2013 09:17:02 UTC
205   uw 60497387       3    Friday, January 25, 2013 09:11:56 UTC
206   nc 71928451       2    Friday, January 25, 2013 09:11:20 UTC
207   uw 60497382       3    Friday, January 25, 2013 08:58:33 UTC
208   nc 71928446       2    Friday, January 25, 2013 08:24:03 UTC
209   ak 10644624       1    Friday, January 25, 2013 08:17:30 UTC
210   nn 00400866       9    Friday, January 25, 2013 08:16:27 UTC
211   ak 10644625       2    Friday, January 25, 2013 08:15:17 UTC
212   pr 13025003       0    Friday, January 25, 2013 07:49:08 UTC
213   nc 71928416       0    Friday, January 25, 2013 07:19:39 UTC
214   us c000ev85       8    Friday, January 25, 2013 07:01:19 UTC
215   uu 60011352       2    Friday, January 25, 2013 06:53:23 UTC
216   ak 10644613       1    Friday, January 25, 2013 06:49:23 UTC
217   pr 13025002       0    Friday, January 25, 2013 06:47:40 UTC
218   nc 71928401       3    Friday, January 25, 2013 06:44:31 UTC
219   nn 00400863       9    Friday, January 25, 2013 06:39:40 UTC
220   ak 10644604       1    Friday, January 25, 2013 06:37:23 UTC
221   ci 15277377       0    Friday, January 25, 2013 06:35:22 UTC
222   uu 60011347       3    Friday, January 25, 2013 06:21:19 UTC
223   ak 10644599       1    Friday, January 25, 2013 06:19:30 UTC
224   nc 71928391       0    Friday, January 25, 2013 06:17:28 UTC
225   pr 13025001       0    Friday, January 25, 2013 06:12:17 UTC
226   ci 15277369       0    Friday, January 25, 2013 06:10:26 UTC
227   ak 10644590       1    Friday, January 25, 2013 06:05:26 UTC
228   ci 15277361       0    Friday, January 25, 2013 05:59:27 UTC
229   ak 10644586       1    Friday, January 25, 2013 05:58:40 UTC
230   nn 00400861       9    Friday, January 25, 2013 05:58:33 UTC
231   ci 15277353       2    Friday, January 25, 2013 05:45:03 UTC
232   ci 15277345       2    Friday, January 25, 2013 05:38:42 UTC
233   ak 10644575       1    Friday, January 25, 2013 05:37:25 UTC
234   us c000ev7m       4    Friday, January 25, 2013 05:28:39 UTC
235   nn 00400860       9    Friday, January 25, 2013 05:28:20 UTC
236   nc 71928381       0    Friday, January 25, 2013 05:23:09 UTC
237   ak 10644566       1    Friday, January 25, 2013 05:20:21 UTC
238   nc 71928376       3    Friday, January 25, 2013 05:12:27 UTC
239   us c000ev7y       7    Friday, January 25, 2013 05:00:15 UTC
240   nc 71928371       3    Friday, January 25, 2013 04:50:51 UTC
241   nc 71928361       1    Friday, January 25, 2013 04:43:57 UTC
242   pr 13025000       0    Friday, January 25, 2013 04:34:28 UTC
243   ak 10644550       1    Friday, January 25, 2013 04:33:35 UTC
244   nn 00400858       9    Friday, January 25, 2013 04:32:46 UTC
245   uw 60497357       3    Friday, January 25, 2013 04:27:42 UTC
246   nc 71928351       2    Friday, January 25, 2013 04:24:42 UTC
247   nc 71928341       0    Friday, January 25, 2013 04:13:19 UTC
248   uw 60497347       2    Friday, January 25, 2013 03:43:07 UTC
249   nc 71928336       0    Friday, January 25, 2013 03:35:46 UTC
250   nn 00400851       9    Friday, January 25, 2013 03:07:08 UTC
251   ak 10644524       1    Friday, January 25, 2013 02:38:25 UTC
252   hv 60458141       2    Friday, January 25, 2013 02:30:58 UTC
253   ak 10644518       1    Friday, January 25, 2013 02:30:32 UTC
254   nc 71928306       0    Friday, January 25, 2013 02:20:37 UTC
255   ci 15277321       2    Friday, January 25, 2013 02:08:50 UTC
256   nc 71928296       3    Friday, January 25, 2013 02:03:25 UTC
257   nc 71928276       2    Friday, January 25, 2013 01:23:27 UTC
258   nc 71928271       2    Friday, January 25, 2013 01:20:05 UTC
259   nn 00400841       9    Friday, January 25, 2013 01:17:44 UTC
260   nc 71928261       3    Friday, January 25, 2013 01:13:19 UTC
261   nc 71928251       3    Friday, January 25, 2013 00:56:10 UTC
262   nn 00400838       9    Friday, January 25, 2013 00:46:03 UTC
263   ak 10644482       1    Friday, January 25, 2013 00:44:22 UTC
264   uw 60497317       1    Friday, January 25, 2013 00:41:11 UTC
265   ak 10644477       1    Friday, January 25, 2013 00:36:32 UTC
266   nn 00400834       9    Friday, January 25, 2013 00:22:03 UTC
267   nn 00400833       9    Friday, January 25, 2013 00:18:54 UTC
268   nn 00400830       9    Friday, January 25, 2013 00:12:53 UTC
269   nn 00400828       9    Friday, January 25, 2013 00:11:41 UTC
270   ak 10644461       1    Friday, January 25, 2013 00:10:02 UTC
271   nc 71928221       0    Friday, January 25, 2013 00:06:25 UTC
272   nc 71928216       2  Thursday, January 24, 2013 23:59:10 UTC
273   hv 60458081       1  Thursday, January 24, 2013 23:43:41 UTC
274   nc 71928211       0  Thursday, January 24, 2013 23:38:57 UTC
275   nn 00400817       9  Thursday, January 24, 2013 23:37:36 UTC
276   nc 71928206       0  Thursday, January 24, 2013 23:33:34 UTC
277   ak 10644443       1  Thursday, January 24, 2013 23:28:21 UTC
278   nc 71928201       A  Thursday, January 24, 2013 23:25:51 UTC
279   nc 71928191       0  Thursday, January 24, 2013 23:14:45 UTC
280   ci 15277273       2  Thursday, January 24, 2013 23:09:10 UTC
281   nc 71928176       2  Thursday, January 24, 2013 23:02:55 UTC
282   ak 10644415       1  Thursday, January 24, 2013 22:57:47 UTC
283   ci 15277257       2  Thursday, January 24, 2013 22:37:12 UTC
284   nn 00400807       9  Thursday, January 24, 2013 22:30:52 UTC
285   nc 71928166       0  Thursday, January 24, 2013 22:28:55 UTC
286   nc 71928161       2  Thursday, January 24, 2013 22:23:35 UTC
287   nn 00400804       9  Thursday, January 24, 2013 22:22:41 UTC
288   nc 71928156       0  Thursday, January 24, 2013 21:31:16 UTC
289   ak 10644186       2  Thursday, January 24, 2013 21:28:07 UTC
290   ak 10644180       2  Thursday, January 24, 2013 21:16:44 UTC
291   nn 00400795       9  Thursday, January 24, 2013 21:15:34 UTC
292   ci 15277233       2  Thursday, January 24, 2013 21:15:23 UTC
293   ci 15277225       2  Thursday, January 24, 2013 21:00:15 UTC
294   uw 60497272       2  Thursday, January 24, 2013 20:48:05 UTC
295   nn 00400787       9  Thursday, January 24, 2013 20:43:35 UTC
296   nc 71928146       3  Thursday, January 24, 2013 20:40:05 UTC
297   ci 15277217       2  Thursday, January 24, 2013 20:39:40 UTC
298   nc 71928136       1  Thursday, January 24, 2013 20:24:10 UTC
299   uu 60011302       3  Thursday, January 24, 2013 20:22:39 UTC
300   ak 10644157       1  Thursday, January 24, 2013 19:46:00 UTC
301   ci 15277209       2  Thursday, January 24, 2013 19:38:39 UTC
302   nc 71928131       1  Thursday, January 24, 2013 19:37:05 UTC
303   nc 71928126       0  Thursday, January 24, 2013 19:35:28 UTC
304   ak 10644143       1  Thursday, January 24, 2013 19:32:47 UTC
305   nc 71928116       0  Thursday, January 24, 2013 19:10:10 UTC
306   ak 10644107       1  Thursday, January 24, 2013 18:55:11 UTC
307   uw 60497252       1  Thursday, January 24, 2013 18:42:48 UTC
308   ci 15277201       2  Thursday, January 24, 2013 18:36:13 UTC
309   nc 71928111       0  Thursday, January 24, 2013 18:30:22 UTC
310   ci 15277185       2  Thursday, January 24, 2013 18:05:50 UTC
311   nc 71928086       2  Thursday, January 24, 2013 17:31:04 UTC
312   ci 15277177       2  Thursday, January 24, 2013 17:07:10 UTC
313   pr 13024004       0  Thursday, January 24, 2013 16:59:32 UTC
314   ci 15277161       3  Thursday, January 24, 2013 16:29:35 UTC
315   ci 15277137       2  Thursday, January 24, 2013 16:26:02 UTC
316   ak 10644047       2  Thursday, January 24, 2013 16:19:46 UTC
317   nc 71928051       0  Thursday, January 24, 2013 15:57:37 UTC
318   ak 10644040       2  Thursday, January 24, 2013 15:56:17 UTC
319   pr 13024005       0  Thursday, January 24, 2013 15:51:40 UTC
320   ci 15277121       2  Thursday, January 24, 2013 15:30:06 UTC
321   nn 00400738       9  Thursday, January 24, 2013 15:00:47 UTC
322   ci 15277097       2  Thursday, January 24, 2013 14:25:56 UTC
323   hv 60457781       1  Thursday, January 24, 2013 14:21:24 UTC
324   nc 71928021       2  Thursday, January 24, 2013 14:16:53 UTC
325   us c000eutf       4  Thursday, January 24, 2013 14:15:49 UTC
326   nc 71928016       0  Thursday, January 24, 2013 14:13:37 UTC
327   ak 10644020       1  Thursday, January 24, 2013 14:10:32 UTC
328   pr 13024003       0  Thursday, January 24, 2013 13:53:38 UTC
329   nc 71928006       3  Thursday, January 24, 2013 13:50:59 UTC
330   nc 71927996       0  Thursday, January 24, 2013 13:22:59 UTC
331   ak 10644132       2  Thursday, January 24, 2013 12:58:16 UTC
332   uw 60497212       1  Thursday, January 24, 2013 12:57:12 UTC
333   nc 71927981       0  Thursday, January 24, 2013 12:40:40 UTC
334   ak 10643998       1  Thursday, January 24, 2013 12:36:29 UTC
335   nn 00400715       9  Thursday, January 24, 2013 12:15:51 UTC
336   pr 13024002       0  Thursday, January 24, 2013 12:13:16 UTC
337   nn 00400714       9  Thursday, January 24, 2013 12:04:45 UTC
338   ci 15277065       2  Thursday, January 24, 2013 12:02:26 UTC
339   ak 10643988       1  Thursday, January 24, 2013 11:54:55 UTC
340   nc 71927961       3  Thursday, January 24, 2013 11:50:15 UTC
341   nc 71927966       2  Thursday, January 24, 2013 11:49:36 UTC
342   ak 10643983       2  Thursday, January 24, 2013 11:40:35 UTC
343   nn 00400713       9  Thursday, January 24, 2013 11:35:11 UTC
344   nn 00400712       9  Thursday, January 24, 2013 11:27:28 UTC
345   nc 71927951       9  Thursday, January 24, 2013 11:22:57 UTC
346   nc 71927946       1  Thursday, January 24, 2013 11:18:45 UTC
347   ak 10643969       1  Thursday, January 24, 2013 11:07:59 UTC
348   us c000eurh       6  Thursday, January 24, 2013 10:39:54 UTC
349   nc 71927931       3  Thursday, January 24, 2013 10:26:50 UTC
350   nc 71927926       2  Thursday, January 24, 2013 10:21:26 UTC
351   nn 00400708       9  Thursday, January 24, 2013 10:17:47 UTC
352   nn 00400706       9  Thursday, January 24, 2013 10:06:35 UTC
353   uw 60497197       2  Thursday, January 24, 2013 09:50:41 UTC
354   ak 10643951       1  Thursday, January 24, 2013 09:50:25 UTC
355   nn 00400702       9  Thursday, January 24, 2013 09:42:07 UTC
356   us c000euqx       7  Thursday, January 24, 2013 09:35:54 UTC
357   nc 71927916       3  Thursday, January 24, 2013 09:33:53 UTC
358   nn 00400699       9  Thursday, January 24, 2013 09:28:30 UTC
359   us c000euqv       7  Thursday, January 24, 2013 09:28:29 UTC
360   nn 00400698       9  Thursday, January 24, 2013 09:21:31 UTC
361   nn 00400697       9  Thursday, January 24, 2013 09:13:46 UTC
362   nc 71927906       0  Thursday, January 24, 2013 09:12:01 UTC
363   nn 00400695       9  Thursday, January 24, 2013 09:05:59 UTC
364   ak 10643940       1  Thursday, January 24, 2013 09:01:27 UTC
365   ak 10643939       2  Thursday, January 24, 2013 08:57:38 UTC
366   nn 00400694       9  Thursday, January 24, 2013 08:56:12 UTC
367   nn 00400693       9  Thursday, January 24, 2013 08:43:25 UTC
368   nc 71927896       0  Thursday, January 24, 2013 08:33:01 UTC
369   nc 71927891       0  Thursday, January 24, 2013 08:32:49 UTC
370   nn 00400690       9  Thursday, January 24, 2013 08:30:12 UTC
371   nc 71927886       0  Thursday, January 24, 2013 08:28:05 UTC
372   nc 71927876       3  Thursday, January 24, 2013 08:25:24 UTC
373   nc 71069289       6  Thursday, January 24, 2013 08:23:30 UTC
374   nc 71069294       2  Thursday, January 24, 2013 08:23:19 UTC
375   nc 71927871       B  Thursday, January 24, 2013 08:21:48 UTC
376   ci 15276985       2  Thursday, January 24, 2013 08:18:45 UTC
377   nc 71927866       0  Thursday, January 24, 2013 08:16:31 UTC
378   ci 15276977       2  Thursday, January 24, 2013 08:07:43 UTC
379   nn 00400684       9  Thursday, January 24, 2013 08:06:42 UTC
380   nc 71927851       0  Thursday, January 24, 2013 07:56:53 UTC
381   nn 00400683       9  Thursday, January 24, 2013 07:55:38 UTC
382   nc 71927846       1  Thursday, January 24, 2013 07:54:01 UTC
383   nc 71927836       4  Thursday, January 24, 2013 07:42:21 UTC
384   nc 71927831       2  Thursday, January 24, 2013 07:41:21 UTC
385   us c000euq3       5  Thursday, January 24, 2013 07:35:42 UTC
386   ak 10643901       1  Thursday, January 24, 2013 07:31:42 UTC
387   ci 15276961       2  Thursday, January 24, 2013 07:30:41 UTC
388   us c000eupr       7  Thursday, January 24, 2013 07:08:16 UTC
389   nc 71927811       3  Thursday, January 24, 2013 06:48:13 UTC
390   ak 10643885       1  Thursday, January 24, 2013 06:42:50 UTC
391   nc 71927806       0  Thursday, January 24, 2013 06:40:42 UTC
392   nc 71927796       1  Thursday, January 24, 2013 06:36:39 UTC
393   nc 71927791       1  Thursday, January 24, 2013 06:35:19 UTC
394   nc 71927786       3  Thursday, January 24, 2013 06:30:00 UTC
395   ak 10643875       2  Thursday, January 24, 2013 06:26:02 UTC
396   nc 71927781       2  Thursday, January 24, 2013 06:24:25 UTC
397   nc 71927776       2  Thursday, January 24, 2013 06:23:54 UTC
398   ci 15276945       2  Thursday, January 24, 2013 06:22:44 UTC
399   ak 10643868       1  Thursday, January 24, 2013 06:18:09 UTC
400   ak 10643861       2  Thursday, January 24, 2013 06:07:37 UTC
401   ci 15276937       2  Thursday, January 24, 2013 05:53:39 UTC
402   nc 71927761       6  Thursday, January 24, 2013 05:43:10 UTC
403   nc 71927756       1  Thursday, January 24, 2013 05:20:38 UTC
404   nc 71927751       0  Thursday, January 24, 2013 05:13:16 UTC
405   uu 60011247       3  Thursday, January 24, 2013 05:05:58 UTC
406   uw 60497122       1  Thursday, January 24, 2013 05:00:12 UTC
407   nc 71927741       0  Thursday, January 24, 2013 04:52:53 UTC
408   us c000eup1       5  Thursday, January 24, 2013 04:51:06 UTC
409   uu 60011237       6  Thursday, January 24, 2013 04:46:39 UTC
410   nn 00400674       9  Thursday, January 24, 2013 04:43:29 UTC
411   nc 71927731       3  Thursday, January 24, 2013 04:08:22 UTC
412   ak 10643837       2  Thursday, January 24, 2013 04:02:56 UTC
413   uu 60011227       4  Thursday, January 24, 2013 04:01:05 UTC
414   ak 10643831       1  Thursday, January 24, 2013 03:48:44 UTC
415   ak 10643828       2  Thursday, January 24, 2013 03:44:14 UTC
416   nn 00400671       9  Thursday, January 24, 2013 03:36:18 UTC
417   nn 00400667       9  Thursday, January 24, 2013 02:30:58 UTC
418   ak 10643810       1  Thursday, January 24, 2013 02:30:56 UTC
419   nn 00400664       9  Thursday, January 24, 2013 02:28:02 UTC
420   pr 13024001       0  Thursday, January 24, 2013 02:21:46 UTC
421   us c000eun4       4  Thursday, January 24, 2013 02:17:10 UTC
422   ak 10643800       1  Thursday, January 24, 2013 01:41:39 UTC
423   ak 10643799       1  Thursday, January 24, 2013 01:39:44 UTC
424   ci 15276849       2  Thursday, January 24, 2013 00:58:31 UTC
425   nc 71927696       0  Thursday, January 24, 2013 00:55:07 UTC
426   nc 71927691       0  Thursday, January 24, 2013 00:54:46 UTC
427   nc 71927686       0  Thursday, January 24, 2013 00:53:37 UTC
428   pr 13024000       0  Thursday, January 24, 2013 00:08:30 UTC
429   ak 10643763       1  Thursday, January 24, 2013 00:07:01 UTC
430   ak 10643761       1  Thursday, January 24, 2013 00:04:07 UTC
431   uw 60497082       1  Thursday, January 24, 2013 00:04:06 UTC
432   uw 60497077       1 Wednesday, January 23, 2013 23:37:40 UTC
433   nn 00400643       9 Wednesday, January 23, 2013 23:32:10 UTC
434   nc 71927671       4 Wednesday, January 23, 2013 23:15:46 UTC
435   nc 71927666       1 Wednesday, January 23, 2013 23:14:38 UTC
436   nc 71927661       1 Wednesday, January 23, 2013 22:54:13 UTC
437   ak 10643707       1 Wednesday, January 23, 2013 22:40:22 UTC
438   mb 13496898       2 Wednesday, January 23, 2013 22:30:48 UTC
439   ci 15276817       2 Wednesday, January 23, 2013 22:28:36 UTC
440   ak 10643678       1 Wednesday, January 23, 2013 22:18:37 UTC
441   nc 71927646       0 Wednesday, January 23, 2013 22:13:54 UTC
442   uw 60496962       1 Wednesday, January 23, 2013 22:11:24 UTC
443   ak 10643672       2 Wednesday, January 23, 2013 22:05:30 UTC
444   pr 13023008       0 Wednesday, January 23, 2013 21:59:04 UTC
445   nc 71927636       0 Wednesday, January 23, 2013 21:49:34 UTC
446   ci 15276793       2 Wednesday, January 23, 2013 21:38:11 UTC
447   us c000euil       6 Wednesday, January 23, 2013 21:34:32 UTC
448   us c000euhy       B Wednesday, January 23, 2013 21:31:06 UTC
449   ak 10643631       1 Wednesday, January 23, 2013 21:14:13 UTC
450   ci 15276761       2 Wednesday, January 23, 2013 20:42:00 UTC
451   pr 13023007       0 Wednesday, January 23, 2013 20:36:51 UTC
452   ci 15276753       2 Wednesday, January 23, 2013 20:25:19 UTC
453   ak 10643433       2 Wednesday, January 23, 2013 19:58:39 UTC
454   nc 71927586       2 Wednesday, January 23, 2013 19:55:12 UTC
455   nc 71927571       0 Wednesday, January 23, 2013 19:37:05 UTC
456   nn 00400598       9 Wednesday, January 23, 2013 19:36:03 UTC
457   uu 60011187       5 Wednesday, January 23, 2013 19:25:59 UTC
458   nc 71927566       2 Wednesday, January 23, 2013 19:20:13 UTC
459   uu 60011182       2 Wednesday, January 23, 2013 19:20:07 UTC
460   nm  012413a       A Wednesday, January 23, 2013 19:09:03 UTC
461   nc 71927551       0 Wednesday, January 23, 2013 18:57:08 UTC
462   ak 10643383       2 Wednesday, January 23, 2013 18:51:38 UTC
463   nc 71927536       1 Wednesday, January 23, 2013 18:15:34 UTC
464   nc 71927531       0 Wednesday, January 23, 2013 18:12:32 UTC
465   ak 10643350       1 Wednesday, January 23, 2013 18:10:49 UTC
466   ak 10643346       2 Wednesday, January 23, 2013 18:04:49 UTC
467   us b000etal       2 Wednesday, January 23, 2013 18:01:56 UTC
468   mb 13523744       2 Wednesday, January 23, 2013 17:58:25 UTC
469   nc 71927521       0 Wednesday, January 23, 2013 17:52:21 UTC
470   us b000et9x       2 Wednesday, January 23, 2013 17:05:17 UTC
471   ak 10643321       1 Wednesday, January 23, 2013 16:52:39 UTC
472   nc 71927506       0 Wednesday, January 23, 2013 16:50:11 UTC
473   ak 10643312       1 Wednesday, January 23, 2013 16:35:50 UTC
474   hv 60457406       2 Wednesday, January 23, 2013 16:29:07 UTC
475   ci 15276721       3 Wednesday, January 23, 2013 16:14:10 UTC
476   nc 71927491       2 Wednesday, January 23, 2013 16:14:01 UTC
477   nc 71927481       3 Wednesday, January 23, 2013 15:43:05 UTC
478   nc 71927471       0 Wednesday, January 23, 2013 15:37:22 UTC
479   ci 15276713       2 Wednesday, January 23, 2013 15:30:31 UTC
480   ci 15276705       2 Wednesday, January 23, 2013 14:33:29 UTC
481   nc 71927456       3 Wednesday, January 23, 2013 14:22:00 UTC
482   uu 60011162       6 Wednesday, January 23, 2013 13:41:56 UTC
483   pr 13023003       0 Wednesday, January 23, 2013 13:38:11 UTC
484   ak 10643274       1 Wednesday, January 23, 2013 13:19:45 UTC
485   mb 13770585       2 Wednesday, January 23, 2013 12:41:07 UTC
486   us b000et7j       6 Wednesday, January 23, 2013 12:39:41 UTC
487   nc 71927421       3 Wednesday, January 23, 2013 12:37:28 UTC
488   us b000et7d       6 Wednesday, January 23, 2013 12:36:56 UTC
489   ak 10643265       2 Wednesday, January 23, 2013 12:33:39 UTC
490   pr 13023002       0 Wednesday, January 23, 2013 12:21:14 UTC
491   nc 71927411       0 Wednesday, January 23, 2013 12:14:33 UTC
492   ak 10643259       1 Wednesday, January 23, 2013 12:06:35 UTC
493   nc 71927391       2 Wednesday, January 23, 2013 11:45:08 UTC
494   nc 71927381       7 Wednesday, January 23, 2013 11:09:32 UTC
495   ci 15276673       2 Wednesday, January 23, 2013 10:45:39 UTC
496   nn 00400573       9 Wednesday, January 23, 2013 10:31:24 UTC
497   ak 10643251       1 Wednesday, January 23, 2013 10:27:36 UTC
498   pr 13023004       0 Wednesday, January 23, 2013 10:16:54 UTC
499   pr 13023006       0 Wednesday, January 23, 2013 10:16:26 UTC
500   nc 71927361       0 Wednesday, January 23, 2013 10:10:59 UTC
501   us b000et6b       6 Wednesday, January 23, 2013 09:51:26 UTC
502   ak 10643243       1 Wednesday, January 23, 2013 09:46:34 UTC
503   nc 71927341       2 Wednesday, January 23, 2013 09:20:22 UTC
504   nc 71927336       1 Wednesday, January 23, 2013 09:19:46 UTC
505   ak 10643236       1 Wednesday, January 23, 2013 09:18:17 UTC
506   ci 15276649       2 Wednesday, January 23, 2013 08:45:48 UTC
507   ci 15276633       0 Wednesday, January 23, 2013 08:39:56 UTC
508   pr 13023001       0 Wednesday, January 23, 2013 08:33:58 UTC
509   us b000et5r       7 Wednesday, January 23, 2013 08:23:00 UTC
510   ci 15276625       0 Wednesday, January 23, 2013 08:17:32 UTC
511   ak 10643221       1 Wednesday, January 23, 2013 08:14:03 UTC
512   ci 15276617       0 Wednesday, January 23, 2013 07:58:23 UTC
513   us b000et5h       9 Wednesday, January 23, 2013 07:43:02 UTC
514   nc 71927271       0 Wednesday, January 23, 2013 07:18:49 UTC
515   nc 71927261       1 Wednesday, January 23, 2013 06:57:59 UTC
516   nc 71927256       0 Wednesday, January 23, 2013 06:46:35 UTC
517   ak 10643347       2 Wednesday, January 23, 2013 06:44:05 UTC
518   ak 10643205       1 Wednesday, January 23, 2013 06:28:54 UTC
519   ak 10643202       1 Wednesday, January 23, 2013 06:23:55 UTC
520   nc 71927246       0 Wednesday, January 23, 2013 06:10:48 UTC
521   nc 71927241       0 Wednesday, January 23, 2013 06:00:40 UTC
522   uu 60011152       3 Wednesday, January 23, 2013 05:53:43 UTC
523   uu 60011147       4 Wednesday, January 23, 2013 05:40:15 UTC
524   uu 60011142       4 Wednesday, January 23, 2013 05:31:48 UTC
525   ak 10643197       1 Wednesday, January 23, 2013 04:52:15 UTC
526   us b000et4v       6 Wednesday, January 23, 2013 04:42:58 UTC
527   uu 60011132       4 Wednesday, January 23, 2013 04:42:37 UTC
528   nc 71927221       3 Wednesday, January 23, 2013 04:38:01 UTC
529   us b000et4q       8 Wednesday, January 23, 2013 04:29:38 UTC
530   ci 15276609       0 Wednesday, January 23, 2013 04:28:06 UTC
531   ci 15276601       0 Wednesday, January 23, 2013 04:27:29 UTC
532   nc 71927211       4 Wednesday, January 23, 2013 04:26:09 UTC
533   us b000et4k       7 Wednesday, January 23, 2013 04:18:18 UTC
534   us b000et4i       5 Wednesday, January 23, 2013 04:16:20 UTC
535   nn 00400561       9 Wednesday, January 23, 2013 04:10:02 UTC
536   ak 10643177       2 Wednesday, January 23, 2013 03:25:13 UTC
537   pr 13023000       0 Wednesday, January 23, 2013 03:23:10 UTC
538   us b000et4d       5 Wednesday, January 23, 2013 03:21:55 UTC
539   nc 71927186       0 Wednesday, January 23, 2013 03:10:30 UTC
540   ci 15276585       0 Wednesday, January 23, 2013 03:03:20 UTC
541   nc 71927181       0 Wednesday, January 23, 2013 02:49:27 UTC
542   us b000et4b       6 Wednesday, January 23, 2013 02:47:38 UTC
543   nc 71927166       1 Wednesday, January 23, 2013 02:33:46 UTC
544   ci 15276577       6 Wednesday, January 23, 2013 02:06:48 UTC
545   us b000et48       6 Wednesday, January 23, 2013 01:49:22 UTC
546   ak 10643163       1 Wednesday, January 23, 2013 01:37:10 UTC
547   ak 10643142       1 Wednesday, January 23, 2013 00:52:49 UTC
548   nc 71927141       0 Wednesday, January 23, 2013 00:37:26 UTC
549   ak 10643129       1 Wednesday, January 23, 2013 00:23:10 UTC
550   ak 10643124       1 Wednesday, January 23, 2013 00:06:19 UTC
551   ci 15276553       2   Tuesday, January 22, 2013 23:59:44 UTC
552   nc 71927126       2   Tuesday, January 22, 2013 23:59:23 UTC
553   us b000et0q       4   Tuesday, January 22, 2013 23:54:29 UTC
554   ci 15276545       2   Tuesday, January 22, 2013 23:47:53 UTC
555   nc 71927106       2   Tuesday, January 22, 2013 23:47:37 UTC
556   uw 60496707       1   Tuesday, January 22, 2013 23:39:28 UTC
557   nc 71927101       5   Tuesday, January 22, 2013 23:36:56 UTC
558   uw 60496697       1   Tuesday, January 22, 2013 23:29:33 UTC
559   ak 10643078       3   Tuesday, January 22, 2013 23:01:32 UTC
560   pr 13022002       0   Tuesday, January 22, 2013 23:01:29 UTC
561   ak 10643075       2   Tuesday, January 22, 2013 22:57:42 UTC
562   ak 10643063       2   Tuesday, January 22, 2013 22:30:47 UTC
563   nc 71927051       4   Tuesday, January 22, 2013 22:17:25 UTC
564   ak 10643045       3   Tuesday, January 22, 2013 21:47:48 UTC
565   ak 10645026       2   Tuesday, January 22, 2013 21:44:42 UTC
566   ak 10643042       2   Tuesday, January 22, 2013 21:41:12 UTC
567   ak 10643036       2   Tuesday, January 22, 2013 21:30:28 UTC
568   us c000eupd       4   Tuesday, January 22, 2013 21:29:33 UTC
569   ak 10643028       2   Tuesday, January 22, 2013 21:28:48 UTC
570   ak 10643024       2   Tuesday, January 22, 2013 21:22:44 UTC
571   nn 00400457       9   Tuesday, January 22, 2013 21:11:02 UTC
572   uw 60496602       3   Tuesday, January 22, 2013 20:50:09 UTC
573   nc 71926996       3   Tuesday, January 22, 2013 20:47:48 UTC
574   ak 10642992       2   Tuesday, January 22, 2013 20:41:02 UTC
575   ci 15276529       2   Tuesday, January 22, 2013 20:38:29 UTC
576   ak 10645020       2   Tuesday, January 22, 2013 20:36:14 UTC
577   ak 10645019       2   Tuesday, January 22, 2013 20:35:42 UTC
578   ak 10645018       2   Tuesday, January 22, 2013 20:28:18 UTC
579   us b000esu0       4   Tuesday, January 22, 2013 20:04:39 UTC
580   us b000estr       5   Tuesday, January 22, 2013 19:58:23 UTC
581   ak 10645017       2   Tuesday, January 22, 2013 19:51:49 UTC
582   uw 60496512       1   Tuesday, January 22, 2013 19:49:23 UTC
583   ak 10645016       2   Tuesday, January 22, 2013 19:22:24 UTC
584   ak 10642944       2   Tuesday, January 22, 2013 19:18:48 UTC
585   ak 10642939       3   Tuesday, January 22, 2013 19:15:40 UTC
586   us b000est3       8   Tuesday, January 22, 2013 19:05:54 UTC
587   nc 71926941       2   Tuesday, January 22, 2013 19:03:45 UTC
588   nn 00400432       9   Tuesday, January 22, 2013 19:01:29 UTC
589   nc 71926921       3   Tuesday, January 22, 2013 18:56:38 UTC
590   ak 10645012       2   Tuesday, January 22, 2013 18:47:40 UTC
591   nc 71926916       2   Tuesday, January 22, 2013 18:45:57 UTC
592   ci 15276473       2   Tuesday, January 22, 2013 18:33:48 UTC
593   us b000essi       6   Tuesday, January 22, 2013 18:29:57 UTC
594   ak 10642899       2   Tuesday, January 22, 2013 18:28:15 UTC
595   ak 10642893       2   Tuesday, January 22, 2013 18:26:09 UTC
596   ak 10645009       2   Tuesday, January 22, 2013 18:20:53 UTC
597   ak 10645008       2   Tuesday, January 22, 2013 18:19:52 UTC
598   nc 71926891       4   Tuesday, January 22, 2013 17:58:41 UTC
599   us b000esrf       6   Tuesday, January 22, 2013 17:07:17 UTC
600   ci 15276449       2   Tuesday, January 22, 2013 16:59:07 UTC
601   ak 10642862       3   Tuesday, January 22, 2013 16:38:45 UTC
602   ak 10645006       2   Tuesday, January 22, 2013 16:13:24 UTC
603   ak 10645005       2   Tuesday, January 22, 2013 16:10:17 UTC
604   ak 10645004       2   Tuesday, January 22, 2013 16:06:44 UTC
605   hv 60456741       1   Tuesday, January 22, 2013 15:59:13 UTC
606   nc 71927581       2   Tuesday, January 22, 2013 15:57:44 UTC
607   us 2013ksam       4   Tuesday, January 22, 2013 15:49:24 UTC
608   ak 10642837       2   Tuesday, January 22, 2013 15:35:20 UTC
609   ak 10642830       2   Tuesday, January 22, 2013 15:17:24 UTC
610   us b000esq0       A   Tuesday, January 22, 2013 15:09:22 UTC
611   nc 71926826       2   Tuesday, January 22, 2013 15:07:57 UTC
612   ak 10645000       2   Tuesday, January 22, 2013 14:34:56 UTC
613   uw 60496432       2   Tuesday, January 22, 2013 14:24:19 UTC
614   ak 10644999       2   Tuesday, January 22, 2013 13:58:31 UTC
615   nc 71926791       0   Tuesday, January 22, 2013 13:56:36 UTC
616   uw 60496427       2   Tuesday, January 22, 2013 13:56:07 UTC
617   us b000esns       7   Tuesday, January 22, 2013 13:29:22 UTC
618   ci 15276425       2   Tuesday, January 22, 2013 13:19:09 UTC
619   hv 60456681       1   Tuesday, January 22, 2013 13:11:40 UTC
620   ak 10642798       3   Tuesday, January 22, 2013 12:55:57 UTC
621   us b000esnh       5   Tuesday, January 22, 2013 12:54:04 UTC
622   ak 10642800       3   Tuesday, January 22, 2013 12:46:54 UTC
623   ak 10642795       2   Tuesday, January 22, 2013 12:45:27 UTC
624   nc 71926766       5   Tuesday, January 22, 2013 12:45:02 UTC
625   ak 10644995       2   Tuesday, January 22, 2013 12:44:06 UTC
626   ci 15276385       2   Tuesday, January 22, 2013 11:37:50 UTC
627   nc 71069274       2   Tuesday, January 22, 2013 11:22:33 UTC
628   ak 10642777       2   Tuesday, January 22, 2013 11:22:18 UTC
629   ak 10642776       2   Tuesday, January 22, 2013 11:16:03 UTC
630   ak 10642774       2   Tuesday, January 22, 2013 11:15:02 UTC
631   us b000esmf       8   Tuesday, January 22, 2013 11:12:22 UTC
632   ak 10644990       2   Tuesday, January 22, 2013 11:10:15 UTC
633   ci 15276369       2   Tuesday, January 22, 2013 11:06:49 UTC
634   ci 15276361       5   Tuesday, January 22, 2013 10:54:55 UTC
635   us b000esm3       4   Tuesday, January 22, 2013 10:43:11 UTC
636   ci 15276353       0   Tuesday, January 22, 2013 10:40:18 UTC
637   hv 60456611       4   Tuesday, January 22, 2013 10:40:07 UTC
638   uw 60496402       1   Tuesday, January 22, 2013 10:26:36 UTC
639   ak 10642764       2   Tuesday, January 22, 2013 10:26:12 UTC
640   us b000esln       6   Tuesday, January 22, 2013 10:24:23 UTC
641   ci 15276345       0   Tuesday, January 22, 2013 10:20:23 UTC
642   nn 00400366       9   Tuesday, January 22, 2013 10:12:13 UTC
643   nc 71926731       3   Tuesday, January 22, 2013 10:11:58 UTC
644   nc 71926736       2   Tuesday, January 22, 2013 10:10:59 UTC
645   ak 10642758       2   Tuesday, January 22, 2013 10:07:09 UTC
646   ak 10642757       2   Tuesday, January 22, 2013 09:51:41 UTC
647   ak 10644986       2   Tuesday, January 22, 2013 09:49:58 UTC
648   nc 71926721       1   Tuesday, January 22, 2013 09:37:40 UTC
649   uu 60011017       2   Tuesday, January 22, 2013 09:32:02 UTC
650   nc 71926711       5   Tuesday, January 22, 2013 09:25:58 UTC
651   ak 10642746       2   Tuesday, January 22, 2013 09:11:19 UTC
652   ak 10642744       2   Tuesday, January 22, 2013 08:53:06 UTC
653   ak 10642742       2   Tuesday, January 22, 2013 08:44:04 UTC
654   us b000esl6       9   Tuesday, January 22, 2013 08:40:51 UTC
655   nc 71926696       2   Tuesday, January 22, 2013 08:37:50 UTC
656   uu 60011012       5   Tuesday, January 22, 2013 08:11:31 UTC
657   ak 10644982       2   Tuesday, January 22, 2013 08:09:51 UTC
658   ak 10642737       3   Tuesday, January 22, 2013 08:06:16 UTC
659   ak 10642730       2   Tuesday, January 22, 2013 07:43:08 UTC
660   ak 10642731       2   Tuesday, January 22, 2013 07:41:24 UTC
661   uw 60496282       2   Tuesday, January 22, 2013 07:36:36 UTC
662   us b000esku       8   Tuesday, January 22, 2013 07:29:30 UTC
663   ak 10644978       2   Tuesday, January 22, 2013 07:23:19 UTC
664   pr 13022001       0   Tuesday, January 22, 2013 07:01:33 UTC
665   ak 10642725       2   Tuesday, January 22, 2013 07:00:19 UTC
666   ak 10644976       2   Tuesday, January 22, 2013 06:59:05 UTC
667   nc 71926636       2   Tuesday, January 22, 2013 06:59:03 UTC
668   ci 15276321       0   Tuesday, January 22, 2013 06:58:07 UTC
669   ak 10642722       3   Tuesday, January 22, 2013 06:56:09 UTC
670   ak 10642720       2   Tuesday, January 22, 2013 06:54:25 UTC
671   ci 15276313       0   Tuesday, January 22, 2013 06:38:34 UTC
672   ak 10644973       2   Tuesday, January 22, 2013 06:38:04 UTC
673   mb 13578767       2   Tuesday, January 22, 2013 06:26:35 UTC
674   ak 10642715       2   Tuesday, January 22, 2013 06:23:29 UTC
675   nc 71926621       0   Tuesday, January 22, 2013 06:13:21 UTC
676   ci 15276305       2   Tuesday, January 22, 2013 06:03:50 UTC
677   ak 10644971       2   Tuesday, January 22, 2013 06:01:02 UTC
678   ak 10644970       2   Tuesday, January 22, 2013 05:56:51 UTC
679   ak 10644969       2   Tuesday, January 22, 2013 05:54:47 UTC
680   nc 71926601       3   Tuesday, January 22, 2013 05:52:10 UTC
681   ak 10644968       2   Tuesday, January 22, 2013 05:40:42 UTC
682   ak 10644967       2   Tuesday, January 22, 2013 05:34:55 UTC
683   ak 10642706       2   Tuesday, January 22, 2013 05:31:47 UTC
684   ak 10642704       2   Tuesday, January 22, 2013 05:29:44 UTC
685   uu 60011007       3   Tuesday, January 22, 2013 05:18:54 UTC
686   hv 60456441       2   Tuesday, January 22, 2013 05:12:28 UTC
687   ak 10642697       2   Tuesday, January 22, 2013 05:00:33 UTC
688   ak 10644963       2   Tuesday, January 22, 2013 04:55:10 UTC
689   ak 10644962       2   Tuesday, January 22, 2013 04:37:29 UTC
690   ak 10642689       2   Tuesday, January 22, 2013 04:29:54 UTC
691   ci 15276297       0   Tuesday, January 22, 2013 04:22:46 UTC
692   pr 13022000       0   Tuesday, January 22, 2013 03:48:57 UTC
693   ak 10644960       2   Tuesday, January 22, 2013 03:37:54 UTC
694   ak 10642680       2   Tuesday, January 22, 2013 03:31:42 UTC
695   nn 00400359       9   Tuesday, January 22, 2013 03:19:20 UTC
696   ak 10642674       2   Tuesday, January 22, 2013 03:17:04 UTC
697   ak 10644957       2   Tuesday, January 22, 2013 03:09:19 UTC
698   ci 15276289       5   Tuesday, January 22, 2013 03:07:12 UTC
699   ak 10642668       2   Tuesday, January 22, 2013 02:58:20 UTC
700   nc 71926531       0   Tuesday, January 22, 2013 02:51:32 UTC
701   ak 10642664       2   Tuesday, January 22, 2013 02:15:48 UTC
702   ak 10644954       2   Tuesday, January 22, 2013 02:14:21 UTC
703   ak 10644953       2   Tuesday, January 22, 2013 02:11:17 UTC
704   ak 10642659       2   Tuesday, January 22, 2013 02:09:17 UTC
705   ak 10642658       2   Tuesday, January 22, 2013 02:00:31 UTC
706   ak 10642654       2   Tuesday, January 22, 2013 01:56:05 UTC
707   ak 10642653       2   Tuesday, January 22, 2013 01:42:04 UTC
708   ak 10644948       2   Tuesday, January 22, 2013 01:39:34 UTC
709   ci 15276273       2   Tuesday, January 22, 2013 01:38:53 UTC
710   ak 10644947       2   Tuesday, January 22, 2013 01:37:46 UTC
711   nc 71926521       2   Tuesday, January 22, 2013 01:31:04 UTC
712   ak 10642648       3   Tuesday, January 22, 2013 01:24:17 UTC
713   nc 71926506       0   Tuesday, January 22, 2013 01:21:11 UTC
714   ak 10644945       2   Tuesday, January 22, 2013 01:20:44 UTC
715   ak 10642590       2   Tuesday, January 22, 2013 01:11:02 UTC
716   ak 10644943       2   Tuesday, January 22, 2013 01:08:41 UTC
717   uw 60496187       1   Tuesday, January 22, 2013 01:08:38 UTC
718   nc 71926491       3   Tuesday, January 22, 2013 01:06:36 UTC
719   ak 10644942       2   Tuesday, January 22, 2013 01:00:50 UTC
720   hv 60456226       1   Tuesday, January 22, 2013 00:55:23 UTC
721   nn 00400353       9   Tuesday, January 22, 2013 00:55:18 UTC
722   ak 10642524       2   Tuesday, January 22, 2013 00:35:56 UTC
723   ak 10642521       3   Tuesday, January 22, 2013 00:32:51 UTC
724   ak 10642519       2   Tuesday, January 22, 2013 00:31:52 UTC
725   ak 10642525       2   Tuesday, January 22, 2013 00:28:58 UTC
726   ci 15276233       0   Tuesday, January 22, 2013 00:23:18 UTC
727   ci 15276241       2   Tuesday, January 22, 2013 00:20:41 UTC
728   ak 10642515       2   Tuesday, January 22, 2013 00:08:50 UTC
729   nc 71926481       3   Tuesday, January 22, 2013 00:05:03 UTC
730   nc 71926476       0    Monday, January 21, 2013 23:56:00 UTC
731   ak 10642511       2    Monday, January 21, 2013 23:54:14 UTC
732   ci 15276209       0    Monday, January 21, 2013 23:26:30 UTC
733   ak 10644307       2    Monday, January 21, 2013 23:26:02 UTC
734   nc 71926461       0    Monday, January 21, 2013 23:12:20 UTC
735   ak 10642496       2    Monday, January 21, 2013 23:10:43 UTC
736   ak 10642497       2    Monday, January 21, 2013 23:09:14 UTC
737   ci 15276201       0    Monday, January 21, 2013 23:06:02 UTC
738   us b000eshb       8    Monday, January 21, 2013 22:48:07 UTC
739   uw 60496152       2    Monday, January 21, 2013 22:37:23 UTC
740   us b000esh7       7    Monday, January 21, 2013 22:34:58 UTC
741   us b000esgn       B    Monday, January 21, 2013 22:22:54 UTC
742   uw 60496142       2    Monday, January 21, 2013 22:07:28 UTC
743   ak 10642473       2    Monday, January 21, 2013 21:57:59 UTC
744   nc 71926416       3    Monday, January 21, 2013 21:52:41 UTC
745   ak 10642465       2    Monday, January 21, 2013 21:49:57 UTC
746   uu 60010982       2    Monday, January 21, 2013 21:36:33 UTC
747   uw 60496132       2    Monday, January 21, 2013 21:11:17 UTC
748   ak 10642443       2    Monday, January 21, 2013 21:09:56 UTC
749   ak 10642432       2    Monday, January 21, 2013 20:49:22 UTC
750   nn 00400325       9    Monday, January 21, 2013 20:38:32 UTC
751   ak 10644300       2    Monday, January 21, 2013 20:35:49 UTC
752   ak 10644298       2    Monday, January 21, 2013 20:15:39 UTC
753   nc 71926336       4    Monday, January 21, 2013 20:14:06 UTC
754   ak 10642409       3    Monday, January 21, 2013 20:00:16 UTC
755   mb 13921078       2    Monday, January 21, 2013 19:53:06 UTC
756   us b000esbm       5    Monday, January 21, 2013 19:49:02 UTC
757   us b000esbl       6    Monday, January 21, 2013 19:46:57 UTC
758   ak 10642394       2    Monday, January 21, 2013 19:21:46 UTC
759   ak 10644294       2    Monday, January 21, 2013 19:21:01 UTC
760   pr 13021007       0    Monday, January 21, 2013 19:17:41 UTC
761   ak 10642390       2    Monday, January 21, 2013 19:01:54 UTC
762   ci 15276153       2    Monday, January 21, 2013 18:59:15 UTC
763   nc 71926291       0    Monday, January 21, 2013 18:54:27 UTC
764   us b000esa2       7    Monday, January 21, 2013 18:32:26 UTC
765   ak 10644292       2    Monday, January 21, 2013 18:25:05 UTC
766   ak 10642378       3    Monday, January 21, 2013 18:14:48 UTC
767   nc 71926276       0    Monday, January 21, 2013 18:14:11 UTC
768   ak 10644290       2    Monday, January 21, 2013 17:58:34 UTC
769   ci 15276145       0    Monday, January 21, 2013 17:49:08 UTC
770   nn 00400305       9    Monday, January 21, 2013 17:43:17 UTC
771   ak 10642367       2    Monday, January 21, 2013 17:41:17 UTC
772   ak 10642365       2    Monday, January 21, 2013 17:39:44 UTC
773   ci 15276129       0    Monday, January 21, 2013 17:38:50 UTC
774   nc 71926256       1    Monday, January 21, 2013 17:33:43 UTC
775   ci 15276121       2    Monday, January 21, 2013 17:24:58 UTC
776   ak 10642350       2    Monday, January 21, 2013 17:23:44 UTC
777   ci 15276105       0    Monday, January 21, 2013 17:22:16 UTC
778   ci 15276097       3    Monday, January 21, 2013 16:54:50 UTC
779   nc 71926231       1    Monday, January 21, 2013 16:50:51 UTC
780   ak 10644286       2    Monday, January 21, 2013 16:48:38 UTC
781   ak 10642339       2    Monday, January 21, 2013 16:42:38 UTC
782   nc 71926216       3    Monday, January 21, 2013 16:39:15 UTC
783   us 2013krah       6    Monday, January 21, 2013 16:34:19 UTC
784   us 2013krag       6    Monday, January 21, 2013 16:32:47 UTC
785   ak 10642332       2    Monday, January 21, 2013 16:27:17 UTC
786   ak 10642331       2    Monday, January 21, 2013 16:26:40 UTC
787   ak 10644281       2    Monday, January 21, 2013 16:20:08 UTC
788   ak 10642328       3    Monday, January 21, 2013 16:15:11 UTC
789   nc 71926186       3    Monday, January 21, 2013 16:02:47 UTC
790   ak 10644279       2    Monday, January 21, 2013 15:47:10 UTC
791   ci 15276081       0    Monday, January 21, 2013 15:34:08 UTC
792   nc 71926181       0    Monday, January 21, 2013 15:25:51 UTC
793   ak 10644278       2    Monday, January 21, 2013 15:21:11 UTC
794   ak 10642321       2    Monday, January 21, 2013 15:11:00 UTC
795   nc 71926166       3    Monday, January 21, 2013 15:07:57 UTC
796   ci 15276073       4    Monday, January 21, 2013 15:05:12 UTC
797   ci 15276065       2    Monday, January 21, 2013 15:00:18 UTC
798   ak 10644276       2    Monday, January 21, 2013 14:56:25 UTC
799   nc 71926156       3    Monday, January 21, 2013 14:54:22 UTC
800   nc 71926151       2    Monday, January 21, 2013 14:52:16 UTC
801   ak 10644275       2    Monday, January 21, 2013 14:48:32 UTC
802   mb 13409570       2    Monday, January 21, 2013 14:38:00 UTC
803   ak 10642311       2    Monday, January 21, 2013 14:36:51 UTC
804   ak 10642310       2    Monday, January 21, 2013 14:15:20 UTC
805   ci 15276057       2    Monday, January 21, 2013 14:02:17 UTC
806   ak 10642305       3    Monday, January 21, 2013 13:57:35 UTC
807   ci 15276033       3    Monday, January 21, 2013 13:48:33 UTC
808   ci 15276025       2    Monday, January 21, 2013 13:42:32 UTC
809   ak 10642300       2    Monday, January 21, 2013 13:40:20 UTC
810   ak 10644270       2    Monday, January 21, 2013 13:32:57 UTC
811   ak 10642296       2    Monday, January 21, 2013 13:26:46 UTC
812   ak 10644268       2    Monday, January 21, 2013 13:19:40 UTC
813   ak 10644267       2    Monday, January 21, 2013 13:07:02 UTC
814   ak 10644266       2    Monday, January 21, 2013 13:02:47 UTC
815   ak 10644265       2    Monday, January 21, 2013 12:57:36 UTC
816   ak 10644264       2    Monday, January 21, 2013 12:56:26 UTC
817   ak 10642290       2    Monday, January 21, 2013 12:41:09 UTC
818   ak 10642287       3    Monday, January 21, 2013 12:33:19 UTC
819   ak 10642284       3    Monday, January 21, 2013 12:13:15 UTC
820   pr 13021005       0    Monday, January 21, 2013 12:10:42 UTC
821   nc 71926066       2    Monday, January 21, 2013 12:10:18 UTC
822   ak 10642276       2    Monday, January 21, 2013 12:01:09 UTC
823   ak 10644259       2    Monday, January 21, 2013 11:54:48 UTC
824   ak 10642273       2    Monday, January 21, 2013 11:52:22 UTC
825   ak 10642272       2    Monday, January 21, 2013 11:48:00 UTC
826   ak 10642266       2    Monday, January 21, 2013 11:44:34 UTC
827   ak 10642261       3    Monday, January 21, 2013 11:42:34 UTC
828   nc 71926051       0    Monday, January 21, 2013 11:39:33 UTC
829   nc 71926046       2    Monday, January 21, 2013 11:33:17 UTC
830   us b000es47       9    Monday, January 21, 2013 11:32:19 UTC
831   nc 71926036       0    Monday, January 21, 2013 11:30:26 UTC
832   ci 15275977       0    Monday, January 21, 2013 11:19:06 UTC
833   uu 60010932       4    Monday, January 21, 2013 11:07:20 UTC
834   ak 10642248       2    Monday, January 21, 2013 11:00:00 UTC
835   ak 10644252       2    Monday, January 21, 2013 11:00:00 UTC
836   uw 60495892       2    Monday, January 21, 2013 10:50:12 UTC
837   ci 15275961       2    Monday, January 21, 2013 10:47:58 UTC
838   ak 10642245       2    Monday, January 21, 2013 10:47:11 UTC
839   nc 71926016       4    Monday, January 21, 2013 10:42:54 UTC
840   us b000es3t       5    Monday, January 21, 2013 10:38:59 UTC
841   nc 71926001       1    Monday, January 21, 2013 10:07:05 UTC
842   pr 13021004       0    Monday, January 21, 2013 09:31:02 UTC
843   pr 13021006       0    Monday, January 21, 2013 09:14:12 UTC
844   ak 10642238       2    Monday, January 21, 2013 08:56:36 UTC
845   ak 10642236       2    Monday, January 21, 2013 08:45:46 UTC
846   uu 60010927       2    Monday, January 21, 2013 08:43:20 UTC
847   ak 10642226       2    Monday, January 21, 2013 08:33:33 UTC
848   nc 71925966       1    Monday, January 21, 2013 08:33:16 UTC
849   nc 71925961       6    Monday, January 21, 2013 08:28:29 UTC
850   nc 71925946       2    Monday, January 21, 2013 08:19:35 UTC
851   nn 00400281       9    Monday, January 21, 2013 08:18:56 UTC
852   pr 13021003       0    Monday, January 21, 2013 08:00:06 UTC
853   ak 10642217       3    Monday, January 21, 2013 07:54:50 UTC
854   nc 71925901       2    Monday, January 21, 2013 07:48:04 UTC
855   ak 10642216       3    Monday, January 21, 2013 07:35:59 UTC
856   uw 60495872       2    Monday, January 21, 2013 07:15:53 UTC
857   ak 10644245       2    Monday, January 21, 2013 07:15:30 UTC
858   ak 10642210       2    Monday, January 21, 2013 07:13:03 UTC
859   ak 10642207       2    Monday, January 21, 2013 07:06:16 UTC
860   ci 15275953       0    Monday, January 21, 2013 06:57:28 UTC
861   ak 10642193       2    Monday, January 21, 2013 06:46:43 UTC
862   nc 71925866       2    Monday, January 21, 2013 06:37:15 UTC
863   uu 60010922       4    Monday, January 21, 2013 06:35:18 UTC
864   ak 10642184       2    Monday, January 21, 2013 06:35:12 UTC
865   uu 60010917       5    Monday, January 21, 2013 06:33:57 UTC
866   ci 15275945       2    Monday, January 21, 2013 06:28:26 UTC
867   ci 15275937       2    Monday, January 21, 2013 06:27:33 UTC
868   nc 71925861       0    Monday, January 21, 2013 06:27:19 UTC
869   ak 10642170       2    Monday, January 21, 2013 06:17:06 UTC
870   nc 71925851       0    Monday, January 21, 2013 06:12:27 UTC
871   ak 10642168       2    Monday, January 21, 2013 06:07:47 UTC
872   nc 71925841       1    Monday, January 21, 2013 06:06:24 UTC
873   ak 10644237       2    Monday, January 21, 2013 06:01:44 UTC
874   ak 10644236       2    Monday, January 21, 2013 06:00:33 UTC
875   ak 10644235       2    Monday, January 21, 2013 05:53:08 UTC
876   nc 71925826       1    Monday, January 21, 2013 05:48:41 UTC
877   ak 10644234       2    Monday, January 21, 2013 05:41:47 UTC
878   ci 15275921       0    Monday, January 21, 2013 05:30:00 UTC
879   ak 10642155       2    Monday, January 21, 2013 05:14:03 UTC
880   ak 10642151       2    Monday, January 21, 2013 05:07:47 UTC
881   pr 13021001       0    Monday, January 21, 2013 04:56:49 UTC
882   nc 71925801       0    Monday, January 21, 2013 04:42:41 UTC
883   ci 15275897       2    Monday, January 21, 2013 04:38:10 UTC
884   nc 71925796       1    Monday, January 21, 2013 04:29:36 UTC
885   ci 15275889       2    Monday, January 21, 2013 04:28:43 UTC
886   ci 15275881       2    Monday, January 21, 2013 04:28:12 UTC
887   pr 13021000       0    Monday, January 21, 2013 04:25:39 UTC
888   ak 10642136       2    Monday, January 21, 2013 04:19:26 UTC
889   pr 13021002       0    Monday, January 21, 2013 04:07:03 UTC
890   ak 10644230       2    Monday, January 21, 2013 03:45:09 UTC
891   uu 60010912       4    Monday, January 21, 2013 03:38:55 UTC
892   ak 10642131       2    Monday, January 21, 2013 03:25:27 UTC
893   ci 15275849       3    Monday, January 21, 2013 03:21:28 UTC
894   ak 10642128       3    Monday, January 21, 2013 03:19:43 UTC
895   us b000es0s       4    Monday, January 21, 2013 03:16:49 UTC
896   mb 13014957       2    Monday, January 21, 2013 03:15:53 UTC
897   ak 10642121       2    Monday, January 21, 2013 02:56:11 UTC
898   ak 10642119       2    Monday, January 21, 2013 02:49:45 UTC
899   nc 71925781       3    Monday, January 21, 2013 02:36:31 UTC
900   ak 10644225       2    Monday, January 21, 2013 02:34:44 UTC
901   mb 13488805       2    Monday, January 21, 2013 02:23:29 UTC
902   uu 60010902       4    Monday, January 21, 2013 01:55:20 UTC
903   ak 10642106       2    Monday, January 21, 2013 01:45:45 UTC
904   ak 10644223       2    Monday, January 21, 2013 01:39:41 UTC
905   nc 71925776       0    Monday, January 21, 2013 01:27:51 UTC
906   ci 15275793       3    Monday, January 21, 2013 01:25:57 UTC
907   nc 71925751       2    Monday, January 21, 2013 01:05:31 UTC
908   nc 71925756       2    Monday, January 21, 2013 01:03:41 UTC
909   ak 10642096       2    Monday, January 21, 2013 00:59:47 UTC
910   ak 10642017       3    Monday, January 21, 2013 00:41:49 UTC
911   ak 10641937       2    Monday, January 21, 2013 00:38:06 UTC
912   nc 71925741       4    Monday, January 21, 2013 00:28:37 UTC
913   ak 10644218       2    Monday, January 21, 2013 00:21:32 UTC
914   ak 10641931       3    Monday, January 21, 2013 00:11:33 UTC
915   uu 60010887       4    Monday, January 21, 2013 00:09:25 UTC
916   nc 71925731       3    Monday, January 21, 2013 00:08:21 UTC
917   ci 15275777       2    Monday, January 21, 2013 00:06:37 UTC
918   uu 60010882       2    Sunday, January 20, 2013 23:58:16 UTC
919   uu 60010877       2    Sunday, January 20, 2013 23:53:15 UTC
920   uu 60000715       2    Sunday, January 20, 2013 23:49:46 UTC
921   uu 60010872       2    Sunday, January 20, 2013 23:48:58 UTC
922   uu 60010867       2    Sunday, January 20, 2013 23:47:34 UTC
923   uw 60495802       2    Sunday, January 20, 2013 23:36:42 UTC
924   uu 60010857       4    Sunday, January 20, 2013 23:36:30 UTC
925   us b000eryt       5    Sunday, January 20, 2013 23:32:22 UTC
926   ak 10642588       2    Sunday, January 20, 2013 23:26:58 UTC
927   ak 10641923       2    Sunday, January 20, 2013 23:26:52 UTC
928   ci 15275761       3    Sunday, January 20, 2013 23:08:52 UTC
929   uu 60010847       4    Sunday, January 20, 2013 22:56:32 UTC
930   ak 10642585       2    Sunday, January 20, 2013 22:40:27 UTC
931   ak 10641901       3    Sunday, January 20, 2013 22:29:38 UTC
932   us b000erxb       8    Sunday, January 20, 2013 22:14:09 UTC
933   ak 10642581       2    Sunday, January 20, 2013 22:08:22 UTC
934   ak 10641878       3    Sunday, January 20, 2013 22:03:04 UTC
935   pr 13020007       0    Sunday, January 20, 2013 22:02:50 UTC
936   uu 60010842       2    Sunday, January 20, 2013 22:00:53 UTC
937   ak 10641871       3    Sunday, January 20, 2013 21:56:58 UTC
938   us b000erwy       8    Sunday, January 20, 2013 21:40:31 UTC
939   ak 10642578       2    Sunday, January 20, 2013 21:28:33 UTC
940   us b000erwt       6    Sunday, January 20, 2013 21:26:28 UTC
941   us b000erwu       5    Sunday, January 20, 2013 21:25:06 UTC
942   ci 15275753       2    Sunday, January 20, 2013 21:19:29 UTC
943   ci 15275745       2    Sunday, January 20, 2013 21:11:59 UTC
944   ak 10642576       2    Sunday, January 20, 2013 21:09:30 UTC
945   us b000erwj       7    Sunday, January 20, 2013 21:05:22 UTC
946   nn 00400245       9    Sunday, January 20, 2013 20:56:35 UTC
947   nc 71925641       1    Sunday, January 20, 2013 20:53:08 UTC
948   nn 00400244       9    Sunday, January 20, 2013 20:52:04 UTC
949   pr 13020006       0    Sunday, January 20, 2013 20:27:12 UTC
950   hv 60455161       1    Sunday, January 20, 2013 20:22:17 UTC
951   ci 15275729       0    Sunday, January 20, 2013 20:21:20 UTC
952   nn 00400241       9    Sunday, January 20, 2013 20:20:57 UTC
953   ci 15275721       2    Sunday, January 20, 2013 20:19:31 UTC
954   nc 71925621       2    Sunday, January 20, 2013 20:13:46 UTC
955   pr 13020005       0    Sunday, January 20, 2013 20:09:34 UTC
956   ci 15275713       2    Sunday, January 20, 2013 20:08:07 UTC
957   ci 15275697       0    Sunday, January 20, 2013 19:54:05 UTC
958   uu 60010817       2    Sunday, January 20, 2013 19:52:21 UTC
959   ak 10642575       2    Sunday, January 20, 2013 19:42:35 UTC
960   uu 60010812       2    Sunday, January 20, 2013 19:33:28 UTC
961   ak 10642574       2    Sunday, January 20, 2013 19:32:59 UTC
962   nn 00400236       9    Sunday, January 20, 2013 19:24:21 UTC
963   ak 10641839       2    Sunday, January 20, 2013 19:21:07 UTC
964   uu 60010802       4    Sunday, January 20, 2013 19:10:50 UTC
965   us b000ervr       7    Sunday, January 20, 2013 19:10:11 UTC
966   us b000ervq       6    Sunday, January 20, 2013 19:09:45 UTC
967   nc 71925591       1    Sunday, January 20, 2013 19:04:25 UTC
968   nc 71925576       1    Sunday, January 20, 2013 18:28:20 UTC
969   us b000es4x       4    Sunday, January 20, 2013 18:26:32 UTC
970   nn 00400224       9    Sunday, January 20, 2013 18:14:31 UTC
971   ak 10642572       2    Sunday, January 20, 2013 18:11:55 UTC
972   ci 15275665       2    Sunday, January 20, 2013 18:05:00 UTC
973   nn 00400221       9    Sunday, January 20, 2013 18:04:27 UTC
974   nc 71925566       0    Sunday, January 20, 2013 18:02:27 UTC
975   hv 60455001       2    Sunday, January 20, 2013 17:59:39 UTC
976   ak 10641815       2    Sunday, January 20, 2013 17:58:55 UTC
977   ci 15275657       0    Sunday, January 20, 2013 17:55:44 UTC
978   nn 00400220       9    Sunday, January 20, 2013 17:55:42 UTC
979   nc 71925541       0    Sunday, January 20, 2013 17:48:14 UTC
980   nc 71925526       1    Sunday, January 20, 2013 17:43:12 UTC
981   nn 00400213       9    Sunday, January 20, 2013 17:33:00 UTC
982   nn 00400210       9    Sunday, January 20, 2013 17:18:32 UTC
983   nc 71925516       0    Sunday, January 20, 2013 17:16:04 UTC
984   ci 15275641       2    Sunday, January 20, 2013 17:15:41 UTC
985   ci 15275633       5    Sunday, January 20, 2013 17:13:54 UTC
986   us b000ertx       5    Sunday, January 20, 2013 17:12:32 UTC
987   nn 00400209       9    Sunday, January 20, 2013 16:49:33 UTC
988   ci 15275625       2    Sunday, January 20, 2013 16:48:06 UTC
989   nc 71925471       3    Sunday, January 20, 2013 16:20:28 UTC
990   nn 00400205       9    Sunday, January 20, 2013 16:01:48 UTC
991   ak 10642570       2    Sunday, January 20, 2013 15:35:39 UTC
992   nn 00400200       9    Sunday, January 20, 2013 15:00:39 UTC
993   ci 15275609       0    Sunday, January 20, 2013 15:00:38 UTC
994   nn 00400199       9    Sunday, January 20, 2013 14:57:17 UTC
995   nn 00400198       9    Sunday, January 20, 2013 14:54:57 UTC
996   nc 71925436       2    Sunday, January 20, 2013 14:45:40 UTC
997   ci 15275601       2    Sunday, January 20, 2013 14:37:27 UTC
998   ak 10641761       2    Sunday, January 20, 2013 14:37:24 UTC
999   ak 10641759       2    Sunday, January 20, 2013 14:28:14 UTC
1000  nn 00400191       9    Sunday, January 20, 2013 13:54:58 UTC
          Lat     Lon Magnitude Depth NST
1     38.8292 -122.81       1.4   1.0  27
2     36.0403 -117.35       1.6   3.7  22
3     65.2271 -149.51       1.3   9.8   7
4     39.5573 -121.99       1.9   1.3   8
5     37.2587 -114.07       1.9   7.2  19
6     62.1046 -150.70       1.7  73.2  13
7     19.4065 -155.26       2.3  14.5  52
8     63.5132 -150.83       1.6   0.0  11
9     32.9112 -116.25       1.3   6.5  34
10    -5.1704  102.94       5.0  58.1  75
11    35.5633 -118.53       1.7   0.2  18
12    19.2960 -155.38       1.7   4.1   8
13    19.9262 -155.54       3.1  22.0  43
14    62.1638 -149.58       1.6  42.9  12
15    63.2917 -149.24       2.1   0.0  28
16    34.2925 -106.71       2.9   5.0  25
17    33.6293 -116.69       1.5  16.6  60
18    32.9282 -116.37       1.5   5.5  12
19    37.5777 -122.51       1.2   8.4  11
20    33.0542 -116.44       1.0   7.0  26
21    36.8237 -121.55       2.8   5.4  58
22    38.7873 -122.76       1.5   1.2  23
23   -44.6350   37.43       4.8  15.2  21
24    19.3460 -155.09       2.5   6.9  35
25    18.0025  -65.62       2.4  18.0   5
26    -9.5294  121.89       4.9  59.5  55
27    36.2972 -120.87       1.0   5.5   8
28    60.1621 -150.54       2.6  35.1  12
29    61.6813 -151.51       2.2  74.6  23
30    63.2819 -152.34       1.3   9.4   4
31    38.1572 -118.04       1.7   7.6  12
32    32.9265 -116.30       1.8   5.1  75
33    40.8640 -118.56       1.8   4.5   5
34    33.8917 -117.55       1.4  10.7  11
35    38.0600 -118.94       2.0   8.5  27
36    38.7878 -122.76       1.0   1.6  16
37    38.1545 -118.02       1.5   3.4  23
38    51.6242 -175.91       1.1  42.3   9
39    51.5409 -177.78       1.4  47.9  11
40    33.1673 -116.43       1.5  14.3  58
41    33.0172 -116.44       1.3  11.0  37
42    34.2008 -117.39       1.3  12.2  33
43    34.3328 -116.89       1.4   1.0  20
44    38.7970 -122.78       1.9   3.9  36
45    40.1442 -123.84       1.7  22.1   5
46    37.1773 -122.34       2.7  10.3  56
47    33.0387 -116.44       1.7   9.1  84
48    36.2718 -120.84       1.9   6.9   6
49    36.2697 -120.84       3.4   7.6  75
50    36.7472 -121.41       1.6   8.3  17
51     5.4858  127.05       5.0 119.7  63
52    36.2708 -120.84       2.2   7.1  31
53    38.7952 -122.81       1.3   3.1  28
54    64.3717 -130.81       3.8  10.0  38
55    38.9462 -118.70       1.4  14.1  11
56    39.7489   77.30       4.8  35.3  34
57    38.8378 -122.85       1.4   1.3  21
58    38.2948   46.81       4.8  18.4  35
59    47.8815 -121.65       1.7   8.8  31
60    38.5208 -119.40       1.4   1.1   9
61    38.5146 -119.42       1.2   4.0   8
62    62.3487 -149.04       1.8  13.5   9
63    34.2225 -117.48       1.5  23.6  16
64    33.3773 -116.84       1.1   9.5  51
65    35.4860 -118.29       1.6   8.2  25
66    36.0778 -117.88       2.3   0.4  24
67    32.5807 -115.70       1.6   8.9  25
68    62.0858 -145.19       1.9   9.1  11
69    39.8178 -123.63       3.5   7.3  25
70    34.0417 -117.25       1.3  19.9  68
71    38.8168 -122.82       2.0   2.7  35
72    38.8205 -122.76       1.0   2.4  18
73    35.5567 -120.83       1.4   6.9  18
74    63.2206 -147.11       1.7   1.0   9
75    59.4485 -153.58       3.1 131.4  50
76    38.8050 -122.80       2.0   3.0  37
77    32.6072 -115.69       1.4  11.8  21
78    63.3318 -144.70       1.4  13.8   6
79    60.3764 -152.20       2.4 117.7  17
80    34.8777 -120.32       1.8   0.7  13
81    -6.1335  149.81       4.9  41.3  65
82    32.4860 -115.58       1.5   9.6  15
83    34.1245 -117.41       1.2   5.8  54
84    63.3213 -145.22       1.6   0.0   8
85    19.3815 -155.24       1.8   2.1  11
86    19.3770 -155.24       1.7   2.5  16
87    19.3768 -155.24       1.8   3.2  10
88    19.3783 -155.24       2.1   2.2  14
89    19.3818 -155.24       2.9   0.1  25
90    19.3780 -155.24       2.1   2.7  36
91    48.2052 -121.76       1.8   9.6  27
92    63.9433 -149.08       1.5   0.0   9
93    60.0108 -152.73       2.6  95.0  30
94    38.1486 -118.05       1.4  10.0  12
95    13.1058  -89.22       4.5  76.5  60
96    35.2596  -92.33       2.0   6.9  15
97    38.8077 -122.78       1.2   2.2  21
98    19.3872 -155.28       2.4   3.1  25
99    65.9677 -150.32       1.6   0.0   8
100   63.5410 -147.30       1.8   0.2  18
101   61.6783 -149.64       2.0  39.2  24
102   60.4754 -141.24       1.8  19.9  10
103   33.7777 -116.16       1.3   6.3  60
104   32.6210 -115.72       2.0   8.1  39
105   38.8375 -122.85       1.7   1.5  26
106   33.0210 -116.53       1.2  16.3  26
107   33.3815 -116.79       1.0   6.8  30
108   38.5484 -119.63       1.0   8.5   7
109   61.6291 -151.56       3.4  76.5  75
110   34.5712   24.10       4.3  10.0  71
111   19.2875 -155.44       1.8   0.0  15
112   18.9839  -66.20       3.2 123.0   5
113   19.6533 -155.66       1.9  15.2  30
114   63.3845 -151.14       2.7   1.3  28
115   33.7785 -116.16       1.1   6.3  50
116   37.5202 -118.66       1.4  13.8  10
117   37.5593 -121.83       1.4   8.3  13
118   37.3528 -121.72       2.2   6.4  50
119   40.5313 -122.25       2.9  30.6  20
120   63.3364 -145.21       1.5   0.0  10
121   60.2413 -152.20       1.4  51.2  10
122   63.3625 -145.32       3.2   0.3  37
123   33.5707 -116.65       1.2  11.5  26
124   38.8145 -122.82       1.1   2.6  15
125   37.8828 -122.23       1.8   7.9  41
126   33.7778 -116.16       1.4   6.1  62
127   40.0897 -119.66       1.0  12.7  11
128   65.0142 -147.34       1.6  12.4   8
129   51.1302  179.35       2.9  11.1   9
130   38.8372 -122.85       1.4   1.4  25
131  -23.6541   43.55       5.3  14.0 217
132   38.0557 -118.95       1.3   0.1  22
133   38.8353 -122.78       1.2   2.3  19
134    9.4380  126.10       4.7  83.7  51
135   58.2593 -155.12       1.5   1.9   5
136   36.0785 -120.64       1.1   2.2  20
137   33.7757 -116.16       2.0   4.5  98
138   49.4560 -120.50       2.4   0.0  12
139   63.2658 -151.34       1.3  16.1   4
140   37.3210 -122.11       1.5   0.0   8
141   38.5743 -119.61       1.0   5.2   9
142   62.8756 -148.13       1.0  56.7   5
143   63.5667 -150.79       1.8   4.8   9
144   47.4443 -116.01       1.9   2.0  21
145   38.7558 -122.74       1.0   3.8   7
146   38.4261   73.36       4.2 118.5  22
147   40.2987 -124.87       2.3   0.2  13
148   60.6546 -150.92       1.9  15.7  10
149   19.4892  -65.50       3.3  87.0  10
150   61.9375 -148.29       2.0  23.5  15
151   38.8350 -122.77       1.7   2.7  30
152  -24.1408  -65.31       5.1  41.9 154
153   49.7278  155.69       4.9  62.7 222
154   36.5573 -121.07       1.0   7.2  12
155   43.3369   18.77       4.2  11.0  56
156   36.0028 -120.56       2.0   4.4  76
157   47.1993 -121.89       1.5   8.1  33
158   34.6292 -117.30       1.2   0.0  22
159   34.6760 -116.35       1.8   3.7  45
160   29.3787  132.20       4.8   9.7 105
161   38.2393 -122.06       2.9   8.3 151
162   61.5897 -150.36       1.9  48.9  18
163   38.8185 -122.82       1.2   2.8  24
164   34.6292 -117.30       1.2   2.9  27
165   32.9878 -116.22       1.7   9.2  80
166   38.8175 -122.82       1.6   2.8  32
167   36.0012 -120.56       2.8   5.0  91
168   62.1888 -151.16       1.8  84.3  17
169   62.1963 -149.46       1.7   9.6  11
170   37.4665 -112.28       2.3  17.0  17
171   38.1580 -118.04       1.5   0.0  18
172   38.1510 -118.03       1.9   5.7  15
173   37.4752 -118.84       1.5   6.0  38
174   38.1571 -118.03       1.4   0.0  10
175   44.2804   10.53       5.0   4.8  65
176   36.2408 -120.79       1.2   6.5  19
177   60.1313 -153.12       3.6 138.2  96
178   47.7295 -113.69       1.3   9.8  15
179   38.8248 -122.79       1.1   3.3  25
180   37.4637 -112.28       1.2  13.9   9
181   37.4687 -112.28       1.7  15.9  16
182   37.4712 -112.29       1.5  15.2  17
183   38.8128 -122.78       1.2   1.7  20
184   55.9029 -135.30       3.5  10.0  19
185   61.3620 -146.65       2.5  19.7  32
186   47.8385 -122.29       1.6  26.8  29
187   38.7792 -122.75       1.1   2.0  20
188   60.7766 -145.73       1.8  57.1   4
189   20.3130 -155.57       2.3  37.2  43
190   37.5377 -117.60       1.3  10.0  11
191   53.9156 -164.96       2.1  34.2  12
192   37.4817 -118.39       1.8   9.6  26
193   31.7629   50.95       5.1  10.0 138
194   63.3898 -151.78       1.8   6.6  11
195   36.4688 -120.95       2.6  10.2  76
196   44.4458 -110.99       1.5   4.5   8
197   62.0429 -145.13       1.7  17.9   6
198   19.4585 -155.87       1.8  16.5  10
199   37.4705 -118.84       1.1   6.6  33
200   64.5271 -149.31       1.0  12.8   4
201   36.6292 -121.04       1.1  21.4   9
202   38.3165 -122.39       2.0  10.2  23
203   61.4820 -151.88       1.9   3.1  19
204   38.7667 -122.71       1.0   1.8  10
205   48.4293 -122.55       3.4  22.5  89
206   40.2797 -121.06       1.6   5.3  16
207   44.4655 -124.61       2.9  40.0  20
208   37.4715 -118.84       1.0   6.3  24
209   63.3945 -150.11       1.8   0.7  16
210   38.5542 -119.63       1.5   5.4   8
211   52.5805 -169.61       3.1   9.6  15
212   19.5454  -64.58       3.2  83.0   5
213   38.7677 -122.74       1.1   2.0   9
214   31.9131  -94.43       4.1   5.0  35
215   42.0903 -112.46       1.4   8.3  20
216   63.2671 -151.23       1.4  16.7   6
217   18.2259  -66.97       1.9  28.0   3
218   40.3787 -124.55       2.2  24.7  22
219   38.5443 -119.62       1.4  11.1  11
220   60.8392 -151.43       1.6  26.0  17
221   32.7865 -116.64       1.7  17.8  72
222   37.7387 -113.05       1.2   2.7  10
223   63.9972 -149.15       1.5 154.5   9
224   37.0762 -121.49       1.2   8.4  15
225   18.1459  -64.72       2.7 127.0   8
226   33.9553 -116.86       1.4   6.5  72
227   61.1097 -146.99       1.7  17.3   5
228   33.9568 -116.86       1.2   7.6  55
229   61.7877 -149.56       1.5  38.5  13
230   38.5534 -119.62       1.4  10.3  14
231   33.3935 -116.38       1.3   6.9  55
232   33.6745 -116.74       1.0  17.9  56
233   62.8620 -150.85       1.4  70.3   5
234  -55.8834  -28.14       4.7 114.4  22
235   38.5576 -119.62       1.6  11.2  12
236   38.5553 -119.62       1.7   8.6  10
237   58.2978 -151.20       3.1  35.0  38
238   37.8827 -122.23       2.0   8.3 122
239    4.9979   95.96       4.5   7.0  40
240   38.8248 -122.83       1.9   2.9  64
241   38.7907 -122.74       1.8   2.0  27
242   18.1415  -64.06       2.8  23.0  10
243   57.3086 -154.87       2.5  45.6  15
244   38.1496 -118.03       1.9   6.8  13
245   44.4572 -124.69       2.8  35.3  19
246   40.0930 -123.75       1.4  22.7  17
247   38.5465 -119.63       2.0   5.7   9
248   44.4613 -124.66       3.4  36.7  15
249   38.8085 -122.83       1.1   0.0   9
250   38.1532 -118.03       1.2   6.2   9
251   62.9976 -149.59       2.3  74.1  34
252   19.4073 -155.28       1.9   0.5  15
253   61.3014 -150.83       1.7   0.0  16
254   38.8248 -122.82       1.0   2.7  20
255   34.3052 -118.72       1.5  10.6  22
256   40.0942 -123.75       1.7  22.1  29
257   38.5473 -119.62       2.1   7.5  14
258   38.5535 -119.62       2.0   9.1  12
259   38.5475 -119.62       1.2  10.3  12
260   38.8267 -122.86       2.0   2.9  61
261   40.4820 -124.63       2.2  20.5  22
262   38.5566 -119.62       1.4   8.7   9
263   65.0080 -147.32       1.5   3.1   8
264   44.4572 -124.67       3.0  33.8  12
265   61.2225 -150.78       1.5  54.9  11
266   40.3362 -118.31       1.7   0.0   6
267   38.1511 -118.00       2.3   9.7  14
268   38.1545 -118.02       2.3   6.8  15
269   38.5630 -119.62       1.2   4.9   9
270   63.9610 -148.83       1.8   0.7  18
271   38.5490 -119.62       1.7  10.5   6
272   39.6030 -122.03       1.3  22.4  12
273   19.4367 -155.44       2.0   6.9   8
274   38.5492 -119.61       1.7  10.7   8
275   38.5630 -119.63       1.5   4.8  13
276   38.5497 -119.64       1.9   0.8   8
277   62.1994 -148.71       1.5  33.2  13
278   38.5598 -119.62       4.0   6.7  31
279   38.8263 -122.86       1.1   1.7  13
280   33.0758 -115.00       2.0   0.0   6
281   37.2583 -121.62       1.0   4.2   9
282   61.2295 -150.84       2.0  49.1  17
283   33.1787 -116.02       2.0   7.6  89
284   38.1510 -118.02       2.5   6.1  16
285   38.8237 -122.75       1.0   1.6  14
286   36.5673 -121.12       1.2   3.8  10
287   38.1566 -118.03       1.5   8.2  13
288   38.8283 -122.85       1.1   2.2  16
289   61.2468 -149.64       3.2  27.6  58
290   53.1450 -166.64       2.6  13.9  12
291   38.1543 -118.01       1.3   6.3  10
292   32.5852 -115.71       1.5   7.2  16
293   34.8400 -118.98       2.5  16.1  68
294   45.0193 -122.59       1.6  18.7  18
295   38.5503 -119.63       1.4  10.0  16
296   36.8223 -121.55       2.8   5.6  64
297   33.8473 -117.49       1.2   0.0  25
298   38.7887 -122.76       1.6   1.5  24
299   44.4717 -110.70       1.3   2.5  12
300   62.6357 -151.28       1.6  23.2   8
301   33.2785 -116.78       1.3  12.7  61
302   38.8078 -122.79       1.1   0.9  24
303   38.8043 -122.81       1.0   2.0  12
304   63.5295 -147.42       1.5   0.2   7
305   38.8270 -122.85       1.0   2.5  22
306   64.8549 -149.57       2.3  21.1  16
307   44.6823 -125.60       2.1  28.3  20
308   34.6323 -117.13       1.1   0.0  11
309   38.8243 -122.79       1.1   2.2  21
310   33.8448 -117.50       1.2   0.0   6
311   38.0633 -118.94       1.7  11.3  26
312   32.5340 -115.63       2.3  12.4  26
313   18.8404  -65.22       2.9  52.0   7
314   37.1925 -117.54       1.7  14.4   8
315   33.2992 -116.25       1.2  10.2  43
316   59.9080 -152.71       1.9  80.6  19
317   38.7732 -122.92       1.0   2.7   5
318   51.5027 -178.74       2.4  34.1  16
319   19.6476  -65.24       2.7  53.0   3
320   36.0842 -117.84       1.7   2.7  33
321   38.1574 -118.07       1.5   4.0  13
322   32.9657 -116.25       2.2  12.3  96
323   19.3332 -155.05       1.8   4.2  32
324   35.9778 -120.55       1.2   3.5  27
325   53.5639  142.75       4.9   9.0  49
326   39.3790 -120.45       1.3  11.4   9
327   61.9769 -150.34       1.8  29.8   7
328   19.1537  -64.02       3.0  91.0   5
329   39.3740 -120.45       2.4   9.6  31
330   40.5212 -124.52       2.9   0.7  11
331   51.3091 -178.22       2.7  25.7  17
332   48.5097 -122.67       1.0  22.9  14
333   38.5760 -119.60       1.8   3.9   6
334   61.0910 -150.41       2.0  34.9  23
335   38.5802 -119.59       1.5   8.0  16
336   19.5214  -64.36       3.0  77.0   6
337   38.1587 -118.01       1.6   4.0  26
338   34.2918 -116.91       1.3   8.3  60
339   63.5595 -147.31       1.7   2.7  18
340   36.5927 -121.15       2.3  11.7  63
341   36.5958 -121.15       1.6  11.5  39
342   62.7692 -150.48       1.1  66.4  14
343   38.5611 -119.62       1.5   2.0  16
344   38.5611 -119.62       1.2   8.0   9
345   40.4415 -125.64       4.0  17.9  55
346   38.8427 -122.83       1.3   2.4  26
347   63.2587 -151.30       1.9   2.0  12
348   38.6078   73.49       4.5 113.5  37
349   40.2857 -124.45       2.4  20.3  19
350   38.5560 -119.61       2.1   9.8  13
351   38.1542 -117.97       2.0   0.8  30
352   38.2138 -118.05       1.2  16.0   5
353   47.4545 -122.70       1.9  24.2  52
354   60.7503 -151.64       1.9  48.2  16
355   38.5611 -119.62       1.4  12.0   9
356   -4.2135  122.84       5.0 642.5  90
357   38.5548 -119.62       2.3   8.8  15
358   38.5802 -119.59       1.2   8.0  12
359   27.7707   56.41       4.2  10.0  28
360   38.5802 -119.59       1.1   0.0  13
361   38.5494 -119.62       1.4  10.1  12
362   38.5553 -119.62       1.7   8.8   8
363   38.5475 -119.62       1.6  10.5  10
364   62.3818 -148.39       1.7  50.4   5
365   53.5668 -166.81       2.1  64.9   9
366   38.5645 -119.61       1.2   8.5  10
367   38.5417 -119.66       1.1  16.0   5
368   38.7868 -122.75       1.2   3.6  19
369   38.8160 -122.82       1.1   2.8  22
370   38.5565 -119.62       1.0  11.3  14
371   38.5542 -119.59       1.8   1.2  11
372   38.5523 -119.62       2.6   7.8  26
373   38.5683 -119.62       2.8   1.5  14
374   38.5500 -119.62       1.3   8.1  11
375   38.5590 -119.62       3.7   6.0  38
376   34.0875 -117.30       1.5  15.7  79
377   38.8170 -122.82       1.4   2.6  21
378   35.9268 -117.70       1.3   2.7  34
379   36.6590 -116.34       1.1   4.0  19
380   38.7710 -122.72       1.3   2.2  17
381   37.1810 -117.34       1.0   6.0  10
382   38.8113 -122.80       1.8   1.5  30
383   36.0752 -120.65       1.0   1.7  30
384   35.6470 -121.00       1.3   9.4  24
385   49.8255   87.60       5.3  41.8 320
386   62.5670 -151.19       1.6   4.0   6
387   33.1358 -116.45       1.4  14.6  61
388    9.9707  -84.45       4.9  62.8 279
389   38.8107 -122.79       1.9   1.4  60
390   65.1882 -146.12       2.0  10.1  12
391   36.6530 -121.28       1.1   7.5   8
392   38.8108 -122.80       1.4   1.4  22
393   38.8118 -122.79       1.7   1.4  28
394   36.5612 -121.15       2.0   3.4  51
395   50.9494 -179.78       2.4  26.1  12
396   37.6987 -119.43       1.7   0.4  21
397   37.6047 -119.10       1.4  10.1  30
398   34.1578 -116.41       1.1   9.1  45
399   62.8605 -149.54       1.4  62.5  12
400   59.8096 -153.08       2.6 111.6  46
401   33.6763 -116.73       1.1  18.8  74
402   40.7610 -124.52       2.6  21.5  28
403   37.7260 -122.00       1.7  16.4  29
404   38.8215 -122.76       1.1   2.4  19
405   39.5588 -111.27       1.1   1.9  17
406   47.0395 -122.09       1.4   0.0   6
407   38.7518 -122.73       1.4   1.1  15
408   27.8766   56.56       4.6   9.9  50
409   38.3238 -108.99       3.9   1.2  27
410   38.1572 -117.97       2.9   4.2  40
411   37.7448 -122.58       1.0   8.2  15
412   51.4873 -175.98       2.4  21.9  16
413   38.9972 -111.35       1.5   2.9   8
414   58.4611 -150.51       3.0   0.1  25
415   63.0961 -150.41       1.5 106.4  18
416   38.4501 -119.31       1.0   7.0   6
417   38.1516 -118.00       1.8  12.7  13
418   61.5453 -146.43       1.9  19.8   7
419   38.1531 -118.00       1.3   7.5   8
420   19.6485  -64.30       3.0  61.0   4
421  -16.6170  177.71       5.1  34.1 120
422   63.9640 -148.77       1.7   0.0  15
423   62.8988 -149.46       1.2  61.8   7
424   35.9265 -117.70       1.0   2.8  31
425   38.8237 -122.80       1.4   0.0  14
426   38.8220 -122.80       1.6   0.0  21
427   38.8197 -122.80       1.1   0.5  14
428   19.5900  -64.44       3.1  37.0   9
429   65.0031 -147.32       1.3   6.5   7
430   61.0692 -152.73       1.2  22.8   7
431   44.3712 -121.04       1.9   0.0   7
432   46.2150 -122.88       1.8   0.0  14
433   38.1365 -118.04       1.4   7.0  16
434   38.8305 -122.81       1.0   2.4  25
435   36.7977 -121.27       1.5   8.2  19
436   38.8438 -122.83       1.6   2.5  25
437   58.6301 -155.17       3.0 198.5  16
438   47.4483 -115.99       1.5   2.0  18
439   32.9208 -117.50       3.1  15.5  82
440   61.6223 -150.48       2.0  41.3  20
441   38.8060 -122.79       1.0   2.0  10
442   49.4102 -120.49       2.4   0.0  14
443   50.2981 -175.81       2.8  32.8  14
444   19.3104  -64.24       2.9  85.0   6
445   38.8097 -122.83       1.0   2.6  10
446   32.6028 -116.97       1.7   3.4  37
447   43.1448  145.71       5.2  59.5 257
448   37.8082  141.54       4.9  36.3  43
449   61.2406 -150.85       1.8  50.5  20
450   35.8845 -118.36       1.8   3.1  46
451   18.2180  -66.90       1.7   9.0   3
452   34.0027 -116.82       1.0  14.4  24
453   60.3398 -152.39       3.0  86.5  23
454   36.0717 -120.65       1.4   3.2  47
455   38.8248 -122.79       1.0   3.0  20
456   38.1564 -118.01       1.5   3.8  10
457   37.7342 -112.98       1.2   2.5   7
458   37.4787 -118.84       1.3   6.8  24
459   37.7667 -113.00       1.7   1.6  10
460   36.2338  -89.60       1.5   6.0  15
461   36.7615 -121.59       1.4   0.3  12
462   51.6016 -178.61       2.8  29.8  20
463   38.8353 -122.78       1.8   2.7  30
464   38.7948 -122.79       1.2   0.6  18
465   66.0779 -151.43       3.1  18.1  28
466   51.4445 -178.82       3.2  34.0  21
467   37.8437  118.71       4.5  14.9  32
468   46.8504 -113.36       1.3   3.9  28
469   38.7897 -122.78       1.1   3.1  21
470   -3.3941  136.35       4.8  48.2  40
471   64.7657 -151.96       2.2   6.2  13
472   38.8198 -122.76       1.0   2.2  20
473   60.3586 -151.78       2.0  63.8  16
474   19.1997 -155.40       2.5  36.8  47
475   32.1035 -115.19       2.6  10.0  15
476   36.5315 -121.12       1.7   3.3  22
477   36.7367 -120.75       1.7   0.0  21
478   37.5835 -118.88       1.1   4.8  18
479   33.1980 -115.58       1.2   0.2   8
480   32.2260 -115.29       2.5  10.0  19
481   35.6555 -121.09       2.1   4.8  71
482   44.7430 -110.55       1.3   5.3  21
483   18.0440  -64.23       3.3 122.0   7
484   61.6743 -149.81       1.6  31.9   7
485   44.4135 -114.83       2.5  10.3  27
486  -14.8280  167.85       4.7  86.9  47
487   40.3250 -124.86       2.7   9.6  30
488   14.2195  -92.30       4.5  35.0 129
489   51.7074 -178.19       3.5  86.4  21
490   18.9230  -64.25       4.0  36.0  20
491   37.2928 -121.67       1.4   1.6   8
492   62.1426 -147.67       2.1  26.1   6
493   36.5638 -121.07       1.0   7.3  15
494   37.3867 -119.04       1.0   7.7  35
495   32.8095 -116.05       1.4   9.1  32
496   38.5588 -119.62       1.2   9.7  10
497   59.9994 -151.11       1.7   0.0   7
498   19.5345  -64.48       2.5  10.0   5
499   19.1623  -67.96       3.0  60.0   6
500   38.7813 -122.76       1.0   1.1  18
501   -9.8025  119.07       4.5  37.8  30
502   63.2992 -151.31       1.6   9.7   7
503   37.4573 -118.68       1.4  16.2  39
504   38.8068 -122.75       1.6   0.4  24
505   63.6054 -147.35       2.0   0.0  15
506   33.8838 -116.54       2.8  11.1 125
507   33.7042 -116.73       1.4  20.6  68
508   18.8971  -64.45       3.1  64.0   5
509   -3.0297  130.17       5.1  32.4  52
510   33.7010 -116.80       1.1  19.1  44
511   60.2663 -147.24       2.7   4.5  17
512   33.9343 -116.66       1.3  16.5  64
513  -44.4949  -78.99       5.2  26.3  68
514   38.8452 -122.83       1.1   2.4  19
515   38.8450 -122.83       2.0   2.6  39
516   38.8263 -122.85       1.2   2.5  21
517   62.9103 -150.99       1.7 109.2  20
518   59.7160 -153.20       2.0 111.3  13
519   59.7557 -153.24       2.0 111.9   9
520   36.6013 -121.21       1.6   6.4  14
521   38.8152 -122.80       1.3   0.0   8
522   37.9363 -112.39       1.3   7.1  16
523   37.9427 -112.39       1.8   6.0  21
524   39.5673 -111.27       1.4   1.8  24
525   61.6222 -151.65       1.6  76.8   7
526    8.3849  -86.13       4.6  13.9  95
527   37.6862 -113.26       1.1   3.1   5
528   40.7042 -124.52       2.6  29.6  25
529  -34.6258 -109.17       5.1  14.1 193
530   33.0467 -116.44       1.3   9.8  50
531   33.0480 -116.44       1.2   9.2  38
532   36.5673 -121.16       1.7   2.8  39
533   41.5560  122.98       4.8  10.1 184
534   32.8824  -96.98       3.0  16.1  17
535   36.8582 -115.97       1.5   9.2  13
536   61.3394 -150.91       1.4  55.0  17
537   18.0953  -68.48       3.6  78.0  19
538   10.1320  -85.50       4.6  28.2 187
539   38.8498 -122.82       1.0   1.9  17
540   35.9393 -117.67       1.6   0.4  17
541   38.8348 -122.78       1.2   2.5  19
542  -31.6747  -71.47       5.0  29.1 217
543   38.7897 -122.76       1.5   1.9  26
544   34.2002 -117.49       1.1  14.9  20
545   11.6140  -87.08       4.6  46.5 108
546   63.0719 -151.43       1.3   0.0   9
547   58.5915 -153.55       3.0  11.8  14
548   38.8377 -122.78       1.6   1.8  22
549   61.5770 -148.23       1.5  19.1   4
550   65.0013 -147.33       1.6   2.8  12
551   35.0483 -117.67       1.6   0.0  13
552   37.5162 -119.35       1.1   8.2  16
553    7.4008   93.70       4.5  35.5  35
554   33.3377 -117.15       1.1   0.0  16
555   35.9812 -120.93       1.0   5.5   8
556   42.1982 -122.63       1.2   0.0  11
557   36.0710 -120.65       2.7   4.1 103
558   47.8657 -122.72       1.0   0.0  11
559   62.1865 -149.14       3.2   9.0  83
560   18.3306  -68.01       3.1 106.0  12
561   62.2312 -150.24       1.7   9.9  31
562   63.3164 -151.75       1.7   5.5  21
563   40.3723 -125.12       2.7   3.9  39
564   51.3195 -178.28       2.8  24.3  21
565   52.8690 -164.01       2.5  25.7  12
566   60.8913 -152.16       1.9  97.8  34
567   55.5875 -135.59       3.3  17.8  14
568    9.4880  -84.03       4.1  10.0  10
569   63.9225 -148.93       1.9   0.0  29
570   53.4807 -167.13       1.4  13.1  10
571   38.2642 -118.66       1.1   0.6  13
572   46.3650 -122.23       1.2   7.4  34
573   38.7602 -122.72       1.9   1.9  57
574   64.5573 -149.25       1.3   9.9  23
575   32.0983 -115.16       2.7  10.0   9
576   57.7804 -156.40       2.0 115.4  15
577   63.2947 -149.75       1.2  91.5  11
578   62.0568 -145.07       1.4  18.1   8
579   38.6357   43.19       4.0   2.1   0
580  -39.8717  -74.84       4.7   8.9  34
581   63.4069 -149.86       1.3 105.9  11
582   46.3768 -122.26       1.3  10.3  31
583   62.7315 -149.76       1.2  70.4  13
584   51.6188 -178.38       1.6  14.9  17
585   51.5616 -178.41       2.2   6.2  21
586   52.9377 -169.32       4.4  76.9 175
587   35.6642 -121.08       1.6   5.1  49
588   37.3024 -118.32       1.3  12.0  15
589   36.6020 -121.21       2.4   6.8  69
590   63.7572 -146.66       1.3   4.4  26
591   37.5323 -118.82       1.0   7.2  31
592   33.1543 -115.65       1.4   0.0  17
593   20.9775 -106.09       4.7  58.8 297
594   63.5613 -147.14       1.3   1.9  20
595   62.1857 -151.19       1.9  88.4  33
596   63.2345 -150.74       1.4 122.0  21
597   54.0107 -164.91       2.1  65.0  18
598   38.7930 -122.77       2.9   4.1  88
599  -20.0880  -69.35       4.1  84.2   0
600   35.1420 -118.40       1.2   0.0  14
601   55.6254 -135.16       3.6  15.8  30
602   54.4741 -161.56       2.2  25.6  11
603   63.0848 -150.41       1.3 106.9  21
604   63.2608 -150.67       1.4 122.2  22
605   19.4227 -155.40       2.0   7.8  26
606   37.7160 -119.42       1.3  16.7  12
607   34.1382   80.18       4.0  47.0  13
608   51.8139 -174.51       3.2  41.7  32
609   63.4846 -150.90       1.1  14.9  17
610   36.3282   68.84       5.2  51.7 148
611   38.4915 -122.72       1.3   4.4  13
612   63.4742 -146.64       1.1  14.7  21
613   45.5687 -121.77       1.3   0.0  13
614   55.2415 -134.58       2.6  20.0  11
615   38.8178 -122.79       1.2   3.6  18
616   47.2943 -122.44       1.0  20.4  35
617   44.4937  140.94       4.9 232.2 459
618   32.9035 -116.26       1.3   9.1  45
619   19.3690 -155.23       1.7   3.5  17
620   60.6926 -151.97       1.9  82.7  29
621   39.6648  142.94       4.5  33.0  44
622   61.5633 -148.45       1.0  18.4  15
623   52.1107 -176.10       2.0 127.0  21
624   37.6542 -119.43       2.5  25.5  47
625   63.1702 -150.79       1.4 127.1  26
626   32.1987 -115.28       2.4   0.0  20
627   35.7212 -121.08       1.3   6.3  17
628   60.8516 -151.67       2.6  74.3  54
629   51.5427 -178.49       2.0   7.6  15
630   64.4324 -149.52       1.0   9.0  21
631   33.3657   48.52       4.8  49.8  90
632   52.7174 -164.00       2.8  25.3  10
633   32.3390 -115.20       2.1   0.0  16
634   35.5617 -118.53       1.4   2.0  19
635   39.4774   73.04       4.7  56.6  26
636   33.0250 -116.44       1.8   5.0  87
637   18.9817 -155.37       1.6  29.8  37
638   41.5487 -124.97       2.4   5.0   8
639   62.1897 -151.01       1.8  71.3  42
640  -25.4691  -68.82       4.4  99.9  98
641   35.5678 -118.52       1.9   0.1  31
642   38.1547 -117.99       1.3   9.8  10
643   35.6612 -121.09       1.8   5.7  67
644   36.0038 -120.57       1.1   3.7  38
645   51.6117 -178.41       2.1  11.9  21
646   51.5982 -178.37       2.0   6.9  19
647   60.0824 -152.89       2.1 116.0  31
648   38.7962 -122.80       1.3   3.1  24
649   39.7022 -110.72       1.6   3.0   8
650   36.5475 -121.13       1.3   8.7  30
651   59.6165 -152.47       2.8  64.6  76
652   51.5555 -178.44       2.1  10.5  21
653   51.5291 -178.44       2.5   3.5  24
654  -61.3005  154.06       5.3  10.0 103
655   35.4692 -120.78       1.2   4.1  30
656   44.7563 -111.22       1.2  14.5  15
657   64.8539 -147.46       1.6  13.1  18
658   51.6006 -178.48       2.2  13.1  19
659   51.4362 -178.17       1.7  13.1  22
660   64.1296 -150.17       1.6   1.0  11
661   47.3367 -120.02       1.6   4.6  21
662  -16.4985 -173.91       4.8 101.8 224
663   63.2111 -150.53       1.3 118.9  16
664   18.3045  -65.62       3.0 110.0   5
665   51.5809 -178.48       2.0  12.3  22
666   63.4099 -149.76       1.5 104.4  24
667   36.3042 -120.83       1.4   9.4  18
668   32.6622 -115.80       1.3   9.5  24
669   51.5847 -178.44       2.1   4.9  20
670   62.9650 -148.08       1.4  68.4  31
671   33.4373 -116.56       1.3  11.4  51
672   51.5371 -178.45       2.1   7.8  18
673   45.3778 -112.60       1.3  10.1   8
674   63.2492 -151.13       1.5   8.1  20
675   36.9107 -121.09       1.0   6.7   7
676   32.1947 -115.25       2.3   0.0  17
677   62.3600 -149.04       1.0   4.6  23
678   63.4375 -147.57       1.3   2.6  21
679   55.4698 -134.95       2.5  20.0  12
680   36.6558 -121.28       2.7   7.3  74
681   60.1955 -152.90       2.0 128.0  29
682   54.4216 -161.50       1.9  13.2   9
683   59.7137 -136.07       1.5  10.7  15
684   51.5468 -178.44       3.0   7.8  27
685   41.6318 -112.63       1.3   4.3  20
686   19.4872 -155.67       2.3   1.6  18
687   51.5935 -178.47       2.5  13.1  22
688   62.8885 -150.56       1.2  88.2  19
689   62.9178 -150.54       1.5  91.7  30
690   63.4415 -147.58       2.8   2.8  63
691   34.3372 -116.94       1.4   5.8  38
692   19.6879  -64.33       2.9  35.0   5
693   62.8634 -150.02       1.1  80.0  17
694   61.4181 -146.76       1.8  28.1  40
695   37.9130 -118.18       1.8   0.0  21
696   62.8550 -150.48       1.7  96.1  40
697   63.3706 -151.51       1.0   0.9  15
698   34.0067 -119.22       2.1   8.2  22
699   51.5989 -178.42       2.6   9.7  20
700   38.7018 -122.80       1.3   7.1   9
701   53.6889 -166.41       2.4  74.3  24
702   62.4281 -149.61       1.3  65.0  22
703   51.6001 -178.45       1.8  14.9  15
704   63.9221 -148.90       1.4   0.0  15
705   61.7608 -148.40       1.0   7.4  25
706   62.7366 -152.01       1.9  12.2  31
707   51.6213 -178.43       2.4  12.0  16
708   58.3223 -138.11       2.3   3.4  19
709   34.6097 -119.03       2.5   0.0  62
710   63.5119 -150.88       1.0   8.8  11
711   36.3107 -120.85       1.7   7.6  41
712   51.4176 -174.15       1.9   0.3  10
713   38.8250 -122.77       1.1   1.1  10
714   49.9972  179.26       2.9  10.0  13
715   51.6417 -178.42       2.5  18.3  19
716   52.1973 -178.65       1.9   4.0  14
717   43.8900 -122.98       1.1   0.0   9
718   35.6582 -121.09       2.3   5.2  79
719   51.7309 -178.48       1.7  29.3  13
720   19.4650 -155.34       2.0   4.4  15
721   38.1417 -118.01       1.3   5.0   7
722   51.5470 -178.19       2.1  27.4  18
723   51.5877 -178.41       2.5   4.8  22
724   65.0300 -147.57       1.1   0.0  14
725   51.6348 -178.39       1.7   4.0  14
726   35.7258 -117.66       1.5   2.8  29
727   35.0310 -117.68       1.5   0.0  12
728   51.6276 -178.46       2.9  13.3  27
729   40.4338 -122.14       1.4  20.1   8
730   36.6515 -121.27       1.4   5.2  11
731   51.6106 -178.43       3.3  16.9  29
732   33.3505 -116.30       1.3  12.7  73
733   58.4531 -136.87       1.7  10.4  13
734   38.8093 -122.80       1.1   2.1  20
735   60.3847 -147.74       2.0   9.9  30
736   51.5530 -178.47       2.3   4.8  19
737   33.2195 -116.08       1.8   8.3 107
738    5.0087   96.04       4.7  14.4  49
739   48.0692 -122.88       1.0  22.8  10
740   -7.6475  -33.98       5.8  15.1  19
741    4.9611   96.08       5.9  16.6 429
742   49.4627 -120.51       1.5   0.0  10
743   51.6002 -178.11       3.0  13.7  27
744   38.8003 -122.79       2.9   0.6  74
745   51.5240 -178.43       2.7   3.9  20
746   37.9630 -112.38       1.3   2.9  12
747   48.0907 -121.93       1.0   0.0  14
748   63.5303 -150.83       2.5   8.4  37
749   60.8998 -146.45       2.2  15.0  41
750   39.9710 -118.78       1.4   0.0   8
751   65.8181 -150.94       1.9  13.0  16
752   55.5908 -135.02       2.7  20.0  10
753   37.4022 -118.48       1.1  12.8  18
754   62.6873 -149.53       4.0  65.7 106
755   47.4183 -113.43       1.5  19.5  20
756   30.3641   57.47       5.3  31.9 129
757   35.8320  140.87       4.9   5.7 204
758   51.6652 -178.53       2.8  28.6  23
759   61.5414 -141.26       1.4   5.0  15
760   18.7803  -64.23       2.2  41.0   6
761   51.5645 -178.45       2.5  13.0  20
762   35.0483 -118.36       1.1   0.0  11
763   38.8203 -122.77       1.0   2.2  17
764   -4.4449  134.85       5.4  27.3  66
765   51.1596  179.66       2.9   3.8  14
766   60.3766 -152.15       2.3  90.1  41
767   38.7990 -122.73       1.6   7.2   9
768   54.1910 -164.21       2.4  40.9  23
769   34.9757 -118.56       1.7  11.6  29
770   38.1556 -118.01       2.4   8.1  18
771   51.6027 -178.06       2.1   4.5  17
772   51.6095 -178.46       2.4  17.6  21
773   34.9767 -118.56       1.8   7.5  33
774   38.7912 -122.78       1.4   1.2  27
775   36.0303 -117.82       1.7   0.7  19
776   63.2831 -151.46       2.1   6.7  40
777   33.5997 -116.82       1.4  10.3  62
778   32.5493 -115.65       1.4  12.0  21
779   36.8288 -121.28       1.9   7.5  33
780   51.5820 -178.40       2.5   8.3  17
781   63.5122 -145.97       1.0  15.4  18
782   38.8228 -122.81       2.0   3.5  58
783   53.1350 -166.80       4.3  44.4  73
784  -20.4981  170.62       4.7 195.5  13
785   61.4241 -146.36       1.4  21.8  31
786   51.5990 -178.46       2.1  17.0  18
787   52.0532 -178.59       2.3   3.5  15
788   51.5920 -178.44       3.3   3.3  20
789   37.5385 -118.86       2.4   8.9  48
790   51.5599 -178.47       1.8   1.1  13
791   33.9772 -116.31       1.2   9.6  36
792   38.8397 -122.76       1.2   1.8  18
793   59.4492 -152.76       2.1  77.5  33
794   51.5891 -178.40       2.5   6.6  15
795   39.9998 -122.88       1.5   3.1  12
796   34.6048 -116.61       2.1   8.3  89
797   35.3537 -118.64       1.8   8.5  28
798   51.6318 -178.54       1.7  11.2  12
799   39.5232 -123.32       2.3   9.8  33
800   37.5235 -121.80       1.5   5.3  33
801   59.4378 -153.13       2.2 102.8  35
802   44.6933 -111.90       1.4   6.3  23
803   51.6083 -178.40       2.5   3.8  18
804   51.5368 -178.44       2.6   7.0  22
805   34.6278 -116.54       1.3   7.3  52
806   59.6577 -153.19       2.3 101.1  47
807   33.6342 -116.70       1.1  15.3  61
808   33.0118 -116.36       2.5   8.1 110
809   57.2825 -155.76       2.3   5.3  16
810   51.5860 -178.43       2.3   7.3  17
811   51.6085 -178.40       2.7   8.1  17
812   55.0582 -159.68       2.1  13.2   9
813   51.6291 -178.44       1.9  15.2  12
814   51.5019 -178.54       1.9  10.2  11
815   52.1900 -175.92       2.2 151.6  13
816   51.5825 -178.42       2.1  10.9  16
817   51.6296 -178.48       2.6  22.0  18
818   51.6546 -178.47       2.9  13.2  20
819   51.6290 -178.43       2.8  12.2  20
820   19.3341  -64.26       3.3  87.0   9
821   36.2965 -120.84       1.3   7.4  17
822   62.2448 -150.99       1.8  78.3  50
823   51.5899 -178.45       2.4  18.4  14
824   63.3525 -145.34       1.3   2.6  20
825   51.5998 -178.46       2.4  21.6  17
826   51.6087 -178.52       2.5  11.2  14
827   51.5920 -178.43       2.8  12.9  21
828   38.8158 -122.80       1.2   3.2  22
829   40.2647 -123.10       1.9  39.6  15
830   51.6270 -178.34       5.1   7.0 306
831   38.8373 -122.80       1.2   2.0  17
832   33.5165 -116.46       1.2  10.5  47
833   37.9467 -112.39       1.6   6.4  18
834   64.4853 -146.45       1.0  13.3  20
835   52.5859 -170.61       2.9  25.7  13
836   48.5155 -122.66       1.0  22.0  15
837   33.0958 -115.80       1.2  10.9  20
838   61.7606 -148.41       1.0   9.9  20
839   38.4228 -122.43       1.2   1.6  13
840   11.5523  -87.36       4.3  48.4  39
841   38.8108 -122.79       1.5   3.3  29
842   19.6707  -64.32       2.8  13.0   4
843   17.3561  -68.87       3.4 131.0   4
844   63.3780 -151.47       1.7  12.6  27
845   60.6203 -145.24       1.7  18.9  23
846   37.9432 -112.38       1.3   0.4  15
847   62.8670 -150.43       2.5  93.1  67
848   38.8100 -122.79       1.3   3.2  28
849   37.2907 -119.94       2.1  20.4  16
850   37.4330 -118.56       1.0  12.1  12
851   37.3107 -114.97       1.7   0.7  10
852   18.5608  -66.69       2.9  13.0  11
853   62.0646 -145.10       1.8  13.9  25
854   36.5327 -121.12       1.0   7.9  14
855   59.1431 -153.96       2.4 124.3  47
856   42.2173 -124.57       1.7   0.0  11
857   52.0677 -175.83       2.2 144.9  14
858   63.2969 -151.35       2.2  10.0  37
859   60.9684 -151.97       1.8  92.1  28
860   33.3882 -116.38       1.3   5.0  38
861   61.6786 -146.50       1.7  20.1  34
862   37.6657 -119.42       1.6  18.7  27
863   37.9565 -112.39       1.2   1.9   8
864   63.5022 -147.36       1.3   5.1  31
865   37.9498 -112.39       1.2   1.9  15
866   33.0852 -115.78       2.0   7.9  72
867   33.0868 -115.78       2.6   8.5  86
868   36.8908 -121.40       1.0   8.8  14
869   60.5603 -152.22       3.0  85.3  76
870   38.7860 -122.90       1.1   4.5  17
871   62.2417 -149.69       1.2  10.0  27
872   38.8192 -122.81       1.3   2.1  26
873   61.3309 -151.10       1.4  66.1  21
874   56.9411 -154.22       1.9   3.4  14
875   57.1706 -154.48       1.9  52.2  11
876   38.8100 -122.79       1.4   3.1  27
877   55.6295 -135.00       2.3  20.0  10
878   33.2755 -116.78       1.3  12.5  77
879   63.3597 -145.43       1.0  10.3  15
880   63.1893 -143.10       1.8   0.9  17
881   18.5361  -64.56       2.9  28.0  17
882   38.8432 -122.83       1.1   2.7  22
883   35.8277 -117.74       1.3   7.8  13
884   38.8103 -122.78       1.9   1.4  33
885   32.5498 -115.65       2.4  13.3  30
886   32.5505 -115.65       2.8  13.6  42
887   19.6674  -64.42       3.7  42.0  18
888   63.3165 -151.07       1.4  15.6  29
889   19.4720  -64.25       2.7  78.0   6
890   56.0504 -135.32       2.4  20.0  10
891   39.2290 -110.47       2.4  12.4  28
892   62.9395 -151.24       1.7 131.9  29
893   34.2865 -116.81       1.0   5.4  36
894   64.6381 -149.20       1.0  22.0  19
895   -0.1371  124.73       4.8  77.3  31
896   45.6175 -111.74       1.3   5.3  12
897   61.1266 -150.26       1.6  40.8  28
898   63.7488 -146.83       1.1   0.9  21
899   38.7910 -122.75       1.9   1.8  71
900   62.6786 -150.44       1.4  75.1  26
901   44.8098 -112.97       1.6   7.0  24
902   37.9513 -112.38       1.6   5.4  18
903   63.3112 -151.32       2.5  12.6  45
904   57.8571 -153.96       1.8  60.2   9
905   38.0527 -118.94       1.8   6.2   6
906   34.7858 -119.48       3.3  13.3  65
907   37.5720 -122.54       1.1  10.3  11
908   37.5670 -122.55       1.2  10.8  12
909   63.1454 -150.52       1.7 117.4  31
910   60.2145 -147.17       1.8   8.8  24
911   63.3195 -151.34       1.0  11.5  21
912   36.3060 -120.84       1.4   8.8  23
913   67.6639 -149.02       1.8  10.2  14
914   61.0038 -150.91       2.5  19.8  51
915   37.9515 -112.39       2.0   6.4  23
916   39.2230 -123.23       1.2   4.9  12
917   35.0445 -117.68       1.4   0.0  10
918   37.9542 -112.38       1.1   5.3  16
919   37.9508 -112.39       1.1   1.6  11
920   37.9608 -112.38       1.2   1.6   8
921   37.9587 -112.39       1.0   2.8  10
922   37.9335 -112.37       1.4   6.0  10
923   45.6727 -122.56       1.4  11.4  13
924   37.9423 -112.38       1.5   4.1  18
925   53.8764  -35.18       4.9  10.4 292
926   63.0774 -149.47       1.1  81.2  17
927   61.1894 -148.44       1.5  30.5  19
928   32.5440 -115.65       1.3   9.6  15
929   37.9495 -112.38       1.8   6.2  18
930   63.2677 -151.33       1.0   9.5  15
931   63.3080 -151.34       3.3  12.2  62
932   16.7111  -98.12       4.2  29.8  59
933   63.2959 -151.35       1.3  12.0  13
934   63.3121 -151.33       4.4  11.6  95
935   18.1408  -67.26       2.1  21.0   5
936   37.9578 -112.39       1.6   2.0  15
937   62.1946 -150.41       3.4  13.0  85
938   54.0531  -35.16       4.9  10.1 348
939   62.4175 -151.41       1.4  89.3  21
940   54.0696  -35.12       5.0  10.1 306
941   54.0041  -35.08       4.7  10.1 221
942   32.5317 -115.65       1.4   8.9  15
943   33.5343 -115.89       1.9   4.3  76
944   63.2808 -151.49       1.2   0.9  18
945    9.9978  -85.28       4.3  39.2  79
946   38.1982 -118.12       1.5   0.0  17
947   36.6770 -121.31       1.8   5.4  25
948   38.1377 -118.03       1.8   7.4  13
949   17.9978  -67.02       1.7  12.0   4
950   19.3335 -155.19       1.7   6.7  25
951   32.5303 -115.66       1.8  10.4  30
952   38.0438 -117.67       1.7  16.0   5
953   34.0172 -117.22       1.0  12.2  28
954   36.4625 -121.04       1.4   5.2  21
955   18.2803  -63.97       2.9  25.0   5
956   33.9485 -117.01       1.1  12.9  35
957   33.3200 -116.89       1.1  18.7  54
958   37.9485 -112.38       1.5   0.2  14
959   62.7603 -149.49       1.2  65.6  22
960   37.9580 -112.39       1.6   4.0  15
961   55.4932 -134.99       2.8  20.0  11
962   37.3618 -114.94       1.4   6.2   9
963   61.8596 -150.45       2.0  53.0  39
964   44.7498 -111.23       1.5   9.7  16
965   12.6290  -87.74       5.1  87.3 283
966   24.7542  122.56       4.9 114.4  62
967   38.8295 -122.85       1.6   2.3  32
968   36.8422 -121.44       1.9   6.3  35
969   51.1400    5.96       2.7  14.0   0
970   38.1782 -118.07       1.2  19.6   5
971   59.7883 -152.93       2.0  85.9  24
972   32.2057 -115.29       2.0  10.0  17
973   38.1538 -118.04       1.6   5.2  17
974   38.7923 -122.75       1.2   1.2  18
975   19.4018 -155.28       1.9   2.0  14
976   64.8805 -148.98       1.6  19.9  29
977   34.0193 -116.61       1.2  10.6  36
978   38.1471 -118.01       1.0  10.6  10
979   38.7693 -122.74       1.0   1.6  18
980   36.8882 -121.40       1.9   9.3  41
981   38.1544 -118.01       1.2  13.2  10
982   38.1510 -117.99       2.1   6.6  21
983   38.7182 -122.65       1.0   5.5  13
984   35.5083 -119.91       1.5  20.1   8
985   32.2040 -115.27       3.2  10.0  19
986   31.6199   46.02       4.2  10.1  22
987   38.1703 -118.04       1.6   0.0  19
988   33.0303 -115.61       2.0   9.8  54
989   38.0433 -118.80       1.0  12.7  10
990   38.1370 -118.03       1.2   8.5  10
991   55.6879 -135.48       2.4  20.0   8
992   38.5491 -117.26       1.6   2.0   4
993   33.8322 -116.73       1.0  14.5  47
994   37.8375 -118.38       2.2   8.0  20
995   38.1482 -118.04       1.4   8.3  12
996   37.5318 -118.82       1.3   7.6  32
997   34.3153 -119.51       2.1   8.4  14
998   63.7318 -149.20       1.1   9.4  20
999   58.5496 -152.28       2.5  47.0  31
1000  38.1516 -118.00       1.3   5.5  11
                                          Region
1                            Northern California
2                             Central California
3                                northern Alaska
4                            Northern California
5                                         Nevada
6                                 Central Alaska
7                       Island of Hawaii, Hawaii
8                                 Central Alaska
9                            Southern California
10                   southern Sumatra, Indonesia
11                            Central California
12                      Island of Hawaii, Hawaii
13                      Island of Hawaii, Hawaii
14                                Central Alaska
15                                Central Alaska
16                                    New Mexico
17                           Southern California
18                           Southern California
19            San Francisco Bay area, California
20                           Southern California
21                            Central California
22                           Northern California
23                  Prince Edward Islands region
24                      Island of Hawaii, Hawaii
25                            Puerto Rico region
26                                      Savu Sea
27                            Central California
28                       Kenai Peninsula, Alaska
29                               Southern Alaska
30                                Central Alaska
31                                        Nevada
32                           Southern California
33                                        Nevada
34          Greater Los Angeles area, California
35                            Central California
36                           Northern California
37                                        Nevada
38   Andreanof Islands, Aleutian Islands, Alaska
39   Andreanof Islands, Aleutian Islands, Alaska
40                           Southern California
41                           Southern California
42          Greater Los Angeles area, California
43                           Southern California
44                           Northern California
45                           Northern California
46                           Northern California
47                           Southern California
48                            Central California
49                            Central California
50                            Central California
51                     Philippine Islands region
52                            Central California
53                           Northern California
54                 Northwest Territories, Canada
55                                        Nevada
56                      southern Xinjiang, China
57                           Northern California
58                             northwestern Iran
59                                    Washington
60                            Central California
61                            Central California
62                                Central Alaska
63          Greater Los Angeles area, California
64                           Southern California
65                            Central California
66                            Central California
67                       Baja California, Mexico
68                                Central Alaska
69                           Northern California
70          Greater Los Angeles area, California
71                           Northern California
72                           Northern California
73                            Central California
74                                Central Alaska
75                               Southern Alaska
76                           Northern California
77                       Baja California, Mexico
78                                Central Alaska
79                               Southern Alaska
80                            Central California
81          New Britain region, Papua New Guinea
82                       Baja California, Mexico
83          Greater Los Angeles area, California
84                                Central Alaska
85                      Island of Hawaii, Hawaii
86                      Island of Hawaii, Hawaii
87                      Island of Hawaii, Hawaii
88                      Island of Hawaii, Hawaii
89                      Island of Hawaii, Hawaii
90                      Island of Hawaii, Hawaii
91                                    Washington
92                                Central Alaska
93                               Southern Alaska
94                                        Nevada
95                          offshore El Salvador
96                                      Arkansas
97                           Northern California
98                      Island of Hawaii, Hawaii
99                               northern Alaska
100                               Central Alaska
101                              Southern Alaska
102                              Southern Alaska
103                          Southern California
104                      Baja California, Mexico
105                          Northern California
106                          Southern California
107                          Southern California
108                          Northern California
109                              Southern Alaska
110                                Crete, Greece
111                     Island of Hawaii, Hawaii
112                           Puerto Rico region
113                     Island of Hawaii, Hawaii
114                               Central Alaska
115                          Southern California
116                           Central California
117           San Francisco Bay area, California
118           San Francisco Bay area, California
119                          Northern California
120                               Central Alaska
121                              Southern Alaska
122                               Central Alaska
123                          Southern California
124                          Northern California
125           San Francisco Bay area, California
126                          Southern California
127                                       Nevada
128                              northern Alaska
129        Rat Islands, Aleutian Islands, Alaska
130                          Northern California
131                                   Madagascar
132                           Central California
133                          Northern California
134                        Mindanao, Philippines
135                             Alaska Peninsula
136                           Central California
137                          Southern California
138                     British Columbia, Canada
139                               Central Alaska
140           San Francisco Bay area, California
141                          Northern California
142                               Central Alaska
143                               Central Alaska
144                               northern Idaho
145                          Northern California
146                                   Tajikistan
147                 offshore Northern California
148                      Kenai Peninsula, Alaska
149                           Puerto Rico region
150                              Southern Alaska
151                          Northern California
152                             Jujuy, Argentina
153                                Kuril Islands
154                           Central California
155                       Bosnia and Herzegovina
156                           Central California
157                                   Washington
158                          Southern California
159                          Southern California
160                  southeast of Shikoku, Japan
161                          Northern California
162                              Southern Alaska
163                          Northern California
164                          Southern California
165                          Southern California
166                          Northern California
167                           Central California
168                               Central Alaska
169                               Central Alaska
170                                         Utah
171                                       Nevada
172                                       Nevada
173                           Central California
174                                       Nevada
175                               northern Italy
176                           Central California
177                              Southern Alaska
178                              western Montana
179                          Northern California
180                                         Utah
181                                         Utah
182                                         Utah
183                          Northern California
184         off the coast of Southeastern Alaska
185                              Southern Alaska
186        Seattle-Tacoma urban area, Washington
187                          Northern California
188                              Southern Alaska
189                        Hawaii region, Hawaii
190                                       Nevada
191                 Unimak Island region, Alaska
192                           Central California
193                                 western Iran
194                               Central Alaska
195                           Central California
196           Yellowstone National Park, Wyoming
197                               Central Alaska
198                     Island of Hawaii, Hawaii
199                           Central California
200                               Central Alaska
201                           Central California
202                          Northern California
203                              Southern Alaska
204                          Northern California
205          San Juan Islands region, Washington
206                          Northern California
207                              offshore Oregon
208                           Central California
209                               Central Alaska
210                          Northern California
211        Fox Islands, Aleutian Islands, Alaska
212                        Virgin Islands region
213                          Northern California
214                                eastern Texas
215                               southern Idaho
216                               Central Alaska
217                                  Puerto Rico
218                 offshore Northern California
219                          Northern California
220                      Kenai Peninsula, Alaska
221                          Southern California
222                                         Utah
223                               Central Alaska
224                          Northern California
225                        Virgin Islands region
226                          Southern California
227                              Southern Alaska
228                          Southern California
229                              Southern Alaska
230                          Northern California
231                          Southern California
232                          Southern California
233                               Central Alaska
234                South Sandwich Islands region
235                          Northern California
236                          Northern California
237                 Kodiak Island region, Alaska
238           San Francisco Bay area, California
239                  northern Sumatra, Indonesia
240                          Northern California
241                          Northern California
242                        Virgin Islands region
243                 Kodiak Island region, Alaska
244                                       Nevada
245                              offshore Oregon
246                          Northern California
247                          Northern California
248                              offshore Oregon
249                          Northern California
250                                       Nevada
251                               Central Alaska
252                     Island of Hawaii, Hawaii
253                              Southern Alaska
254                          Northern California
255         Greater Los Angeles area, California
256                          Northern California
257                          Northern California
258                          Northern California
259                          Northern California
260                          Northern California
261                 offshore Northern California
262                          Northern California
263                              northern Alaska
264                              offshore Oregon
265                              Southern Alaska
266                                       Nevada
267                                       Nevada
268                                       Nevada
269                          Northern California
270                               Central Alaska
271                          Northern California
272                          Northern California
273                     Island of Hawaii, Hawaii
274                          Northern California
275                          Northern California
276                          Northern California
277                               Central Alaska
278                          Northern California
279                          Northern California
280                          Southern California
281                          Northern California
282                              Southern Alaska
283                          Southern California
284                                       Nevada
285                          Northern California
286                           Central California
287                                       Nevada
288                          Northern California
289                              Southern Alaska
290        Fox Islands, Aleutian Islands, Alaska
291                                       Nevada
292                      Baja California, Mexico
293                           Central California
294                                       Oregon
295                          Northern California
296                           Central California
297         Greater Los Angeles area, California
298                          Northern California
299           Yellowstone National Park, Wyoming
300                               Central Alaska
301                          Southern California
302                          Northern California
303                          Northern California
304                               Central Alaska
305                          Northern California
306                               Central Alaska
307                      off the coast of Oregon
308                          Southern California
309                          Northern California
310         Greater Los Angeles area, California
311                           Central California
312                      Baja California, Mexico
313                           Puerto Rico region
314                           Central California
315                          Southern California
316                              Southern Alaska
317                          Northern California
318  Andreanof Islands, Aleutian Islands, Alaska
319                           Puerto Rico region
320                           Central California
321                                       Nevada
322                          Southern California
323                     Island of Hawaii, Hawaii
324                           Central California
325                             Sakhalin, Russia
326                          Northern California
327                              Southern Alaska
328                        Virgin Islands region
329                          Northern California
330                 offshore Northern California
331  Andreanof Islands, Aleutian Islands, Alaska
332          San Juan Islands region, Washington
333                          Northern California
334                              Southern Alaska
335                          Northern California
336                        Virgin Islands region
337                                       Nevada
338                          Southern California
339                               Central Alaska
340                           Central California
341                           Central California
342                               Central Alaska
343                          Northern California
344                          Northern California
345                 offshore Northern California
346                          Northern California
347                               Central Alaska
348                                   Tajikistan
349                 offshore Northern California
350                          Northern California
351                                       Nevada
352                                       Nevada
353        Seattle-Tacoma urban area, Washington
354                      Kenai Peninsula, Alaska
355                          Northern California
356                          Sulawesi, Indonesia
357                          Northern California
358                          Northern California
359                                southern Iran
360                          Northern California
361                          Northern California
362                          Northern California
363                          Northern California
364                               Central Alaska
365        Fox Islands, Aleutian Islands, Alaska
366                          Northern California
367                          Northern California
368                          Northern California
369                          Northern California
370                          Northern California
371                          Northern California
372                          Northern California
373                          Northern California
374                          Northern California
375                          Northern California
376         Greater Los Angeles area, California
377                          Northern California
378                           Central California
379                                       Nevada
380                          Northern California
381                                       Nevada
382                          Northern California
383                           Central California
384                           Central California
385     Russia-Kazakhstan-Xinjiang border region
386                               Central Alaska
387                          Southern California
388                                   Costa Rica
389                          Northern California
390                              northern Alaska
391                           Central California
392                          Northern California
393                          Northern California
394                           Central California
395  Andreanof Islands, Aleutian Islands, Alaska
396                           Central California
397                           Central California
398                          Southern California
399                               Central Alaska
400                              Southern Alaska
401                          Southern California
402                 offshore Northern California
403           San Francisco Bay area, California
404                          Northern California
405                                         Utah
406                                   Washington
407                          Northern California
408                                southern Iran
409                                     Colorado
410                                       Nevada
411                 offshore Northern California
412  Andreanof Islands, Aleutian Islands, Alaska
413                                         Utah
414                               Gulf of Alaska
415                               Central Alaska
416                           Central California
417                                       Nevada
418                              Southern Alaska
419                                       Nevada
420                        Virgin Islands region
421                                         Fiji
422                               Central Alaska
423                               Central Alaska
424                           Central California
425                          Northern California
426                          Northern California
427                          Northern California
428                        Virgin Islands region
429                              northern Alaska
430                              Southern Alaska
431                                       Oregon
432                                   Washington
433                                       Nevada
434                          Northern California
435                           Central California
436                          Northern California
437                             Alaska Peninsula
438                               northern Idaho
439           Gulf of Santa Catalina, California
440                              Southern Alaska
441                          Northern California
442                     British Columbia, Canada
443  Andreanof Islands, Aleutian Islands, Alaska
444                        Virgin Islands region
445                          Northern California
446      San Diego County urban area, California
447                       Hokkaido, Japan region
448         near the east coast of Honshu, Japan
449                              Southern Alaska
450                           Central California
451                                  Puerto Rico
452                          Southern California
453                              Southern Alaska
454                           Central California
455                          Northern California
456                                       Nevada
457                                         Utah
458                           Central California
459                                         Utah
460                                    Tennessee
461                           Central California
462  Andreanof Islands, Aleutian Islands, Alaska
463                          Northern California
464                          Northern California
465                              northern Alaska
466  Andreanof Islands, Aleutian Islands, Alaska
467                              Shandong, China
468                              western Montana
469                          Northern California
470                             Papua, Indonesia
471                               Central Alaska
472                          Northern California
473                      Kenai Peninsula, Alaska
474                     Island of Hawaii, Hawaii
475                      Baja California, Mexico
476                           Central California
477                           Central California
478                           Central California
479                          Southern California
480                      Baja California, Mexico
481                           Central California
482           Yellowstone National Park, Wyoming
483                        Virgin Islands region
484                              Southern Alaska
485                               southern Idaho
486                                      Vanuatu
487                 offshore Northern California
488                           offshore Guatemala
489  Andreanof Islands, Aleutian Islands, Alaska
490                        Virgin Islands region
491                          Northern California
492                               Central Alaska
493                           Central California
494                           Central California
495                          Southern California
496                          Northern California
497                      Kenai Peninsula, Alaska
498                        Virgin Islands region
499                    Dominican Republic region
500                          Northern California
501                      Sumba region, Indonesia
502                               Central Alaska
503                           Central California
504                          Northern California
505                               Central Alaska
506                          Southern California
507                          Southern California
508                        Virgin Islands region
509                             Seram, Indonesia
510                          Southern California
511                              Southern Alaska
512                          Southern California
513                off the coast of Aisen, Chile
514                          Northern California
515                          Northern California
516                          Northern California
517                               Central Alaska
518                              Southern Alaska
519                              Southern Alaska
520                           Central California
521                          Northern California
522                                         Utah
523                                         Utah
524                                         Utah
525                              Southern Alaska
526                  off the coast of Costa Rica
527                                         Utah
528                 offshore Northern California
529                   southern East Pacific Rise
530                          Southern California
531                          Southern California
532                           Central California
533                              Liaoning, China
534                               northern Texas
535                                       Nevada
536                              Southern Alaska
537                    Dominican Republic region
538                                   Costa Rica
539                          Northern California
540                           Central California
541                          Northern California
542                              Coquimbo, Chile
543                          Northern California
544         Greater Los Angeles area, California
545                  near the coast of Nicaragua
546                               Central Alaska
547                 Kodiak Island region, Alaska
548                          Northern California
549                              Southern Alaska
550                              northern Alaska
551                          Southern California
552                           Central California
553                Nicobar Islands, India region
554                          Southern California
555                           Central California
556                                       Oregon
557                           Central California
558               Puget Sound region, Washington
559                               Central Alaska
560             Mona Passage, Dominican Republic
561                               Central Alaska
562                               Central Alaska
563                 offshore Northern California
564  Andreanof Islands, Aleutian Islands, Alaska
565                              south of Alaska
566                              Southern Alaska
567         off the coast of Southeastern Alaska
568                                   Costa Rica
569                               Central Alaska
570        Fox Islands, Aleutian Islands, Alaska
571                                       Nevada
572                                   Washington
573                          Northern California
574                               Central Alaska
575                      Baja California, Mexico
576                             Alaska Peninsula
577                               Central Alaska
578                               Central Alaska
579                               eastern Turkey
580                    offshore Los Lagos, Chile
581                               Central Alaska
582                                   Washington
583                               Central Alaska
584  Andreanof Islands, Aleutian Islands, Alaska
585  Andreanof Islands, Aleutian Islands, Alaska
586        Fox Islands, Aleutian Islands, Alaska
587                           Central California
588                           Central California
589                           Central California
590                               Central Alaska
591                           Central California
592                          Southern California
593                     offshore Nayarit, Mexico
594                               Central Alaska
595                               Central Alaska
596                               Central Alaska
597                 Unimak Island region, Alaska
598                          Northern California
599                              Tarapaca, Chile
600                           Central California
601         off the coast of Southeastern Alaska
602                             Alaska Peninsula
603                               Central Alaska
604                               Central Alaska
605                     Island of Hawaii, Hawaii
606                           Central California
607                               western Xizang
608  Andreanof Islands, Aleutian Islands, Alaska
609                               Central Alaska
610               Hindu Kush region, Afghanistan
611                          Northern California
612                               Central Alaska
613                                       Oregon
614                          Southeastern Alaska
615                          Northern California
616        Seattle-Tacoma urban area, Washington
617                         eastern Sea of Japan
618                          Southern California
619                     Island of Hawaii, Hawaii
620                      Kenai Peninsula, Alaska
621         near the east coast of Honshu, Japan
622                              Southern Alaska
623  Andreanof Islands, Aleutian Islands, Alaska
624                           Central California
625                               Central Alaska
626                      Baja California, Mexico
627                           Central California
628                      Kenai Peninsula, Alaska
629  Andreanof Islands, Aleutian Islands, Alaska
630                               Central Alaska
631                                 western Iran
632                              south of Alaska
633                      Baja California, Mexico
634                           Central California
635                                   Kyrgyzstan
636                          Southern California
637                        Hawaii region, Hawaii
638                 offshore Northern California
639                               Central Alaska
640                               Atacama, Chile
641                           Central California
642                                       Nevada
643                           Central California
644                           Central California
645  Andreanof Islands, Aleutian Islands, Alaska
646  Andreanof Islands, Aleutian Islands, Alaska
647                              Southern Alaska
648                          Northern California
649                                         Utah
650                           Central California
651                              Southern Alaska
652  Andreanof Islands, Aleutian Islands, Alaska
653  Andreanof Islands, Aleutian Islands, Alaska
654                       Balleny Islands region
655                           Central California
656                              western Montana
657                               Central Alaska
658  Andreanof Islands, Aleutian Islands, Alaska
659  Andreanof Islands, Aleutian Islands, Alaska
660                               Central Alaska
661                                   Washington
662                                        Tonga
663                               Central Alaska
664                           Puerto Rico region
665  Andreanof Islands, Aleutian Islands, Alaska
666                               Central Alaska
667                           Central California
668                          Southern California
669  Andreanof Islands, Aleutian Islands, Alaska
670                               Central Alaska
671                          Southern California
672  Andreanof Islands, Aleutian Islands, Alaska
673                              western Montana
674                               Central Alaska
675                           Central California
676                      Baja California, Mexico
677                               Central Alaska
678                               Central Alaska
679                          Southeastern Alaska
680                           Central California
681                              Southern Alaska
682                             Alaska Peninsula
683                          Southeastern Alaska
684  Andreanof Islands, Aleutian Islands, Alaska
685                                         Utah
686                     Island of Hawaii, Hawaii
687  Andreanof Islands, Aleutian Islands, Alaska
688                               Central Alaska
689                               Central Alaska
690                               Central Alaska
691                          Southern California
692                        Virgin Islands region
693                               Central Alaska
694                              Southern Alaska
695                                       Nevada
696                               Central Alaska
697                               Central Alaska
698           Channel Islands region, California
699  Andreanof Islands, Aleutian Islands, Alaska
700                          Northern California
701        Fox Islands, Aleutian Islands, Alaska
702                               Central Alaska
703  Andreanof Islands, Aleutian Islands, Alaska
704                               Central Alaska
705                              Southern Alaska
706                               Central Alaska
707  Andreanof Islands, Aleutian Islands, Alaska
708                          Southeastern Alaska
709                          Southern California
710                               Central Alaska
711                           Central California
712  Andreanof Islands, Aleutian Islands, Alaska
713                          Northern California
714                south of the Aleutian Islands
715  Andreanof Islands, Aleutian Islands, Alaska
716  Andreanof Islands, Aleutian Islands, Alaska
717                                       Oregon
718                           Central California
719  Andreanof Islands, Aleutian Islands, Alaska
720                     Island of Hawaii, Hawaii
721                                       Nevada
722  Andreanof Islands, Aleutian Islands, Alaska
723  Andreanof Islands, Aleutian Islands, Alaska
724                              northern Alaska
725  Andreanof Islands, Aleutian Islands, Alaska
726                          Southern California
727                          Southern California
728  Andreanof Islands, Aleutian Islands, Alaska
729                          Northern California
730                           Central California
731  Andreanof Islands, Aleutian Islands, Alaska
732                          Southern California
733                          Southeastern Alaska
734                          Northern California
735                              Southern Alaska
736  Andreanof Islands, Aleutian Islands, Alaska
737                          Southern California
738                  northern Sumatra, Indonesia
739               Puget Sound region, Washington
740                         South Atlantic Ocean
741                  northern Sumatra, Indonesia
742                     British Columbia, Canada
743  Andreanof Islands, Aleutian Islands, Alaska
744                          Northern California
745  Andreanof Islands, Aleutian Islands, Alaska
746                                         Utah
747                                   Washington
748                               Central Alaska
749                              Southern Alaska
750                                       Nevada
751                              northern Alaska
752         off the coast of Southeastern Alaska
753                           Central California
754                               Central Alaska
755                              western Montana
756                                 eastern Iran
757         near the east coast of Honshu, Japan
758  Andreanof Islands, Aleutian Islands, Alaska
759                              Southern Alaska
760                        Virgin Islands region
761  Andreanof Islands, Aleutian Islands, Alaska
762                          Southern California
763                          Northern California
764     near the south coast of Papua, Indonesia
765        Rat Islands, Aleutian Islands, Alaska
766                              Southern Alaska
767                          Northern California
768                 Unimak Island region, Alaska
769                           Central California
770                                       Nevada
771  Andreanof Islands, Aleutian Islands, Alaska
772  Andreanof Islands, Aleutian Islands, Alaska
773                           Central California
774                          Northern California
775                           Central California
776                               Central Alaska
777                          Southern California
778                      Baja California, Mexico
779                           Central California
780  Andreanof Islands, Aleutian Islands, Alaska
781                               Central Alaska
782                          Northern California
783        Fox Islands, Aleutian Islands, Alaska
784                                      Vanuatu
785                              Southern Alaska
786  Andreanof Islands, Aleutian Islands, Alaska
787  Andreanof Islands, Aleutian Islands, Alaska
788  Andreanof Islands, Aleutian Islands, Alaska
789                           Central California
790  Andreanof Islands, Aleutian Islands, Alaska
791                          Southern California
792                          Northern California
793                              Southern Alaska
794  Andreanof Islands, Aleutian Islands, Alaska
795                          Northern California
796                          Southern California
797                           Central California
798  Andreanof Islands, Aleutian Islands, Alaska
799                          Northern California
800           San Francisco Bay area, California
801                              Southern Alaska
802                              western Montana
803  Andreanof Islands, Aleutian Islands, Alaska
804  Andreanof Islands, Aleutian Islands, Alaska
805                          Southern California
806                              Southern Alaska
807                          Southern California
808                          Southern California
809                             Alaska Peninsula
810  Andreanof Islands, Aleutian Islands, Alaska
811  Andreanof Islands, Aleutian Islands, Alaska
812                             Alaska Peninsula
813  Andreanof Islands, Aleutian Islands, Alaska
814  Andreanof Islands, Aleutian Islands, Alaska
815  Andreanof Islands, Aleutian Islands, Alaska
816  Andreanof Islands, Aleutian Islands, Alaska
817  Andreanof Islands, Aleutian Islands, Alaska
818  Andreanof Islands, Aleutian Islands, Alaska
819  Andreanof Islands, Aleutian Islands, Alaska
820                        Virgin Islands region
821                           Central California
822                               Central Alaska
823  Andreanof Islands, Aleutian Islands, Alaska
824                               Central Alaska
825  Andreanof Islands, Aleutian Islands, Alaska
826  Andreanof Islands, Aleutian Islands, Alaska
827  Andreanof Islands, Aleutian Islands, Alaska
828                          Northern California
829                          Northern California
830  Andreanof Islands, Aleutian Islands, Alaska
831                          Northern California
832                          Southern California
833                                         Utah
834                               Central Alaska
835        Fox Islands, Aleutian Islands, Alaska
836          San Juan Islands region, Washington
837                          Southern California
838                              Southern Alaska
839                          Northern California
840                  near the coast of Nicaragua
841                          Northern California
842                        Virgin Islands region
843                    Dominican Republic region
844                               Central Alaska
845                              Southern Alaska
846                                         Utah
847                               Central Alaska
848                          Northern California
849                           Central California
850                           Central California
851                                       Nevada
852                           Puerto Rico region
853                               Central Alaska
854                           Central California
855                              Southern Alaska
856                              offshore Oregon
857  Andreanof Islands, Aleutian Islands, Alaska
858                               Central Alaska
859                      Kenai Peninsula, Alaska
860                          Southern California
861                              Southern Alaska
862                           Central California
863                                         Utah
864                               Central Alaska
865                                         Utah
866                          Southern California
867                          Southern California
868                           Central California
869                              Southern Alaska
870                          Northern California
871                               Central Alaska
872                          Northern California
873                              Southern Alaska
874                 Kodiak Island region, Alaska
875                 Kodiak Island region, Alaska
876                          Northern California
877         off the coast of Southeastern Alaska
878                          Southern California
879                               Central Alaska
880                               Central Alaska
881                        Virgin Islands region
882                          Northern California
883                           Central California
884                          Northern California
885                      Baja California, Mexico
886                      Baja California, Mexico
887                        Virgin Islands region
888                               Central Alaska
889                        Virgin Islands region
890                          Southeastern Alaska
891                                         Utah
892                               Central Alaska
893                          Southern California
894                               Central Alaska
895                                  Molucca Sea
896                              western Montana
897                              Southern Alaska
898                               Central Alaska
899                          Northern California
900                               Central Alaska
901                              western Montana
902                                         Utah
903                               Central Alaska
904                 Kodiak Island region, Alaska
905                           Central California
906                           Central California
907                 offshore Northern California
908                 offshore Northern California
909                               Central Alaska
910                              Southern Alaska
911                               Central Alaska
912                           Central California
913                              northern Alaska
914                              Southern Alaska
915                                         Utah
916                          Northern California
917                          Southern California
918                                         Utah
919                                         Utah
920                                         Utah
921                                         Utah
922                                         Utah
923              Portland urban area, Washington
924                                         Utah
925                              Reykjanes Ridge
926                               Central Alaska
927                              Southern Alaska
928                      Baja California, Mexico
929                                         Utah
930                               Central Alaska
931                               Central Alaska
932                               Oaxaca, Mexico
933                               Central Alaska
934                               Central Alaska
935                    Mona Passage, Puerto Rico
936                                         Utah
937                               Central Alaska
938                              Reykjanes Ridge
939                               Central Alaska
940                              Reykjanes Ridge
941                              Reykjanes Ridge
942                      Baja California, Mexico
943                          Southern California
944                               Central Alaska
945                  off the coast of Costa Rica
946                                       Nevada
947                           Central California
948                                       Nevada
949                                  Puerto Rico
950                     Island of Hawaii, Hawaii
951                      Baja California, Mexico
952                                       Nevada
953         Greater Los Angeles area, California
954                           Central California
955                        Virgin Islands region
956                          Southern California
957                          Southern California
958                                         Utah
959                               Central Alaska
960                                         Utah
961                          Southeastern Alaska
962                                       Nevada
963                              Southern Alaska
964                              western Montana
965                  near the coast of Nicaragua
966                                Taiwan region
967                          Northern California
968                           Central California
969                              The Netherlands
970                                       Nevada
971                              Southern Alaska
972                      Baja California, Mexico
973                                       Nevada
974                          Northern California
975                     Island of Hawaii, Hawaii
976                               Central Alaska
977                          Southern California
978                                       Nevada
979                          Northern California
980                           Central California
981                                       Nevada
982                                       Nevada
983                          Northern California
984                           Central California
985                      Baja California, Mexico
986                                         Iraq
987                                       Nevada
988                          Southern California
989                           Central California
990                                       Nevada
991         off the coast of Southeastern Alaska
992                                       Nevada
993                          Southern California
994                           Central California
995                                       Nevada
996                           Central California
997            Santa Barbara Channel, California
998                               Central Alaska
999                 Kodiak Island region, Alaska
1000                                      Nevada
 [ reached getOption("max.print") -- omitted 57 rows ]
```


---

## Looking at data - dim(),names(),nrow(),ncol()

```r
dim(eData)
```

```
[1] 1057   10
```

```r
names(eData)
```

```
 [1] "Src"       "Eqid"      "Version"   "Datetime"  "Lat"      
 [6] "Lon"       "Magnitude" "Depth"     "NST"       "Region"   
```

```r
nrow(eData)
```

```
[1] 1057
```


---

## Looking at the data - quantile(),summary()


```r
quantile(eData$Lat)
```

```
    0%    25%    50%    75%   100% 
-61.30  35.56  38.77  52.58  67.66 
```

```r
summary(eData)
```

```
      Src            Eqid         Version   
 ak     :330   00400150:   1   2      :379  
 nc     :247   00400153:   1   0      :195  
 ci     :145   00400155:   1   1      :168  
 nn     : 92   00400156:   1   9      : 97  
 us     : 89   00400157:   1   3      : 82  
 pr     : 40   00400159:   1   4      : 43  
 (Other):114   (Other) :1051   (Other): 93  
                                  Datetime         Lat       
 Monday, January 21, 2013 11:00:00 UTC:   2   Min.   :-61.3  
 Friday, January 25, 2013 00:06:25 UTC:   1   1st Qu.: 35.6  
 Friday, January 25, 2013 00:10:02 UTC:   1   Median : 38.8  
 Friday, January 25, 2013 00:11:41 UTC:   1   Mean   : 41.3  
 Friday, January 25, 2013 00:12:53 UTC:   1   3rd Qu.: 52.6  
 Friday, January 25, 2013 00:18:54 UTC:   1   Max.   : 67.7  
 (Other)                              :1050                  
      Lon         Magnitude        Depth            NST       
 Min.   :-180   Min.   :1.00   Min.   :  0.0   Min.   :  0.0  
 1st Qu.:-150   1st Qu.:1.30   1st Qu.:  3.8   1st Qu.: 12.0  
 Median :-122   Median :1.70   Median :  9.4   Median : 19.0  
 Mean   :-117   Mean   :2.04   Mean   : 21.5   Mean   : 31.3  
 3rd Qu.:-117   3rd Qu.:2.40   3rd Qu.: 20.1   3rd Qu.: 31.0  
 Max.   : 180   Max.   :5.90   Max.   :642.5   Max.   :548.0  
                                                              
                                         Region   
 Northern California                        :162  
 Central Alaska                             :123  
 Central California                         :113  
 Southern California                        : 84  
 Andreanof Islands, Aleutian Islands, Alaska: 72  
 Southern Alaska                            : 69  
 (Other)                                    :434  
```




---

## Looking at data - class()


```r
class(eData)
```

```
[1] "data.frame"
```

```r
sapply(eData[1,],class)
```

```
      Src      Eqid   Version  Datetime       Lat       Lon Magnitude 
 "factor"  "factor"  "factor"  "factor" "numeric" "numeric" "numeric" 
    Depth       NST    Region 
"numeric" "integer"  "factor" 
```


---

## Looking at data - unique(),length(),table()


```r
unique(eData$Src)
```

```
 [1] nc ci ak nn hv us pr uw nm mb uu
Levels: ak ci hv mb nc nm nn pr us uu uw
```

```r
length(unique(eData$Src))
```

```
[1] 11
```

```r
table(eData$Src)
```

```

 ak  ci  hv  mb  nc  nm  nn  pr  us  uu  uw 
330 145  29  10 247   2  92  40  89  40  33 
```


---

## Looking at data - table()


```r
table(eData$Src,eData$Version)
```

```
    
       0   1   2   3   4   5   6   7   8   9   A   B   D   E
  ak   0  93 211  26   0   0   0   0   0   0   0   0   0   0
  ci  64   0  67   7   3   3   1   0   0   0   0   0   0   0
  hv   0  14  11   0   2   2   0   0   0   0   0   0   0   0
  mb   0   0  10   0   0   0   0   0   0   0   0   0   0   0
  nc  91  46  51  37  10   4   3   1   1   1   1   1   0   0
  nm   0   0   0   0   0   0   0   0   0   0   2   0   0   0
  nn   0   0   0   0   0   0   0   0   0  92   0   0   0   0
  pr  40   0   0   0   0   0   0   0   0   0   0   0   0   0
  us   0   0   2   0  14  13  24  13  11   4   4   2   1   1
  uu   0   0  15   6  14   3   2   0   0   0   0   0   0   0
  uw   0  15  12   6   0   0   0   0   0   0   0   0   0   0
```



---

## Looking at data - any(), all()

```r
eData$Lat[1:10]
```

```
 [1] 38.83 36.04 65.23 39.56 37.26 62.10 19.41 63.51 32.91 -5.17
```

```r
eData$Lat[1:10] > 40
```

```
 [1] FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE
```

```r
any(eData$Lat[1:10] > 40)
```

```
[1] TRUE
```


---

## Looking at data - all()

```r

eData$Lat[1:10] > 40
```

```
 [1] FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE
```

```r
all(eData$Lat[1:10] > 40)
```

```
[1] FALSE
```




---

## Looking at subsets - &


```r
eData[eData$Lat > 0 & eData$Lon > 0,c("Lat","Lon")]
```

```
        Lat    Lon
51    5.486 127.05
56   39.749  77.30
58   38.295  46.81
110  34.571  24.10
129  51.130 179.35
134   9.438 126.10
146  38.426  73.36
153  49.728 155.69
155  43.337  18.77
160  29.379 132.20
175  44.280  10.53
193  31.763  50.95
239   4.998  95.96
325  53.564 142.75
348  38.608  73.49
359  27.771  56.41
385  49.825  87.60
408  27.877  56.56
447  43.145 145.71
448  37.808 141.54
467  37.844 118.71
533  41.556 122.98
553   7.401  93.70
579  38.636  43.19
607  34.138  80.18
610  36.328  68.84
617  44.494 140.94
621  39.665 142.94
631  33.366  48.52
635  39.477  73.04
714  49.997 179.26
738   5.009  96.04
741   4.961  96.08
756  30.364  57.47
757  35.832 140.87
765  51.160 179.66
966  24.754 122.56
969  51.140   5.96
986  31.620  46.02
1020 64.791 146.60
```


---

## Looking at subsets - |


```r
eData[eData$Lat > 0 | eData$Lon > 0,c("Lat","Lon")]
```

```
          Lat     Lon
1     38.8292 -122.81
2     36.0403 -117.35
3     65.2271 -149.51
4     39.5573 -121.99
5     37.2587 -114.07
6     62.1046 -150.70
7     19.4065 -155.26
8     63.5132 -150.83
9     32.9112 -116.25
10    -5.1704  102.94
11    35.5633 -118.53
12    19.2960 -155.38
13    19.9262 -155.54
14    62.1638 -149.58
15    63.2917 -149.24
16    34.2925 -106.71
17    33.6293 -116.69
18    32.9282 -116.37
19    37.5777 -122.51
20    33.0542 -116.44
21    36.8237 -121.55
22    38.7873 -122.76
23   -44.6350   37.43
24    19.3460 -155.09
25    18.0025  -65.62
26    -9.5294  121.89
27    36.2972 -120.87
28    60.1621 -150.54
29    61.6813 -151.51
30    63.2819 -152.34
31    38.1572 -118.04
32    32.9265 -116.30
33    40.8640 -118.56
34    33.8917 -117.55
35    38.0600 -118.94
36    38.7878 -122.76
37    38.1545 -118.02
38    51.6242 -175.91
39    51.5409 -177.78
40    33.1673 -116.43
41    33.0172 -116.44
42    34.2008 -117.39
43    34.3328 -116.89
44    38.7970 -122.78
45    40.1442 -123.84
46    37.1773 -122.34
47    33.0387 -116.44
48    36.2718 -120.84
49    36.2697 -120.84
50    36.7472 -121.41
51     5.4858  127.05
52    36.2708 -120.84
53    38.7952 -122.81
54    64.3717 -130.81
55    38.9462 -118.70
56    39.7489   77.30
57    38.8378 -122.85
58    38.2948   46.81
59    47.8815 -121.65
60    38.5208 -119.40
61    38.5146 -119.42
62    62.3487 -149.04
63    34.2225 -117.48
64    33.3773 -116.84
65    35.4860 -118.29
66    36.0778 -117.88
67    32.5807 -115.70
68    62.0858 -145.19
69    39.8178 -123.63
70    34.0417 -117.25
71    38.8168 -122.82
72    38.8205 -122.76
73    35.5567 -120.83
74    63.2206 -147.11
75    59.4485 -153.58
76    38.8050 -122.80
77    32.6072 -115.69
78    63.3318 -144.70
79    60.3764 -152.20
80    34.8777 -120.32
81    -6.1335  149.81
82    32.4860 -115.58
83    34.1245 -117.41
84    63.3213 -145.22
85    19.3815 -155.24
86    19.3770 -155.24
87    19.3768 -155.24
88    19.3783 -155.24
89    19.3818 -155.24
90    19.3780 -155.24
91    48.2052 -121.76
92    63.9433 -149.08
93    60.0108 -152.73
94    38.1486 -118.05
95    13.1058  -89.22
96    35.2596  -92.33
97    38.8077 -122.78
98    19.3872 -155.28
99    65.9677 -150.32
100   63.5410 -147.30
101   61.6783 -149.64
102   60.4754 -141.24
103   33.7777 -116.16
104   32.6210 -115.72
105   38.8375 -122.85
106   33.0210 -116.53
107   33.3815 -116.79
108   38.5484 -119.63
109   61.6291 -151.56
110   34.5712   24.10
111   19.2875 -155.44
112   18.9839  -66.20
113   19.6533 -155.66
114   63.3845 -151.14
115   33.7785 -116.16
116   37.5202 -118.66
117   37.5593 -121.83
118   37.3528 -121.72
119   40.5313 -122.25
120   63.3364 -145.21
121   60.2413 -152.20
122   63.3625 -145.32
123   33.5707 -116.65
124   38.8145 -122.82
125   37.8828 -122.23
126   33.7778 -116.16
127   40.0897 -119.66
128   65.0142 -147.34
129   51.1302  179.35
130   38.8372 -122.85
131  -23.6541   43.55
132   38.0557 -118.95
133   38.8353 -122.78
134    9.4380  126.10
135   58.2593 -155.12
136   36.0785 -120.64
137   33.7757 -116.16
138   49.4560 -120.50
139   63.2658 -151.34
140   37.3210 -122.11
141   38.5743 -119.61
142   62.8756 -148.13
143   63.5667 -150.79
144   47.4443 -116.01
145   38.7558 -122.74
146   38.4261   73.36
147   40.2987 -124.87
148   60.6546 -150.92
149   19.4892  -65.50
150   61.9375 -148.29
151   38.8350 -122.77
153   49.7278  155.69
154   36.5573 -121.07
155   43.3369   18.77
156   36.0028 -120.56
157   47.1993 -121.89
158   34.6292 -117.30
159   34.6760 -116.35
160   29.3787  132.20
161   38.2393 -122.06
162   61.5897 -150.36
163   38.8185 -122.82
164   34.6292 -117.30
165   32.9878 -116.22
166   38.8175 -122.82
167   36.0012 -120.56
168   62.1888 -151.16
169   62.1963 -149.46
170   37.4665 -112.28
171   38.1580 -118.04
172   38.1510 -118.03
173   37.4752 -118.84
174   38.1571 -118.03
175   44.2804   10.53
176   36.2408 -120.79
177   60.1313 -153.12
178   47.7295 -113.69
179   38.8248 -122.79
180   37.4637 -112.28
181   37.4687 -112.28
182   37.4712 -112.29
183   38.8128 -122.78
184   55.9029 -135.30
185   61.3620 -146.65
186   47.8385 -122.29
187   38.7792 -122.75
188   60.7766 -145.73
189   20.3130 -155.57
190   37.5377 -117.60
191   53.9156 -164.96
192   37.4817 -118.39
193   31.7629   50.95
194   63.3898 -151.78
195   36.4688 -120.95
196   44.4458 -110.99
197   62.0429 -145.13
198   19.4585 -155.87
199   37.4705 -118.84
200   64.5271 -149.31
201   36.6292 -121.04
202   38.3165 -122.39
203   61.4820 -151.88
204   38.7667 -122.71
205   48.4293 -122.55
206   40.2797 -121.06
207   44.4655 -124.61
208   37.4715 -118.84
209   63.3945 -150.11
210   38.5542 -119.63
211   52.5805 -169.61
212   19.5454  -64.58
213   38.7677 -122.74
214   31.9131  -94.43
215   42.0903 -112.46
216   63.2671 -151.23
217   18.2259  -66.97
218   40.3787 -124.55
219   38.5443 -119.62
220   60.8392 -151.43
221   32.7865 -116.64
222   37.7387 -113.05
223   63.9972 -149.15
224   37.0762 -121.49
225   18.1459  -64.72
226   33.9553 -116.86
227   61.1097 -146.99
228   33.9568 -116.86
229   61.7877 -149.56
230   38.5534 -119.62
231   33.3935 -116.38
232   33.6745 -116.74
233   62.8620 -150.85
235   38.5576 -119.62
236   38.5553 -119.62
237   58.2978 -151.20
238   37.8827 -122.23
239    4.9979   95.96
240   38.8248 -122.83
241   38.7907 -122.74
242   18.1415  -64.06
243   57.3086 -154.87
244   38.1496 -118.03
245   44.4572 -124.69
246   40.0930 -123.75
247   38.5465 -119.63
248   44.4613 -124.66
249   38.8085 -122.83
250   38.1532 -118.03
251   62.9976 -149.59
252   19.4073 -155.28
253   61.3014 -150.83
254   38.8248 -122.82
255   34.3052 -118.72
256   40.0942 -123.75
257   38.5473 -119.62
258   38.5535 -119.62
259   38.5475 -119.62
260   38.8267 -122.86
261   40.4820 -124.63
262   38.5566 -119.62
263   65.0080 -147.32
264   44.4572 -124.67
265   61.2225 -150.78
266   40.3362 -118.31
267   38.1511 -118.00
268   38.1545 -118.02
269   38.5630 -119.62
270   63.9610 -148.83
271   38.5490 -119.62
272   39.6030 -122.03
273   19.4367 -155.44
274   38.5492 -119.61
275   38.5630 -119.63
276   38.5497 -119.64
277   62.1994 -148.71
278   38.5598 -119.62
279   38.8263 -122.86
280   33.0758 -115.00
281   37.2583 -121.62
282   61.2295 -150.84
283   33.1787 -116.02
284   38.1510 -118.02
285   38.8237 -122.75
286   36.5673 -121.12
287   38.1566 -118.03
288   38.8283 -122.85
289   61.2468 -149.64
290   53.1450 -166.64
291   38.1543 -118.01
292   32.5852 -115.71
293   34.8400 -118.98
294   45.0193 -122.59
295   38.5503 -119.63
296   36.8223 -121.55
297   33.8473 -117.49
298   38.7887 -122.76
299   44.4717 -110.70
300   62.6357 -151.28
301   33.2785 -116.78
302   38.8078 -122.79
303   38.8043 -122.81
304   63.5295 -147.42
305   38.8270 -122.85
306   64.8549 -149.57
307   44.6823 -125.60
308   34.6323 -117.13
309   38.8243 -122.79
310   33.8448 -117.50
311   38.0633 -118.94
312   32.5340 -115.63
313   18.8404  -65.22
314   37.1925 -117.54
315   33.2992 -116.25
316   59.9080 -152.71
317   38.7732 -122.92
318   51.5027 -178.74
319   19.6476  -65.24
320   36.0842 -117.84
321   38.1574 -118.07
322   32.9657 -116.25
323   19.3332 -155.05
324   35.9778 -120.55
325   53.5639  142.75
326   39.3790 -120.45
327   61.9769 -150.34
328   19.1537  -64.02
329   39.3740 -120.45
330   40.5212 -124.52
331   51.3091 -178.22
332   48.5097 -122.67
333   38.5760 -119.60
334   61.0910 -150.41
335   38.5802 -119.59
336   19.5214  -64.36
337   38.1587 -118.01
338   34.2918 -116.91
339   63.5595 -147.31
340   36.5927 -121.15
341   36.5958 -121.15
342   62.7692 -150.48
343   38.5611 -119.62
344   38.5611 -119.62
345   40.4415 -125.64
346   38.8427 -122.83
347   63.2587 -151.30
348   38.6078   73.49
349   40.2857 -124.45
350   38.5560 -119.61
351   38.1542 -117.97
352   38.2138 -118.05
353   47.4545 -122.70
354   60.7503 -151.64
355   38.5611 -119.62
356   -4.2135  122.84
357   38.5548 -119.62
358   38.5802 -119.59
359   27.7707   56.41
360   38.5802 -119.59
361   38.5494 -119.62
362   38.5553 -119.62
363   38.5475 -119.62
364   62.3818 -148.39
365   53.5668 -166.81
366   38.5645 -119.61
367   38.5417 -119.66
368   38.7868 -122.75
369   38.8160 -122.82
370   38.5565 -119.62
371   38.5542 -119.59
372   38.5523 -119.62
373   38.5683 -119.62
374   38.5500 -119.62
375   38.5590 -119.62
376   34.0875 -117.30
377   38.8170 -122.82
378   35.9268 -117.70
379   36.6590 -116.34
380   38.7710 -122.72
381   37.1810 -117.34
382   38.8113 -122.80
383   36.0752 -120.65
384   35.6470 -121.00
385   49.8255   87.60
386   62.5670 -151.19
387   33.1358 -116.45
388    9.9707  -84.45
389   38.8107 -122.79
390   65.1882 -146.12
391   36.6530 -121.28
392   38.8108 -122.80
393   38.8118 -122.79
394   36.5612 -121.15
395   50.9494 -179.78
396   37.6987 -119.43
397   37.6047 -119.10
398   34.1578 -116.41
399   62.8605 -149.54
400   59.8096 -153.08
401   33.6763 -116.73
402   40.7610 -124.52
403   37.7260 -122.00
404   38.8215 -122.76
405   39.5588 -111.27
406   47.0395 -122.09
407   38.7518 -122.73
408   27.8766   56.56
409   38.3238 -108.99
410   38.1572 -117.97
411   37.7448 -122.58
412   51.4873 -175.98
413   38.9972 -111.35
414   58.4611 -150.51
415   63.0961 -150.41
416   38.4501 -119.31
417   38.1516 -118.00
418   61.5453 -146.43
419   38.1531 -118.00
420   19.6485  -64.30
421  -16.6170  177.71
422   63.9640 -148.77
423   62.8988 -149.46
424   35.9265 -117.70
425   38.8237 -122.80
426   38.8220 -122.80
427   38.8197 -122.80
428   19.5900  -64.44
429   65.0031 -147.32
430   61.0692 -152.73
431   44.3712 -121.04
432   46.2150 -122.88
433   38.1365 -118.04
434   38.8305 -122.81
435   36.7977 -121.27
436   38.8438 -122.83
437   58.6301 -155.17
438   47.4483 -115.99
439   32.9208 -117.50
440   61.6223 -150.48
441   38.8060 -122.79
442   49.4102 -120.49
443   50.2981 -175.81
444   19.3104  -64.24
445   38.8097 -122.83
446   32.6028 -116.97
447   43.1448  145.71
448   37.8082  141.54
449   61.2406 -150.85
450   35.8845 -118.36
451   18.2180  -66.90
452   34.0027 -116.82
453   60.3398 -152.39
454   36.0717 -120.65
455   38.8248 -122.79
456   38.1564 -118.01
457   37.7342 -112.98
458   37.4787 -118.84
459   37.7667 -113.00
460   36.2338  -89.60
461   36.7615 -121.59
462   51.6016 -178.61
463   38.8353 -122.78
464   38.7948 -122.79
465   66.0779 -151.43
466   51.4445 -178.82
467   37.8437  118.71
468   46.8504 -113.36
469   38.7897 -122.78
470   -3.3941  136.35
471   64.7657 -151.96
472   38.8198 -122.76
473   60.3586 -151.78
474   19.1997 -155.40
475   32.1035 -115.19
476   36.5315 -121.12
477   36.7367 -120.75
478   37.5835 -118.88
479   33.1980 -115.58
480   32.2260 -115.29
481   35.6555 -121.09
482   44.7430 -110.55
483   18.0440  -64.23
484   61.6743 -149.81
485   44.4135 -114.83
486  -14.8280  167.85
487   40.3250 -124.86
488   14.2195  -92.30
489   51.7074 -178.19
490   18.9230  -64.25
491   37.2928 -121.67
492   62.1426 -147.67
493   36.5638 -121.07
494   37.3867 -119.04
495   32.8095 -116.05
496   38.5588 -119.62
497   59.9994 -151.11
498   19.5345  -64.48
499   19.1623  -67.96
500   38.7813 -122.76
501   -9.8025  119.07
502   63.2992 -151.31
503   37.4573 -118.68
504   38.8068 -122.75
505   63.6054 -147.35
506   33.8838 -116.54
507   33.7042 -116.73
508   18.8971  -64.45
509   -3.0297  130.17
510   33.7010 -116.80
511   60.2663 -147.24
512   33.9343 -116.66
514   38.8452 -122.83
515   38.8450 -122.83
516   38.8263 -122.85
517   62.9103 -150.99
518   59.7160 -153.20
519   59.7557 -153.24
520   36.6013 -121.21
521   38.8152 -122.80
522   37.9363 -112.39
523   37.9427 -112.39
524   39.5673 -111.27
525   61.6222 -151.65
526    8.3849  -86.13
527   37.6862 -113.26
528   40.7042 -124.52
530   33.0467 -116.44
531   33.0480 -116.44
532   36.5673 -121.16
533   41.5560  122.98
534   32.8824  -96.98
535   36.8582 -115.97
536   61.3394 -150.91
537   18.0953  -68.48
538   10.1320  -85.50
539   38.8498 -122.82
540   35.9393 -117.67
541   38.8348 -122.78
543   38.7897 -122.76
544   34.2002 -117.49
545   11.6140  -87.08
546   63.0719 -151.43
547   58.5915 -153.55
548   38.8377 -122.78
549   61.5770 -148.23
550   65.0013 -147.33
551   35.0483 -117.67
552   37.5162 -119.35
553    7.4008   93.70
554   33.3377 -117.15
555   35.9812 -120.93
556   42.1982 -122.63
557   36.0710 -120.65
558   47.8657 -122.72
559   62.1865 -149.14
560   18.3306  -68.01
561   62.2312 -150.24
562   63.3164 -151.75
563   40.3723 -125.12
564   51.3195 -178.28
565   52.8690 -164.01
566   60.8913 -152.16
567   55.5875 -135.59
568    9.4880  -84.03
569   63.9225 -148.93
570   53.4807 -167.13
571   38.2642 -118.66
572   46.3650 -122.23
573   38.7602 -122.72
574   64.5573 -149.25
575   32.0983 -115.16
576   57.7804 -156.40
577   63.2947 -149.75
578   62.0568 -145.07
579   38.6357   43.19
581   63.4069 -149.86
582   46.3768 -122.26
583   62.7315 -149.76
584   51.6188 -178.38
585   51.5616 -178.41
586   52.9377 -169.32
587   35.6642 -121.08
588   37.3024 -118.32
589   36.6020 -121.21
590   63.7572 -146.66
591   37.5323 -118.82
592   33.1543 -115.65
593   20.9775 -106.09
594   63.5613 -147.14
595   62.1857 -151.19
596   63.2345 -150.74
597   54.0107 -164.91
598   38.7930 -122.77
600   35.1420 -118.40
601   55.6254 -135.16
602   54.4741 -161.56
603   63.0848 -150.41
604   63.2608 -150.67
605   19.4227 -155.40
606   37.7160 -119.42
607   34.1382   80.18
608   51.8139 -174.51
609   63.4846 -150.90
610   36.3282   68.84
611   38.4915 -122.72
612   63.4742 -146.64
613   45.5687 -121.77
614   55.2415 -134.58
615   38.8178 -122.79
616   47.2943 -122.44
617   44.4937  140.94
618   32.9035 -116.26
619   19.3690 -155.23
620   60.6926 -151.97
621   39.6648  142.94
622   61.5633 -148.45
623   52.1107 -176.10
624   37.6542 -119.43
625   63.1702 -150.79
626   32.1987 -115.28
627   35.7212 -121.08
628   60.8516 -151.67
629   51.5427 -178.49
630   64.4324 -149.52
631   33.3657   48.52
632   52.7174 -164.00
633   32.3390 -115.20
634   35.5617 -118.53
635   39.4774   73.04
636   33.0250 -116.44
637   18.9817 -155.37
638   41.5487 -124.97
639   62.1897 -151.01
641   35.5678 -118.52
642   38.1547 -117.99
643   35.6612 -121.09
644   36.0038 -120.57
645   51.6117 -178.41
646   51.5982 -178.37
647   60.0824 -152.89
648   38.7962 -122.80
649   39.7022 -110.72
650   36.5475 -121.13
651   59.6165 -152.47
652   51.5555 -178.44
653   51.5291 -178.44
654  -61.3005  154.06
655   35.4692 -120.78
656   44.7563 -111.22
657   64.8539 -147.46
658   51.6006 -178.48
659   51.4362 -178.17
660   64.1296 -150.17
661   47.3367 -120.02
663   63.2111 -150.53
664   18.3045  -65.62
665   51.5809 -178.48
666   63.4099 -149.76
667   36.3042 -120.83
668   32.6622 -115.80
669   51.5847 -178.44
670   62.9650 -148.08
671   33.4373 -116.56
672   51.5371 -178.45
673   45.3778 -112.60
674   63.2492 -151.13
675   36.9107 -121.09
676   32.1947 -115.25
677   62.3600 -149.04
678   63.4375 -147.57
679   55.4698 -134.95
680   36.6558 -121.28
681   60.1955 -152.90
682   54.4216 -161.50
683   59.7137 -136.07
684   51.5468 -178.44
685   41.6318 -112.63
686   19.4872 -155.67
687   51.5935 -178.47
688   62.8885 -150.56
689   62.9178 -150.54
690   63.4415 -147.58
691   34.3372 -116.94
692   19.6879  -64.33
693   62.8634 -150.02
694   61.4181 -146.76
695   37.9130 -118.18
696   62.8550 -150.48
697   63.3706 -151.51
698   34.0067 -119.22
699   51.5989 -178.42
700   38.7018 -122.80
701   53.6889 -166.41
702   62.4281 -149.61
703   51.6001 -178.45
704   63.9221 -148.90
705   61.7608 -148.40
706   62.7366 -152.01
707   51.6213 -178.43
708   58.3223 -138.11
709   34.6097 -119.03
710   63.5119 -150.88
711   36.3107 -120.85
712   51.4176 -174.15
713   38.8250 -122.77
714   49.9972  179.26
715   51.6417 -178.42
716   52.1973 -178.65
717   43.8900 -122.98
718   35.6582 -121.09
719   51.7309 -178.48
720   19.4650 -155.34
721   38.1417 -118.01
722   51.5470 -178.19
723   51.5877 -178.41
724   65.0300 -147.57
725   51.6348 -178.39
726   35.7258 -117.66
727   35.0310 -117.68
728   51.6276 -178.46
729   40.4338 -122.14
730   36.6515 -121.27
731   51.6106 -178.43
732   33.3505 -116.30
733   58.4531 -136.87
734   38.8093 -122.80
735   60.3847 -147.74
736   51.5530 -178.47
737   33.2195 -116.08
738    5.0087   96.04
739   48.0692 -122.88
741    4.9611   96.08
742   49.4627 -120.51
743   51.6002 -178.11
744   38.8003 -122.79
745   51.5240 -178.43
746   37.9630 -112.38
747   48.0907 -121.93
748   63.5303 -150.83
749   60.8998 -146.45
750   39.9710 -118.78
751   65.8181 -150.94
752   55.5908 -135.02
753   37.4022 -118.48
754   62.6873 -149.53
755   47.4183 -113.43
756   30.3641   57.47
757   35.8320  140.87
758   51.6652 -178.53
759   61.5414 -141.26
760   18.7803  -64.23
761   51.5645 -178.45
762   35.0483 -118.36
763   38.8203 -122.77
764   -4.4449  134.85
765   51.1596  179.66
766   60.3766 -152.15
767   38.7990 -122.73
768   54.1910 -164.21
769   34.9757 -118.56
770   38.1556 -118.01
771   51.6027 -178.06
772   51.6095 -178.46
773   34.9767 -118.56
774   38.7912 -122.78
775   36.0303 -117.82
776   63.2831 -151.46
777   33.5997 -116.82
778   32.5493 -115.65
779   36.8288 -121.28
780   51.5820 -178.40
781   63.5122 -145.97
782   38.8228 -122.81
783   53.1350 -166.80
784  -20.4981  170.62
785   61.4241 -146.36
786   51.5990 -178.46
787   52.0532 -178.59
788   51.5920 -178.44
789   37.5385 -118.86
790   51.5599 -178.47
791   33.9772 -116.31
792   38.8397 -122.76
793   59.4492 -152.76
794   51.5891 -178.40
795   39.9998 -122.88
796   34.6048 -116.61
797   35.3537 -118.64
798   51.6318 -178.54
799   39.5232 -123.32
800   37.5235 -121.80
801   59.4378 -153.13
802   44.6933 -111.90
803   51.6083 -178.40
804   51.5368 -178.44
805   34.6278 -116.54
806   59.6577 -153.19
807   33.6342 -116.70
808   33.0118 -116.36
809   57.2825 -155.76
810   51.5860 -178.43
811   51.6085 -178.40
812   55.0582 -159.68
813   51.6291 -178.44
814   51.5019 -178.54
815   52.1900 -175.92
816   51.5825 -178.42
817   51.6296 -178.48
818   51.6546 -178.47
819   51.6290 -178.43
820   19.3341  -64.26
821   36.2965 -120.84
822   62.2448 -150.99
823   51.5899 -178.45
824   63.3525 -145.34
825   51.5998 -178.46
826   51.6087 -178.52
827   51.5920 -178.43
828   38.8158 -122.80
829   40.2647 -123.10
830   51.6270 -178.34
831   38.8373 -122.80
832   33.5165 -116.46
833   37.9467 -112.39
834   64.4853 -146.45
835   52.5859 -170.61
836   48.5155 -122.66
837   33.0958 -115.80
838   61.7606 -148.41
839   38.4228 -122.43
840   11.5523  -87.36
841   38.8108 -122.79
842   19.6707  -64.32
843   17.3561  -68.87
844   63.3780 -151.47
845   60.6203 -145.24
846   37.9432 -112.38
847   62.8670 -150.43
848   38.8100 -122.79
849   37.2907 -119.94
850   37.4330 -118.56
851   37.3107 -114.97
852   18.5608  -66.69
853   62.0646 -145.10
854   36.5327 -121.12
855   59.1431 -153.96
856   42.2173 -124.57
857   52.0677 -175.83
858   63.2969 -151.35
859   60.9684 -151.97
860   33.3882 -116.38
861   61.6786 -146.50
862   37.6657 -119.42
863   37.9565 -112.39
864   63.5022 -147.36
865   37.9498 -112.39
866   33.0852 -115.78
867   33.0868 -115.78
868   36.8908 -121.40
869   60.5603 -152.22
870   38.7860 -122.90
871   62.2417 -149.69
872   38.8192 -122.81
873   61.3309 -151.10
874   56.9411 -154.22
875   57.1706 -154.48
876   38.8100 -122.79
877   55.6295 -135.00
878   33.2755 -116.78
879   63.3597 -145.43
880   63.1893 -143.10
881   18.5361  -64.56
882   38.8432 -122.83
883   35.8277 -117.74
884   38.8103 -122.78
885   32.5498 -115.65
886   32.5505 -115.65
887   19.6674  -64.42
888   63.3165 -151.07
889   19.4720  -64.25
890   56.0504 -135.32
891   39.2290 -110.47
892   62.9395 -151.24
893   34.2865 -116.81
894   64.6381 -149.20
895   -0.1371  124.73
896   45.6175 -111.74
897   61.1266 -150.26
898   63.7488 -146.83
899   38.7910 -122.75
900   62.6786 -150.44
901   44.8098 -112.97
902   37.9513 -112.38
903   63.3112 -151.32
904   57.8571 -153.96
905   38.0527 -118.94
906   34.7858 -119.48
907   37.5720 -122.54
908   37.5670 -122.55
909   63.1454 -150.52
910   60.2145 -147.17
911   63.3195 -151.34
912   36.3060 -120.84
913   67.6639 -149.02
914   61.0038 -150.91
915   37.9515 -112.39
916   39.2230 -123.23
917   35.0445 -117.68
918   37.9542 -112.38
919   37.9508 -112.39
920   37.9608 -112.38
921   37.9587 -112.39
922   37.9335 -112.37
923   45.6727 -122.56
924   37.9423 -112.38
925   53.8764  -35.18
926   63.0774 -149.47
927   61.1894 -148.44
928   32.5440 -115.65
929   37.9495 -112.38
930   63.2677 -151.33
931   63.3080 -151.34
932   16.7111  -98.12
933   63.2959 -151.35
934   63.3121 -151.33
935   18.1408  -67.26
936   37.9578 -112.39
937   62.1946 -150.41
938   54.0531  -35.16
939   62.4175 -151.41
940   54.0696  -35.12
941   54.0041  -35.08
942   32.5317 -115.65
943   33.5343 -115.89
944   63.2808 -151.49
945    9.9978  -85.28
946   38.1982 -118.12
947   36.6770 -121.31
948   38.1377 -118.03
949   17.9978  -67.02
950   19.3335 -155.19
951   32.5303 -115.66
952   38.0438 -117.67
953   34.0172 -117.22
954   36.4625 -121.04
955   18.2803  -63.97
956   33.9485 -117.01
957   33.3200 -116.89
958   37.9485 -112.38
959   62.7603 -149.49
960   37.9580 -112.39
961   55.4932 -134.99
962   37.3618 -114.94
963   61.8596 -150.45
964   44.7498 -111.23
965   12.6290  -87.74
966   24.7542  122.56
967   38.8295 -122.85
968   36.8422 -121.44
969   51.1400    5.96
970   38.1782 -118.07
971   59.7883 -152.93
972   32.2057 -115.29
973   38.1538 -118.04
974   38.7923 -122.75
975   19.4018 -155.28
976   64.8805 -148.98
977   34.0193 -116.61
978   38.1471 -118.01
979   38.7693 -122.74
980   36.8882 -121.40
981   38.1544 -118.01
982   38.1510 -117.99
983   38.7182 -122.65
984   35.5083 -119.91
985   32.2040 -115.27
986   31.6199   46.02
987   38.1703 -118.04
988   33.0303 -115.61
989   38.0433 -118.80
990   38.1370 -118.03
991   55.6879 -135.48
992   38.5491 -117.26
993   33.8322 -116.73
994   37.8375 -118.38
995   38.1482 -118.04
996   37.5318 -118.82
997   34.3153 -119.51
998   63.7318 -149.20
999   58.5496 -152.28
1000  38.1516 -118.00
1002  19.1725  -64.78
1003  35.7222 -121.05
1004  38.1474 -117.96
1005  38.1477 -118.03
1006  19.2785 -155.49
1007  19.3309  -68.84
1008  58.1465 -136.84
1009  63.4700 -146.01
1011  36.1667 -120.72
1012  33.6023 -116.81
1013  63.2774 -150.73
1014  61.2394 -150.82
1015  51.2777 -177.91
1016  52.6831 -164.74
1017  62.9112 -151.07
1018  38.1585 -118.02
1019  18.8827  -64.26
1020  64.7907  146.60
1021  33.6795 -116.73
1022  34.9877 -116.95
1023  36.6537 -121.28
1024  32.2582 -115.33
1025  36.3047 -120.85
1026  38.1540 -118.20
1027  38.1559 -118.00
1028  32.4618 -115.58
1029  52.9684 -164.39
1030  61.0500 -145.42
1031  34.2215 -117.25
1032  33.7790 -116.17
1033  61.5895 -148.26
1034  31.8438 -116.73
1035  36.4735 -122.49
1036  16.9220  -98.18
1037  19.3848 -155.28
1038  38.8215 -122.76
1039  -6.6199  130.16
1040  38.1513 -118.03
1041  61.0106 -150.19
1042  61.6215 -152.12
1043  38.1574 -118.05
1044  38.1574 -118.05
1045  38.1574 -118.05
1046  38.1574 -118.02
1047  38.1587 -117.99
1048  19.4741  -67.88
1049  18.4955  -66.12
1050  38.7827 -122.73
1051  33.9340 -120.56
1052  61.9727 -150.58
1053  55.7978 -135.16
1054  19.1560 -155.43
1055  51.6937 -175.24
1056  55.6001 -162.13
1057  38.1536 -118.00
```



---

## Peer review experiment data

* Data on submissions/reviews in an experiment 

<img class=center src=assets/img/cooperation.png height='60%'/>

[http://www.plosone.org/article/info:doi/10.1371/journal.pone.0026895](http://www.plosone.org/article/info:doi/10.1371/journal.pone.0026895)


---

## Peer review data



```r
fileUrl1 <- "https://dl.dropbox.com/u/7710864/data/reviews-apr29.csv"
fileUrl2 <- "https://dl.dropbox.com/u/7710864/data/solutions-apr29.csv"
download.file(fileUrl1,destfile="./data/reviews.csv",method="curl")
download.file(fileUrl2,destfile="./data/solutions.csv",method="curl")
reviews <- read.csv("./data/reviews.csv"); solutions <- read.csv("./data/solutions.csv")
head(reviews,2)
```

```
  id solution_id reviewer_id      start       stop time_left accept
1  1           3          27 1304095698 1304095758      1754      1
2  2           4          22 1304095188 1304095206      2306      1
```

```r
head(solutions,2)
```

```
  id problem_id subject_id      start       stop time_left answer
1  1        156         29 1304095119 1304095169      2343      B
2  2        269         25 1304095119 1304095183      2329      C
```


---

## Find if there are missing values - is.na()


```r
is.na(reviews$time_left[1:10])
```

```
 [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
```

```r
sum(is.na(reviews$time_left))
```

```
[1] 84
```

```r
table(is.na(reviews$time_left))
```

```

FALSE  TRUE 
  115    84 
```


---

## Important table()/NA issue


```r
table(c(0,1,2,3,NA,3,3,2,2,3))
```

```

0 1 2 3 
1 1 3 4 
```

```r
table(c(0,1,2,3,NA,3,3,2,2,3),useNA="ifany")
```

```

   0    1    2    3 <NA> 
   1    1    3    4    1 
```


---

## Summarizing columns/rows - rowSums(),rowMeans(),colSums(),colMeans()

* Important parameters: _x_, _na.rm_

```r
colSums(reviews)
```

```
         id solution_id reviewer_id       start        stop 
      19900       19929        5064          NA          NA 
  time_left      accept 
         NA          NA 
```


---

## Summarizing columns/rows - rowSums(),rowMeans(),colSums(),colMeans()


```r
colMeans(reviews,na.rm=TRUE)
```

```
         id solution_id reviewer_id       start        stop 
  1.000e+02   1.001e+02   2.545e+01   1.304e+09   1.304e+09 
  time_left      accept 
  1.114e+03   6.435e-01 
```

```r
rowMeans(reviews,na.rm=TRUE)
```

```
  [1] 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.726e+08
  [7] 3.726e+08 1.300e+01 3.726e+08 3.726e+08 3.726e+08 3.726e+08
 [13] 3.726e+08 3.726e+08 3.726e+08 3.726e+08 1.967e+01 3.726e+08
 [19] 3.726e+08 1.933e+01 3.726e+08 3.726e+08 3.726e+08 2.433e+01
 [25] 2.367e+01 2.367e+01 3.726e+08 3.726e+08 3.726e+08 3.726e+08
 [31] 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.133e+01 3.726e+08
 [37] 3.267e+01 3.726e+08 3.400e+01 3.726e+08 3.200e+01 3.726e+08
 [43] 3.833e+01 3.633e+01 3.726e+08 3.726e+08 3.726e+08 3.726e+08
 [49] 3.726e+08 3.726e+08 4.167e+01 3.726e+08 4.433e+01 3.726e+08
 [55] 3.726e+08 3.726e+08 3.726e+08 3.726e+08 4.800e+01 4.633e+01
 [61] 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.726e+08 5.333e+01
 [67] 3.726e+08 3.726e+08 5.533e+01 5.567e+01 3.726e+08 5.533e+01
 [73] 3.726e+08 3.726e+08 3.726e+08 5.900e+01 3.726e+08 3.726e+08
 [79] 3.726e+08 3.726e+08 6.267e+01 3.726e+08 3.726e+08 6.433e+01
 [85] 3.726e+08 6.600e+01 3.726e+08 3.726e+08 6.833e+01 6.900e+01
 [91] 3.726e+08 7.000e+01 7.033e+01 3.726e+08 3.726e+08 3.726e+08
 [97] 7.333e+01 3.726e+08 7.433e+01 3.726e+08 3.726e+08 7.600e+01
[103] 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.726e+08
[109] 3.726e+08 3.726e+08 3.726e+08 7.267e+01 3.726e+08 8.567e+01
[115] 8.633e+01 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.726e+08
[121] 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.726e+08 3.726e+08
[127] 3.726e+08 3.726e+08 3.726e+08 9.433e+01 9.600e+01 9.700e+01
[133] 3.726e+08 3.726e+08 9.967e+01 3.726e+08 9.333e+01 3.726e+08
[139] 3.726e+08 3.726e+08 3.726e+08 1.030e+02 1.027e+02 1.043e+02
[145] 3.726e+08 3.726e+08 3.726e+08 3.726e+08 1.080e+02 1.083e+02
[151] 1.090e+02 1.097e+02 1.113e+02 1.107e+02 1.113e+02 1.123e+02
[157] 3.726e+08 1.127e+02 3.726e+08 3.726e+08 1.157e+02 1.177e+02
[163] 1.120e+02 1.170e+02 1.197e+02 1.183e+02 1.200e+02 3.726e+08
[169] 1.213e+02 1.213e+02 3.726e+08 1.257e+02 3.726e+08 1.213e+02
[175] 1.240e+02 1.257e+02 1.270e+02 1.263e+02 3.726e+08 1.287e+02
[181] 1.293e+02 1.293e+02 1.290e+02 1.303e+02 1.327e+02 1.333e+02
[187] 1.343e+02 1.340e+02 3.726e+08 1.357e+02 1.370e+02 3.726e+08
[193] 1.390e+02 1.383e+02 1.367e+02 1.410e+02 1.397e+02 1.420e+02
[199] 1.393e+02
```





