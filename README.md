# Notification
Enterprise Java Bean (*EJB*) Message Driven Bean (*MDB*) that consumes from **IBM MQ** and calls an **OpenWhisk** action sequence that posts to a **Slack** channel.

This *MDB* responds to the **JMS** *TextMessage*s that the *loyalty-level* microservice delivers to **MQ** whenever a portfolio changes levels, such as from *Silver* to *Gold*.

Note that this is the only microservice in the **IBM Stock Trader** sample that uses the traditional **Java EE** programming model (*EJB*s, *JMS*, *JNDI*, etc.).  As such, its server.xml depends on many more features, including the feature for interacting with **IBM MQ**.

This *MDB* expects to receive a *TextMessage* containing a *JSON* object with three fields: `owner`, `old`, and `new`.  For example, if you post a message like `{"owner": "John", "old": "Silver", "new": "Gold"}` to its **MQ** queue, it will make a *REST* call to an *action sequence* in **OpenWhisk** (in **Bluemix**) which results in a post of a message to the *#slack-test* channel on ibm-cloud.slack.com that says `John has changed status from Silver to Gold.`.
