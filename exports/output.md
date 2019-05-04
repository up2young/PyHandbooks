
# Python IO相关


```python
import tushare as ts
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt 
import datetime
import tabula
```

## 用户输入


```python
str = input('请输入文件名：')
print(str)
```

    请输入文件名： filename
    

    filename
    

## 读取网页数据


```python
df_web = pd.read_html('http://www.multpl.com/table?f=m',header=0)
df_web[0].head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Value Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>May 3, 2019</td>
      <td>22.25 estimate</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apr 1, 2019</td>
      <td>21.66 estimate</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mar 1, 2019</td>
      <td>21.27 estimate</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Feb 1, 2019</td>
      <td>21.09 estimate</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jan 1, 2019</td>
      <td>19.66 estimate</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_web = pd.read_html('http://finance.stockstar.com/finance/macrodata/gdp.htm')
df_web[1]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>数据日期</th>
      <th colspan="2" halign="left">国内生产总值</th>
      <th colspan="2" halign="left">第一产业</th>
      <th colspan="2" halign="left">第二产业</th>
      <th colspan="2" halign="left">第三产业</th>
    </tr>
    <tr>
      <th></th>
      <th>数据日期</th>
      <th>绝对额</th>
      <th>同比增减</th>
      <th>绝对额</th>
      <th>同比增减</th>
      <th>绝对额</th>
      <th>同比增减</th>
      <th>绝对额</th>
      <th>同比增减</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018年一至四季度</td>
      <td>900309.0</td>
      <td>6.60%</td>
      <td>64734.0</td>
      <td>3.50%</td>
      <td>366001.0</td>
      <td>5.80%</td>
      <td>469575.0</td>
      <td>7.60%</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018年一至三季度</td>
      <td>650899.0</td>
      <td>6.70%</td>
      <td>42173.0</td>
      <td>3.40%</td>
      <td>262953.0</td>
      <td>5.80%</td>
      <td>345773.0</td>
      <td>7.70%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018年一至二季度</td>
      <td>418961.0</td>
      <td>6.80%</td>
      <td>22087.0</td>
      <td>3.20%</td>
      <td>169299.0</td>
      <td>6.10%</td>
      <td>227576.0</td>
      <td>7.60%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018年一季度</td>
      <td>198783.0</td>
      <td>6.80%</td>
      <td>8904.0</td>
      <td>3.20%</td>
      <td>77451.0</td>
      <td>6.30%</td>
      <td>112428.0</td>
      <td>7.50%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017年一至四季度</td>
      <td>820754.0</td>
      <td>6.80%</td>
      <td>62100.0</td>
      <td>4.00%</td>
      <td>332743.0</td>
      <td>5.90%</td>
      <td>425912.0</td>
      <td>7.90%</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2017年一至三季度</td>
      <td>593288.0</td>
      <td>6.90%</td>
      <td>41229.0</td>
      <td>3.70%</td>
      <td>238109.0</td>
      <td>6.30%</td>
      <td>313951.0</td>
      <td>7.80%</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2017年一至二季度</td>
      <td>381490.0</td>
      <td>6.90%</td>
      <td>21987.0</td>
      <td>3.50%</td>
      <td>152987.0</td>
      <td>6.40%</td>
      <td>206516.0</td>
      <td>7.70%</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017年一季度</td>
      <td>180683.0</td>
      <td>6.90%</td>
      <td>8654.0</td>
      <td>3.00%</td>
      <td>70005.0</td>
      <td>6.40%</td>
      <td>102024.0</td>
      <td>7.70%</td>
    </tr>
  </tbody>
</table>
</div>



## 使用tabula库读取PDF表格数据（需java环境）
[查看文档](https://github.com/chezou/tabula-py)


```python
#需安装java，检查环境
tabula.environment_info()
```

    Python version:
        3.7.2 (default, Feb 21 2019, 17:35:59) [MSC v.1915 64 bit (AMD64)]
    Java version:
        java version "1.8.0_201"
    Java(TM) SE Runtime Environment (build 1.8.0_201-b09)
    Java HotSpot(TM) Client VM (build 25.201-b09, mixed mode, sharing)
    tabula-py version: 1.3.1
    platform: Windows-10-10.0.17134-SP0
    uname:
        uname_result(system='Windows', node='DESKTOP-VV14MB0', release='10', version='10.0.17134', machine='AMD64', processor='Intel64 Family 6 Model 158 Stepping 10, GenuineIntel')
    linux_distribution: ('', '', '')
    mac_ver: ('', ('', '', ''), '')
        
    


```python
df_pdf = tabula.read_pdf('http://kcb.cs.com.cn/file/projectAudit/audit/pdftemp/6cb9b97495db4b80aeeb99eac8e35c49.pdf',pages=3)
df_pdf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>证券种类</th>
      <th>中国存托凭证(CDR)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>本次拟向存托人发行不超过7,040,917股A类普通股股票,作为拟</td>
    </tr>
    <tr>
      <th>1</th>
      <td>发行基础股票数量</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>转换为CDR的基础股票,占CDR发行后总股本的比例不低于10%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>基础股票与CDR之间的</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>按照1股/10份CDR的比例进行转换</td>
    </tr>
    <tr>
      <th>5</th>
      <td>转换比例</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>发行价格</td>
      <td>人民币【】元/CDR</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>-117.98元(按2018年12月31日经审计的归属于母公司所有者权</td>
    </tr>
    <tr>
      <th>8</th>
      <td>发行前每股净资产</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>益除以本次发行前总股本计算)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>【】元(按2018年12月31日经审计的归属于母公司所有者权益</td>
    </tr>
    <tr>
      <th>11</th>
      <td>发行后每股净资产</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>NaN</td>
      <td>与预计的募集资金净额之和除以本次发行后总股本计算)</td>
    </tr>
    <tr>
      <th>13</th>
      <td>预计发行日期</td>
      <td>【】年【】月【】日</td>
    </tr>
    <tr>
      <th>14</th>
      <td>拟上市的交易所和板块</td>
      <td>上海证券交易所科创板</td>
    </tr>
    <tr>
      <th>15</th>
      <td>CDR发行后总股本</td>
      <td>不超过70,409,167股</td>
    </tr>
    <tr>
      <th>16</th>
      <td>NaN</td>
      <td>保荐机构将安排子公司国泰君安证裕投资有限公司参与本次发</td>
    </tr>
    <tr>
      <th>17</th>
      <td>保荐人相关子公司拟参与</td>
      <td>行战略配售,具体按照上交所相关规定执行。保荐机构及其相</td>
    </tr>
    <tr>
      <th>18</th>
      <td>战略配售情况</td>
      <td>关子公司后续将按要求进一步明确参与本次发行战略配售的具</td>
    </tr>
    <tr>
      <th>19</th>
      <td>NaN</td>
      <td>体方案,并按规定向上交所提交相关文件</td>
    </tr>
    <tr>
      <th>20</th>
      <td>发行方式</td>
      <td>CDR发行采用询价方式确定价格</td>
    </tr>
    <tr>
      <th>21</th>
      <td>NaN</td>
      <td>符合资格的询价对象和符合法律法规规定的自然人、法人及其</td>
    </tr>
    <tr>
      <th>22</th>
      <td>发行对象</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>23</th>
      <td>NaN</td>
      <td>他投资者(国家法律、法规禁止购买者除外)</td>
    </tr>
    <tr>
      <th>24</th>
      <td>承销方式</td>
      <td>余额包销</td>
    </tr>
    <tr>
      <th>25</th>
      <td>保荐机构(主承销商)</td>
      <td>国泰君安证券股份有限公司</td>
    </tr>
    <tr>
      <th>26</th>
      <td>招股说明书签署日期</td>
      <td>2019年4月【】日</td>
    </tr>
  </tbody>
