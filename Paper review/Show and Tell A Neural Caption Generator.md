# Show and Tell: A Neural Caption Generator

### Overview

- Image description은 challenging task → CV + NLP
- Image description에 관한 end-to-end system
- vision, language model 중 SOTA인 model architecture의 일부를 조합
- 기존 SOTA보다 좋은 성능

### Show and Tell Summary

- GoogleNet + LSTM
- LSTM 직전에 이미지 벡터 공간을 워드 벡터 공간으로 mapping하는 layer
- word2vec
- BeamSearch: k개의 후보를 항상 유지하다가 마지막 단계에서 후보를 선택. k가 너무 크면 overfitting 문제 발생
- BLEU-n 평가 방식
- overfitting이 심했음 → 해결: CNN은 pre-trained model을 사용함
- 2단계 학습: Inception model의 fixed weight로 train, Fine-Tuning

### Experiments

- human evaluation; 사람보다 좋은 점수를 받은 것도 있었으나 실제로 결과를 보면 그렇지 않음
- word embedding vector는 유사한 단어들끼리 잘 뭉쳐있도록 학습됨
