ARG REPO=mcr.microsoft.com/dotnet/runtime

# Installer image
FROM arm32v7/buildpack-deps:focal-curl as installer

# Retrieve ASP.NET Core
RUN curl -fSL --output aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/5.0.13/aspnetcore-runtime-5.0.13-linux-arm.tar.gz \
    && aspnetcore_sha512='4b92e7a686c852149e228c777f899d2426d81691b2cbc0a2a8708b9c8ab5b504dd544c1c291c848339c7c59d139d9e91e8914059326b0e84e662bcf32d3fb472' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && tar -ozxf aspnetcore.tar.gz ./shared/Microsoft.AspNetCore.App \
    && rm aspnetcore.tar.gz


# ASP.NET Core image
FROM $REPO:5.0.13-focal-arm32v7

ENV ASPNET_VERSION=5.0.13

COPY --from=installer ["/shared/Microsoft.AspNetCore.App", "/usr/share/dotnet/shared/Microsoft.AspNetCore.App"]
