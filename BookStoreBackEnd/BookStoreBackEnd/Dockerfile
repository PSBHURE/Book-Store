# =========================
# Stage 1: Build the project
# =========================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy solution and project files
COPY *.sln ./
COPY BookStoreBackEnd/*.csproj ./BookStoreBackEnd/
RUN dotnet restore

# Copy the rest of the code
COPY . .

# Build and publish
WORKDIR /src/BookStoreBackEnd
RUN dotnet publish -c Release -o /app/publish

# =========================
# Stage 2: Run the app
# =========================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copy published output
COPY --from=build /app/publish .

# Expose port (internal container port)
EXPOSE 8080

# Run the app
ENTRYPOINT ["dotnet", "BookStoreBackEnd.dll"]
