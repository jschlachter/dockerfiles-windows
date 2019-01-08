# escape=`

FROM mcr.microsoft.com/dotnet/framework/aspnet:4.7.2-windowsservercore-ltsc2019
LABEL maintainer "Jeremy Schlachter"

ARG site_root=.
ADD ${site_root} /inetpub/wwwroot

WORKDIR C:/
COPY *.pfx .https/

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# $cert = (Get-ChildItem cert:\LocalMachine\My 
#       | where-object { $_.Subject -like "*$portland.local*" } 
#       | Select-Object -First 1).Thumbprint

EXPOSE 443

RUN Import-Module WebAdministration; `
    New-WebBinding -Name 'Default Web Site' -IP "*" -Port 443 -Protocol https; `
    certutil  -p Manticor3? -importpfx .https/PORTLAND.pfx; `
    cd IIS:\SSLBindings; `
    get-item cert:\LocalMachine\MY\8EE574700BD8E3B9A18ED71459D4481F851A187D | new-item 0.0.0.0!443