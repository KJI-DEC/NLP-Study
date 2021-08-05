# BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding

논문: [BERT](https://arxiv.org/pdf/1810.04805.pdf)

## Overview


- 기존 LM 모델은 undirectional, Left-to-Right/shallow concatenation
- `Transformer`의 인코더를 쌓아올린 구조
- Pre-training, Fine-tuning
    - task-specific한 parameter 최소화
- Bidirectional
- `Masked Language Model`, `Next Sentence Prediction`

## Related work


- Unsupervised Feature-based Approaches
    - 다양한 적용이 가능한 representation을 학습하는 것. modern NLP System에서는 word embedding을 pretrain함. left-to-right language modeling objectives가 사용됨
    - ELMo
- Unsupervised Fine-tuning Approaches
    - word embedding을 unlabeled text로부터 pretrain
- Transfer Learning from Supervised Data
    - supervised learning으로부터 효과적인 transfer → large pretrained model에서 transfer learning의 중요성 대두

## BERT


- importance of bidirectional pre-training LM
- Pre-training & Fine-Tuning
    - Pre-training: train unlabeled data; MLM, NSP
    - Fine-Tuning: fine-tuned by using labeled data from downstream task

![Pre-training and Fine-Tuning](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c71e0335-7b00-4d5f-a799-8caf51f4ca7c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210801%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210801T075531Z&X-Amz-Expires=86400&X-Amz-Signature=6489db1913fe8f23e5bc36fa0c1da01b3d61909e3bf279c878e1cb5d91d58a06&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### BERT Architecture

- 다른 task에서도 같은 architecture 사용
- Multi-layer bidirectional Transformer encoder
- 기호
    - L: number of layers
    - H: hidden size
    - A: number of self-attention heads
- Base ver: 12개의 transformer encoder
    - Bert-Base: L = 12, D = 768, A = 12, 110M params
- Large ver: 24개의 transformer encoder
    - Bert-Large: L = 24, D = 1024, A = 16. 340M params
- Input/Output: single sentence or pair of sentences
- WordPiece embedding
- start: [CLS] token, next sentence: [SEP]

![BERT Architecture](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cc06b80c-4e6e-4128-b35c-c1c91febd03f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210801%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210801T075637Z&X-Amz-Expires=86400&X-Amz-Signature=8742f8211e8cb9ff158cc0573f0362a7430b6577284a963896f61ec7929a21f0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### Masked LM

- input sequence의 15%를 random으로 masking한 후 해당 자리에 뭐가 들어가는지 예측하는 train
    - Randomly 80% of tokens, gonna be a `[MASK]` token
    - Randomly 10% of tokens, gonna be a `[RANDOM]` token
    - Randomly 10% of tokens, will be remain as same, but need to be predicted

### Next Sentence Prediction

- 다음 sentence 예측
- 50%의 확률로 sample data의 두 문장 중 뒤의 문장을 다른 문장으로 바꿈
- pre-train model을 token에서 sentence-level로 확장하여 사용하기 위한 것
- 문장 사이의 연관성 train

### Fine-tuning

- Task specific inputs와 outputs를 BERT에 넣은 후 end-to-end로 fine-tune
- Fine-tuning 별로 input의 형태가 달라질 수 있음

![Fine-Tuning](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4a7be17a-1432-467b-acf9-9f00284af11e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210801%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210801T075455Z&X-Amz-Expires=86400&X-Amz-Signature=0d279d1ebbd7006d0e7b7ed6d883a0a8d32fd3876d2cb292e3c02279edec9163&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### Ablation Studies

- Effect of Pre-training Task
    - No NSP: MLM으로만 학습. QNLI, MNLI, SQuAD 1.1에서 성능 떨어짐
    - LTR + No NSP: LTR 사용하는 경우 모든 task에서 MLM에 비해 성능 저하
    - LTR과 RTL을 합친 모델은 bidirectional model에 비해 2배의 비용이 추가도 들어감
- Effect of Model Size
    - model의 크기가 모델의 성능에 직접적인 영향을 미침 → 큰 모델, 더 좋은 성능
    - 큰 모델은 small scale task에서도 성능 향상이 큼
- Feature-based Approach with BERT
    - Transformer encoder는 모든 task에 적용 불가. task-specific model 추가하여 사용해야 함
    - 컴퓨팅 비용 절감 가능

## Conclusion


> Recent empirical improvements due to transfer learning with language models have demonstrated that rich, unsupervised pre-training is an integral part of many language understanding systems. In particular, these results enable even low-resource tasks to benefit from deep unidirectional architectures. *Our major contribution is further generalizing these findings to deep bidirectional architectures, allowing the same pre-trained model to successfully tackle a broad set of NLP tasks.*

- 해당 연구를 통해 deep bidirectional architectures를 통해 방대한 NLP task를 성공적으로 처리하게 함

## References

references for additional study about BERT

- [https://lsjsj92.tistory.com/618](https://lsjsj92.tistory.com/618)
- [https://wikidocs.net/115055](https://wikidocs.net/115055)
