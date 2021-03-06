# LogBackendPlugin
a plugin for neo to integrate with a log backend.
## system architecture
![system](https://github.com/KickSeason/LogBackend/blob/master/log-monitor.png)

[LogBackendPlugin](https://github.com/KickSeason/LogBackendPlugin) is for sending neo-cli's log to log-server.  
[log-server](https://github.com/KickSeason/log-server) is for persisting logs into files and sending to partners  
[log-monitor](https://github.com/KickSeason/log-monitor) is the website to view realtime logs
## prepation
set up a backend server based on http protocol, follow this [log-server](https://github.com/KickSeason/log-server)
so you can get a url: http://log-server:port

### build
1. clone this repository
2. build using dotnet or visual studio
3. you can got LogBackends.dll and LogBackends/config.json
### download
you can download release version directly at [releases](https://github.com/KickSeason/LogBackend/releases)
## configuration
```
{
  "PluginConfiguration": {
    "CacheCount": 256,
    "Backend": "http://47.74.50.11:8090"
    }
}
```
> __CacheCount__:this is how many logs can store in the queue. when more than CacheCount logs are not sent, oldest logs will be abandoned.
> __Backend__: the log-server you establish to receive logs using http.
## usage
4. copy LogBackend.dll and LogBackends/config.json into *Plugins* under *neo-cli*
5. start *neo-cli*
now  you can get the consensus logs at your log server.
## trouble shooting
1. if you cannt start because of exception: **Unable to load DLL 'System.Net.Http.Native': The specified module or one of its dependencies could not be found**.
please check [dotnet core 2.x requisite](https://docs.microsoft.com/en-us/dotnet/core/linux-prerequisites?tabs=netcore2x), specially libcurl3 for ubuntu and libcurl for centos.
## todo
1. add a buffer in Backend, so wont connection every log.
2. long term: consider long connection tcp or http.
