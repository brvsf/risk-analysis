# Data Analyst (Risk)
## Bruno Vieira - Case

## Understand the Industry:

### Main Players:
* Consumer: Iniciates the purchase
* Merchant: Sell a service or product
* Payment Gateway: Technology that connects the merchant to the acquirer and payment networks in a secure way.
* Acquirer: Intermediates the transactions and assumes risks.
* Payment Network: Connect issuers and acquirers, allowing the exchange of information and the authorization of transactions.
* Issuer: Entity that issues the payment card and controls access to the cardholder's funds (e.g. Banks).

### Money and information flow:
1. The consumer decides to make a purchase.
2. The merchant sends the transaction data to the payment gateway.
3. The gateway encrypts the data and sends it to the acquire.
4. The acquirer processes and forwards the transaction to the payment network.
5. The payment network checks if the card is valid and performs security checks, then sends the request to the issuer for authorization.
6. The issuer approves or denies the transaction and sends the response back through the payment network to the acquirer.
7. The acquirer settles the funds and sends the money to the merchant through the payment gateway.

### Differences between Acquirer, Sub-Acquirer and Payment Gateway:

**Acquirer**: Financial institution or company that processes payment transactions on behalf of the merchant.
  * Main Functions:
    - Enroll merchants to accept payments.
    - Process card transactions.
    - Ensure security.
    - Perform financial settlement for the merchant.

**Sub-Acquirer**: Intermediary that operates between the merchant and the acquirer.
  * Main Functions:
    - Aggregate multiple merchants under a single acquirer account.
    - Simplify the onboarding of new merchants.
    - Manage risk and compliance for aggregated merchants
    - Forward transactions to the main acquirer

**Payment Gateway**
   * Main Functions:
    - Capture and encrypt transaction data.
    - Transmit the data to the acquirer or sub-acquirer.
    - Return the authorization or denial to the merchant.
    - Provide integration with different payment methods

**Differences in the flow when a Sub-Acquirer is involved**
  * Adds an extra layer to the payment process.
  * When there is a sub-acquirer, it acts as an intermediary, grouping multiple merchants and forwarding data to the acquirer.
  * Making it more scalable but also more complex.

### Differences between Chargebacks, Cancelations and Chargeback Frauds.

  **Chargebacks**: The process in which a payment transaction is reversed, usually after the consumer disputes the charge with the bank or credit card issuer.
  **Cancelations**: Is when the buyer or seller decides to annul the transaction before it is completed or delivered. When the purchase is canceled, the amount paid is refunded to the customer, and the seller does not deliver the item. Cancellation is different from a chargeback because it is an action agreed upon by the parties involved, without the intervention of a dispute or financial institution.
  **Chargeback Frauds**: Occurs when a customer requests a refund for a purchase they made, claiming fraud or non-receipt of the product, even though the transaction was valid. This results in a financial loss for the seller, who not only does not receive the payment but also loses the product or service.

### Anti-Fraud Solutions used by Acquirers

  1. Behavioral analysis:
    - Analyzing behavior like purchase history, geolocation, and devices used. If unusual behavior is detected, the transaction may be flagged for further analysis.
  2. Multi-factor authentication:
    - Second layer of security in addition to the user's password, such as confirmation via SMS, email, or an authentication app.
  3. Machine learning:
    - Used to learn fraud patterns from large volumes of data. This enables the system to identify new fraudulent techniques as they emerge.
  4. Rule-based algorithms:
    - A set of logical rules defined by experts or through the analysis of historical data, aimed at identifying suspicious behaviors or characteristics that are typically associated with fraud.

## Solve the problem:


**Context:**
A client sends you an email asking for a chargeback status. You check the system, and see that
we have received his defense documents and sent them to the issuer, but the issuer has not
accepted our defense. They claim that the cardholder continued to affirm that she did not
receive the product, and our documents were not sufficient to prove otherwise.

You respond to our client informing that the issuer denied the defense, and the next day he
emails you back, extremely angry and disappointed, claiming the product was delivered and that
this chargeback is not right.
Considering that the chargeback reason is “Product/Service not provided”, what would you do in
this situation? \


**Answer**

  * First of all this scenario requires a careful response, combining empathy, clarity in explaining the process, and, if possible, offering alternatives for the customer to seek a solution.

  * Actions:

    1. Verify stronger evidence:
      - Signed proof of delivery.
      - Customer confirmation via email or chat that they received the product.
      - Proof of service usage (if digital).

    2. Check for potential fraud using historical data:
      - Has the same customer filed chargebacks before?
      - Did they attempt to pay with a different card before the chargeback?
      - Does the purchase significantly deviate from the buyer’s usual spending pattern?


## Get your hands dirty

**Most of the analysis is conducted inside the notebook in this repository.**

