<h1 align="center">灵丹中医大模型</br>LingdanLLM</h1>

<div align=center><img width = '200' height ='200' src ="./image/logo.png"/></div>  


## Introduction

This project aims to build a more robust foundation model by continuing the pre-training on the Baichuan2 model, supporting the development of downstream tasks. We have a particular focus on the field of traditional Chinese medicine (TCM), thus selecting a rich training dataset including TCM ancient books,  textbooks, and Chinese Pharmacopoeias. This process not only enhances the model's understanding of TCM knowledge but also provides a solid basis for it to deeply grasp TCM theories and practices.

Through this project, we aim to significantly elevate the application level of artificial intelligence in the field of TCM, contributing to the modernization of TCM.

## Framework

The framework and workflow of this study. We introduce the Lingdan Pre-trained Model, Lingdan-TCPM-Chat, and Lingdan-PR, covering processes from data handling to model training and evaluation.

![Framework](./image/Figure1.png)

## TODO


- [ ] Upload public dataset of each model

- [ ]  Upload Lingdan Pre-trained Model

- [ ]  Upload Lingdan-TCPM-Chat Model

- [ ]  Upload Lindan-PR Model

  

## Dataset

### Pre-training dataset

| **Data source**                    | **Token** |
| ---------------------------------- | --------- |
| **TCM Ancient Books (Vernacular)** | 132M      |
| **TCM Educational Materials**      | 8M        |
| **Drug Manuals**                   | 12M       |
| **Chinese Pharmacopoeia**          | 940K      |
| **Hospital Formulations**          | 37K       |
| **TCM Case Records**               | 7.2M      |
| **Public Data**                    | 124M      |
| **WuDaoTCM**                       | 20M       |

### Traditional Chinese Patent Medicine (TCPM) dialogue dataset

#### Mutil-turn dialogue dataset

| **Role**    | **Text**                                                     |
| ----------- | ------------------------------------------------------------ |
| **User**    | 医生，我最近总是感觉胃胀，而且便秘，吃东西也没有胃口，这是怎么了？  <br />Doctor, I've been  feeling bloated lately and constipated. I also don't have much appetite.  What's wrong with me? |
| **ChatGPT** | 根据您的症状，可能是脾胃不和，痰食阻滞导致的积滞。您有停食或停乳的情况吗？还有没有其他的症状，比如喘咳或者是感觉痰多？  <br />Based on your symptoms, it could be  accumulation stagnation caused by disharmony between the spleen and stomach,  and phlegm and food stagnation. Do you experience food refusal or weaning?  Are there any other symptoms, such as wheezing cough or feeling of excessive  phlegm? |
| **User**    | 对，我确实感觉痰多，而且有时候会有轻微的喘息。  <br />Yes, I do feel like I have a lot of phlegm,  and sometimes I experience mild wheezing. |
| **ChatGPT** | 这些症状符合食滞证的表现。您可以尝试使用中成药一捻金，它具有消食导滞，祛痰通便的功效。  <br />These symptoms are consistent with the  presentation of Food Stagnation Syndrome. You might try the traditional  Chinese patent medicine Yi Nian Jin, which helps in relieving indigestion and  stagnation, expelling phlegm, and facilitating bowel movements. |
| **User**    | 一捻金是由哪些中药组成的？会不会有副作用？ <br /> What are the ingredients of Yi Nian Jin? Are  there any side effects? |
| **ChatGPT** | 一捻金的主要成分包括大黄、炒牵牛子、槟榔、人参和朱砂。大黄100克，炒牵牛子200克，槟榔和人参各100克，朱砂30克。通常情况下，按照推荐的剂量服用是安全的，但每个人的体质不同，如果有任何不适，请及时停药并咨询医生。 <br /> The main ingredients of Yi Nian Jin include  Rhubarb, Fried Morning Glory Seeds, Betel Nut, Ginseng, and Cinnabar. The  formulation is 100 grams of Rhubarb, 200 grams of Fried Morning Glory Seeds,  100 grams each of Betel Nut and Ginseng, and 30 grams of Cinnabar. It is  generally safe when taken in recommended doses, but individual responses can  vary. If you experience any discomfort, stop taking it immediately and  consult a doctor. |
| **User**    | 了解了，我应该怎么服用，有没有什么特别的指导呢？  <br />Got it. How should I take it? Are there any  specific instructions? |
| **ChatGPT** | 具体服用方法和剂量应该根据个人情况和医生的建议来定。通常，成人的剂量会根据不同的病情来调整。请在开始服用前咨询专业医生，他们会根据您的具体情况给出最合适的建议。  The specific method and dosage should be based  on individual circumstances and the advice of a doctor. Usually, the dosage  for adults is adjusted according to different conditions. Please consult a  professional doctor before starting, as they can offer the most appropriate  advice for your specific situation. |