</table>
</div>




```python
#如发现读取内容不符合预期，可尝试指定lattice=True或steam=True
df_pdf = tabula.read_pdf('datas/test.pdf',pages='33-35',multiple_tables=True,lattice=True)
```


```python
len(df_pdf)
df_pdf[4]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>项目</td>
      <td>2018.12.31</td>
      <td>2017.12.31</td>
      <td>2016.12.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>资产总额(万元)</td>
      <td>370,114.28</td>
      <td>195,293.49</td>
      <td>128,273.43</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>归属于母公司所有者权益(万元)</td>
      <td>-323,049.02</td>
      <td>-126,498.13</td>
      <td>-72,033.34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>资产负债率(合并)</td>
      <td>187.28%</td>
      <td>164.77%</td>
      <td>156.16%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>项目</td>
      <td>2018 年度</td>
      <td>2017 年度</td>
      <td>2016 年度</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>营业收入(万元)</td>
      <td>424,764.87</td>
      <td>138,130.14</td>
      <td>115,287.77</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>净利润(万元)</td>
      <td>-179,927.81</td>
      <td>-62,726.81</td>
      <td>-15,760.42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>归属于母公司所有者的净利润\r(万元)</td>
      <td>-179,927.81</td>
      <td>-62,726.81</td>
      <td>-15,760.42</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>扣除非经常性损益后归属于母公司\r所有者的净利润(万元)</td>
      <td>54,389.08</td>
      <td>-6,160.47</td>
      <td>4,440.18</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>基本每股收益(元)</td>
      <td>-65.71</td>
      <td>-22.92</td>
      <td>-5.76</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>稀释每股收益(元)</td>
      <td>不适用</td>
      <td>不适用</td>
      <td>不适用</td>
    </tr>
    <tr>
      <th>11</th>
      <td>NaN</td>
      <td>每份存托凭证对应的基本每股收益\r(元)</td>
      <td>-6.57</td>
      <td>-2.29</td>
      <td>-0.58</td>
    </tr>
    <tr>
      <th>12</th>
      <td>NaN</td>
      <td>每份存托凭证对应的稀释每股收益\r(元)</td>
      <td>不适用</td>
      <td>不适用</td>
      <td>不适用</td>
    </tr>
    <tr>
      <th>13</th>
      <td>NaN</td>
      <td>加权平均净资产收益率(%)</td>
      <td>不适用</td>
      <td>不适用</td>
      <td>不适用</td>
    </tr>
    <tr>
      <th>14</th>
      <td>NaN</td>
      <td>经营活动产生的现金流量净额\r(万元)</td>
      <td>37,660.68</td>
      <td>13,747.64</td>
      <td>-4,513.85</td>
    </tr>
    <tr>
      <th>15</th>
      <td>NaN</td>
      <td>每份存托凭证对应经营活动产生的\r现金流量(元)</td>
      <td>1.38</td>
      <td>0.50</td>
      <td>-0.16</td>
    </tr>
    <tr>
      <th>16</th>
      <td>NaN</td>
      <td>每份存托凭证对应净现金流量(元)</td>
      <td>2.36</td>
      <td>0.68</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>17</th>
      <td>NaN</td>
      <td>每份存托凭证对应净资产(元)</td>
      <td>-11.80</td>
      <td>-4.62</td>
      <td>-2.63</td>
    </tr>
    <tr>
      <th>18</th>
      <td>NaN</td>
      <td>现金分红(万元)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>NaN</td>
      <td>研发投入占营业收入的比例</td>
      <td>2.90%</td>
      <td>6.61%</td>
      <td>6.19%</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_pdf = tabula.read_pdf('datas/test.pdf',pages='all',multiple_tables=True,lattice=True)
```


