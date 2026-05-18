# syntax = docker/dockerfile:1

# Step 2: Download dependencies
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src
COPY *.csproj ./
RUN dotnet restore

# Step 3: Build the NestJS app (TS -> JS)
COPY . .
RUN dotnet publish -c RELEASE -o /app/publish

# Step 4: Run the compiled app
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

EXPOSE 3000
ENTRYPOINT ["dotnet", "backend.dll"]
