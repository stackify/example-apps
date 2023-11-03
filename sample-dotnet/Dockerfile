FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
RUN apt-get update && apt-get install -y wget
EXPOSE 80
EXPOSE 443

# Start - Stackify
ENV PAL_OUTPUTDEBUGSTRING=1
ENV CORECLR_PROFILER={cf0d821e-299b-5307-a3d8-b283c03916da}
ENV CORECLR_ENABLE_PROFILING=1
ENV CORECLR_PROFILER_PATH="/stackify-dotnet-apm/StackifyProfiler.so"
RUN mkdir -m 0755 -p /stackify-dotnet-apm && \
    cd /stackify-dotnet-apm && \
    wget http://download.stackify.com/stackify-dotnet-apm/stackify-dotnet-apm-install-linux-latest.tar.gz && \
    tar -zxvf stackify-dotnet-apm-install-linux-latest.tar.gz && \
    cd stackify-dotnet-apm-install-linux && \
    chmod +x ./install.sh && \
    ./install.sh --docker && \
    cd .. && \
    rm -rf stackify-dotnet-apm-install-linux && \
    rm stackify-dotnet-apm-install-linux-latest.tar.gz
# End - Stackify

COPY . .
ENTRYPOINT ["dotnet", "Serilog-Stackify.dll"]
