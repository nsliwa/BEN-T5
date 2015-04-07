TeamBEN:
	Nicole Sliwa
	Ender Barillas
	Bre'Shard Busby

For Thought:
	1) The current method of saving the classifier is not always blocking to the tornado IOLoop. Since we now have a dictionary of the classifiers, when we already have the classifier stored, we don't need to call pickle, so we are not blocking. But, when it's not in the dictionary, we will have to call pickle, and block tornado's IOLoop.
	In other words, this method is better, but it's not the most optimal: we still need to block whenever the DSID doesn't exist in the dictionary; the only way to minimize blocking is to process the adding of a new dicitonary entry in a background thread.

	2) Each time we get or post data to the server, we check for errors before processing the response. However, we don't actually handle any errors if they occur (and it doesn't alert the user that they've happened). 