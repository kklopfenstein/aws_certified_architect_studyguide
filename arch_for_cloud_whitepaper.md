Architecting for the Cloud Best Practices Whitepaper
----------

Business Benefits Of Cloud
----------
* Almost zero upfront infrastructure investment
* Just-in-time infrastructure
* More efficient resource utilization
* Usage-based costing
* Reduced time to market

Technical Benefits of Cloud
----------
* Automation - "Scriptable infrastructure"
* Auto-scaling
* Proactive Scaling
* More Efficient Development lifecycle
* Improved Testability
* Disaster Recovery and Business Continuity
* "Overflow" the traffic to the cloud


Design for Failure
------
Rule of thumb: Be a pessimist when designing architecture in the cloud; assume things will fail. In other words, always design, implement and deploy for automated recovery for failure.

In particular, assume that your hardware will fail. Assume that outages will occur. Assume that some disaster will strike your application. Assume that you will be slammed with more than the expected number of requests per second some day. Assume that with time your application software will fail too. By being a pessimist, you end up thinking about recovery strategies during design time, which helps in designing an overall system better.

Decouple your Components
----------
For example, in the case of web application architecture, you can isolate the app server from the web server and from the database. The app server does not know about your web server and vice versa, this gives decoupling between these layers and there are no dependencies code-wise or functional perspectives.

In the case of batch-processing architecture, you can create asynchronous components that are independent of each other.

Implement Elasticity
----------

The cloud brings a new concept of elasticity in your applications Elasticity can be implemented in three ways:

1. Proactive Cyclic Scaling: Periodic scaling that occurs at fixed interval (daily, weekly, monthly, quarterly)
2. Proactive Event-based Scaling: Scaling just when you are expecting a big surge of traffic requests due to a schedulued business event (new product launch, marketing campaigns)
3. Auto-scaling based on demand. By using a monitoring service, your system can send triggers to take appropriate actions so that it scales up or down based on metrics (utilization of the servers or network i/o, for instance)

Secure your Application
----------

Only allow ports that are needed between the tiers needed. E.g. port 22 only available in corporate office network.
