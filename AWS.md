# SESSION 9: AWS Global Infrastructure

The AWS Global Infrastructure is a worldwide network of data centers and servers that allows you to run your applications and services wherever you need them. Here's a simple breakdown of its main components:

![aws](https://raw.github.com/karthikeya03/IMAGES/JustMain/9.1.png)

## 1. Availability Zones (AZs)
- **What they are:** These are physical data centers within a region.
- **Function:** They house multiple servers and networking equipment, such as switches, load balancers, and firewalls.
- **Key Point:** Each Availability Zone can be made up of multiple data centers, but they are considered one zone if they are close together.

## 2. Regions
- **What they are:** Large geographical areas that contain multiple Availability Zones.
- **Function:** Regions provide full isolation from other regions, ensuring security and compliance.
- **Key Point:** Every region has at least two Availability Zones connected by high-speed, redundant networking links.

## 3. Edge Locations
- **What they are:** These are smaller sites located in major cities worldwide.
- **Function:** They serve as endpoints for AWS's Content Delivery Network (CDN) called CloudFront, caching content closer to users.
- **Key Point:** Edge locations reduce latency by delivering cached content to users from the nearest location.

## 4. Regional Edge Caches
- **What they are:** Larger caching locations that sit between CloudFront’s edge locations and the original source of the data (origin servers).
- **Function:** They store data that isn't frequently accessed, reducing the need to go back to the origin server.
- **Key Point:** If an edge location doesn't have the requested data, it can retrieve it from a Regional Edge Cache instead of the origin server, which is faster.

## Overview
- **AWS Regions:** 33 globally, each with multiple Availability Zones.
- **Availability Zones:** 105, ensuring high availability and redundancy.
- **Edge Locations:** Over 150, positioned in major cities to improve access speeds.
- **Regional Edge Caches:** 13, enhancing data retrieval efficiency.

## Example: Watching a Movie on a Streaming Service
Imagine you're in Singapore and you want to watch a movie on an online streaming service like Amazon Prime Video.

### 1. Edge Locations
- There’s an edge location (a small data center) in Singapore.
- When you press play on the movie, your request goes to this edge location first.
- If the movie is cached there (stored temporarily because it’s popular), it starts playing almost immediately, giving you a smooth experience with no buffering.

### 2. Regional Edge Caches
- If the movie isn’t cached in the Singapore edge location, it checks a nearby larger cache, called a Regional Edge Cache, which holds less frequently accessed content.
- The Regional Edge Cache also provides fast access but covers a larger area and more data.

### 3. Origin Server
- If the movie isn’t even in the Regional Edge Cache, the request goes to the origin server, where all the movies are stored.
- This server could be located far away, perhaps in the main data center in the US, leading to longer buffering times.

## Breaking Down AWS Components in the Example:
### 1. Availability Zones (AZs)
- These are big data centers where all the movies and other data are stored.
- They have all the necessary equipment to handle large amounts of data and user requests.

### 2. Regions
- The origin server for your streaming service might be in an AWS Region in the US.
- This region has multiple Availability Zones to ensure that even if one data center goes down, your movie is still accessible from another.

### 3. Edge Locations
- These are the smaller, local data centers in major cities like Singapore.
- They cache popular movies and data close to users to reduce lag and buffering times.

### 4. Regional Edge Caches
- These are larger caches between the local edge locations and the origin servers.
- They store less frequently accessed content but still closer to the users than the origin servers, improving access speeds.

## How It Works Together:
1. **You request a movie.**
2. **First Check:** Singapore edge location – if cached, you get the movie instantly.
3. **Second Check:** If not cached, it checks the Regional Edge Cache.
4. **Final Check:** If still not available, it goes to the origin server in the main data center, which takes the longest.

This multi-layered setup ensures that you get the fastest possible access to your movie, minimizing buffering and improving your viewing experience.
