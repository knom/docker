FROM stefanscherer/openjdk-windows:8-nanoserver

AUTHOR Max Knor

# Set the WILDFLY_VERSION env variable
ENV WILDFLY_VERSION 8.2.1.Final
ENV WILDFLY_SHA1 7BD83F071C6BA8E1620F2CF92B9357A44C3FA952
ENV JBOSS_HOME C:/wildfly/

COPY ./wildfly-8.2.1.Final.zip C:/

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN $file = \"wildfly-$env:WILDFLY_VERSION.zip\"; \
	$url = \"https://download.jboss.org/wildfly/$env:WILDFLY_VERSION/wildfly-$env:WILDFLY_VERSION.zip\"; \
#	 Write-Host 'Downloading $env:WILDFLY_VERSION';	\
#    Invoke-WebRequest -Uri $url -OutFile wildfly-$env:WILDFLY_VERSION.zip -Verbose; \
	Write-Host 'File Hash:'; \
	if ((Get-FileHash file -Algorithm sha1).Hash -ne $env:WILDFLY_SHA1) { \
		Write-Host 'FAILED!'; \
		exit 1; \
	}; \
	Write-Host 'Expanding ZIP file'; \
#    Expand-Archive $file -DestinationPath C:/wildfly-$env:WILDFLY_VERSION; \
    Expand-Archive $file C:/; \
#    Move-Item wildfly-$env:WILDFLY_VERSION $env:JBOSS_HOME; \
	Write-Host 'Renaming folder'; \
	Rename-Item wildfly-$env:WILDFLY_VERSION wildfly; \
	Write-Host 'Deleting ZIP file'; \
    Remove-Item $file; \
	Write-Host 'Done'; \

# Expose the ports we're interested in
EXPOSE 8080 9990

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
# CMD [$JBOSS_HOME, "standalone.bat", "-b", "0.0.0.0"]
CMD ["C:\\wildfly\\bin\\standalone.bat", "-b", "0.0.0.0"]