# Architecture

``` mermaid

graph LR

 subgraph WAN
    subgraph InternalNetwork[Internal Network]
        lux(LuxPower Inverter)
        tuya(Smart plugs)
        ana(Analytics)
        
            subgraph Raspberrypi[Raspberry Pi]
                subgraph linux[Linux OS]
                    subgraph docker
                        lxp(lxp-bridge)
                        mqtt(mosquitto <br>message queue)
                        postgres(PostgreSQL <br>database)
                        hass(homeassistant)
                        noder(NodeRed)

                        lxp<-->|port 1883|mqtt
                        mqtt<-->|port 1883|hass
                        lxp-->|port 5432|postgres
                        noder<-->|port 1883|mqtt
                        noder-..-|display only|hass
                    end
                end
            end
    end

   
        subgraph ZeroTier[Zero Tier Virtual Network]
            mobile(Home Assistant<br>mobile app)
            Laptop
        end
    ZeroTier-->linux
    lux-->luxchina(LuxPower Data Endpoint)
end

    lux<-->|port 8000|lxp
    hass-->tuya
    postgres-..->ana

```

## Home Assistant (hass)

- https://github.com/Madelena/hass-config-public
- https://github.com/markgdev/home-assistant_OctopusAgile
- https://github.com/frenck/home-assistant-config
- https://github.com/dlashua/hass-setter


## Lxp-bridge

https://github.com/celsworth/lxp-bridge/tree/master/src


## Node Red


## Zero Tier

## CICD

