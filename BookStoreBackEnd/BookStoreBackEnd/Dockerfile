# =========================
# Stage 1: Build the project
# =========================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy project file and restore dependencies
COPY BookStoreBackEnd.csproj ./
RUN dotnet restore

# Copy the rest of the code
COPY . .

# Build and publish
RUN dotnet publish -c Release -o /app/publish

# =========================
# Stage 2: Run the app
# =========================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copy published output
COPY --from=build /app/publish .

# Expose container port
EXPOSE 8080

# Run the app
ENTRYPOINT ["dotnet", "BookStoreBackEnd.dll"]
