## File Setups
# Pipeline
- This is our pipeline setups which you can use to run watchers and gather data. 
- Put in your NetUnicorn login information and the working node you would like to use.
- Some have speed tests to simulate congestion while others are longer. Make sure to change the endpoint for file collection.
- Link to NetUnicorn Task Library: https://github.com/netunicorn/netunicorn-library/tree/main   
# Model - Data PreProcessing
- Load nessceary data from csv files. If you have a PCAP file, convert it to csv with Tshark or some other method.
- Splice the data for nessecary features and target variable's you are seeking. (This is heavily dependent on your file layouts so double check them with print(filename.columns)
- Our features are Flow size, RTT, CWND, and Average Packet Size.
- Sort your file by timestamp, as it is important packets that came first are picked first.
# Model
```python
(X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, shuffle=False))
```
- This line will split your files into test and train. Shuffle = False as order matters in our case. Test_size means 20% of files will be left for test. This can be edited freely.
- Note: This is not nessecary for our iterations as we define them inside. 
 ```python
scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)

model = SGDRegressor(max_iter=10000, tol=1e-3, learning_rate='optimal', loss='huber', epsilon=1.35)
#model = SGDRegressor(max_iter=10000, tol=1e-3,learning_rate='optimal'
```
- Scale your values in X to assist in SGD. Choose loss function. Default is Squared Error.
 ```python
train_size = 20
test_size = 2
```
- Choose test size and train size.
```python
model.fit(X_train, y_train)
```
- This line can be made to model.partial_fit as well, which will keep past information.


## Reproducing Results
# Network Changes
- Can be simulated by splicing together multiple files from different network points.
- Can be simulated by running a watcher or packet grabber for a long time.
# Congestion
- Multiple Background Tasks such as speed tests or pings. NetUnicorn has both in their library. 
- Brute Force Attacks such as bruteforce_ssh from netunicorn. 
- Grabbing very large files

  