### Suspecious behaviors and conlusions:

  1. Amount:
    - Fraudulent transactions had significantly higher average ($1453.5) and median ($999.47) values compared to all transactions ($767.8 and $415.9).
    - Standard deviation increased from $889.1 to $1169.5, indicating greater variance and possible “test” transactions.
    - Fraud probability increased with transaction amount.

  2. Users:
    - Some of the most active users also had the highest fraud rates.
    - 120 users had 100% of their transactions marked as fraudulent.
    - A high fraud rate was observed for users making frequent transactions within short time frames.

  3. Merchants:
    - Certain merchants had high fraudulent transaction rates, suggesting security issues.

  4. Devices:
    - Only 7% (130 out of 1996) of devices had a fraud history.
    - Users with multiple devices showed a significantly higher fraud rate.

  5. Cards:
    - 9% (274 out of 2925) of credit cards had a fraud history.

  6. Time-based patterns:
    - Fraudulent transactions peaked between Thursday and Sunday.
    - Peak transaction hours were 6 p.m. to 9 p.m.
    - The fraud rate increased from 6 p.m to 2 p.m.

### Actions:

  1. Rule-Based Approach - Requiring More Security Measures or Blocking Transactions Following:
    - User-Oriented Threshold.
    - Merchant-Oriented Threshold.
    - Flag users, cards, or devices with previous fraudulent behavior.
    - Monitor sequence of transactions.

  2. User Behavior Analysis:
    - Identify and analyze patterns in user transaction behaviors.
    - Suspect transactions with unusual patterns.

  3. Keep the merchants close:
    - Talk to merchants with high fraudulent transaction rates to detect possible security issues.

  4. Machine Learning for Fraud Detection:
    - Develop a predictive model based on identified fraud patterns to automatically block or flag suspicious transactions.


### Aditional Data:

  1. Geographical and IP Address Anomalies:
    - If a user suddenly makes a transaction from a country or region far from their usual location, it could be a sign of account takeover.
    - Geolocation tracking and flagging inconsistent activity (e.g., logging in from the U.S. and then transacting from Europe minutes later) can help prevent fraud.

  2. Service/Product bought in the transaction:
    - Tracking which products/services are associated with higher fraud rates can inform the development of more targeted fraud prevention measures.

  3. Type of Device:
    - Knowing more about the device type could help identify patterns in which certain devices are more used by fraudsters.

### Suggestions:

  1. Keep the data team consistently working together to enhance the fraud prevention process.
  2. Continuously feed and improve the prediction model.
  3. Know your costumer: Understand the patterns of customers and vendors.
  4. Possibly restrict devices, cards, or users with a history of fraud.
  5. Stay updated on techniques and methods used by fraudsters.
  6. Clearly define, using rule-based methods, what qualifies as a high-risk transaction.

### Anti-Fraud Solution: ML Approach:

  **Steps**:
  1. Load and split data.
  2. Feature Engineering (weekday, hour, device_missing, user_avg_amount, merchant_avg_amount) and preprocess in pipeline.
  3. Select metrics to monitor (F1-score, Class 1 Recall, ROC AUC).
  4. Random Search in F1-score.
  5. Evaluate.

  **Baseline model** - Logistic Regression(class_weight='balanced’):
  * Class 0 (Negative):
    - Precision (0.93): Few false alarms.
    - Recall (0.76): Identifies 76% of the actual class 0 samples.
    - F1-Score (0.84): Good balance between precision and recall.

  * Class 1 (Positive):
    - Precision (0.30): Lot false alarms.
    - Recall (0.63): Identifies 63% of the actual class 1 samples.
    - F1-Score (0.41): Poor performance due to low precision.

  **XGBoost (without balancing)** - scale_pos_weight=[len(data_non_fraud) / len(data_fraud)]

    - Class 0 (Not Fraud): the model shows high precision (0.94), recall (0.97), and a balanced F1-score (0.96).
    - For Class 1 (Fraud), precision (0.79) and recall (0.60) are lower, leading to an F1-score of 0.68.
    - The overall ROC AUC of 0.9 suggests the model has strong discriminative ability between classes.

  **XGBoost (with undersampling)**

    - Class 0 (Not Fraud), the model shows high precision (0.90), recall (0.98), and a balanced F1-score (0.93).
    - Class 1 (Fraud), precision (0.68) is decent, but recall (0.38) is low, resulting in an F1-score of 0.42.
    - The overall ROC AUC of 0.87 indicates a reasonable ability to differentiate between classes.

    **More information about both XGBoost models, like Learning curves and confusion matrices, can be found in the notebook, under the 'Anti-Fraud Solution: ML Approach' section.**


### Anti-Fraud Solution: Rule Based:

Each risk situation adds points to a score. If the final score is >= 3, the transaction is denied.

  **Rules:**
  1. Transaction Amount
    - High Risk: More than 3 standard deviations above the user's average. (+3)
    - Medium Risk: More than 2 standard deviations above the user's average. (+2)
    - Low Risk: More than 1 standard deviation above the user's average. (+1)

  2. Fraud History
    - Medium Risk: If the user, card or device used in the transaction has a history of fraud. (+2)

  3. Device Usage
    - Low Risk: If the user has used more than one device for transactions. (+1)

  4. Sequential Transactions
    - Medium Risk: User has made multiple transactions in succession (less than 30 minutes apart). (+2)

  5. Transaction Time
    - Low Risk: If the transaction occurs between 9 PM and 3AM (+1)

  **Evaluation**
  Testing in the original data: The model predicts all transactions and we compare with the real values.

  * Metrics:
    1. Accuracy: 0.96
    2. Precision: 0.76
    3. Recall: 1.00
    4. F1-Score: 0.87

  **More information about this Rule Based algorithm, can be found in the notebook, under the 'Anti-Fraud Solution: Rule Based' section.**
