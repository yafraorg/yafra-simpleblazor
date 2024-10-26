# docker
# docker -p -v HOST:CONTAINER
#
# docker build --no-cache -t simpleblazor .
# docker builder prune -a
# docker run -it --rm -p 8080:80 mcr.microsoft.com/dotnet/sdk:8.0-noble
# docker run -d --rm -p 8080:80 simpleblazor
# dotnet run --launch-profile https

# build image and copy source files
FROM mcr.microsoft.com/dotnet/sdk:8.0-noble AS build
WORKDIR /src
COPY . .
# install nodejs
RUN apt-get update; apt-get upgrade -y
RUN curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install -y nodejs
RUN npm install
# build web page
RUN npm run css
RUN dotnet restore
RUN dotnet publish -c Release -o dist

# runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
COPY --from=build /src/dist ./
ENTRYPOINT ["dotnet", "simpleblazor.dll"]