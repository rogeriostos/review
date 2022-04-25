# image build
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ./*.sln .
COPY Review.Web/*.csproj ./Review.Web/
RUN dotnet restore
COPY Review.Web/. ./Review.Web/
WORKDIR /src/Review.Web
RUN dotnet publish -c release -o /app --no-restore

# image production
FROM mcr.microsoft.com/dotnet/aspnet:5.0 as production
LABEL vendor=Rogerio\ dos\ Santos\ Silva \
    email=roger7331@gmail.com \
    version="1.0" \
    release-date="2022-04-24"
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "Review.Web.dll"]