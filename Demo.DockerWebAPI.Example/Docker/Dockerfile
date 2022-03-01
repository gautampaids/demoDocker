FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
# COPY *.sln .
COPY *.csproj ./Demo.DockerWebAPI.Example/
RUN dotnet restore Demo.DockerWebAPI.Example/Demo.DockerWebAPI.Example.csproj

# copy everything else and build app
COPY . ./Demo.DockerWebAPI.Example/
WORKDIR /app/Demo.DockerWebAPI.Example
RUN dotnet publish -c Release -o out

FROM 9168623303/aspnetcore-runtimetwo AS runtime
WORKDIR /app
COPY --from=build /app/Demo.DockerWebAPI.Example/out ./

ENV ASPNETCORE_URLS http://+:11000
EXPOSE 11000

ENTRYPOINT ["dotnet", "Demo.DockerWebAPI.Example.dll"]
