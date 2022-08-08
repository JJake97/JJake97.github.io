## RNN이란?

- 정해지지 않은 길이의 배열을 읽고 설명하는 신경망
- Input data의 순차적 흐름을 모두 내포한다

### 영화 리뷰 감정 분석 with RNN

- 실습에 사용하는 IMDB Dataset은 숫자로 이루어진 Tensor나 Vector 형태가 아닌 자연어 텍스트입니다. 따라서, 해당 자연어를 숫자로 나타내는 전처리 과정이 필요한데 단어의 최소단위인 'token'으로 데이터를 나눈 뒤 해당 token을 벡터 형태로 변환하는 작업을 의미합니다
- Pytorch에서는 torchtext의 전처리 기능들과 nn.Embedding 기능을 사용하여 쉽게 처리할 수 있습니다

#### 라이브러리 Import


```python
import os
import torch
import torch.nn as nn
import torch.nn.functional as F
from torchtext import data, datasets
```

#### 모델 구현과 학습에 필요한 Hyperparameters를 정의


```python
# 하이퍼파라미터
BATCH_SIZE = 64
lr = 0.001
EPOCHS = 10
USE_CUDA = torch.cuda.is_available()
DEVICE = torch.device("cuda" if USE_CUDA else "cpu")
print("다음 기기로 학습합니다:", DEVICE)
```

    다음 기기로 학습합니다: cuda


#### Dataset Loading하고 Tensor로 변환 후, 데이터 split


```python
# 데이터 로딩하기
print("데이터 로딩중...")
TEXT = data.Field(sequential=True, batch_first=True, lower=True)
LABEL = data.Field(sequential=False, batch_first=True)
trainset, testset = datasets.IMDB.splits(TEXT, LABEL)
TEXT.build_vocab(trainset, min_freq=5)
LABEL.build_vocab(trainset)

# 학습용 데이터를 학습셋 80% 검증셋 20% 로 나누기
trainset, valset = trainset.split(split_ratio=0.8)
train_iter, val_iter, test_iter = data.BucketIterator.splits(
        (trainset, valset, testset), batch_size=BATCH_SIZE,
        shuffle=True, repeat=False)


vocab_size = len(TEXT.vocab)
n_classes = 2
```

    데이터 로딩중...
    downloading aclImdb_v1.tar.gz


    aclImdb_v1.tar.gz: 100%|██████████| 84.1M/84.1M [00:02<00:00, 35.0MB/s]



```python
print("[학습셋]: %d [검증셋]: %d [테스트셋]: %d [단어수]: %d [클래스] %d"
      % (len(trainset),len(valset), len(testset), vocab_size, n_classes))
```

    [학습셋]: 20000 [검증셋]: 5000 [테스트셋]: 25000 [단어수]: 46159 [클래스] 2


#### RNN 모델 구현 (GRU)


```python
class BasicGRU(nn.Module):
    def __init__(self, n_layers, hidden_dim, n_vocab, embed_dim, n_classes, dropout_p=0.2):
        super(BasicGRU, self).__init__()
        print("Building Basic GRU model...")
        self.n_layers = n_layers
        self.embed = nn.Embedding(n_vocab, embed_dim)
        self.hidden_dim = hidden_dim
        self.dropout = nn.Dropout(dropout_p)
        self.gru = nn.GRU(embed_dim, self.hidden_dim,
                          num_layers=self.n_layers,
                          batch_first=True)
        self.out = nn.Linear(self.hidden_dim, n_classes)

    def forward(self, x):
        x = self.embed(x)
        h_0 = self._init_state(batch_size=x.size(0))
        x, _ = self.gru(x, h_0)  # [i, b, h]
        h_t = x[:,-1,:]
        self.dropout(h_t)
        logit = self.out(h_t)  # [b, h] -> [b, o]
        return logit
    
    def _init_state(self, batch_size=1):
        weight = next(self.parameters()).data
        return weight.new(self.n_layers, batch_size, self.hidden_dim).zero_()
```

#### 학습 함수 구현


```python
def train(model, optimizer, train_iter):
    model.train()
    for b, batch in enumerate(train_iter):
        x, y = batch.text.to(DEVICE), batch.label.to(DEVICE)
        y.data.sub_(1)  # 레이블 값을 0과 1로 변환
        optimizer.zero_grad()

        logit = model(x)
        loss = F.cross_entropy(logit, y)
        loss.backward()
        optimizer.step()
```

#### 평가 함수 구현


```python
def evaluate(model, val_iter):
    """evaluate model"""
    model.eval()
    corrects, total_loss = 0, 0
    for batch in val_iter:
        x, y = batch.text.to(DEVICE), batch.label.to(DEVICE)
        y.data.sub_(1) # 레이블 값을 0과 1로 변환
        logit = model(x)
        loss = F.cross_entropy(logit, y, reduction='sum')
        total_loss += loss.item()
        corrects += (logit.max(1)[1].view(y.size()).data == y.data).sum()
    size = len(val_iter.dataset)
    avg_loss = total_loss / size
    avg_accuracy = 100.0 * corrects / size
    return avg_loss, avg_accuracy
```

#### 모델 생성, 최적화 알고리즘 정의


```python
model = BasicGRU(1, 256, vocab_size, 128, n_classes, 0.5).to(DEVICE)
optimizer = torch.optim.Adam(model.parameters(), lr=lr)
```

    Building Basic GRU model...



```python
best_val_loss = None
for e in range(1, EPOCHS+1):
    train(model, optimizer, train_iter)
    val_loss, val_accuracy = evaluate(model, val_iter)

    print("[이폭: %d] 검증 오차:%5.2f | 검증 정확도:%5.2f" % (e, val_loss, val_accuracy))
    
    # 검증 오차가 가장 적은 최적의 모델을 저장
    if not best_val_loss or val_loss < best_val_loss:
        if not os.path.isdir("snapshot"):
            os.makedirs("snapshot")
        torch.save(model.state_dict(), './snapshot/txtclassification.pt')
        best_val_loss = val_loss
```

    [이폭: 1] 검증 오차: 0.69 | 검증 정확도:51.58
    [이폭: 2] 검증 오차: 0.69 | 검증 정확도:52.66
    [이폭: 3] 검증 오차: 0.69 | 검증 정확도:52.16
    [이폭: 4] 검증 오차: 0.69 | 검증 정확도:53.68
    [이폭: 5] 검증 오차: 0.60 | 검증 정확도:68.16
    [이폭: 6] 검증 오차: 0.43 | 검증 정확도:81.92
    [이폭: 7] 검증 오차: 0.36 | 검증 정확도:84.58
    [이폭: 8] 검증 오차: 0.37 | 검증 정확도:85.80
    [이폭: 9] 검증 오차: 0.40 | 검증 정확도:85.36
    [이폭: 10] 검증 오차: 0.44 | 검증 정확도:84.58



```python
model.load_state_dict(torch.load('./snapshot/txtclassification.pt'))
test_loss, test_acc = evaluate(model, test_iter)
print('테스트 오차: %5.2f | 테스트 정확도: %5.2f' % (test_loss, test_acc))
```

    테스트 오차:  0.35 | 테스트 정확도: 85.68