```python
len(df_pdf)
#df_pdf[300]
```




    577



## 使用nbconvert进行格式化输出
nbconvert除了通过命令行调用，还可作为library来使用，配合自定义模板，非常有潜力，[官方文档](https://nbconvert.readthedocs.io/en/latest/index.html)
* --TemplateExporter.exclude_code_cell 使用该参数可以控制需要导出的内容，可选项如下：

```
"exclude_output": exclude_output,
"exclude_input": exclude_input,
"exclude_input_prompt": exclude_input_prompt,
"exclude_output_prompt": exclude_output_prompt,
"exclude_markdown": exclude_markdown,
"exclude_code_cell": exclude_code_cell
```
注意如果需要保留markdown和输出内容要使用--TemplateExporter.exclude_input=True，而不是exclude_code_cell，否则效果是仅保留markdown的内容，[更多参数](https://nbconvert.readthedocs.io/en/latest/config_options.html)


```python
!jupyter nbconvert IO.ipynb --to html --output exports/output.html --TemplateExporter.exclude_input=True
```

    [NbConvertApp] Converting notebook IO.ipynb to html
    [NbConvertApp] Writing 277138 bytes to exports/output.html
    


```python
!jupyter nbconvert IO.ipynb --to markdown --output exports/output.md 
```

    [NbConvertApp] Converting notebook IO.ipynb to markdown
    [NbConvertApp] Writing 2102 bytes to exports/output.md
    


```python
!jupyter nbconvert IO.ipynb --to html --template basic --output exports/output.html
```

    [NbConvertApp] Converting notebook IO.ipynb to html
    [NbConvertApp] Writing 11710 bytes to exports/output.html
    


```python
#当前环境直接转换，可指定排除不需要的内容
#!jupyter nbconvert IO.ipynb --to python --stdout 
```
