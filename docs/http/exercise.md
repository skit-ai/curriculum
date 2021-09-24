# A Simple cURL Exercise

Here's a simple cURL exercise to get you familiar with the basics.

In this exercise you'll be communicating with a service having a public url
which you can use to communicate with it using [cURL](https://curl.se/docs/manpage.html).
This public url is `[https://curriculum-http-curl.skit.ai](https://curriculum-http-curl.skit.ai)`,
which will be referenced as `BASE_URL` from now onwards. So if the url of the 
login api is given as `{{BASE_URL}}/login`, it means `https://curriculum-http-curl.skit.ai/login`.
The __{{}}__ shows a variable. Most often, you'll have to replace these values 
with your own values similar to how it was done for `{{BASE_URL}}`.

While going through the exercise, try typing every command out instead of just
copy-pasting. Make sure you understand everything that you type and every bit
of what you get in the response.

Say hello to the service by running:

```
curl --location -g --request GET '{{BASE_URL}}'
```

The service is a mock employee record keeper using which you can create data of
emplyees, fetch that data, update the data and remove it. Since this data can
be sensitive, it also has a form of email-password authentication with a 
persistent jwt access token ([bearer token](https://stackoverflow.com/questions/25838183/what-is-the-oauth-2-0-bearer-token-exactly/25843058)).

## Employee

An employee has the following properties:
* Email: `string`
* Password: `string`
* ID: `unsigned int`
* First name: `string`
* Second name: `string`
* Age: `int`
* Address: `object`

The address of an employee further has following properties:
* City: `string`
* State: `string`
* Street: `string`
* House number: `string`

## New Employee

Now that you know what an employee looks like, let's get you started with creating a new one.

Make this request from your terminal after replacing `{{EMAIL}}` and `{{PASSWORD}}` with that of your employee's.

```
curl --location -g --request POST '{{BASE_URL}}/employees' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email": "{{EMAIL}}",
    "password": "{{PASSWORD}}",
    "first_name": "{{FIRST_NAME}}",
    "second_name": "{{SECOND_NAME}}"
}'
```

You may get a `Email already exists` message in response, which means the 
email you entered is already in use. In this case you will have to provide a 
new email which isn't already present in the system.

If you get status code as 200, you've successfully created a new employee. Note down the 
ID of your employee and the returned bearer token as it will be needed for the 
rest of the exercise.

## Logging Out

You've done a great job creating an entry for your employee and now you're tired. Let's log you out.

Run this command after putting in your ID and access token

```
curl --location -g --request POST '{{BASE_URL}}/logout/:ID' \
--header 'Authorization: Bearer {{TOKEN}}'
```

A status code of 200 means you've successfully logged out.

## Logging In

You've created your employee, but now you want to update its address.

Run this command and note down the newly returned access token

```
curl --location -g --request POST '{{BASE_URL}}/login' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email": "{{EMAIL}}",
    "password": "{{PASSWORD}}"
}'
```

## Update details

You can update the following details of your employee: email, password and address.
To update your employee's address, run the following command:

```
curl --location -g --request PUT '{{BASE_URL}}/employee/:ID \
--header 'Authorization: Bearer {{TOKEN}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "address": {
        "city": "{{CITY}}",
        "state": "{{STATE}}",
        "street": "{{STREET}}",
        "house_number": "{{HOUSE_NUMBER}}"
    }
}'
```

Make sure you've replaced the variables with appropriate values. You may also 
update the password or email of your employee with a command similar to

```
curl --location -g --request PUT '{{BASE_URL}}/employee/:ID \
--header 'Authorization: Bearer {{TOKEN}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email": "{{EMAIL}}",
    "password": "{{PASSWORD}}"
}'
```

If you get the message `Nothing updated`, you probably didn't provide any new
information.

Let's now check if our employee's address has indeed been updated in our system.

## Fetch details of your Employee

Running this command will give you the details of your employee, except the password of course.

```
curl --location -g --request GET '{{BASE_URL}}/employee/:ID' \
--header 'Authorization: Bearer {{TOKEN}}'
```

Found any information wrong? You may update it! :)

## List all the Employees

Running this command will give you a list of all the employees currently saved on the system.

```
curl --location -g --request GET '{{BASE_URL}}/employees' \
--header 'Authorization: Bearer {{TOKEN}}'
```

## Delete an Employee

Just like getting hired, employees get fired all the time. You may fire yours by

```
curl --location -g --request DELETE '{{BASE_URL}}/employee/:ID' \
--header 'Authorization: Bearer {{TOKEN}}'
```

This will completely remove the employee from the system.

## Play around

The exercise should have now made you comfortable with the basics of http and 
using cURL. Try playing around with it a little and make sure understand what 
each line does.
