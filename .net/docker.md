~~~
docker pull mcr.microsoft.com/dotnet/core/sdk:3.1
~~~

~~~
docker run --name=dotnet -itd -p 8080:8080 -p 8081:8081 -v D:/workspace:/workspace -w /workspace mcr.microsoft.com/dotnet/core/sdk:3.1
~~~