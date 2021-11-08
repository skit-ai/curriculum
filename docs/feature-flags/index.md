# Feature Flags

The basic idea behind feature flags is to turn a particular feature on/off based on some flag, or condition. A simple pseudocode translation can be:

```
if useNewCoolFeature == true {
  newCoolFeature()
} else {
  sameOldBehaviour()
}
```

This pseudocode demonstrates a simple statement that checks if a "new cool feature" is enabled. If it is, the behaviour of the new feature is observed, and if it isn't, nothing new happens and everything works as it had previously. Feature flags are essentially "if statements" that allows you to validate your new features and test out their functionalities, thus minimizing risks without much disruptions.

When this code is deployed to production, it will be deployed as usual. However, it will remain inactive until the feature flag is explicitly activated.

Now that you understand the basic idea behind feature flags, let's get you set up for an exercise to get you familiar with a few practices and an amazing tool [Flagr](https://checkr.github.io/flagr/#/home).

## Setting you up

Clone the following repository:

```
https://gitlab.com/vernacularai/tools/curriculum-feature-flag
```

Enter the cloned directory and run:

```
go run main.go
```

and make an HTTP request:

```
curl --location --request GET 'localhost:8080'
```

You should get the text `Hello!` in the response.

## An example Feature flag

Assume you're developing a new feature in which instead of just returning a simple `Hello!` message, you want to send something more friendly like `Hello! Have fun with this excercise!`. But you are not sure if this is a good idea and want to validate it first with some, say 10%, of your users. This "new feature" is already implemented with a make-do feature flag and all you need to do is update its rollout percentage. Do:

```
curl --location --request PUT 'localhost:8080/rollout/10'
```

You may enter any float value, less than 100, for the new rollout percentage.

This will tell our service to send the new message to 10% of all our users, after which you will use some metric to calculate its success.

Now all that's left is to check if our feature flag is actually working. Manually make the "hello" request for a sufficient number of times and compare the number times your new feature works with those times it didn't. The ratio should roughly amount to the rollout percentage you provided as an input.

```
curl --location --request PUT 'localhost:8080/rollout/10'
```

## Targetted testing

Suppose you're a part of an MNC with clients in Russia. There, your service says "Hello!" in Russian as "Privyet!". Since "Privyet" is like an informal "Hi" and you would like to test if saying a more formal "Zdrastvuyte", which is also Russian for "Hello", you implement a feature flag that rollouts this new feature to 40% of the Russian clients. Also, to identify a Russian client, your service uses a query param `?location=ru`.

Let's test out our existing Russian "Hello" first:

```
curl --location --request GET 'localhost:8080?location=ru'
```

You'll get "Privyet" in Cyrillic script, which is the writing system used for the Russian language, in the response message.

Update the rollout percentage for Russia too:

```
curl --location --request PUT 'localhost:8080/rollout/40?location=ru'
```

Test out our feature flag for Russian clients similar to the previous example and compare the responses to confirm if the rollout is similar to what was provided in input.


## Flagr

Flagr is a great tool for implementing feature flags and A/B testing. You'll be employing it for continuing the rest of this exercise. Be sure to go through its 

For using Flagr, let's dial our use case up a notch. Suppose your MNC now serves clients in multiple regions throughout the world, with each region having any number of languages and people of different ages. Currently, you respond with a "Hello" indiscrimately but your product manager recently asked you to start tuning this greeting for various combinations of all these properties. The api that handles this greeting supports query params, `location`, `lang` and `age`, for identifying demographies concerning region, language and age respectively.

The api you'll be is of the form:

```
curl --location --request GET 'localhost:8080/flagr-hello?location=<region>&lang=<language>&age=<age>&key=<flagrKey>
```

The query param "key" here is the `flagKey` of the flag you'll be creating shortly. Try making requests to the api. For example:

```
curl --location --request GET 'localhost:8080/flagr-hello?lang=en&location=us&age=20&key=kzpo6597au5ivg876'
```

You should get always get a message "Hello!" in response.

We have a flagr instance hosted on our server that you can use. Ask _#devops_ for:
* URL for the hosted Flagr
* Credentials for authenticating into the instance: _username_ and _password_

Stop the currently running exercise server on port 8080 and export the above values as environment variables:

```
export FLAGR_URL = <FLAGR_URL>
export FLAGR_USERNAME = <FLAGR_USERNAME>
export FLAGR_PASSWORD = <FLAGR_PASSWORD>
```

and start it again:

```
go run main.go
```

If you've added the environment variables correctly, you should have a valid Flagr client for employing your _soon to be created_ new flag. Go to the hosted flagr on a browser and authenticate using the credentials you received. Create a new flag by giving it a name and clicking on the _Create New Flag_ button. The new flag should be visible in the list now. Select it.

You should now see the configuration page for the flag. Make note of your _Flag Key_. The next steps involve creating a "Variant" and a "Segment".

#### Variant

Variant represents the possible variation of a flag. For example, control/treatment, green/yellow/red, etc. It is any property that one would like to vary based on certain condition described in the "Segments".

Enter a name for your variant in "Key" input box and click on "Create Variant". Select the "Variant Attachment" expansion panel and in the editor, enter the new message you'd like to show your audience. For example:

```
{
	"message": "Privyet"
}
```

Save the variant and move to the "Segments" section.

#### Segment

Create a new segment by clicking on the "New Segment" button and then defining its description and rollout settings in the slider. The rollout defines the fraction of the control buckets that would be impacted by the new feature. The default is 50 and you can let it remain the same.

On creating a new segment, you'll notice "No constraints (ALL will pass)" being displayed. This means since we haven't provided any constraints on our segment, all our requests will be a part of the control buckets. You may leave it to be empty for now.

To finish our initial setup, we'll have to define a distribution among the variants for the segment. Click on "edit", select your variant's checkbox and use the slider to increase its percentage to 100. This means all our requests passing the segment will be distrubuted completely to the variant. Save the distribution and now make a request to the `flagr-hello` api endpoint. Make sure you have correctly initialised the environment variables and provided your `flagKey` in the `?key` query param. If you initialised the rollout to 50% and the message in your variant says "Privyet", you should receive "Privyet" in response half the times you make a request.

#### Further Customisation

Create a new variant, and this time enter a new message, say "Zdrastvuyte". In your segment, add a constraint on the location to be Russia. You can do this by adding `location` in "Property" and the value as `ru` with the conditional `==`. Click on "Add Constraint" and save your segment. Now, edit your distibution with the both the variants having 50-50 fractions. You may increase your rollout to 100% if you want all your Russian users to be greeted in the new fashion only. Test your api and observe how your response messages are distributed. Make sure you provide `ru` in the `?location` query param.

If you followed all the steps correctly, you should get a mix of "Zdrastvuyte" and "Privyet", with a bit of "Hello!" too if the rollout was less than 100. Try playing around with your flag, customising your audience based on other properties like `language` and `age` and creating different segments for different demographic groups with their own distributions of different variants. When exploited to the fullest, you'll get to appreciate how handy Flagr is.

I hope this exercise helped in your understanding of feature flags and made you gain more confidence in implementing them using Flagr. 
