# Chapter 1: Scaling From Zero Users to Millions of Users

## Single Sever Setup
1. users access wesbites through domain names
    - the DNS or Domain Name System is provided by 3rd parties
2. Internet Protocol or IP address is returned to browser -> 15.125.23.214
3. Once IP is obtained the HTTP or Hypertext Transfer Prorocol requests are sent directly to your web server
4. The web server returns HTML pages or JSON response

## Database
- choose between relational or non relational database

### Relational DB
- stored in tables and rows
can perform join operations using SQL

### Non-Relational DB
- aka NoSQL
grouped into four categories: key-value stores, graph stores, column stores, and document stores
- join is not supported

- for most developers, relational dbs are the best option because they have been proven to work well over a long period of ti e
- NoSQL might be the best option if the application requies super-low latency, data is unstructures, only need to serialize and deserialize data, need to store a massive amount of data

## Vertical vs Horizontal Scaling
- Vertical: "scale up", adding more power to servers
    - good for when traffic is low, bad when limiting is an issue
    - does not have failover and redundancy
- Horizontal: "scale out", allows you to scale by adding more servers into pool of resources
    - good for large scale applications

## Load Balancer
- even distributes incoming traffic w/ web servers
- communicates with web severs through private IPs
- when web traffic grows rapidly and two servers are not enough to handle the traffic, the laod balancer handles this problem

## Database Replication
- a master database supports only write operations and a slave db gets copies of the data from the master db and only supports read opertaions
- all CUD operations are sent to the master database
- most apps use a much higher ratios of reads to wrties

Advantages:
1. better perfromance
2. reliability
3. high availibility

This architectural design handles database offline cases very well

## Cache
- temporary storage area that stores the result of the expensive or frequently accessed responses in memory so that it is served more quickly

## Cache Tier
- temporary data store layer, much faster than the database
Advantages:
- better system perfromance
- ability to reduce database worklads
- ability to scale the cache tier independently

First checks if cache has the availible response, if it does, send it back to the client. If not, queries database, stores the response in cache, and sends it back to the client. This is called *read-through cache*

Considerations for using cache:
- when data is read frequently but modified infrequently
- volatile memory, a cache server is not ideal for persisting data
    - for ex. if cache server restarts, all the data in memory is lost
- when there is no expiration policy

LRU (Least Recently Used) is the most popular eviction policy

## Content Delivery Network (CDN)
- network of geographically dispersed servers used to deliver static content
    - ex. videos, images, CSS, js files, etc
- when a user visits a site, CDN server closest to the user will deliver static content

1. static assets are no longer servers by the web servers but instead fetched from the CDN for better perfromance
2. db load is lightened by caching data