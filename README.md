# ST-DenseNet-GCN version 2

## update 2020/11/01

The best c, p, t values for the both datasets are 5, 4, 1, respectively. The learning rate is 1e-4


## update 2020/08/22

The best c, p, t values for the Taxi dataset are 4, 5, 1, respectively. The learning rate is 4e-5

The best c, p, t values for the Bike dataset are 4(5), 3, 1, respectively. The learning rate is 4e-5.

## update 2020/08/15
We use a small network to preporcessing the traffic volume and traffic flow data.

The traffic data and flow data are fed to a Lt-layer CNN network and a Lf-layer GCN network, respectively. After this operation we get their output denoted as F_traffic and F_flow. Then we perform F_traffic * \sigma (F_flow) and get the new traffic feature F'_traffic.

The above operation is repeated k times and we can get the final feature maps F_traffic_flow, which incorparate the spatial ralationships of different areas. F_traffic_flow is fed into densenet to learn features.

Best on Taxi--> Pickup RMSE: 23.4369, MAPE: 16.0%, Dropoff RMSE: 18.9033, MAPE: 15.97%

Best on Bike--> Pickup RMSE: 8.5552, MAPE: 21.4%, Dropoff RMSE: 7.6472, MAPE: 19.96%

~~For the Taxi dataset, the MAPE results of our method are better than STDN, and the results of RMSE are slightly worse than STDN. For the Bike dataset, both the MAPE and RMSE results are better than STDN.~~

**Latest**:
```diff
+ Our method has successfully beat STDN
```

### To do list
- Divide the whole dataset into sub-matrix, in order to get fine-granularity control of traffic pattern.
- Explore different data normalization techniques.
- Make the code simple and clear.

## update 2020/08/14
The GCN take the flow traffic as input, then output a threhold $\eta \in [0, 1]$, which is acted as a gating operation.

Best on Taxi: Pickup RMSE: 24.9140 MAPE: 16.5%, Drop off RMSE: 20.4065, MAPE: 16.57% better than DMVST-Net

Best on Bike: Pickup RMSE: 9.5867 MAPE: 24.0%, Drop off RMSE: 8.9538, MAPE: 22.75% better than ST-ResNet

## STDN traning results

Max epochs: 100, stops at 47th epoch

Namespace(att_lstm_num=3, batch_size=64, cnn_flat_size=128, cnn_nbhd_size=3, dataset='taxi', long_term_lstm_seq_len=3, max_epochs=100, model_name='stdn', nbhd_size=2, short_term_lstm_seq_len=7)

Start training stdn with input shape (287400, 7, 7, 2) / (287400, 7, 160)

Evaluating threshold: 0.00779423226812159.

pickup rmse = 0.01855004975541077, pickup mape = 16.15834886445782%

dropoff rmse = 0.014951758386474607, dropoff mape = 16.663443629335838%
