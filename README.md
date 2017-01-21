# Anonpay


## /request/main

Input parameters:


* public_key - your public key (API key available after signing up at http://anonpay.org)
* notification_url - Payment notification will be send to this URL.
* amount - transaction amount in your local currency (available PLN)
* description - your personal description (can be used to identify the transaction)
* wallet address - target wallet address on which you want to receive Bitcoins
* firstname - customer first name
* lastname - customer last name
* email - customer email

Output parameters:

* unique_hash - transaction unique hash
* payment_link - generated payment link for user
* security_code - generated confirmation hash md5($amount.$unique_hash.$private$key)

## notifications

Notifications will be send using the POST method to the URL that was provided in /request/main step.

Post parameters: 
* security_code - the same as in /request/main step
* amount - transaction amount with commission substracted
* commission - transaction commission amount
* unique_hash - unique transaction hash
* description - personal description sent with /request/main function
* btc - amount of btc after exchange (the exact value will be send when the status is 4 or 5).
* status - current transaction status

```
1 - transaction paid
2 - transaction notification sent
3 - started exchange
4 - exchange finished
5 - sent to user
```

## Examples

### Send a request

```
$ch = curl_init('https://anonpay.org/request/main');
curl_setopt($ch, CURLOPT_POST, true);

$data = array(
  'public_key' => 'public_key',
  'notification_url' => 'http://Mydomain.com/notificationUrl',
  'amount' => 21.38,
  'description' => 'Order number: #12475',
  'wallet_address' => 'correct_wallet_address'
);

curl_setopt($ch, CURLOPT_POSTFIELDS, $data);

curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
$result = curl_exec($ch);

curl_close($ch);
var_dump($result);
```

### Receive notification information


```
$data = $_POST;

print_r($data);

```