#### Single-turn dialogue dataset

Around **200K** Q&A on basic knowledge of TCPM, sourced from Drug Manuals and the Chinese Pharmacopoeia.

### Prescription Recommendation (PR) Dataset



| **Type**        | **Text**                                                     |
| --------------- | ------------------------------------------------------------ |
| **Instruction** | 请根据以下病人的病情，为其开具中药处方：<br />Please prescribe a traditional Chinese medicine formula based on the  following patient's condition: |
| **Input**       | 现病史:进食多则痞满，嗳气，咽部异物感，纳少，体重下降，急躁易怒，睡眠欠佳，大便干，3－4日1次，排出不畅，小便正常。体重下降。舌暗红，苔薄黄略腻，脉沉。  <br />Present Illness History: Feels full and bloated after eating a lot,  experiences belching and a sensation of a foreign object in the throat, poor  appetite, weight loss, irritability, poor sleep, dry stool, bowel movements  once every 3-4 days with difficulty in evacuation, normal urination. Weight  loss. The tongue is dark red with a thin, slightly greasy yellow coating, and  the pulse is deep. |
| **Output**      | 中药处方: 当归 15.0, 黄连 6.0, 麸炒枳壳 30.0, 旋复花 20.0, 柴胡 7.0, 黄芩 10.0, 合欢皮 15.0, 煅赭石 30.0, 姜厚朴 20.0, 炒白芍 15.0, 三七粉 3.0, 法半夏 15.0, 陈皮 15.0, 川芎 15.0 <br />Chinese Herbal Prescription: Angelica Sinensis (Dang Gui) 15.0g, Coptis  Chinensis (Huang Lian) 6.0g, Fried Aurantium (Wheat-Fried Zhi Qiao) 30.0g,  Xuan Fu Hua (Inula Flower) 20.0g, Bupleurum (Chai Hu) 7.0g, Scutellaria  Baicalensis (Huang Qin) 10.0g, Albizia Julibrissin Bark (He Huan Pi) 15.0g,  Calcined Hematite (Duan Da Zhe Shi) 30.0g, Zingiber Officinale  (Ginger-Processed Hou Po) 20.0g, Fried White Peony Root (Chao Bai Shao)  15.0g, Panax Notoginseng Powder (San Qi Fen) 3.0g, Pinellia Ternata  (Processed Ban Xia) 15.0g, Aged Tangerine Peel (Chen Pi) 15.0g, Ligusticum  Chuanxiong (Chuan Xiong) 15.0g. |



## Model evaluation

### Lingdan-TCPM-Chat Model



| **Role**    | **Text**                                                     |
| ----------- | ------------------------------------------------------------ |
| **User**    | 医生，最近我总是感觉小便频繁，尤其是晚上，还会出现夜间遗尿的情况，这是怎么回事呢？ <br />Doctor, recently I have been experiencing frequent urination, especially  at night, and there have been instances of nocturnal enuresis. What could be  the reason for this? |
| **Lingdan** | 您可能是肾气不足导致的遗尿，出现了小便频数的情况。您有没有出现腰膝酸软的情况？<br />You might be experiencing enuresis due to insufficient kidney qi,  resulting in frequent urination. Have you experienced any soreness or  weakness in your lower back and knees? |
| **User**    | 是的，还有腰膝酸软。  <br />Yes, I also have soreness and weakness in my lower back and knees. |
| **Lingdan** | 这些症状符合肾气不足证的表现。您可以考虑使用中成药缩泉丸，它具有补肾缩尿的功效，适用于肾气不足所致的小便频数、夜间遗尿等症状。<br />These symptoms are consistent with the manifestation of insufficient  kidney qi. You might consider using the traditional Chinese medicine Shuquan  Wan, which has the effect of nourishing the kidney and reducing urination. It  is suitable for symptoms such as frequent urination and nocturnal enuresis  caused by insufficient kidney qi. |
| **User**    | 缩泉丸的中药组成是什么？<br />What are the components of Shuquan Wan in traditional Chinese medicine? |
| **Lingdan** | 缩泉丸的中药组成包括山药、益智仁（盐炒）、乌药。<br />The components of Shuquan Wan in traditional Chinese medicine include  Chinese yam, Alpinia oxyphylla (salt-roasted), and Lindera aggregata. |
| **User**    | 服用该中成药有什么需要注意的吗？<br />Are there any precautions to be aware of when taking this traditional  Chinese medicine? |
| **Lingdan** | 缩泉丸适用于肾气不足所致的小便频数、夜间遗尿等症状，但服用时需要注意剂量和禁忌，建议在医生指导下使用。如果出现不适，应立即停药并咨询医生。 <br />Shuquan Wan is suitable for symptoms such as frequent urination and  nocturnal enuresis caused by insufficient kidney qi. However, attention  should be paid to the dosage and contraindications when taking it, and it's  recommended to use under the guidance of a doctor. If any discomfort occurs,  you should immediately stop taking the medicine and consult a doctor. |

