# docker
# docker -p -v HOST:CONTAINER
#
# docker build --no-cache -t simpleblazor .
# docker run -d --rm -p 8080:80 simpleblazor
# dotnet run --launch-profile https
FROM mcr.microsoft.com/dotnet/sdk:8.0-noble AS build
WORKDIR /src
COPY . .
RUN dotnet restore
RUN dotnet publish -c Release -o dist

FROM mcr.microsoft.com/dotnet/aspnet:8.0
COPY --from=build /src/dist ./
ENTRYPOINT ["dotnet", "simpleblazor.dll"]