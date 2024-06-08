### The _flespisoftware-parameters-datasource_ plugin works with grafana 10+

![Logo](https://github.com/flespi-software/flespi-grafana-datasource/blob/main/src/img/logo.svg "flespisoftware parameters grafana plugin")

Plugin allows to visualize parameters of [flespi devices](https://flespi.io/docs/#/gw/devices/get_devices_dev_selector_messages), [statistics of flespi accounts](https://flespi.io/docs/#/platform/statistics), parameters of [streams'](https://flespi.io/docs/#/gw/streams/get_streams_stream_selector_logs) and [devices' logs](https://flespi.io/docs/#/gw/devices/get_devices_dev_selector_logs), flespi [storage containers](https://flespi.io/docs/#/storage/containers/get_containers_container_selector_messages) and flespi analytics [intervals](https://flespi.io/docs/#/gw/calculators/get_calcs_calcs_selector_devices_calc_devices_selector_intervals_calc_device_intervals_selector).

### Installation

________________________________________________

1. Install grafana as standalone binaries
    - <details>
        <summary>MacOS installation</summary>

        You can find the latest version of the commands here: [Install Grafana](https://grafana.com/grafana/download?edition=oss&pg=get&platform=mac&plcmt=selfmanaged-box1-cta1)

        ```bash
        curl -O https://dl.grafana.com/oss/release/grafana-10.2.3.darwin-amd64.tar.gz

        tar -zxvf grafana-10.2.3.darwin-amd64.tar.gz
        ```
      </details>

    - <details>
        <summary>Linux installation</summary>

        You can find the latest version of the commands here: [Install Grafana](https://grafana.com/grafana/download?edition=oss&pg=get&platform=linux&plcmt=selfmanaged-box1-cta1)

        ```bash
        curl -O https://dl.grafana.com/oss/release/grafana-10.2.3.linux-amd64.tar.gz

        tar -zxvf grafana-10.2.3.linux-amd64.tar.gz
        ```

      </details>

2. <details>
    <summary>Install plugin</summary>

    ```bash
    cd grafana-v10.2.3

    mkdir  -p ./data/plugins

    ./bin/grafana cli --pluginsDir ./data/plugins --pluginUrl https://github.com/flespi-software/flespi-grafana-datasource/releases/latest/download/flespisoftware-parameters-datasource.zip plugins install flespisoftware-parameters-datasource
    ```
    As soon as _flespisoftware-parameters-datasource_ plugin is not signed, in order to be able to install and run the plugin, you should specify plugin's id in [allow_loading_unsigned_plugins](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/#allow_loading_unsigned_plugins) Grafana configuration variable.

    Make copy of your `./conf/defaults.ini`
    ```bash
    cp ./conf/defaults.ini ./conf/custom.ini
    ```

    Now edit your `./conf/custom.ini` and set
    ```bash
    allow_loading_unsigned_plugins = flespisoftware-parameters-datasource
    ```

    Start grafana server

    ```bash
    ./bin/grafana server
    ```
  </details>

________________________________________________

<details>
  <summary>Ubuntu/Debian system-wide installation</summary>

  ```
  sudo apt-get install -y adduser libfontconfig1 musl

  wget https://dl.grafana.com/oss/release/grafana_10.2.3_amd64.deb

  sudo dpkg -i grafana_10.2.3_amd64.deb
  ```
  You can find the latest version of the commands here: [Install Grafana](https://grafana.com/grafana/download?edition=oss&pg=get&platform=linux&plcmt=selfmanaged-box1-cta1)

  As soon as _flespisoftware-parameters-datasource_ plugin is not signed, in order to be able to install and run the plugin, you should specify plugin's id in [allow_loading_unsigned_plugins](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/#allow_loading_unsigned_plugins) Grafana configuration variable:

  ```
  allow_loading_unsigned_plugins = flespisoftware-parameters-datasource
  ```

  To install this plugin using the [grafana cli](https://grafana.com/docs/grafana/latest/cli/) tool, execute the following command:
  ```
  cd /usr/share/grafana/bin
  sudo ./grafana cli --pluginUrl https://github.com/flespi-software/flespi-grafana-datasource/releases/latest/download/flespisoftware-parameters-datasource.zip plugins install flespisoftware-parameters-datasource
  ```
  and then restart your grafana server.

  Alternatively, you may manually copy source code from `flespisoftware-parameters-datasource` directory into grafana plugins directory and restart grafana server.
  By default plugins directory is: `/var/lib/grafana/plugins`
  To check plugins directory in Grafana interface open: Toggle menu in top left corner > Administration > Settings > paths/plugins

  To remove plugin run:
  ```
  cd /usr/share/grafana/bin
  sudo ./grafana cli plugins remove flespisoftware-parameters-datasource
  ```

</details>

________________________________________________

### To setup the datasource you need to configure your [Flespi Token](https://flespi.com/kb/tokens-access-keys-to-flespi-platform) in datasource's settings.

### Plugin supports template variables.
The following queries can be used to create variable:

| Query                                                    | Description                                                     |
| ---------------------------------------------------------|:---------------------------------------------------------------:|
| devices.*                                                | fetch all devices available for given token                     |
| devices.${device}.parameters.*                           | fetch telemetry parameters for the selected device              |
| accounts.*                                               | fetch account and subaccounts available for given token         |
| accounts.${account}.statistics.*                         | fetch statistics parameters for the selected (sub)accounts      |
| streams.*                                                | fetch all streams available for given token                     |
| containers.*                                             | fetch all containers available for given token                  |
| containers.${container}.parameters.*                     | fetch parameters of the selected container                      |
| calculators.*                                            | fetch all calculators available for given token                 |
| calculators.${calculator}.devices.*                      | fetch devices assigned to the selectede calculator              |
| calculators.${calculator}.devices.${device}.parameters.* | fetch parameters of the selected calculator and assigned device |


### Dev setup

To install frontend dependencies run:

`npm install`

To build and watch the plugin frontend code:

`npm run dev`

### Changelog

1.0.0
  Initial implementation
  
1.1.0
  Added visualization of flespi accounts' statistics

1.2.0 
  Added visualization of flespi containers' parameters

1.3.0
  Added visualization of logs of flespi devices and streams

1.4.0
  Added visualization of flespi analytics's intervals

1.4.8
  Changed build release workflow. Readme updated accordingly

1.5.0
  Plugin ID changed from _flespi-parameters-datasource_ to _flespisoftware-parameters-datasource_ and plugin's code is moved into another git repository
