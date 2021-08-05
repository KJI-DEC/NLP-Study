# Phrase-Based & Neural Unsupervised Machine Translation

### Overview

- Neural translation model과 Phrase-Based translation model에서 unsupervised machine translation을 실현함
- 이전 연구보다 대폭 상승한 SOTA 성능

### Phrase-Based & Neural Unsupervised Machine Translation Summary

- Initialization - words, short phrases, sub-word 등이 정렬되도록 모델 초기화
- Language Modeling - large amounts of monolingual data가 주어지면 source/target language에 대한 language model 학습 가능
- Iterative Back-translation - monolingual data를 사용한 unsupervised setting을 supervised setting으로 활용할 수 있게 함
- Unsupervised NMT/Unsupervised PBSMT

### Experiments

- low resource의 상황에서는 supervised model을 능가하는 성능
- 단일 model의 경우 충분히 훈련된 PBSMT model이 성능이 가장 높음
- PBSMT + NMT인 경우 성능이 가장 좋았음 (NMT + PBSMT의 경우는 딱히)