### Lingdan-PR Model



| **Methods**         | **P@5**    | **R@5**    | **F1@5**   | **P@10**   | **R@10**   | **F1@10**  | **P@20**   | **R@20**   | **F1@20**  |
| ------------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| **MLKNN**           | 0.7002     | 0.1523     | 0.2502     | 0.6140     | 0.2652     | 0.3704     | 0.5212     | 0.4473     | 0.4814     |
| **BlockLDA**        | *0.7375*   | *0.1611*   | *0.2644*   | 0.6553     | 0.2853     | 0.3975     | 0.5340     | 0.4615     | 0.4951     |
| **LinkLDA**         | 0.7348     | 0.1601     | 0.2630     | *0.6554*   | *0.2855*   | *0.3977*   | *0.5359*   | *0.4631*   | *0.4969*   |
| **Link-PLSA-LDA**   | 0.7338     | 0.1603     | 0.2632     | 0.6477     | 0.2823     | 0.3932     | 0.5342     | 0.4614     | 0.4952     |
| **TCMPR**           | 0.6934     | 0.1518     | 0.2491     | 0.6037     | 0.2633     | 0.3667     | 0.5024     | 0.4339     | 0.4657     |
| **KDHR**            | 0.6462     | 0.1440     | 0.2356     | 0.5818     | 0.2599     | 0.3593     | 0.4738     | 0.4188     | 0.4446     |
| **Baichuan2-PR**    | 0.6809     | 0.1520     | 0.2465     | 0.6322     | 0.2810     | 0.3849     | 0.5211     | 0.4589     | 0.4822     |
| **Lingdan-PR**      | **0.7698** | **0.1729** | **0.2798** | **0.7287** | **0.3257** | **0.4450** | **0.6352** | **0.5608** | **0.5883** |
| **Improvement (%)** | **4.38**   | **7.32**   | **5.82**   | **11.18**  | **14.08**  | **11.89**  | **18.53**  | **21.10**  | **18.39**  |



**Baichuan2-PR**: We implemented Baichuan2-PR, adhering to the same hyperparameters and methodologies as Lingdan-PR, while basing it on the Baichuan2-13B-Base.

## Training details



| **Model**               | NVIDIA A100-80G GPUs | card hours | **Token** |
| :---------------------- | :------------------- | :--------- | :-------- |
| **Lingdan Pre-trained** | 6                    | 208        | 304M      |
| **Baichuan2-TCPM-Chat** | 1                    | 32         | 9.6M      |
| **Lingdan-TCPM-Chat**   | 1                    | 29         | 9.6M      |
| **Lingdan-PR**          | 8                    | 171        | 77M       |
| **Baichuan2-PR**        | 4                    | 120        | 77M       |



## Citation

This work was completed in collaboration with the following organizations:

1. Institute of Medical Intelligence, Beijing Key Lab of Traffic Data Analysis and Mining, School of Computer and Information Technology, Beijing Jiaotong University
2. Cloudphar Pharmaceuticals Co., Ltd., Shenzhen
3. Department of Gastroenterology, Guang’anmen Hospital, China Academy of Chinese Medical Sciences

The mentor of this work is Professor [Zhou Xuezhong](https://www.researchgate.net/profile/Xuezhong-Zhou).

If you would like to cite this work, please use the following format:

```tex
@misc{LingdanLLM,
      title={LingdanLLM}, 
      author={Rui Hua},
      year={2023},
      publisher = {GitHub},
      journal = {GitHub repository},
      howpublished = {\url{https://github.com/TCMAI-BJTU/LingdanLLM}},
}
```

**Acknowledgements**

The work was carried out at National Supercomputer Center in Tianjin, and the calculations were performed on Tianhe new generation supercomputer.

## Reference

[Baichuan2](https://github.com/baichuan-inc/Baichuan2),  [LLaMA Factory](https://github.com/hiyouga/LLaMA-Factory)