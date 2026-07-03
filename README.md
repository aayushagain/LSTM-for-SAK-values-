This contains lstm for sak values observed at gitterköpf station using precipitation data from 2 rain gauges above the basin.
LSTM for all time series, and one for each season are also compared.
Box-cox transformation, robust scaler, and standard scaler are compared for normalizing the precipitation dataset. This transformation was deemed necessary, so that the information about extreme values are well incorporated into the training.   
<img width="1990" height="494" alt="image" src="https://github.com/user-attachments/assets/50209b48-72f2-4fdc-b49c-700115e8ea3e" />
Fig.1. Results of different transformation.

Boxcox method was used for transformation, as this transformation handled extreme values well compared to others where outliers can still be observed. 

A lag time of 15 days is taken from previous cross correlation analysis.

Different loss functions i.e. NSE, MSELoss, and HuberLoss were experimented with. NSE loss was perturbed with a noise to keep it continuous.
Adam optimizer was used, as this allowed a larger learning rate compared to SGD. 

Due to smaller dataset, longer stride length, lower epoch was selected so that overfitting could be avoided.

A single LSTM for the entire time series, as well as different LSTM for different seasons were created.

<img width="578" height="467" alt="image" src="https://github.com/user-attachments/assets/1420ad59-eacd-4ca2-9558-27fabaedfb63" />
Fig.2. Training evolution. 

<img width="565" height="467" alt="image" src="https://github.com/user-attachments/assets/ead7aa7b-03fe-4d13-8a0f-00017efea454" />
Fig. 3. Testing evolution. 

<img width="1455" height="659" alt="image" src="https://github.com/user-attachments/assets/26314b3c-dedc-40e9-97c6-6dc4236643fe" />
Fig. 4. Testing evaluation. MSE: 357.8842, 	 NSE: -0.1111, 	 corrcoeff = 0.6487. Precipitation were backtransformed before plotting. 

Here, a limitation can be observed. Despite keeping the epochs as minimum as possible, it rapidly jumps to overfitting without any real improvement in testing dataset. Further development with upstream climate data, catchment attributes could not be implemented due to time limitation. Similar results were observed for seasonal LSTMs as well. 


<img width="1400" height="637" alt="image" src="https://github.com/user-attachments/assets/5dd4e7f5-549b-4771-a293-d3391cf0f793" />
Fig.5. Training evolution for Autumn LSTM. 

<img width="1387" height="637" alt="image" src="https://github.com/user-attachments/assets/f697efa3-83f8-4717-a8c6-035a4d411dbf" />
Fig.6. Testing evolution for Autumn LSTM. 

<img width="1451" height="682" alt="image" src="https://github.com/user-attachments/assets/3c524739-9a28-458a-9356-b8687a4b8216" />
Fig.6. LSTM Autumn prediction for a batch training dataset. Here, overfitting can be clearly observed. 

<img width="1451" height="682" alt="image" src="https://github.com/user-attachments/assets/821354ab-1add-4b2b-a49a-a495ec6fa383" />
Fig.7. LSTM Autum prediction for a batch of testing dataset. Despite an NSE < 0, a positive correlation between the observed and predicted values can be oserved. 

