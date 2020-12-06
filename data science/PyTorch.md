PyTorch for Deep Learning with Python Bootcamp
===============================================
17 hrs
1. Installation
install Anaconda
```shell script
cd D:\Python\PyTorch
conda env create -f pytorch_course_env.yml
conda activate pytorchenv
jupyter lab
```

## PyTorch
### Tensor basics
```shell script
arr = np.array([1, 2, 3, 4, 5])
torch.from_numpy(arr)
torch.as_tensor(arr)
torch.tensor(arr) # deep copy, no reference to original arr

mat = np.arange(0.0, 12.0).reshape(4, 3)
torch.from_numpy(mat)

torch.Tensor(arr) # Capital Tensor -> float type
torch.FloatTensor(arr) # same as above

torch.empty(4,2)
torch.zeros(4,3)
torch.linspace(0, 18, 12).reshape(3, 4)
torch.tensor([1, 2, 3])

torch.randn(4, 3) # normal dist, 4 by 3 matrix
torch.randint(low=0, high=10, size=(5, 5))
torch.randn_like(arr) # take the size/shape of arr
torch.randint_like(arr, low=0, high=11)
torch.manual_seed(42)

x = x.type(torch.int64) # change dtype of x from int32 to int64
x.dtype
```

### Tensor Operations
```shell script
test = torch.arange(6).reshape(3,2)
test[:, 1:]
torch.arange(6).view(3,2) # similar to reshape, reflect most current data

x = torch.arange(10)
x.view(2, -1) # 2 rows, -1 means torch will infer count of cols

# a + b: torch.add(a, b), a.add_(b) (a is changed in place)
# a - b: 

# matrix dot product
a.dot(b) # col count in a should match row count in b
torch.mm(a, b) # matrix multiplication, or a @ b
x.norm() # Eucl norm
x.numel # number of elements; len(x) returns row count for matrix
```

## Machine Learning
### Supervised learning
trained with labeld examples, such as input where desired output is known
- spam vs legitimate email
- positive vs negative movie review
historical data predicts future: training data -> validation data -> test data

- Overfitting (too complex model) & underfitting (too simple model)
- Evaluating performance: 
    - classification error metrics (for categorical values)
    accuracy, precision (identify only relevant data points)
    F1-Score：harmonic mean 2*(precision * recall / (precision + recall)), punish extreame case
    confusion matrix
    - regression error metrics (for continuous values)

### Unsupervised learning
- Clustering: grouping together unlabeled data
- Anomaly detection: fradulent transactions
- Dimensionality reduction

