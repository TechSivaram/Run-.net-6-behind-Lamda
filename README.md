# Run-.net-6-behind-Lamda

I have a reason to run lambda behind lambda.

Some API causing the asp.net core API server to hang or crash

Idea is divert the traffic of those problem (but very much needed for functionality) API to temporary isolated Eexution environment like lamda.

All .net 6, Lamda & AWS images do have arm support. So we can get cost benefit from AWS arm processors.

Dockerizing the existing code using by following the below link. Struggled a lot to connect these dots. So adding all these here

public.ecr.aws/lambda/dotnet:6.2023.01.11.07


![image](https://user-images.githubusercontent.com/85802871/213964892-d223e166-ed90-4590-ae3f-f28b9b861b12.png)


Following small piece of code can do the needed magic

![image](https://user-images.githubusercontent.com/85802871/213964357-1bd02e30-d416-404f-8b63-7bd8f4459781.png)


# Chalenge -

## Shared file system.

Ex: Static files like photos, reports...

## Why lambda

1. It won't crash the whole application
2. Event it is not real time, it can provide cost effective solution to run on need basis.
3. Even something went wrong, it is completely isolated.

## Shared resources

1. Redis / DB connection strings can be accessible via environment variables
2. EFS - mount is also available as shared file system via EFS access points. All security groups has to be properly taken care.

![image](https://user-images.githubusercontent.com/85802871/213963929-6125fe04-76f0-47fc-ac14-781476f37a08.png)

## Reach via load alancer- 
Yes, ALB supports target groups with lambda target. 

In ALB listner rules adding path rule to forward it to lambda trigger. Lamda console do provide this.
I do recommend use it, because AWS console takes care of many permissions.
