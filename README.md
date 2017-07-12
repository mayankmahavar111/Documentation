# Sentiment Analysis
### Requirements
    1. jdk 1.8.0
    2. mongo --versiom=3.4
    3. redis queue 3.0
#### How to start:
    1.Change the constant values in constant.java inside package 
        1.1(
            consumerKey,
            consumerSecret,
            token,
            secret
            )
            These value will be provided by twitter.
        1.2(
            mongoIp,
            mongoPort,
            dbName,
            collectionName
            ) These values are specified by User.
        1.3(
            redisQueue,
            REDIS_HOST,
            REDIS_TIMEOUT,
            REDIS_PORT
            )
            These value are User redis queue values.
    2.Start redis and mongodb server.
#### How to Run 
    1.Run the vertexServer.java class , This will start taking live input when user post a request to the api 
    2.Post the Request to the api : sentiment/twitter/startCampaign , Here request.method is "POST"    
        2.1 Request format has to be in JSON format :
            {
	        "campaign_id":"< Any Alphanumerical Value >",
	        "keywords":["< Any Trending Tweets Keywords >"],
	        "end_time":"< Time upto which tweet has to be taken >"
	        The time will be in UTC format (only tweets untill that time will be streamed).
            }
            For Eg:
            {
	        "campaign_id":"1234",
	        "keywords":["#Trending"],
	        "end_time":"2017-07-07T07:00:45.95z"
            }
    3.
        3.1 After completion of step (4),
        Post another request to api for getting sentiment of specific campaign id
        Request will be post to api : sentiment/twitter/getSentiment
            3.1.1  Request will be in the JSON format 
                {
	            "campaign_id":"< campaign id whose sentiment  user want >"
                }
               After this process the results of all the sentiments will get store in database.
        3.2 After completion of step (4)
        Post another request to api for getting sentiment to according to location
        Request will be post to api : sentiment/twitter/getSentiment2
        3.1.2  Request will be given in the format
        {
    	"campaign_id":"< campaign id whose sentiment  user want >"  ,
        "location":"< location from where you want to see your sentiment score>"
        }
 This will give you sentiment score of tweets you streamed into a text file name resorces-test.txt.
