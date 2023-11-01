# SMEs Fraud Detection and Prevention System

Small and Medium Enterprises (SMEs) often struggle with managing their finances and protecting their online payment transactions from fraudulent activities. This project aims to provide an affordable and user-friendly fraud detection and prevention system tailored for SMEs. The system leverages machine learning algorithms to analyze transaction data, including user behavior, transaction history, and various attributes, to identify potentially fraudulent activities.

## Table of Contents

1. [Introduction](#introduction)
2. [Approach and Methodology](#approach-and-methodology)
3. [Features Description](#features-description)
4. [Data Generation](#data-generation)
5. [Data Transformation](#data-transformation)
6. [Model Training](#model-training)
7. [Usage](#usage)
8. [Contributing](#contributing)
9. [License](#license)

## Introduction

SMEs face significant challenges in managing their finances and ensuring the security of online payment transactions. Fraudulent activities in online payment systems can result in significant financial losses for SMEs. Therefore, there is a need for a fraud detection and prevention system that is affordable and easy to use for SMEs. This project addresses that need by developing a system that can analyze transaction data and identify potentially fraudulent activities using machine learning algorithms.

## Approach and Methodology

The approach to building this fraud detection and prevention system involves several key steps:

1. **Feature Identification**: Identify the relevant features for analyzing transaction data.

2. **Data Generation**: Generate synthetic transaction data using tools like Faker, random, numpy, and pandas. This data includes SME profiles, customer profiles, and transactions (both normal and fraudulent).

3. **Feature Engineering**: Transform attribute values based on feature type to prepare the data for analysis.

4. **Model Training**: Train a fraud detection model using the XGBoost classification algorithm.

5. **Data Transformation**: Transform data for specific attributes such as date/time, customer ID, SME ID, and more.

## Features Description

Here's a description of the key features used in the system:

- **TRANSACTION ID**: Numeric - A unique identifier for the transaction.
- **TX DATETIME**: Panda timestamp - Date and time at which the transaction occurs.
- **CUSTOMER ID**: Numeric - The identifier for the customer.
- **SME ID**: Numeric - The identifier for the SME (merchant).
- **TX AMOUNT**: Numeric - The amount of the transaction.
- **TX TIME SECOND**: Numeric - Second of the transaction, starting from 0 to the last transaction day * 86400.
- **TX TIME DAYS**: Numeric - Day of transaction, starting from 0 to the last transaction day.
- **CARD NO**: Categorical - The credit card used by customers in the transactions.
- **CARD TYPE**: Categorical - The type of credit card being used.
- **EMAIL DOMAIN**: Categorical - The email domain that customers used to register their accounts.
- **IP ADDRESS**: Categorical - The IP address of the customers when the transaction happened.
- **PHONE NO**: Categorical - The phone number of the customers used for transactions.
- **TX FRAUD**: Binary - Labels indicating legitimate or fraudulent transactions.

## Data Generation

The data generation process involves creating normal and fraudulent transactions for model training. This includes:

- Generation of customer profiles with unique properties.
- Generation of SME profiles.
- Association of customer profiles with SMEs based on geographical proximity.
- Generation of transactions based on customer profiles.
- Labeling transactions as legitimate or fraudulent using various fraud scenarios.

#### Step 1: Normal Transactions

1. **Generation of Customer Profiles**: Every customer is unique in their spending habits. In this step, you'll simulate customer profiles, defining properties like geographical location, spending frequency, and spending amounts. These customer properties will be represented in a table, referred to as the customer profile table.

2. **Generation of SME Profiles**: SME properties will consist of a product position. These SME properties will be represented as a table, referred to as the SME profile table.

3. **Association of Customer Profiles to Terminals**: You'll assume that customers make transactions with SMEs that are in close geographic proximity. This simple assumption ensures that a customer primarily transacts with SMEs near their location.

4. **Generation of Transactions**: A simulator will loop over the set of customer profiles and generate transactions based on their properties, including spending frequencies, amounts, and available SMEs. This will result in a table of transactions representing normal behavior.

#### Step 2: Fraudulent Transactions

  The normal transactions table is expanded by introducing fraudulent transactions using specific fraud scenarios:

  1. **Scenario 1**: Any transaction with an amount greater than 300 is considered 20% likely to be a fraud. The amount is drawn from a normal distribution with a mean between 5 and 100 and a standard deviation as double the mean.

  2. **Scenario 2**: Daily, a list of 3 customers is randomly selected. Over the next 14 days, 1/3 of their transactions have their amounts multiplied by 5 and marked as fraudulent. This scenario simulates card-not-present fraud, where a customer's credentials have been leaked, and the fraudster continues to make transactions, aiming for higher gains.
  
  3. **Scenario 3**: Define some suspicious features randomly, like unusual email domains, credit card types, credit card numbers, IP addresses, or phone numbers ending with specific numbers.

  4. An extra transactions table is generated similarly to the normal one, but with fraudulent behavior of the fraudster. This includes multiple payments made with a wide and nonspecific individual preference, different IP addresses/phone numbers/email domains for the same card, and much higher purchasing frequency than normal customers.

### Resulting Data

The data generation process results in two primary data tables: one containing normal transactions and another containing fraudulent transactions. These tables can be used for model training and testing. The fraudulent transactions are labeled as such to help train the model to distinguish between legitimate and fraudulent activities.

This data generation process ensures that your fraud detection model has a diverse and realistic dataset to learn from, enhancing its ability to identify potentially fraudulent transactions in real-world scenarios.

Make sure to implement the data generation process with attention to detail and accuracy to create a reliable dataset for training your fraud detection model.


## Data Transformation

Data transformation is crucial to prepare the data for model training. Key transformations include:

- Creating binary features for relevant time periods (weekday/weekend, day/night).
- Characterizing customer spending behaviors using the RFM framework.
- Creating features that characterize the risk associated with SME terminals.
- Transforming attributes like Card Number, Card Type, Email Domain, Phone Number, and IP Address to numerical values.
- Logarithmic transformation of transaction amounts.

## Model Training

The model training phase uses the XGBoost classification algorithm to build a fraud detection model. The transaction data is split into training, validation, and testing sets. The trained model can then be used to detect fraud in real-world transaction data.

## Usage

To use this fraud detection and prevention system, follow these steps:

1. Generate or collect transaction data.
2. Preprocess the data to match the required format.
3. Train the model using the provided approach and methodology.
4. Use the trained model to detect fraudulent activities in your transaction data.

For a detailed example and demonstration of how to use this system, you can review the example in the [Demo.ipynb](https://github.com/Ashetoto/Fraud-Detection/blob/main/Demo.ipynb) notebook on GitHub.



## Contributing

We welcome contributions to this project. If you have ideas for improvements or want to collaborate, please open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE). Feel free to use and modify it for your needs.

