# [Online Demo](http://140.116.245.147:7432/)

# Coreference Resolution
Coreference resolution is the process of identifying the relationships between words or phrases in a natural language text that refer to the same entity. For example, when pronouns such as "he", "she", or "it" are used in a text, coreference resolution determines the entity that the pronoun refers to.

Our coreference resolution focuses on resolving pronouns.

# How to use
Install dependencies:
```
$ pip install requirements.txt
```
Use the following code to perform coreference resolution on your input text:
```
from coreference_with_hanlp_np import coref

input = "７６歲的金大忠面帶微笑，領取了諾貝爾和平獎，他表示：他和韓國人民還有北韓領袖金正日一起分享這份榮譽。"
result = coref(input)
print(result)
```

# Dataset and Accuracy
We have selected three sets of 200 examples each from the Chinese_v4 dataset in conll2012_ontonotesv5 for testing. The dataset contains many incorrectly labeled examples, which we have removed.

| dataset       | accuracy |
| ------------- |:-------------:|
| dataset 1     | 0.97          |
| dataset 2     | 0.89          |
| dataset 3     | 0.916         |

# Versions
- version 1 (黃柏洋)  
Build the structure of NP features and the algorithm for matching pronouns and noun phrases.  
Acurracy: 0.4
- version 2 (許逸翔)  
Modifiy gender、number、animacy rules.  
Acurracy: 0.66
- version 3 (李晨瑞)  
Add additional rules for pronoun and noun phrase matching to improve the accuracy of the matching.
 - Using collocation to determine whether an NP represents a person or a country.  
    e.g. "科什圖尼察表示由於南國國內的政治危機，他無法離開南斯拉夫。"  
    If we look directly forward, we will find '南國國內,' but a country will not have a "離開" action.
 - When a pronoun serves as the subject, we prioritize searching for an antecedent among the subjects.  
    e.g. "張宏寶的律師今天證實張宏寶已經向關島地方法院申請人身保護令狀，他說法院可能在明年１月中旬開庭審理。"  
    We observe that when a pronoun is the subject, the corresponding noun phrase is often also the subject.
 - Extract SVO from the sentence where the pronoun is located, and if the pronoun is the object, the subject will not be considered.  
    e.g. "其中一名重傷的乘客陷在撞爛的車廂當中，結果由消防人員費了很大的力氣才把他救出來"  
    If we simply look for the antecedent before the pronoun, we would retrieve "消防人員" instead of "其中一名重傷的乘客". However, sometimes the pronoun does represent the subject, such as in the sentence "馬英九說他是總統". In such cases, we skip verbs that may refer to the subject, such as "說", "評價", "提出" , "否認", and "表示".

# Author
[NCKU mi2s lab](https://wmmks.csie.ncku.edu.tw/)  
Professor: 盧文祥(Wen-Hsiang Lu)   
Student: 李晨瑞(CHEN-RUEI LI)、許逸翔(I-HSIANG HSU)、黃柏洋(Bo-yang HUANG)

contact us: nckucsuewmmks@gmail.com

# Acknowledgments
We used EHownet and HanLP for implementing our coreference resolution algorithm.
