#
# Stage 1: Build dotnet app
#

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
ARG CONFIGURATION=Release

WORKDIR /app

# copy only nuget instructions (so that this can be cached if not changed)
COPY *.csproj ./
RUN dotnet restore

# copy app files (will be changing, this image layer is unlikely to be cached)
COPY . ./

RUN dotnet publish WebTemplate.csproj -c ${CONFIGURATION} -o out

#
# Stage 2: Run dotnet app
#

FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app

EXPOSE 80
COPY --from=build /app/out .

ENTRYPOINT ["dotnet", "WebTemplate.dll"]