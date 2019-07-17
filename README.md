# Python-Parse-Autosar-Armxl
Analysis of automotive electronic matrix file ARXML file based on python

* you have a  basic knowledge on python
* [XPATH](http://www.w3school.com.cn/xpath/xpath_syntax.asp)
* [xml.etree.ElementTree 语法](https://docs.python.org/3/library/xml.etree.elementtree.html)

*****
*****
## load arxml file
```python
import re
import xml.etree.ElementTree as ET
tree = ET.parse('FLC2_SystemExtract_19011.arxml')
root = tree.getroot()
root.tag
```




    '{http://autosar.org/schema/r4.0}AUTOSAR'
    
    
```python
root2 = root[1] # 第2个 AR-PACKAGE 标签
```


```python
Communication = root2.findall("./{http://autosar.org/schema/r4.0}AR-PACKAGES/{http://autosar.org/schema/r4.0}AR-PACKAGE")

```


```python
Communication
```




    [<Element '{http://autosar.org/schema/r4.0}AR-PACKAGE' at 0x000002C9599A1188>,
     <Element '{http://autosar.org/schema/r4.0}AR-PACKAGE' at 0x000002C959A84E08>,
     <Element '{http://autosar.org/schema/r4.0}AR-PACKAGE' at 0x000002C959AA05E8>,
     <Element '{http://autosar.org/schema/r4.0}AR-PACKAGE' at 0x000002C95C759D68>,
     <Element '{http://autosar.org/schema/r4.0}AR-PACKAGE' at 0x000002C95CDD3F98>,
     <Element '{http://autosar.org/schema/r4.0}AR-PACKAGE' at 0x000002C95CE63818>,
     <Element '{http://autosar.org/schema/r4.0}AR-PACKAGE' at 0x000002C95CE74778>,
     <Element '{http://autosar.org/schema/r4.0}AR-PACKAGE' at 0x000002C95E27A228>]




```python
for child in Communication:
    print(child.tag ,child.attrib)
```

    {http://autosar.org/schema/r4.0}AR-PACKAGE {'UUID': '74a341ea-6fb6-4673-a778-ea0131d1e5eb-Communication-Frame'}
    {http://autosar.org/schema/r4.0}AR-PACKAGE {'UUID': '74a341ea-6fb6-4673-a778-ea0131d1e5eb-Communication-Gateway'}
    {http://autosar.org/schema/r4.0}AR-PACKAGE {'UUID': '74a341ea-6fb6-4673-a778-ea0131d1e5eb-Communication-ISignal'}
    {http://autosar.org/schema/r4.0}AR-PACKAGE {'UUID': '74a341ea-6fb6-4673-a778-ea0131d1e5eb-Communication-ISignalGroup'}
    {http://autosar.org/schema/r4.0}AR-PACKAGE {'UUID': '74a341ea-6fb6-4673-a778-ea0131d1e5eb-Communication-ISignalPduGroup'}
    {http://autosar.org/schema/r4.0}AR-PACKAGE {'UUID': '74a341ea-6fb6-4673-a778-ea0131d1e5eb-Communication-NmConfig'}
    {http://autosar.org/schema/r4.0}AR-PACKAGE {'UUID': '74a341ea-6fb6-4673-a778-ea0131d1e5eb-Communication-Pdu'}
    {http://autosar.org/schema/r4.0}AR-PACKAGE {'UUID': '74a341ea-6fb6-4673-a778-ea0131d1e5eb-Communication-TpConfig'}
    

# *获取所有的frame*


```python
ELEMENTS = Communication[0].findall(".//{http://autosar.org/schema/r4.0}ELEMENTS/*")
```


```python
frames = [child[0].text for child in ELEMENTS]
```


```python
frames
```




    ['ASDMCanFD2TimeSynchFr',
     'ASDMFlcFlexTimeSynchFr',
     'ASDMSafetyCANFD2Frame5',
     'ASDMSafetyCANFD2Frame6',
     'AsdmFLC_FlexrayFr00',
     'AsdmFLC_FlexrayFr01',
     'AsdmFLC_FlexrayFr02',
     'AsdmFLC_FlexrayFr03',
     'AsdmFLC_FlexrayNMFr',
     'AsdmFlcFrDiagReqFrame1',
     'AsdmFlcFrDiagReqFrame2',
     'AsdmFlcFrDiagReqFrame3',
     'AsdmFlcFrDiagReqFrame4',
     'BbmAdRedundancyFr01',
     'BbmAdRedundancyFr02',
     'BbmAdRedundancyFr03',
     'BbmAdRedundancyFr04',
     'BbmAdRedundancyFr05',
     'BbmAdRedundancyFr06',
     'BbmAdRedundancyFr07',
     'BbmAdRedundancyFr08',
     'BbmAdRedundancyFr10',
     'BbmAdRedundancyFr11',
     'BbmAdRedundancyFr12',
     'FlcADRedundancyNMFr',
     'FlcAdRedundancyFr01',
     'FlcAdRedundancyFr02',
     'FlcAdRedundancyFr03',
     'FlcAdRedundancyFr05',
     'FlcAdRedundancyFr06',
     'FlcAdRedundancyFr07',
     'FlcFLC_FlexrayCalDataFr01',
     'FlcFLC_FlexrayFr01',
     'FlcFLC_FlexrayFr02',
     'FlcFLC_FlexrayFr03',
     'FlcFLC_FlexrayFr04',
     'FlcFLC_FlexrayFr05',
     'FlcFLC_FlexrayFr06',
     'FlcFLC_FlexrayFr07',
     'FlcFLC_FlexrayFr08',
     'FlcFLC_FlexrayFr09',
     'FlcFLC_FlexrayFr10',
     'FlcFLC_FlexrayFr100',
     'FlcFLC_FlexrayFr101',
     'FlcFLC_FlexrayFr102',
     'FlcFLC_FlexrayFr103',
     'FlcFLC_FlexrayFr104',
     'FlcFLC_FlexrayFr105',
     'FlcFLC_FlexrayFr106',
     'FlcFLC_FlexrayFr107',
     'FlcFLC_FlexrayFr108',
     'FlcFLC_FlexrayFr109',
     'FlcFLC_FlexrayFr111',
     'FlcFLC_FlexrayFr124',
     'FlcFLC_FlexrayFr126',
     'FlcFLC_FlexrayFr127',
     'FlcFLC_FlexrayFr129',
     'FlcFLC_FlexrayFr131',
     'FlcFLC_FlexrayFr133',
     'FlcFLC_FlexrayFr135',
     'FlcFLC_FlexrayFr137',
     'FlcFLC_FlexrayFr139',
     'FlcFLC_FlexrayFr14',
     'FlcFLC_FlexrayFr141',
     'FlcFLC_FlexrayFr142',
     'FlcFLC_FlexrayFr144',
     'FlcFLC_FlexrayFr145',
     'FlcFLC_FlexrayFr147',
     'FlcFLC_FlexrayFr149',
     'FlcFLC_FlexrayFr15',
     'FlcFLC_FlexrayFr152',
     'FlcFLC_FlexrayFr155',
     'FlcFLC_FlexrayFr158',
     'FlcFLC_FlexrayFr16',
     'FlcFLC_FlexrayFr161',
     'FlcFLC_FlexrayFr164',
     'FlcFLC_FlexrayFr167',
     'FlcFLC_FlexrayFr17',
     'FlcFLC_FlexrayFr170',
     'FlcFLC_FlexrayFr173',
     'FlcFLC_FlexrayFr176',
     'FlcFLC_FlexrayFr179',
     'FlcFLC_FlexrayFr18',
     'FlcFLC_FlexrayFr182',
     'FlcFLC_FlexrayFr185',
     'FlcFLC_FlexrayFr188',
     'FlcFLC_FlexrayFr19',
     'FlcFLC_FlexrayFr191',
     'FlcFLC_FlexrayFr194',
     'FlcFLC_FlexrayFr197',
     'FlcFLC_FlexrayFr20',
     'FlcFLC_FlexrayFr200',
     'FlcFLC_FlexrayFr203',
     'FlcFLC_FlexrayFr206',
     'FlcFLC_FlexrayFr209',
     'FlcFLC_FlexrayFr21',
     'FlcFLC_FlexrayFr212',
     'FlcFLC_FlexrayFr215',
     'FlcFLC_FlexrayFr218',
     'FlcFLC_FlexrayFr22',
     'FlcFLC_FlexrayFr221',
     'FlcFLC_FlexrayFr225',
     'FlcFLC_FlexrayFr226',
     'FlcFLC_FlexrayFr227',
     'FlcFLC_FlexrayFr228',
     'FlcFLC_FlexrayFr229',
     'FlcFLC_FlexrayFr23',
     'FlcFLC_FlexrayFr238',
     'FlcFLC_FlexrayFr24',
     'FlcFLC_FlexrayFr241',
     'FlcFLC_FlexrayFr246',
     'FlcFLC_FlexrayFr247',
     'FlcFLC_FlexrayFr25',
     'FlcFLC_FlexrayFr250',
     'FlcFLC_FlexrayFr253',
     'FlcFLC_FlexrayFr256',
     'FlcFLC_FlexrayFr259',
     'FlcFLC_FlexrayFr26',
     'FlcFLC_FlexrayFr262',
     'FlcFLC_FlexrayFr265',
     'FlcFLC_FlexrayFr268',
     'FlcFLC_FlexrayFr27',
     'FlcFLC_FlexrayFr271',
     'FlcFLC_FlexrayFr274',
     'FlcFLC_FlexrayFr277',
     'FlcFLC_FlexrayFr28',
     'FlcFLC_FlexrayFr282',
     'FlcFLC_FlexrayFr285',
     'FlcFLC_FlexrayFr288',
     'FlcFLC_FlexrayFr29',
     'FlcFLC_FlexrayFr292',
     'FlcFLC_FlexrayFr295',
     'FlcFLC_FlexrayFr298',
     'FlcFLC_FlexrayFr300',
     'FlcFLC_FlexrayFr303',
     'FlcFLC_FlexrayFr306',
     'FlcFLC_FlexrayFr309',
     'FlcFLC_FlexrayFr31',
     'FlcFLC_FlexrayFr312',
     'FlcFLC_FlexrayFr315',
     'FlcFLC_FlexrayFr318',
     'FlcFLC_FlexrayFr321',
     'FlcFLC_FlexrayFr324',
     'FlcFLC_FlexrayFr327',
     'FlcFLC_FlexrayFr33',
     'FlcFLC_FlexrayFr330',
     'FlcFLC_FlexrayFr333',
     'FlcFLC_FlexrayFr336',
     'FlcFLC_FlexrayFr338',
     'FlcFLC_FlexrayFr34',
     'FlcFLC_FlexrayFr341',
     'FlcFLC_FlexrayFr344',
     'FlcFLC_FlexrayFr347',
     'FlcFLC_FlexrayFr35',
     'FlcFLC_FlexrayFr350',
     'FlcFLC_FlexrayFr353',
     'FlcFLC_FlexrayFr356',
     'FlcFLC_FlexrayFr359',
     'FlcFLC_FlexrayFr36',
     'FlcFLC_FlexrayFr362',
     'FlcFLC_FlexrayFr365',
     'FlcFLC_FlexrayFr368',
     'FlcFLC_FlexrayFr37',
     'FlcFLC_FlexrayFr371',
     'FlcFLC_FlexrayFr374',
     'FlcFLC_FlexrayFr377',
     'FlcFLC_FlexrayFr38',
     'FlcFLC_FlexrayFr380',
     'FlcFLC_FlexrayFr383',
     'FlcFLC_FlexrayFr39',
     'FlcFLC_FlexrayFr392',
     'FlcFLC_FlexrayFr40',
     'FlcFLC_FlexrayFr404',
     'FlcFLC_FlexrayFr41',
     'FlcFLC_FlexrayFr416',
     'FlcFLC_FlexrayFr42',
     'FlcFLC_FlexrayFr425',
     'FlcFLC_FlexrayFr43',
     'FlcFLC_FlexrayFr44',
     'FlcFLC_FlexrayFr46',
     'FlcFLC_FlexrayFr48',
     'FlcFLC_FlexrayFr51',
     'FlcFLC_FlexrayFr54',
     'FlcFLC_FlexrayFr57',
     'FlcFLC_FlexrayFr58',
     'FlcFLC_FlexrayFr61',
     'FlcFLC_FlexrayFr64',
     'FlcFLC_FlexrayFr67',
     'FlcFLC_FlexrayFr68',
     'FlcFLC_FlexrayFr71',
     'FlcFLC_FlexrayFr74',
     'FlcFLC_FlexrayFr77',
     'FlcFLC_FlexrayFr79',
     'FlcFLC_FlexrayFr81',
     'FlcFLC_FlexrayFr82',
     'FlcFLC_FlexrayFr83',
     'FlcFLC_FlexrayFr84',
     'FlcFLC_FlexrayFr85',
     'FlcFLC_FlexrayFr86',
     'FlcFLC_FlexrayFr87',
     'FlcFLC_FlexrayFr88',
     'FlcFLC_FlexrayFr89',
     'FlcFLC_FlexrayFr90',
     'FlcFLC_FlexrayFr91',
     'FlcFLC_FlexrayFr92',
     'FlcFLC_FlexrayFr93',
     'FlcFLC_FlexrayFr94',
     'FlcFLC_FlexrayFr95',
     'FlcFLC_FlexrayFr96',
     'FlcFLC_FlexrayFr97',
     'FlcFLC_FlexrayFr98',
     'FlcFLC_FlexrayMeasdDataFr01',
     'FlcFLC_FlexrayMeasdDataFr02',
     'FlcFLC_FlexrayMeasdDataFr03',
     'FlcFLC_FlexrayMeasdDataFr04',
     'FlcFLC_FlexrayNMFr',
     'FlcFlcFrDiagResFrame1',
     'FlcFlcFrDiagResFrame2',
     'FlcFlcFrDiagResFrame3',
     'FlcSafetyCANFD2Fr01',
     'FlcSafetyCanFD2NmFr',
     'FlrSafetyCanFD2NmFr',
     'IMUPrivateSafeADCanFr01',
     'IMUPrivateSafeADCanFr02',
     'Pscm2ADRedundancyNMFr',
     'PscmAdRedundancyFr01',
     'PscmAdRedundancyFr02']
