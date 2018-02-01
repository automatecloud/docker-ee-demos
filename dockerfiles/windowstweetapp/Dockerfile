# escape=`
FROM microsoft/iis:windowsservercore-10.0.14393.1715
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN Remove-Website 'Default Web Site';

# Set up website: Default Web Site
RUN New-Item -Path 'C:\inetpub\wwwroot' -Type Directory -Force; 

RUN New-Website -Name 'Default Web Site' -PhysicalPath 'C:\inetpub\wwwroot' -Port 80 -ApplicationPool 'DefaultAppPool' -Force; 

EXPOSE 80

COPY ["wwwroot", "/inetpub/wwwroot"]

RUN $path='C:\inetpub\wwwroot'; `
    $acl = Get-Acl $path; `
    $newOwner = [System.Security.Principal.NTAccount]('BUILTIN\IIS_IUSRS'); `
    $acl.SetOwner($newOwner); `
    dir -r $path | Set-Acl -aclobject  $acl
